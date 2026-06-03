# <a name="ai-coding-agents-acp"></a>KI-Programmieragenten auf dem Mobilgerät (ACP)

Führen Sie **Claude Code**, **OpenAI Codex** oder **Gemini CLI** direkt von Ihrem Smartphone aus über den **AI Chat** des Spck Editors aus. Die Spck CLI verbindet Ihren Editor über das offene [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) mit lokal installierten Agenten-CLIs, sodass das Modell auf Ihrem Rechner, mit Ihrem Abo, gegen Ihre echten Dateien läuft — während Sie es vom Mobilgerät aus überwachen.

![ACP-Modus für lokale KI im AI Chat des Spck Editors, der Claude Code auf einem Desktop von einem Smartphone aus steuert](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>Was ist ACP und warum sollte man es nutzen?

Das Agent Client Protocol (ACP) ist ein offener Standard von Zed Industries für die Kommunikation zwischen Editor und KI-Agent, im selben Geist wie das Language Server Protocol (LSP). Spck CLI 0.6.0+ implementiert ACP und fungiert als **Transportschicht** zwischen dem AI Chat des Spck Editors (dem Client) und jedem ACP-fähigen Agenten-Binary, das Sie installiert haben (dem Agenten).

Im Vergleich zum serverbasierten AI Chat in der App bietet Ihnen der lokale ACP-Pfad:

- **Ihr eigenes Abo** — Agenten-Aufrufe werden Ihrem Claude Code / ChatGPT / Gemini-Konto in Rechnung gestellt, nicht Ihrem AI-Kontingent im Spck Editor.
- **Echter Dateisystemzugriff** — Agenten lesen und schreiben echte Dateien auf der Festplatte über die CLI, nicht die In-Memory-Kopien des Editors.
- **Native Tools** — Datei-Watcher, Language-Server und Shell-Befehle laufen auf Ihrem realen Rechner.
- **Kontinuität mit dem Desktop** — dasselbe `claude` / `gemini` / `codex` Login, das Sie am Schreibtisch verwenden, treibt auch den mobilen Chat an.

## <a name="acp-supported-agents"></a>Unterstützte KI-Agenten

Installieren Sie die Agenten, die Sie verfügbar haben möchten. Spck CLI erkennt sie automatisch beim Start.

| Agent             | Installation                                                                         |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>Installation und Einrichtung

### 1. Spck CLI installieren

Falls Sie es noch nicht haben:

```bash
npm install -g spck
# oder ohne Installation ausführen
npx spck
```

Siehe [Erste Schritte mit der Spck CLI](./cli-start) für den vollständigen Erstkonfigurations-Assistenten.

### 2. Einen oder mehrere Agenten-CLIs installieren

Wählen Sie die gewünschten Agenten. Sie können mehrere installieren — der AI Chat lässt Sie pro Sitzung zwischen ihnen wählen. In der Tabelle [Unterstützte KI-Agenten](#acp-supported-agents) oben finden Sie die Installationsbefehle.

### 3. Jeden Agenten einmal authentifizieren

Die Agenten-CLIs verwalten ihre eigenen Logins außerhalb des Spck Editors:

```bash
claude            # Anthropic Claude Code Login-Flow
codex login       # OpenAI Codex Login-Flow (von codex-acp verwendet)
gemini            # Google Gemini Login-Flow
```

Wenn Sie diesen Schritt überspringen, zeigt der Spck Editor beim ersten Start eines Chats eine Fehlermeldung wie `ACP agent requires authentication; run <binary> login and retry` an.

### 4. Spck CLI starten

```bash
cd /path/to/your/project
spck
```

Beim Start gibt die CLI einen Erkennungsbericht pro Agent aus, der auflistet, welche Agenten verfügbar sind, gefolgt von einer einzeiligen Zusammenfassung wie `✅ ACP agents: Claude Code, Gemini CLI` im Hauptbereich der Funktionen. Wenn nichts verfügbar ist, fällt es stattdessen auf den serverbasierten AI Chat zurück.

### 5. Spck Editor verbinden

Scannen Sie den QR-Code oder verwenden Sie die [manuelle Eingabe](./cli-start#connecting). Sobald die Verbindung steht, öffnen Sie den **AI Chat** im Spck Editor — der Transportumschalter zeigt die lokalen Agenten neben der Cloud-Option an.

## <a name="acp-authentication"></a>Authentifizierung

Jeder Agent verwaltet seine eigenen Zugangsdaten auf dem Rechner, auf dem die Spck CLI läuft. Führen Sie den Login-Flow einmal pro Agent aus:

```bash
# Claude Code
claude

# Codex (codex-acp nutzt das eigene Login der Codex-CLI)
codex login

# Gemini CLI
gemini
```

Wenn Sie neu installieren oder den Rechner wechseln, wiederholen Sie das Login auf dem neuen Host. Die Authentifizierung erfolgt **pro Host, pro Agent** — der Spck Editor selbst speichert diese Zugangsdaten niemals.

## <a name="acp-billing"></a>Abrechnung und Ratenlimits

Da ACP den Agenten auf Ihrem Rechner mit Ihren eigenen Zugangsdaten ausführt, **wird die gesamte Nutzung Ihrem Konto bei diesem Anbieter in Rechnung gestellt** — nicht Ihrem Spck-Editor-Abo. Spck Editor und die Spck-Relay-Server fungieren in diesem Modus als reine Transportschicht und verbrauchen kein AI-Kontingent in der App für ACP-Verkehr.

### Claude Code Abrechnung

> ⚠️ **Wichtig — Claude Code wendet ein separates Ratenlimit-Kontingent an, wenn es von Drittanbieter-Tools angesteuert wird.**
>
> Wenn Claude Code von einem Drittanbieter-Client über ACP aufgerufen wird, zählt Anthropic diesen Verkehr gegen ein **anderes Ratenlimit-Kontingent** als Ihre interaktiven `claude` CLI-Sitzungen mit einem Pro / Max-Abo. Praktische Konsequenz: Sie können das Drittanbieter-Kontingent ausschöpfen, während Sie noch interaktiven Claude-Code-Spielraum haben (oder umgekehrt), und Sie können sie nicht zusammenführen.
>
> Prüfen Sie `/usage` innerhalb von `claude` und die [Anthropic Console](https://platform.claude.com/usage), um Ihren aktuellen Verbrauch zu sehen, und beachten Sie die [Claude Code Kosten- und Limit-Dokumentation](https://code.claude.com/docs/en/costs) für die Zahlen, die zu Ihrem Tarif gehören.

### Codex (codex-acp) Abrechnung

Abgerechnet über das eigene Auth der OpenAI Codex CLI — Ihren OpenAI API-Schlüssel oder ChatGPT-Login. Die Nutzung zählt gegen den Tarif dieses Kontos. Preise und Kontingente entsprechen der interaktiven `codex`-Nutzung; siehe [openai.com/codex](https://github.com/openai/codex) und Ihr OpenAI-Dashboard für aktuelle Zahlen.

### Gemini CLI Abrechnung

Abgerechnet über Ihr Google-Konto oder Ihren Gemini-API-Schlüssel. Die Nutzung zählt gegen den Gemini-Tarif oder das API-Kontingent dieses Logins. Siehe [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) für Ratenlimit-Details.

## <a name="acp-configuration"></a>Konfiguration

ACP ist standardmäßig aktiviert und wird über die `spck-cli.config.json` des Projekts konfiguriert:

```json
{
  "acp": {
    "enabled": true
  }
}
```

Siehe [Konfiguration → ACP-Einstellungen](./cli-config#acp-settings) für das vollständige Schema.

### ACP pro Projekt deaktivieren

Wenn Sie nicht möchten, dass der Spck Editor einen lokalen Agenten auf diesem Host steuern kann:

```json
{
  "acp": {
    "enabled": false
  }
}
```

Bei Deaktivierung versteckt der Transportumschalter des Editors die lokale Agenten-Option und jeder `acp.*`-RPC wird mit `FEATURE_DISABLED` abgelehnt. Der Einrichtungsassistent stellt diese Frage beim ersten Start (Standard `Y`); Konfigurationen, die der Option vorausgehen, werden automatisch mit `acp.enabled: true` geladen und neu gespeichert.

### Einen einzelnen Agenten deaktivieren

Um einen _bestimmten_ Agenten nicht mehr anzubieten und ACP für die anderen aktiviert zu lassen, deinstallieren Sie das Binary dieses Agenten. Die Erkennung läuft bei jedem CLI-Start, sodass der Transportumschalter des Editors ihn aus der Liste entfernt.

## <a name="acp-vs-server-routed"></a>Lokales ACP vs. serverbasierter AI Chat

| Fähigkeit                            | Serverbasiert (Standard, ohne CLI) | Lokal (ACP, CLI verbunden)              |
| ------------------------------------ | ---------------------------------- | --------------------------------------- |
| Wo das Modell läuft                  | Spck Cloud                         | Ihr Rechner                             |
| Zugangsdaten                         | Ihr Spck-Editor-Konto              | Das eigene Login / der API-Schlüssel des Agenten |
| Dateizugriff                         | In-Memory-Dateisystem des Editors  | Echte Dateien auf der Festplatte über das CLI-Root |
| Zählt gegen AI-Kontingent des Spck Editors | Ja                           | **Nein** — wird beim Agenten-Anbieter abgerechnet |
| Funktioniert ohne laufende CLI       | Ja                                 | Nein (CLI + WebSocket erforderlich)     |
| Verfügbare Agenten                   | Spck-gehostete Modelle             | Claude Code, Codex, Gemini CLI          |
| Tool-Berechtigungsabfragen auf dem Smartphone | Wo zutreffend             | Ja, über ACP weitergeleitet             |
| Token-Streaming                      | Ja                                 | Ja                                      |
| Multi-Turn-Chat                      | Ja                                 | Ja                                      |

Sie können den Transport mitten im Projekt wechseln — der AI Chat zeigt jeweils diejenigen Pfade an, die basierend auf dem CLI-Verbindungsstatus und den erkannten Agenten verfügbar sind.

## <a name="acp-tmux"></a>Pairing mit Tmux für langlaufende Sitzungen

ACP-Sitzungen bleiben über Editor-Reconnects hinweg bestehen, aber der Spck-CLI-Prozess selbst endet, wenn sein Terminal geschlossen wird. Für langlaufende Agentenarbeit — große Refactorings, mehrstündige Planungssitzungen — starten Sie die CLI in einer [tmux](./tmux)-Sitzung, damit sie SSH-Abbrüche, Terminal-Schließungen und Laptop-Schlafmodi überlebt:

```bash
tmux new -s spck
spck
# Ctrl+B dann D zum Lösen
```

Sie können sich auch von Ihrem Smartphone aus über das Spck-CLI-Terminal wieder verbinden und mit `tmux attach -t spck` den Agenten live überwachen. Siehe [Tmux verwenden](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) für das vollständige Muster, einschließlich des Betriebs der CLI als dauerhafter Hintergrunddienst.

Für Linux-Hosts bietet die Seite [Claude Skill: Linux Service](./claude-skill) eine Ein-Befehl-Einrichtung, um die Spck CLI als `systemd`-Dienst zu betreiben, sodass die WebSocket — und alle ACP-Sitzungen darauf — beim Booten automatisch starten.

## <a name="acp-faq"></a>Häufig gestellte Fragen

### Kann ich Claude Code auf meinem Smartphone nutzen?

Ja. Installieren Sie Claude Code auf Ihrem Desktop, authentifizieren Sie sich mit `claude`, und starten Sie dann `spck` in Ihrem Projekt. Verbinden Sie den Spck Editor von Ihrem Smartphone aus und wählen Sie Claude Code im Transportumschalter des AI Chats. Das Modell läuft auf Ihrem Desktop mit Ihrem Abo; Sie steuern es vom Smartphone aus.

### Sieht der Spck Editor meinen Claude / OpenAI / Gemini API-Schlüssel?

Nein. Jede Agenten-CLI verwaltet ihre eigenen Zugangsdaten auf dem Rechner, auf dem die Spck CLI läuft. ACP-Nachrichten werden über die verschlüsselte WebSocket-Verbindung zwischen Smartphone und CLI getunnelt, aber die eigenen Auth-Tokens des Agenten verlassen Ihren Host niemals.

### Gibt es zusätzliche Kosten für die Nutzung von Claude Code über den Spck Editor?

Keine zusätzlichen Spck-Editor-Gebühren. Die Nutzung des Agenten zählt gegen Ihren Anthropic- / OpenAI- / Google-Tarif genauso, als würden Sie den Agenten interaktiv am Schreibtisch nutzen — außer dass Anthropic ein separates Ratenlimit-Kontingent für Drittanbieter-Clients anwendet; siehe [Abrechnung und Ratenlimits](#acp-billing) oben.

### Brauche ich ein bezahltes Spck-Editor-Abo, um ACP zu nutzen?

Nein. Die kostenlose Stufe (30 Min/Tag CLI-Verbindung) reicht aus, um jeden ACP-Agenten anzusteuern. Nur der serverbasierte AI Chat in der App verbraucht das Spck-Editor-AI-Kontingent.

### Was passiert, wenn ich meine WLAN-Verbindung mitten im Chat verliere?

Der Agentenprozess bleibt auf dem CLI-Host am Leben. Wenn der Editor sich wieder verbindet, wird die Sitzung mit vollständigem Chatverlauf fortgesetzt. Streaming-Ausgaben, die ankamen, während Sie offline waren, werden bei der erneuten Verbindung wiedergegeben.

### Kann ich Agenten auf einem Remote-Server statt auf meinem Laptop ausführen?

Ja. Führen Sie die Spck CLI auf jedem erreichbaren Linux/macOS-Host aus — einer Dev-VM, einem Heimserver, einer Workstation — und verbinden Sie sich über den Relay-Server. Kombinieren Sie es mit [tmux](./tmux) oder dem [systemd-Skill](./claude-skill), um die CLI zwischen Verbindungen am Leben zu halten.

### Funktioniert ACP mit dem Spck Editor Lite?

Ja. ACP-Verkehr nutzt denselben WebSocket-Transport wie Dateisystem und Git, was Spck Editor Lite unterstützt. Stellen Sie sicher, dass `security.userAuthenticationEnabled` in Ihrer CLI-Konfiguration auf `false` gesetzt ist — Firebase-Auth wird in Lite nicht unterstützt. Siehe [Konfiguration → Benutzerauthentifizierung](./cli-config#user-authentication).

### Warum erscheint mein Agent nicht im AI Chat?

Prüfen Sie das CLI-Startup-Log auf die Zeile pro Agent:

- Agent nicht erkannt — installieren Sie ihn (siehe [Unterstützte KI-Agenten](#acp-supported-agents)).
- Erkannt, aber fehlt im Editor — vergewissern Sie sich, dass Sie den eigenen Login-Flow des Agenten abgeschlossen haben (`claude`, `codex login`, `gemini`).
- ACP deaktiviert — prüfen Sie `acp.enabled` in `.spck-editor/config/spck-cli.config.json`. Siehe [Konfiguration](./cli-config#acp-settings).

## <a name="acp-troubleshooting"></a>Fehlerbehebung

### Agent erkannt, aber Sitzung startet nicht

Meistens bedeutet das, dass der Agent nicht authentifiziert ist. Führen Sie den Login-Flow des Agenten auf dem CLI-Host aus:

```bash
claude              # dann den Browser-Auth abschließen
codex login
gemini
```

Wenn das Problem weiter besteht, prüfen Sie die Logs der CLI in `.spck-editor/logs/` für die stderr-Ausgabe des Agenten, die normalerweise auf das fehlschlagende Auth oder Binary hinweist.

### Ratenlimit-Fehler während eines Chats

Bei Claude Code gibt der Editor die Anthropic-429-Meldung wortwörtlich weiter. Prüfen Sie die [Anthropic Console Nutzungsseite](https://platform.claude.com/usage) und die [Claude Code Kosten-Docs](https://code.claude.com/docs/en/costs) — denken Sie daran, dass das Drittanbieter-Ratenlimit-Kontingent von Ihrem interaktiven `claude`-Kontingent getrennt ist.

Bei Codex und Gemini gibt der Editor den eigenen Kontingentfehler des Anbieters weiter. Lösen Sie es über die Konsole des Anbieters.

### CLI stürzt beim Start einer ACP-Sitzung ab

Spck CLI loggt den ACP-Verkehr nach `.spck-editor/logs/`. Verfolgen Sie die neueste Log-Datei, während Sie das Problem reproduzieren:

```bash
tail -f .spck-editor/logs/spck-*.log
```

Melden Sie einen Bug unter [github.com/spck-editor](https://github.com/spck-editor) mit dem relevanten Ausschnitt.

### Agent ändert Dateien außerhalb des Projekt-Roots

ACP-Agenten sind auf das konfigurierte `root`-Verzeichnis der CLI beschränkt. Wenn Sie Schreibvorgänge außerhalb davon sehen, melden Sie ein Issue — das sollte nicht passieren. Als Workaround führen Sie `spck --root /path/to/specific/project` aus, um den Bereich weiter einzugrenzen.

## <a name="acp-see-also"></a>Siehe auch

- [Erste Schritte mit der Spck CLI](./cli-start) — installieren, authentifizieren und erstmals verbinden
- [CLI-Referenz](./cli) — Relay-Server, täglicher Workflow, Verbindungslimits
- [Konfiguration → ACP-Einstellungen](./cli-config#acp-settings) — die `acp.enabled`-Konfigurationsoption
- [Erweiterte Nutzung](./cli-advanced) — CLI-Flags, mehrere Projekte, Tipps für mobile Prompts
- [Tmux verwenden](./tmux) — ACP-Sitzungen über Reconnects hinweg am Leben halten
- [Claude Skill: Linux Service](./claude-skill) — Spck CLI als `systemd`-Dienst betreiben, sodass ACP immer verfügbar ist
- [Agent Client Protocol Spezifikation](https://agentclientprotocol.com/) — der offene Standard, den ACP implementiert
- [Claude Code Dokumentation](https://docs.claude.com/en/docs/claude-code/overview)
- [Gemini CLI Repository](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
