# <a name="tmux"></a>Использование Tmux со Spck CLI

Tmux (терминальный мультиплексор) позволяет сессиям терминала работать независимо от окна или SSH-соединения, которое их запустило. Для пользователей Spck CLI это означает возможность сохранять сессии при переподключениях, передавать запущенную сессию агента между десктопом и мобильным устройством, а также постоянно держать CLI запущенной на удалённом сервере даже после разрыва SSH-соединения.

## <a name="installation"></a>Установка

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux работает нативно на Linux. В Windows используйте [Подсистему Windows для Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install), а затем установите tmux внутри WSL.

**Шаг 1 — Установите WSL (PowerShell с правами администратора):**

```powershell
wsl --install
```

**Шаг 2 — Откройте терминал WSL и установите tmux:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Сценарий 1: Общий доступ к сессиям агента между десктопом и мобильным устройством

Самый мощный рабочий процесс tmux со Spck CLI — запустить агента ИИ для написания кода на десктопе и продолжить работу с мобильного устройства, или наоборот. Оба клиента видят абсолютно одинаковое состояние терминала, включая полную историю прокрутки.

### Запуск сессии на десктопе

Создайте именованную сессию tmux:

```bash
tmux new -s code
```

Запустите агента ИИ внутри сессии:

```bash
claude
```

Агент работает внутри tmux. Отсоединитесь в любой момент, нажав **Ctrl+B**, затем **D** — сессия и всё, что в ней выполняется, продолжит работу в фоне.

### Подключение с мобильного устройства

1. Откройте Spck Editor и подключитесь к серверу CLI
2. Откройте терминал из панели терминала Spck Editor
3. Присоединитесь к запущенной сессии tmux:

```bash
tmux attach -t code
```

Вы увидите ровно тот же терминал, что и на десктопе — включая запущенного агента, его вывод и полную историю прокрутки. Несколько клиентов могут подключаться одновременно и видеть вывод в реальном времени.

### Возврат на десктоп

Переподключитесь с любого терминала в любое время:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Сценарий 2: Постоянная работа CLI на удалённом сервере

Если вы запускаете Spck CLI на удалённом сервере через SSH, CLI останавливается в момент завершения SSH-сессии — при закрытии ноутбука, потере Wi-Fi или истечении таймаута соединения. Tmux удерживает процесс запущенным на сервере вне зависимости от состояния соединения.

### Настройка на удалённом сервере

Подключитесь к серверу по SSH и запустите именованную сессию tmux перед запуском CLI:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

CLI теперь работает внутри tmux на сервере. Закройте SSH-соединение или полностью потеряйте его — CLI продолжит работу.

### Переподключение после разрыва соединения

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLI возобновляет работу ровно с того места, где остановилась. Мобильные клиенты могут переподключаться через relay-сервер в обычном режиме.

### Список активных сессий

```bash
tmux ls
```

## <a name="linux-service"></a>Альтернатива: Linux-служба

Для полностью автоматизированной настройки, при которой CLI запускается при загрузке без ручного управления tmux, запустите Spck CLI как службу systemd.

### Создание файла службы

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Замените `your-username` и `/path/to/your/project` на реальные значения. Если `spck` установлен глобально (`npm install -g spck`), замените `ExecStart` на вывод команды `which spck`.

### Включение и запуск

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Проверка статуса и журналов

```bash
# Просмотр статуса
sudo systemctl status spck-cli

# Слежение за журналом в реальном времени
journalctl -u spck-cli -f
```

Служба запускается автоматически при каждой перезагрузке и перезапускается при сбое процесса.

## <a name="essential-tmux-commands"></a>Основные команды Tmux

| Команда | Действие |
| --- | --- |
| `tmux new -s name` | Создать новую именованную сессию |
| `tmux attach -t name` | Присоединиться к существующей сессии |
| `tmux ls` | Вывести список всех сессий |
| `tmux kill-session -t name` | Завершить сессию |
| Ctrl+B, D | Отсоединиться от сессии (продолжает работу) |
| Ctrl+B, C | Создать новое окно |
| Ctrl+B, N | Перейти к следующему окну |
| Ctrl+B, P | Перейти к предыдущему окну |
| Ctrl+B, [ | Войти в режим прокрутки (стрелки / PgUp / PgDn) |
| Q | Выйти из режима прокрутки |
