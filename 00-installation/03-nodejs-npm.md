# 03 – Node.js und npm

[← Zurück: Visual Studio Code](./02-vscode.md) | [Weiter: Git →](./04-git.md)

JavaScript läuft ursprünglich im Browser.

Mit **Node.js** können wir JavaScript auch außerhalb des Browsers ausführen.

Das benötigen wir später unter anderem für:

- unsere JavaScript-Übungen,
- Vue und Quasar,
- unser Backend mit Express,
- verschiedene Entwicklungswerkzeuge.

## Node.js installieren

Lade Node.js von der offiziellen Website herunter:

https://nodejs.org/

Verwende eine **LTS-Version**.

LTS steht für:

```text
Long Term Support
```

Eine LTS-Version wird über einen längeren Zeitraum gepflegt und eignet sich deshalb gut für stabile Entwicklungsumgebungen.

> Falls in deinem Ausbildungsbetrieb eine bestimmte Node.js-Version vorgegeben ist, verwende die dort festgelegte Version.

Nach der Installation solltest du VS Code beziehungsweise dein Terminal einmal vollständig schließen und neu öffnen.

## Installation prüfen

Öffne das Terminal in VS Code und führe aus:

```bash
node --version
```

Wenn Node.js korrekt installiert ist, wird eine Versionsnummer angezeigt.

Zum Beispiel:

```text
vXX.XX.X
```

Die genaue Versionsnummer kann bei dir anders aussehen.

## Was ist npm?

Zusammen mit Node.js wird normalerweise auch **npm** installiert.

npm steht für:

```text
Node Package Manager
```

Mit npm können wir später zusätzliche JavaScript-Pakete installieren.

Beispiele dafür sind:

- Vue,
- Express,
- Joi,
- Testbibliotheken.

Prüfe npm mit:

```bash
npm --version
```

Auch hier sollte eine Versionsnummer angezeigt werden.

## Unser erstes JavaScript-Programm

Öffne den Ordner `erste-uebung`, den du im vorherigen Abschnitt angelegt hast.

Die Datei `hello.js` sollte diesen Inhalt haben:

```js
console.log('Hallo Webentwicklung!')
```

Öffne das Terminal und führe aus:

```bash
node hello.js
```

Die Ausgabe sollte sein:

```text
Hallo Webentwicklung!
```

Damit hast du dein erstes JavaScript-Programm mit Node.js ausgeführt.

## Was passiert hier?

Der Befehl:

```bash
node hello.js
```

besteht vereinfacht aus zwei Teilen:

```text
node        → Starte Node.js
hello.js    → Führe diese Datei aus
```

Den JavaScript-Code selbst behandeln wir ausführlich im Kapitel **JavaScript-Grundlagen**.

Für den Moment reicht es, wenn du weißt, wie du eine JavaScript-Datei startest.

## Häufige Probleme

### `node` wurde nicht gefunden

Mögliche Meldungen sind zum Beispiel:

```text
node: command not found
```

oder unter Windows sinngemäß:

```text
'node' is not recognized ...
```

Prüfe in diesem Fall:

1. Wurde Node.js vollständig installiert?
2. Hast du VS Code nach der Installation neu gestartet?
3. Hast du ein neues Terminal geöffnet?

### `npm` wurde nicht gefunden

Wenn `node --version` funktioniert, aber `npm --version` nicht, überprüfe zunächst die Node.js-Installation.

Bei einer normalen Node.js-Installation wird npm mitinstalliert.

### `Cannot find module ...`

Wenn du beispielsweise Folgendes ausführst:

```bash
node hello.js
```

und Node.js die Datei nicht findet, befindet sich dein Terminal wahrscheinlich im falschen Ordner.

Prüfe, ob die Datei `hello.js` im aktuell geöffneten Projektordner liegt.

## Kleine Übung

Ändere den Inhalt von `hello.js` auf:

```js
console.log('Node.js funktioniert!')
```

Führe die Datei erneut aus:

```bash
node hello.js
```

Erwartete Ausgabe:

```text
Node.js funktioniert!
```

## Checkliste

- [ ] `node --version` zeigt eine Versionsnummer.
- [ ] `npm --version` zeigt eine Versionsnummer.
- [ ] Ich kann `hello.js` mit Node.js ausführen.
- [ ] Ich sehe die Ausgabe meines Programms im Terminal.

Als Nächstes installieren wir Git.

[Weiter: Git →](./04-git.md)
