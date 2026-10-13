# 02 – Visual Studio Code

[← Zurück: Voraussetzungen](./01-voraussetzungen.md) | [Weiter: Node.js und npm →](./03-nodejs-npm.md)

Zum Schreiben unseres Codes verwenden wir **Visual Studio Code**, kurz **VS Code**.

VS Code ist ein Code-Editor. Damit können wir Dateien bearbeiten, Programme schreiben und viele Entwicklungswerkzeuge direkt aus einer Oberfläche verwenden.

## Installation

Lade Visual Studio Code von der offiziellen Website herunter:

https://code.visualstudio.com/

Installiere anschließend die für dein Betriebssystem passende Version.

## VS Code starten

Nach dem Start siehst du mehrere Bereiche.

Vereinfacht sieht die Oberfläche ungefähr so aus:

```text
┌──────────────────────────────────────────────┐
│ Explorer │                                   │
│          │                                   │
│ Dateien  │              Editor               │
│          │                                   │
│          │                                   │
├──────────┴───────────────────────────────────┤
│                  Terminal                    │
└──────────────────────────────────────────────┘
```

Die wichtigsten Bereiche für den Anfang sind:

- **Explorer** – zeigt Dateien und Ordner des geöffneten Projekts,
- **Editor** – hier schreiben und bearbeiten wir Code,
- **Terminal** – hier führen wir Befehle aus.

Du musst noch nicht alle Funktionen von VS Code kennen.

## Einen Ordner öffnen

Erstelle zunächst einen Ordner für eine kleine Testübung.

Zum Beispiel:

```text
erste-uebung
```

Öffne diesen Ordner anschließend in VS Code:

```text
File
→ Open Folder
```

Wähle den Ordner `erste-uebung` aus.

Der Ordner sollte jetzt links im Explorer angezeigt werden.

## Eine Datei erstellen

Erstelle im geöffneten Ordner eine neue Datei:

```text
hello.js
```

Schreibe folgenden Inhalt hinein:

```js
console.log('Hallo Webentwicklung!')
```

Speichere die Datei.

Noch können wir sie nicht unbedingt ausführen. Dafür benötigen wir im nächsten Schritt Node.js.

## Das Terminal öffnen

VS Code besitzt ein eingebautes Terminal.

Öffne es über:

```text
Terminal
→ New Terminal
```

Das Terminal erscheint normalerweise im unteren Bereich von VS Code.

Du kannst dort später Befehle wie diese eingeben:

```bash
node hello.js
```

oder:

```bash
git --version
```

## Der aktuelle Ordner im Terminal

Wenn du einen Projektordner in VS Code geöffnet hast, startet das Terminal normalerweise direkt in diesem Ordner.

Das ist wichtig, weil Befehle häufig mit Dateien aus dem aktuellen Ordner arbeiten.

Bei unserem Beispiel sollte sich das Terminal im Ordner `erste-uebung` befinden.

## Erweiterungen

VS Code kann mit Erweiterungen ergänzt werden.

Für den Einstieg installieren wir absichtlich noch keine große Sammlung an Erweiterungen.

Später lernen wir Werkzeuge wie Formatter und Linter genau dann kennen, wenn wir verstehen, welches Problem sie lösen.

## Checkliste

- [ ] VS Code ist installiert.
- [ ] Ich kann VS Code starten.
- [ ] Ich kann einen Ordner öffnen.
- [ ] Ich habe eine Datei `hello.js` erstellt.
- [ ] Ich kann das integrierte Terminal öffnen.

Als Nächstes installieren wir Node.js und prüfen npm.

[Weiter: Node.js und npm →](./03-nodejs-npm.md)
