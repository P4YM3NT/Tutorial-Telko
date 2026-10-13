# 10 – .gitignore und sensible Daten

[← Zurück: Issues und Merge Requests](./09-issues-merge-requests.md) | [Weiter: Praxisworkflow →](./11-praxisworkflow.md)

In deinen bisherigen Git-Übungen hast du Dateien bewusst zu Commits hinzugefügt. Es gibt aber auch Dateien, die **nicht** in ein Repository gehören – etwa temporäre Dateien, installierte Pakete oder Zugangsdaten.

Dafür lernen wir jetzt `.gitignore` kennen. Außerdem sprechen wir über den sicheren Umgang mit sensiblen Daten. Für die Übungen verwenden wir **nur erfundene Beispielwerte**.

## Lernziele

Nach diesem Kapitel kannst du:

- erklären, was `.gitignore` bewirkt,
- häufig ignorierte Dateien und Ordner erkennen,
- `.gitignore` in deinem lokalen `git-uebung`-Repository verwenden,
- erklären, warum `.env` und `.env.example` unterschiedliche Aufgaben haben,
- verstehen, warum `.gitignore` **keine Sicherheitsgarantie** ist,
- beschreiben, was bei versehentlich committeden Zugangsdaten zu tun ist.

## 1. Was macht `.gitignore`?

Eine Datei namens `.gitignore` enthält Regeln für Dateien und Verzeichnisse, die Git bei der normalen Erkennung **nicht verfolgter Dateien** ignorieren soll.

Beispiel:

```gitignore
node_modules/
.env
dist/
```

- `node_modules/` – lokal installierte JavaScript-Pakete,
- `.env` – häufig lokale Konfiguration mit sensiblen Werten,
- `dist/` – häufig automatisch erzeugte Build-Dateien.

> **Wichtig:** Welche Einträge sinnvoll sind, hängt vom Projekt ab. Nicht jedes Projekt hat beispielsweise einen `dist/`-Ordner.

## 2. Warum ignorieren wir `node_modules/`?

Wenn du später mit npm Pakete installierst, entsteht normalerweise ein Ordner `node_modules/`. Dort liegen viele Dateien von Abhängigkeiten, die in der Regel nicht einzeln versioniert werden.

Stattdessen werden normalerweise `package.json` und eine passende Lock-Datei wie `package-lock.json` committed. Damit lässt sich nachvollziehen, welche Pakete benötigt werden.

```text
package.json       → normalerweise versionieren
package-lock.json  → normalerweise versionieren
node_modules/      → normalerweise ignorieren
```

Die genaue Verwendung lernst du später in den JavaScript- und Node.js-Kapiteln.

## 3. Was ist eine `.env`-Datei?

Eine `.env`-Datei kann Konfigurationswerte enthalten, die eine Anwendung einliest. Darunter können auch Geheimnisse sein.

Ein **rein erfundenes Beispiel**:

```dotenv
DATABASE_HOST=localhost
DATABASE_PASSWORD=BEISPIEL_NICHT_VERWENDEN
```

In einer echten Anwendung darf ein tatsächlich genutztes Passwort **nicht** in Git landen – auch nicht in einem privaten Repository.

Für CashFlow gilt zusätzlich: Wir üben mit **fiktiven Einnahmen und Ausgaben**, nicht mit echten privaten Finanzinformationen.

## 4. `.env.example` als Vorlage

Ein Team kann eine Datei `.env.example` ins Repository aufnehmen. Sie zeigt, welche Konfigurationswerte gebraucht werden, enthält aber **keine echten Zugangsdaten**.

```dotenv
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=
DATABASE_PASSWORD=
```

Später kann jeder Entwickler seine eigene lokale Konfiguration anlegen, ohne Geheimnisse zu veröffentlichen.

### Wichtig: `.env` und `.env.example` nicht verwechseln

```text
.env          → lokale Werte; häufig ignorieren
.env.example  → Vorlage ohne Secrets; häufig committen
```

## 5. `.gitignore` schützt keine bereits verfolgten Dateien

Ein wichtiger Punkt: `.gitignore` wirkt **nicht rückwirkend** auf Dateien, die Git bereits verfolgt.

Wenn eine Datei bereits eingecheckt wurde, bleibt sie in der Git-Historie vorhanden, selbst wenn du sie nachträglich zur `.gitignore` hinzufügst.

Für eine bereits verfolgte Datei kann man die Verfolgung im aktuellen Stand beispielsweise so beenden:

```bash
git rm --cached <datei>
```

`--cached` entfernt die Datei aus dem Git-Index, lässt die lokale Datei aber bestehen. Danach muss die Änderung noch committed werden. **Der alte Commit wird dadurch nicht aus der Historie gelöscht.**

> **Merke:** `.gitignore` ist eine Hilfe gegen versehentliches Hinzufügen, aber kein Schutzmechanismus für Geheimnisse, die schon veröffentlicht wurden.

## 6. Was tun, wenn ein echtes Secret versehentlich committed wurde?

Falls du versehentlich ein echtes Passwort, Token oder einen privaten Schlüssel committed hast:

