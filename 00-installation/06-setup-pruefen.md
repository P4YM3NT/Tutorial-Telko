# 06 – Installation prüfen

[← Zurück: Browser und Developer Tools](./05-browser-devtools.md) | [Zurück zur Übersicht](./README.md)

Zum Abschluss prüfen wir, ob deine Entwicklungsumgebung bereit ist.

## 1. Node.js prüfen

Öffne ein Terminal und führe aus:

```bash
node --version
```

Erwartung:

```text
vXX.XX.X
```

Eine konkrete Versionsnummer ist hier nicht vorgegeben. Wichtig ist, dass eine Versionsnummer angezeigt wird.

## 2. npm prüfen

Führe aus:

```bash
npm --version
```

Auch hier sollte eine Versionsnummer erscheinen.

## 3. Git prüfen

Führe aus:

```bash
git --version
```

Erwartung:

```text
git version X.XX.X
```

## 4. JavaScript-Datei ausführen

Erstelle einen Ordner:

```text
erste-uebung
```

Erstelle darin eine Datei:

```text
hello.js
```

Schreibe folgenden Code hinein:

```js
console.log('Meine Entwicklungsumgebung funktioniert!')
```

Öffne das Terminal in diesem Ordner und führe aus:

```bash
node hello.js
```

Die Ausgabe sollte sein:

```text
Meine Entwicklungsumgebung funktioniert!
```

Wenn du diese Ausgabe siehst, funktioniert Node.js.

## 5. Browser Developer Tools prüfen

Öffne deinen Browser und anschließend die Developer Tools.

Prüfe, ob du mindestens diese Bereiche findest:

```text
Elements / Inspector
Console
Network
```

Die genaue Bezeichnung kann je nach Browser unterschiedlich sein.

## Abschluss-Checkliste

Deine Entwicklungsumgebung ist bereit, wenn du alle Punkte abhaken kannst:

- [ ] Visual Studio Code ist installiert.
- [ ] Ich kann einen Projektordner in VS Code öffnen.
- [ ] Ich kann das Terminal in VS Code öffnen.
- [ ] `node --version` funktioniert.
- [ ] `npm --version` funktioniert.
- [ ] `git --version` funktioniert.
- [ ] Mein Git-Name und meine Git-E-Mail-Adresse sind konfiguriert.
- [ ] Ich kann eine JavaScript-Datei mit Node.js ausführen.
- [ ] Ich kann die Developer Tools meines Browsers öffnen.

---

# Abschlussaufgabe – Meine Entwicklungsumgebung

Jetzt zeigst du, dass du die Werkzeuge aus diesem Kapitel selbstständig verwenden kannst.

**Wichtig:** Bearbeite die Aufgabe möglichst eigenständig. Du darfst jederzeit in den vorherigen Kapiteln nachschlagen. Eine Schritt-für-Schritt-Anleitung gibt es diesmal bewusst nicht.

## Teil 1 – Ein kleines Programm erstellen

1. Erstelle einen neuen Ordner mit dem Namen `setup-aufgabe`.
2. Erstelle darin eine JavaScript-Datei namens `app.js`.
3. Schreibe ein Programm, das beim Ausführen **genau diese drei Zeilen** in der angegebenen Reihenfolge ausgibt:

```text
Meine Entwicklungsumgebung ist bereit!
Ich kann JavaScript mit Node.js ausführen.
Jetzt kann es losgehen.
```

4. Starte das Programm selbstständig über das Terminal.
5. Überprüfe, ob alle drei Zeilen korrekt ausgegeben werden.

Du musst dafür noch keine neuen JavaScript-Konzepte kennen. Verwende das, was du in den vorherigen Kapiteln ausprobiert hast.

## Teil 2 – Deine Werkzeuge erklären

Erkläre deiner betreuenden Person mit eigenen Worten:

- Mit welchem Werkzeug hast du die Datei erstellt und den Code geschrieben?
- Wo hast du den Befehl zum Ausführen eingegeben?
- Welches Werkzeug führt den JavaScript-Code aus?
- Wo konntest du überprüfen, ob dein Programm funktioniert?

Du musst keine Definitionen auswendig können. Wichtig ist, dass du beschreiben kannst, was du gemacht hast.

---

# Wissenscheck

Beantworte die folgenden Fragen mit deinen eigenen Worten. Notiere deine Antworten an einem Ort deiner Wahl, beispielsweise auf Papier oder in einer eigenen Textdatei. Versuche zunächst, die Fragen selbstständig zu beantworten. Wenn du nicht weiterkommst, darfst du in den vorherigen Kapiteln nachschlagen.

## Frage 1

Wofür verwenden wir Visual Studio Code?

## Frage 2

Was ist ein Terminal?

## Frage 3

Wofür benötigen wir Node.js?

## Frage 4

Was ist npm?

## Frage 5

Wofür verwenden wir Git?

## Frage 6

Wie prüfst du, ob Git installiert ist?

## Frage 7

Wie führst du die Datei `app.js` mit Node.js aus?

---

# Zusammenfassung

In diesem Kapitel hast du die wichtigsten Werkzeuge für den Einstieg eingerichtet.

```text
Visual Studio Code
        ↓
Code schreiben

Terminal
        ↓
Befehle ausführen

Node.js
        ↓
JavaScript ausführen

npm
        ↓
JavaScript-Pakete verwalten

Git
        ↓
Änderungen am Code verwalten

Browser + DevTools
        ↓
Webanwendungen anzeigen und untersuchen
```

Damit ist deine Entwicklungsumgebung vorbereitet.

Im nächsten Kapitel beschäftigen wir uns mit der Frage:

> **Wie funktioniert das Web eigentlich?**

Dort lernen wir unter anderem:

- Client und Server,
- Requests und Responses,
- HTTP,
- URLs,
- Statuscodes,
- JSON,
- APIs.

Damit sind wir bereit für **01 – Web-Grundlagen**.

## Abgabe

Zeige deiner betreuenden Person die Datei `setup-aufgabe/app.js` und die Ausgabe mit allen drei Zeilen. Erkläre deine verwendeten Werkzeuge und beantworte die sieben Fragen aus dem Wissenscheck in eigenen Worten. Halte deine Antworten bereit, damit ihr sie gemeinsam besprechen könnt. Die Aufgabenlösungen befinden sich nicht in diesem Studentenmaterial.
