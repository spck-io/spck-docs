# <a name="git-support"></a>Git-Unterstützung

Spck unterstützt Git für lokale Projekte auf Android und iOS, im Browser und für entfernte Projekte über Spck CLI. Diese Anleitung behandelt Anbieter-Zugangsdaten, Pull Requests, Commit-Ansichten, das Auflösen von Konflikten und Plattformbeschränkungen.

Die grundlegende Git-Integration, der Commit-Verlauf und das Auflösen von Merge-Konflikten sind in der kostenlosen Version verfügbar. Die [erweiterte Git-Integration](#enhanced-git-integration) ergänzt Pull-Request-Verwaltung und Datei-Diffs von Commits.

## <a name="git-credentials"></a>Git-Zugangsdaten und Pull Requests

Öffnen Sie **Git menu → Git Credentials**, wählen Sie Ihren Anbieter und speichern Sie dessen Zugriffstoken. Die folgenden Einrichtungs- und Hilfelinks öffnen einen neuen Tab, damit Sie anschließend zu Spck zurückkehren und das Token einfügen können.

| Anbieter | Token-Einrichtung | Berechtigungen für Git und Pull Requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">GitHub-Token erstellen</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Einrichtungsanleitung</a> | Wählen Sie das Repository. Der Link wählt **Contents: Read and write**, **Pull requests: Read and write** sowie **Metadata: Read** vor. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">GitLab-Token erstellen</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Einrichtungsanleitung</a> | Der Link wählt den Bereich `api` für Merge Requests vor. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">API-Token erstellen</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Einrichtungsanleitung</a> | Wählen Sie **Create API token with scopes**, dann **Bitbucket** und manuell `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket` und `write:pullrequest:bitbucket`. Die API-Anmeldung verwendet die E-Mail-Adresse Ihres Atlassian-Kontos. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">PAT-Anleitung</a> | Öffnen Sie in Ihrer Organisation **User settings → Personal access tokens → New Token**, wählen Sie die Organisation und manuell **Code (Read & write)**. |

Zum Erstellen eines Pull Requests committen und pushen Sie den Quellbranch und öffnen dann **Git menu → Create PR**. Wählen Sie Remote und Zugangsdaten, einen anderen Zielbranch sowie Titel und Beschreibung. **Generate with AI** kann anhand der committeten Änderungen seit dem gemeinsamen Vorfahren der Branches einen Entwurf erstellen; fetchen Sie den Zielbranch zuvor. Prüfen Sie den Entwurf, bevor Sie **Create PR** wählen. GitLab erstellt einen Merge Request.

Das Erstellen und Verwalten von Pull Requests ist eine **Premium-Funktion** der [erweiterten Git-Integration](#enhanced-git-integration). Lite enthält sie mit dem einmaligen App-Kauf. Melden Sie sich in der Vollversion mit einem aktiven Supporter-, Gold- oder Node-Abonnement oder dem Konto mit dauerhaft freigeschaltetem Spck-for-NodeJS-Terminal an.

## <a name="pull-request-management"></a>Pull Requests verwalten (Premium)

Verwalten Sie Pull Requests direkt im Editor. Unterstützte Remotes sind **GitHub.com, GitLab.com, Bitbucket Cloud und Azure DevOps**; bei GitLab heißen sie Merge Requests.

1. Öffnen Sie ein Git-Projekt und hinterlegen Sie das Anbieter-Token unter **Git menu → Git Credentials** mit den oben genannten Berechtigungen.
2. Öffnen Sie **Git menu → Pull Requests** und wählen Sie Remote und Zugangsdaten, um offene Anfragen aufzulisten.
3. Wählen Sie eine Anfrage für Titel, Beschreibung, Autor, Quell- und Zielbranch sowie Status.
4. Wählen Sie eine geänderte Datei, um vor dem Zusammenführen ihren schreibgeschützten Diff zu prüfen.
5. Mit **Merge** führen Sie eine geeignete Anfrage zusammen; **Close** schließt sie ohne Merge. Erforderliche Reviews, Prüfungen, Token-Berechtigungen und Branch-Regeln gelten weiterhin. Entwürfe und Anfragen mit Konflikten können in diesem Dialog nicht zusammengeführt werden.

Mit **Refresh** laden Sie die Liste nach Änderungen beim Anbieter neu. Die Details verlinken auch zum Anbieter für Reviews, Prüfungen und weitere Aktionen.

Eine neue Anfrage erstellen Sie wie oben über **Git menu → Create PR**. Muss der Quellbranch noch gepusht werden, bietet der Dialog zuvor **Push** an. Optionale KI-Entwürfe nutzen Ihren konfigurierten KI-Dienst und dessen Nutzungslimits; sie sind vom Pull-Request-Zugriff in Lite unabhängig.

Scheitert das Erstellen an Token-Berechtigungen, erstellen oder aktualisieren Sie das Token über den Anbieterlink, speichern Sie es unter **Git Credentials** und versuchen Sie es erneut. Ihr PR-Entwurf bleibt erhalten.

## <a name="enhanced-git-integration"></a>Erweiterte Git-Integration

Die erweiterte Git-Integration ergänzt zwei Werkzeuge zum Prüfen und Teilen von Änderungen:

- **Pull-Request-Verwaltung:** Anfragen erstellen, offene Anfragen durchsuchen, Dateien und Diffs prüfen sowie Anfragen zusammenführen oder schließen. Einrichtung und Schritte finden Sie unter [Pull Requests verwalten](#pull-request-management).
- **Commit-Ansicht:** Geänderte Dateien eines Commits und deren Diffs prüfen, ohne Arbeitsdateien zu verändern.

Öffnen Sie im Git-Bereich **History** und wählen Sie einen Commit für dessen hinzugefügte, geänderte und gelöschte Dateien. Eine Datei öffnet einen schreibgeschützten Diff zum ersten Eltern-Commit. Beim ersten Commit wird mit einem leeren Baum verglichen. Der Viewer verwendet committete Versionen; nicht committete Änderungen beeinflussen den Diff nicht. Binärdateien können nicht als Text-Diffs angezeigt werden.

Alternativ können Sie einen Verlaufseintrag lange drücken oder mit der rechten Maustaste anklicken und **View Commit** wählen.

Die erweiterte Git-Integration ist enthalten in:

- **Spck Editor Lite:** dauerhaft durch den einmaligen App-Kauf freigeschaltet, ohne Anmeldung.
- **Dauerkauf des Spck-for-NodeJS-Terminals:** dauerhaft für das kaufende Konto freigeschaltet; Anmeldung erforderlich.
- **Supporter-, Gold- oder Node-Abonnements:** während des aktiven Abonnements freigeschaltet; Anmeldung erforderlich.

Grundlegende Git-Funktionen und der Commit-Verlauf bleiben in der kostenlosen Version verfügbar. Einzelheiten finden Sie unter [Preise](https://spck.io/pricing).

## <a name="merge-conflict-resolution"></a>Merge-Konflikte auflösen

Der Diff-Viewer hilft auch beim Auflösen von Konflikten in Arbeitsdateien. Dies gehört zur grundlegenden Git-Integration und erfordert kein Premium.

1. Öffnen Sie eine Datei mit Konflikten aus der Git-Änderungsliste.
2. Wählen Sie für jeden Konflikt **Accept Current**, **Accept Incoming** oder **Accept Both**. Sie können Änderungen auch manuell in der Datei zusammenführen.
3. Prüfen Sie das Ergebnis. Sobald alle Konfliktmarkierungen entfernt sind, wählen Sie im Diff-Viewer **Resolve**, um die aufgelöste Datei zu stagen.
4. Lösen Sie weitere Dateien auf und committen Sie anschließend den Merge.

Auf Touch-Geräten öffnen Sie Kontextmenüs durch langes Drücken auf Dateien oder Git-Einträge. Git-Statusbuchstaben ergänzen die Dateinamenfarben, damit Änderungen leichter zu erkennen sind.

## <a name="git-limitations"></a>Git-Einschränkungen

### <a name="git-limitations-overview"></a>Überblick

Die Git-Implementierung richtet sich nach dem Speicherort des Projekts und der verwendeten Spck-Version:

| Umgebung | Git-Implementierung | Wesentliche Einschränkungen |
| --- | --- | --- |
| Android- und iOS-Apps, einschließlich Lite und Spck for NodeJS | Nativ kompilierte **libgit2** für lokale Projekte | Projekt im Gerätespeicher erforderlich; Geräteressourcen und Dateisystembeschränkungen gelten weiterhin. |
| Browser und eingebetteter Editor | [isomorphic-git](https://isomorphic-git.org/) in JavaScript | Speicher-, Ablage- und Netzwerkgrenzen des Browsers. |
| Entfernte Projekte über Spck CLI | **Git-Binary** des Hostrechners | Ressourcen, Dateisystem, Zugangsdaten und Git-Installation des Hosts. |

Aktuelle mobile Versionen nutzen natives Git anstelle der Browser-Engine. Meldet eine lokale Operation **Native Git requires a device folder**, verschieben Sie das Projekt in den Gerätespeicher. Projekte, die nur in der Browserdatenbank des Editors liegen, können den mobilen nativen Git-Client nicht verwenden.

Die Pull-Request-Verwaltung ruft die Anbieter-API direkt mit dem unter **Git Credentials** gespeicherten Token auf. Browser-Anmeldecookies werden nicht verwendet; API-Antworten werden nicht zwischengespeichert, damit eine Aktualisierung aktuelle Anfrage- und Branch-Informationen abruft. Siehe [Git-Zugangsdaten und Pull Requests](#git-credentials) für Berechtigungen und [Pull Requests verwalten](#pull-request-management) für Anbieter und Aktionen.

### <a name="git-limitations-memory"></a>Speicherbeschränkungen

- Natives Git auf Android und iOS führt Repository-Operationen außerhalb der JavaScript-Git-Engine aus. Deren Speichergrenzen sind keine feste Grenze für mobiles Git.
- Natives Git benötigt weiterhin freien Arbeitsspeicher und Speicherplatz. Große Repositories oder Pack-Dateien können die Geräteressourcen überschreiten und Fehler oder eine Beendigung der App durch das Betriebssystem verursachen.
- Browser-Git unterliegt weiterhin den JavaScript-Speicher- und Ablagegrenzen des Browsers. Große Pack-Dateien können viel Speicher benötigen, sodass Klonen oder Fetchen fehlschlägt.

> 💡 **Tipp:** Verwenden Sie für große Repositories nach Möglichkeit flache Klone oder arbeiten Sie mit einem kleineren Teil des Repositorys.

### <a name="git-limitations-symlinks"></a>Symlink-Kompatibilität

- Browserablage und Geräte-Dateisystemschicht des Editors verwenden **emulierte Symlinks** für Repositories mit symbolischen Links.
- Der Wechsel zu libgit2 auf Mobilgeräten hebt Dateisystembeschränkungen nicht auf und garantiert keine echten Betriebssystem-Symlinks.
- Emulierte Links können sich bei Build-Werkzeugen, Paketmanagern oder Skripten anders verhalten, wenn diese echte Links erwarten und Ziele zur Laufzeit auflösen.
- Verwenden Sie für Projekte mit echten Symlinks ein entferntes Projekt auf einem Host mit geeignetem Dateisystem und den nötigen Berechtigungen.

### <a name="git-limitations-cli"></a>Die CLI als Alternative

Verwenden Sie für große Repositories oder Abläufe, die Dateisystem und Git-Werkzeuge des Hosts benötigen, ein **entferntes Projekt über Spck CLI**. Git-Operationen laufen dann mit der **Git-Binary des Hosts**, während Sie Dateien in Spck bearbeiten:

- Operationen nutzen Arbeitsspeicher und Laufwerk des Hosts statt der Ressourcen von Mobilgerät oder Browser.
- Symlinks richten sich nach Dateisystemunterstützung und Berechtigungen des Host-Betriebssystems.
- Verwenden Sie die Git-Werkzeuge des Hosts für Befehle, die die Git-Bedienelemente des Editors nicht anbieten.

Unter [Erste Schritte mit Spck CLI](./cli-start) erfahren Sie, wie Sie einen Host verbinden. Entfernte Projekte benötigen ein Spck-Konto und unterliegen den Zugriffsgrenzen Ihres Tarifs; siehe [Entfernte Projekte](./editor-lite#remote-projects) zu den Abonnementanforderungen von Lite. Beim Klonen in den Gerätespeicher kommt weiterhin der native Git-Client der mobilen App zum Einsatz.

## <a name="git-related-guides"></a>Weiterführende Anleitungen

- [Screenreader-Unterstützung (experimentell)](./screen-reader-support): barrierefreie Navigation, Versionskontrolle und Feedback.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): Git-Werkzeuge des einmaligen App-Kaufs.
- [Erste Schritte mit Spck CLI](./cli-start): ein entferntes Projekt verbinden und Git-Werkzeuge des Hosts nutzen.