1. **Nicht einfach weiterarbeiten und den Fehler ignorieren.**
2. **Informiere unverzüglich deine betreuende Person** beziehungsweise den zuständigen Sicherheitskontakt.
3. Das betroffene Secret muss normalerweise **widerrufen oder ausgetauscht** werden.
4. Gemeinsam wird geprüft, wo die Information bereits verfügbar sein könnte und ob weitere Maßnahmen nötig sind.

Nur das Löschen der Datei oder das Ergänzen der `.gitignore` macht ein kompromittiertes Secret nicht wieder sicher.

## 7. Kleine Praxisübung – `.gitignore` ausprobieren

Verwende dein **lokales** Repository `git-uebung` aus den bisherigen Kapiteln. Die Übung funktioniert ohne GitLab und ohne echte Passwörter.

**Vorbereitung:** Vergewissere dich mit `git status`, dass du im richtigen Repository bist und keine ungesicherten Änderungen aus früheren Aufgaben offen sind. Arbeite nicht im Ordner `git-uebung-remote.git` (dem Bare Repository aus Kapitel 07).

### Schritt 1 – `.gitignore` erstellen

Erstelle im Hauptordner von `git-uebung` eine Datei namens `.gitignore` mit folgendem Inhalt:

```gitignore
node_modules/
.env
dist/
```

### Schritt 2 – Testdateien anlegen

Erstelle zusätzlich:

```text
.env
.env.example
notizen.txt
```

Schreibe in `.env` **nur** diesen ungefährlichen Übungswert:

```dotenv
DEMO_MODE=true
```

Schreibe in `.env.example`:

```dotenv
DEMO_MODE=
```

Die Datei `notizen.txt` darf einen beliebigen kurzen Testtext enthalten.

**Keine echten Passwörter, Tokens oder persönlichen Finanzdaten eintragen.**

### Schritt 3 – Git-Verhalten untersuchen

Führe aus:

```bash
git status
```

Beobachte, welche der neuen Dateien angezeigt werden und welche nicht.

Falls du prüfen möchtest, welche Ignore-Regel greift, kannst du zusätzlich folgenden Befehl verwenden:

```bash
git check-ignore -v .env
```

### Schritt 4 – Bewusst stagen

Füge **nur** die Datei `.gitignore`, die Vorlage `.env.example` und die Textdatei `notizen.txt` für den nächsten Commit hinzu. Überlege selbst, welcher Git-Befehl dafür passt.

Prüfe danach mit:

```bash
git status
git diff --staged
```

Erstelle anschließend einen Commit mit einer sinnvollen Nachricht.

### Schritt 5 – Beobachtungen festhalten

Notiere dir an einem Ort deiner Wahl:

1. Welche deiner neuen Dateien hat Git zunächst angezeigt?
2. Welche Datei wurde ignoriert und warum?
3. Warum ist `.env.example` für ein Team hilfreich?
4. Warum ist das Ignorieren von `.env` keine Garantie, dass nie ein Passwort in Git landet?

## 8. Übung – Was gehört ins Repository?

Stell dir vor, CashFlow hätte folgende Dateien und Ordner:

```text
src/app.js
README.md
package.json
package-lock.json
node_modules/
.env
.env.example
dist/
```

Ordne zu: **eher versionieren** oder **eher ignorieren**. Begründe mindestens zwei deiner Entscheidungen. Bedenke, dass die genaue Projektkonfiguration Ausnahmen haben kann.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten und notiere sie an einem Ort deiner Wahl.

1. Was ist eine `.gitignore`-Datei?
2. Wofür steht die Regel `node_modules/`?
3. Warum werden `package.json` und `package-lock.json` normalerweise versioniert?
4. Warum sollte eine `.env` mit echten Zugangsdaten nicht committed werden?
5. Was ist der Unterschied zwischen `.env` und `.env.example`?
6. Wirkt `.gitignore` automatisch auf Dateien, die Git bereits verfolgt?
7. Was macht `git rm --cached <datei>` grundsätzlich?
8. Ist ein bereits veröffentlichtes Passwort wieder sicher, wenn du die Datei aus Git entfernst?
9. Warum gehört kein echter privater Finanzdatensatz in unser CashFlow-Übungsrepository?
10. Wie überprüfst du vor einem Commit, welche Dateien und Änderungen du tatsächlich aufnimmst?

## Abschluss-Checkliste

- [ ] Ich weiß, welche Arten von Dateien oft ignoriert werden.
- [ ] Ich habe `.gitignore` in meinem lokalen Übungsrepository ausprobiert.
- [ ] Ich kann `.env` und `.env.example` unterscheiden.
- [ ] Ich habe mit `git status` und `git diff --staged` meine Änderungen geprüft.
- [ ] Ich weiß, warum bereits eingecheckte Geheimnisse besonders problematisch sind.
- [ ] Ich habe ausschließlich ungefährliche Testwerte verwendet.

## Zusammenfassung

```text
.gitignore      → Regeln zum Ignorieren nicht verfolgter Dateien
node_modules/   → installierte Abhängigkeiten, meist nicht committen
.env            → lokale Konfiguration, potenziell sensibel
.env.example    → Vorlage ohne echte Secrets
Git-Historie    → bereits gespeicherte Inhalte verschwinden nicht
```

Im nächsten Unterkapitel verbinden wir die bisherigen Schritte zu einem vollständigen Praxisworkflow.

[Weiter: Praxisworkflow →](./11-praxisworkflow.md)
