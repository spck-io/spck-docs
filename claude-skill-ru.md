# <a name="claude-skill"></a>Skill Claude: Запуск Spck CLI как Linux-службы

На этой странице представлена загружаемая [skill для Claude Code](https://docs.claude.com/en/docs/claude-code/skills), которая автоматизирует установку Spck CLI (`spck`) в качестве службы `systemd` на Linux. После установки skill вы можете попросить Claude Code «запустить spck как службу», и он проверит вашу среду, сгенерирует правильный unit-файл с вашими абсолютными путями, установит его и убедится, что он запущен — без необходимости копировать команды из списка.

Skill кодирует ту же настройку systemd, описанную в [Использование Tmux → Альтернатива: Linux-служба](./tmux#linux-service), плюс предварительные проверки и диагностику сбоев, которые легко упустить при ручном написании unit-файла.

## <a name="download"></a>Загрузка

Загрузите файл skill и сохраните его в локальный каталог skills Claude Code:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Или загрузите вручную: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — поместите файл в `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>Что делает skill

При вызове skill проводит Claude Code через полную установку:

1. Проверяет, что хост работает на Linux с `systemd`.
2. Определяет абсолютный путь к `spck` (избегает несоответствия `PATH`, которое ломает `ExecStart`).
3. Предупреждает, если `node` установлен через `nvm` — эти пути меняются при каждом обновлении Node и незаметно ломают unit.
4. Подтверждает, что `~/.spck-editor/.credentials.json` существует (CLI должна быть запущена в интерактивном режиме хотя бы один раз до запуска в качестве службы).
5. Выбирает между **пользовательской службой** (`systemctl --user`, без `sudo`) и **системной службой** в зависимости от ваших потребностей.
6. Записывает unit-файл с заполненными реальными путями — без заполнителей.
7. Выполняет `daemon-reload`, `enable --now`, затем отслеживает журнал, чтобы убедиться, что CLI подключилась к relay-серверу.

Skill также документирует семь наиболее распространённых режимов сбоя (неверный путь `ExecStart`, отсутствующие учётные данные, ошибки прав доступа в каталоге проекта, циклы перезапуска при достижении `start-limit-hit`, устаревшие пути nvm после обновления npm и т.д.), чтобы Claude Code мог диагностировать неисправную службу, а не просто регенерировать unit-файл.

## <a name="installation"></a>Установка

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Шаг 1 — Загрузите файл skill:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Шаг 2 — Убедитесь, что Claude Code обнаружил skill:**

```bash
claude /skills
```

В списке должен появиться `spck-cli-service`. Если нет, перезапустите Claude Code, чтобы он пересканировал каталог skills.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop загружает skills из того же каталога `~/.claude/skills/` на macOS и Linux. В Windows путь — `%USERPROFILE%\.claude\skills\`, но сама skill работает только на Linux-хостах, поэтому устанавливайте её на машину, где вы хотите запускать `spck`, а не на машину с Claude Desktop.

Если вы управляете удалённым Linux-сервером, запустите Claude Code по SSH на этом сервере (или через терминал Spck CLI, который предоставляет полный доступ к оболочке сервера). Установка skill на локальный Mac не поможет настроить удалённую Linux-службу.

</div>
  </div>
</div>

## <a name="usage"></a>Использование

После установки вызывайте skill, обращаясь к Claude Code на естественном языке. Примеры запросов, которые запустят skill:

- «Установи spck как службу systemd»
- «Сделай так, чтобы Spck CLI запускалась при загрузке»
- «Мой spck-cli.service постоянно перезапускается, можешь это отладить?»
- «Запусти spck как демон, чтобы он продолжал работать после разрыва SSH»

Claude Code прочитает skill, выполнит предварительные проверки (с запросом одобрения каждой команды), а затем сгенерирует и установит unit-файл. Просматривайте каждую команду перед одобрением — особенно те, что пишут в `/etc/systemd/system/` под `sudo`.

## <a name="what-gets-installed"></a>Что устанавливается

Skill устанавливает один unit-файл. Для пользовательской службы:

```bash
~/.config/systemd/user/spck-cli.service
```

С содержимым вида:

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

Для системной службы файл размещается в `/etc/systemd/system/spck-cli.service` и содержит дополнительные директивы `User=` и `Group=`. Skill выбирает подходящий вариант в зависимости от вашей среды и записывает реальные абсолютные пути в файл.

## <a name="why-a-skill-instead-of-copy-paste"></a>Почему skill, а не копировать-вставить?

Unit-файл в [документации tmux](./tmux#linux-service) — это лишь отправная точка, но для работы службы нужно правильно настроить несколько вещей:

- `ExecStart` должен быть **абсолютным путём** к `spck`. `which spck` внутри login shell разрешает манипуляции PATH из `.bashrc`, которые systemd не видит.
- Если `spck` установлен под `nvm`, путь содержит версию Node — обновление Node незаметно ломает службу до следующей перезагрузки.
- CLI должна быть запущена в интерактивном режиме хотя бы один раз для создания `~/.spck-editor/.credentials.json`. Новый запуск службы без учётных данных завершается корректно без очевидной ошибки.
- `User=` должен быть владельцем `WorkingDirectory`, иначе мониторинг файлов получает `EACCES` и CLI входит в цикл перезапусков.
- Пользовательские службы требуют `loginctl enable-linger` на headless-серверах, иначе они работают только при активной сессии входа.

Skill кодирует всё это, чтобы вам не нужно было это запоминать.

## <a name="uninstall"></a>Удаление

Отключить и удалить службу:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Для системной службы:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Чтобы удалить саму skill из Claude Code:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Смотрите также

- [Использование Tmux](./tmux) — альтернативный подход с использованием `tmux` для поддержания работы CLI при разрывах SSH.
- [Расширенное использование](./cli-advanced) — полный справочник команд CLI, переопределения конфигурации и настройки нескольких проектов.
- [Конфигурация](./cli-config) — настройки терминала, файловой системы, безопасности и аутентификации, не охватываемые unit-файлом.
