# 02 – Repository, Status und Änderungen

[← Zurück: Git verstehen](./01-git-verstehen.md) | [Weiter: Staging und Commits →](./03-staging-commits.md)

Im vorherigen Abschnitt hast du gelernt, was ein Repository ist und warum Git Änderungen verwaltet. Jetzt legen wir unser **eigenes lokales Übungsrepository** an und beobachten, wie Git auf neue und geänderte Dateien reagiert.

**Wichtig:** Für die Übungen benötigst du weder GitLab noch Programmierkenntnisse. Wir arbeiten ausschließlich in einem neuen Übungsordner – nicht im Repository dieses Tutorials und noch nicht am späteren CashFlow-Projekt.

## Ein lokales Übungsrepository anlegen

Öffne VS Code und lege in deinem Lernprojekt-Ordner einen neuen Ordner an:

```text
git-uebung/
```

Öffne **diesen Ordner** in VS Code. Öffne anschließend das integrierte Terminal und überprüfe, dass du dich im Ordner `git-uebung` befindest.

Initialisiere dort Git:

```bash
git init -b main
```

Damit wird der aktuelle Ordner zu einem Git-Repository. Git legt dafür einen versteckten Ordner namens `.git` an. Du musst ihn nicht öffnen oder bearbeiten.

Der Teil `-b main` legt `main` als Namen des ersten Branches fest. Falls deine Git-Version diese Option nicht unterstützt, kannst du stattdessen `git init` verwenden. Der erste Branch kann dann anders heißen. Das ist für diese Übung noch nicht entscheidend.

> **Achtung:** Führe `git init` nur im neu angelegten Ordner `git-uebung` aus. Wir wollen nicht versehentlich ein weiteres Repository innerhalb des Tutorials anlegen.

## Den Zustand mit `git status` prüfen

Führe im Terminal aus:

```bash
git status
```

`git status` zeigt dir unter anderem:

- den aktuellen Branch,
- ob es bereits Commits gibt,
- welche Dateien Git noch nicht verfolgt,
- welche Änderungen seit dem letzten gespeicherten Stand gemacht wurden,
- welche Änderungen für den nächsten Commit vorgemerkt sind.

Du wirst an dieser Stelle sinngemäß sehen, dass du auf `main` bist und noch keine Commits angelegt hast.

> **Tipp:** Wenn du bei Git nicht sicher bist, was gerade passiert, ist `git status` fast immer ein guter erster Schritt.

## Eine neue Datei erstellen

Erstelle in `git-uebung` die Datei:

```text
README.md
```

Schreibe beispielsweise hinein:

```md
# Meine Git-Übung

Hier lerne ich die Grundlagen von Git.
```

Speichere die Datei und führe erneut aus:

```bash
git status
```

Git sollte die Datei unter **Untracked files** anzeigen.

**Untracked** bedeutet: Die Datei existiert im Projektordner, aber Git verfolgt sie noch nicht als Teil eines Commits.

Die Datei ist trotzdem bereits auf deinem Rechner gespeichert. **Datei speichern** und **in Git committen** sind unterschiedliche Dinge.

## Eine untracked Datei bearbeiten

Ändere den Text in `README.md`, beispielsweise indem du einen weiteren Satz ergänzt. Speichere die Datei und führe `git status` erneut aus.

Die Datei bleibt zunächst **untracked**. Git kennt noch keinen vorherigen Commit dieser Datei, mit dem es ihren Inhalt vergleichen könnte.

Erst wenn wir Dateien in Git aufgenommen und einen Commit erstellt haben, können sie später als **modified** erscheinen. Das üben wir im nächsten Unterkapitel.

## Häufige Zustände im Überblick

| Begriff | Bedeutung |
|---|---|
| `untracked` | Eine neue Datei, die Git noch nicht verfolgt |
| `modified` | Eine bereits verfolgte Datei wurde verändert |
| `staged` | Änderungen wurden für den nächsten Commit ausgewählt |
| `committed` | Änderungen wurden in einem Commit der lokalen Git-Historie gespeichert |

Du musst noch nicht alle Zustände selbst erzeugen können. In diesem Kapitel beobachten wir vor allem **untracked**. Mit `git add` und `git commit` arbeiten wir als Nächstes.

## Aktuellen Branch anzeigen

`git status` nennt dir bereits den aktuellen Branch.

Du kannst außerdem verwenden:

```bash
git branch
```

**Besonderheit bei einem neuen Repository:** Solange du noch keinen ersten Commit angelegt hast, kann `git branch` noch keine Branch-Liste anzeigen. Das ist kein Fehler. Wir erstellen den ersten Commit im nächsten Abschnitt.

## Was ist `git clone`?

Du musst nicht immer ein leeres Repository anlegen. Wenn ein Repository bereits auf einem Git-Server liegt, kannst du es mit `git clone` lokal kopieren:

```bash
git clone <repository-url>
```

`<repository-url>` ist hier ein **Platzhalter**, kein Befehl zum direkten Kopieren. Die tatsächliche URL hängt vom jeweiligen Repository ab.

Zum Beispiel könnte ein geklontes Repository danach in einem neuen Unterordner liegen. Anders als bei `git init` übernimmst du mit `git clone` ein vorhandenes Repository mitsamt seiner Git-Historie.

Wir verwenden **jetzt bewusst `git init`**, damit die Übung vollständig lokal und unabhängig von einem GitLab-Zugang funktioniert. Das gemeinsame Arbeiten mit Remotes folgt später.

## Praxisaufgabe – Dein Übungsrepository

Führe die folgenden Schritte selbstständig aus. Du darfst in den vorherigen Abschnitten nachschlagen.

1. Erstelle und öffne den Ordner `git-uebung` in VS Code.
2. Initialisiere darin ein Git-Repository mit dem Branch-Namen `main` (sofern deine Git-Version dies unterstützt).
3. Prüfe den Repository-Status.
4. Erstelle eine Datei `README.md` mit einer Überschrift und einem kurzen Satz darüber, was du mit Git lernen möchtest.
5. Speichere die Datei und überprüfe ihren Status.
6. Ergänze einen weiteren Satz, speichere erneut und prüfe den Status noch einmal.
7. Erkläre, warum deine neue Datei weiterhin als `untracked` erscheinen kann.

**Noch nicht ausführen:** `git add` oder `git commit`. Diese Befehle behandeln wir im nächsten Unterkapitel. **Lass den Ordner und die Datei bestehen**, denn wir verwenden sie dort weiter.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten und notiere die Antworten an einem Ort deiner Wahl.

1. Was passiert bei `git init`?
2. Wozu dient `git status`?
3. Was bedeutet `untracked`?
4. Warum bleibt eine neue Datei zunächst `untracked`, auch wenn du sie in VS Code bearbeitest und speicherst?
5. Was ist der Unterschied zwischen `git init` und `git clone`?
6. Was ist der versteckte Ordner `.git`?
7. Warum kann `git branch` bei einem frisch initialisierten Repository noch keine Branch-Liste zeigen?

## Zusammenfassung

```text
Neuen Übungsordner öffnen
          ↓
git init -b main
          ↓
git status
          ↓
README.md erstellen und speichern
          ↓
git status → untracked
```

Du hast jetzt dein erstes lokales Git-Übungsrepository. Im nächsten Kapitel lernst du, wie du deine Änderungen mit **Staging und Commits** bewusst in der Git-Historie speicherst.

[Weiter: Staging und Commits →](./03-staging-commits.md)
