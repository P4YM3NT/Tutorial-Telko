# 04 – Historie und Unterschiede

[← Zurück: Staging und Commits](./03-staging-commits.md) | [Weiter: Branches →](./05-branches.md)

In den vorherigen Kapiteln hast du im Ordner `git-uebung` ein Repository erstellt und **zwei Commits** angelegt. Jetzt schauen wir uns an, **welche Änderungen Git gespeichert hat** und **welche Änderungen noch nicht gespeichert wurden**.

Dafür nutzen wir vor allem zwei Befehle:

```text
git log  → gespeicherte Commits ansehen
git diff → Unterschiede zwischen Dateiständen ansehen
```

> **Wichtig:** Arbeite weiterhin nur in deinem lokalen Repository `git-uebung`. Du benötigst weder GitLab noch neue JavaScript-Kenntnisse.

## 1. Den Ausgangszustand prüfen

Öffne `git-uebung` in VS Code und starte dort das Terminal.

```bash
git status
```

Wenn du Kapitel 03 abgeschlossen hast und seitdem nichts verändert hast, sollte Git melden, dass dein Arbeitsverzeichnis sauber ist (`working tree clean`).

Die beiden Commits aus Kapitel 03 sind trotzdem vorhanden. Ein sauberer Status bedeutet **nicht**, dass das Repository leer ist – nur, dass gerade keine neuen Änderungen anstehen.

## 2. Die Commit-Historie lesen

Mit diesem Befehl siehst du die Historie:

```bash
git log
```

Git zeigt dir unter anderem:

- eine **Commit-ID**,
- den Namen und die E-Mail-Adresse des Autors,
- das Datum,
- die Commit-Nachricht.

Für einen schnellen Überblick eignet sich:

```bash
git log --oneline
```

Eine mögliche Ausgabe ist:

```text
b7c8d9e Expand Git exercise README
a1b2c3d Add Git exercise README
```

Deine Commit-IDs werden anders aussehen. Entscheidend ist: **Der neueste Commit steht oben.**

Manchmal öffnet `git log` eine längere Ansicht. Wenn du unten ein `:` oder `(END)` siehst, kannst du diese Ansicht häufig mit `q` verlassen.

## 3. Was ist eine Commit-ID?

Jeder Commit hat eine Kennung (einen sogenannten **Hash**). Du kannst sie dir wie eine eindeutige Referenz auf einen gespeicherten Commit vorstellen.

```text
b7c8d9e
```

Das ist nur eine **verkürzte** Beispiel-ID. Git kann sie verwenden, solange sie im Repository eindeutig ist.

Du brauchst diese Zeichen nicht auswendig zu lernen. Mit `git log --oneline` kannst du sie jederzeit nachsehen.

## 4. Einen gespeicherten Commit untersuchen

Mit `git show` kannst du dir ansehen, was ein bestimmter Commit enthält.

```bash
git show HEAD
```

`HEAD` bezeichnet hier vereinfacht den Commit, auf dem du gerade stehst – bei unserer Übung den **neuesten Commit auf deinem aktuellen Branch**.

Der Befehl zeigt neben Commit-Informationen auch die Änderungen, die dieser Commit gegenüber seinem Vorgänger enthält.

Du kannst alternativ die Commit-ID aus `git log --oneline` verwenden:

```bash
git show <commit-id>
```

`<commit-id>` ist ein Platzhalter: Ersetze ihn durch eine **echte ID aus deinem Repository**.

## 5. Nicht gestagte Änderungen mit `git diff` ansehen

Jetzt soll Git eine neue Änderung erkennen. Öffne die bereits bekannte Datei `README.md` und ergänze einen kurzen Satz, zum Beispiel:

```text
Mit git diff kann ich Änderungen vor dem Commit prüfen.
```

Speichere die Datei. Prüfe dann:

```bash
git status
git diff
```

`git diff` zeigt bei unserer Übung die Änderungen an der bereits verfolgten `README.md`, die **noch nicht gestaged** wurden.

Ein vereinfachter Ausschnitt könnte so aussehen:

```diff
 Hier lerne ich die Grundlagen von Git.
+Mit git diff kann ich Änderungen vor dem Commit prüfen.
```

In einer echten Ausgabe stehen meist noch weitere Zeilen mit Dateinamen und Kontext.

Bei einem Diff bedeutet:

- `+` am Zeilenanfang: Diese Zeile wurde hinzugefügt.
- `-` am Zeilenanfang: Diese Zeile wurde entfernt.
- Zeilen ohne `+` oder `-`: Kontext, damit du die Änderung einordnen kannst.

> **Merke:** `git diff` zeigt normalerweise Änderungen an **bereits verfolgten Dateien**. Eine neue, noch `untracked` Datei erscheint nicht einfach mit ihrem Inhalt im normalen `git diff`.

## 6. Gestagte Änderungen prüfen

Stage jetzt die geänderte README:

```bash
git add README.md
```

Vergleiche anschließend diese beiden Befehle:

```bash
git diff

git diff --staged
```

Was solltest du beobachten?

- `git diff` zeigt die eben vollständig gestagte Änderung an `README.md` **nicht mehr**, sofern du die Datei danach nicht erneut bearbeitet hast.
- `git diff --staged` zeigt die Änderung, die Git aktuell für den **nächsten Commit** vorgemerkt hat.

Das ist ein wichtiger Unterschied: **Arbeitsverzeichnis und Staging Area sind nicht dasselbe.**

Falls du nur eine einzelne Datei untersuchen möchtest, kannst du ihren Namen angeben:

```bash
git diff -- README.md

git diff --staged -- README.md
```

Das `--` trennt hier mögliche Befehlsoptionen vom Dateipfad.

## 7. Warum prüfen wir Änderungen vor einem Commit?

Mit `git diff` und `git diff --staged` kannst du kontrollieren:

- Habe ich nur die gewünschten Zeilen geändert?
- Ist versehentlich zusätzlicher Text in der Datei gelandet?
- Ist die richtige Änderung für den Commit ausgewählt?
- Habe ich aus Versehen Zugangsdaten oder andere sensible Informationen eingefügt?

Gerade beim späteren Projekt **CashFlow** ist das wichtig: Wir wollen nur beabsichtigte Änderungen committen und niemals echte Finanzdaten oder Geheimnisse in Git speichern.

## 8. Den dritten Commit erstellen

Wenn der gestagte Unterschied zu deiner Aufgabe passt, erstelle einen neuen Commit:

```bash
git commit -m "Document Git diff usage"
```

Prüfe danach:

```bash
git status
git log --oneline
```

Wenn alles geklappt hat, ist das Arbeitsverzeichnis wieder sauber und du solltest **drei Commits** sehen.

## Praxisaufgabe – Änderungen bewusst prüfen

Arbeite mit deinem bestehenden Ordner `git-uebung` weiter. Du darfst die Erklärungen oben zum Nachschlagen verwenden.

1. Zeige die Commit-Historie in der kompakten Ansicht an. Wie viele Commits gibt es vor der nächsten Änderung?
2. Untersuche mit Git den Inhalt des neuesten Commits. Was wurde in diesem Commit geändert?
3. Ergänze in `README.md` **einen eigenen Satz** darüber, wofür du `git diff` verwendest. Speichere die Datei.
4. Prüfe den Status und zeige die noch nicht gestagten Änderungen an. Erkläre, woran du den neuen Satz erkennst.
5. Stage **nur** `README.md` und vergleiche die Ausgaben von `git diff` und `git diff --staged`.
6. Kontrolliere den gestagten Unterschied und erstelle einen dritten Commit mit einer verständlichen Nachricht.
7. Prüfe abschließend den Status und die Commit-Historie.

**Bewahre das Repository auf.** Im nächsten Kapitel arbeiten wir darin mit Branches.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten und notiere die Antworten an einem Ort deiner Wahl.

1. Wofür verwenden wir `git log`?
2. Was zeigt `git log --oneline` im Unterschied zu `git log`?
3. Was ist eine Commit-ID?
4. Was bedeutet `HEAD` in unserer bisherigen Übung vereinfacht?
5. Wofür verwenden wir `git show HEAD`?
6. Was zeigt `git diff`, solange du die Änderung noch nicht gestaged hast?
7. Was zeigt `git diff --staged`?
8. Warum kann `git diff` nach einem `git add README.md` leer sein?
9. Erscheint eine neue, noch `untracked` Datei automatisch mit ihrem Inhalt in `git diff`?
10. Warum sollte man gestagte Änderungen vor einem Commit prüfen?

## Zusammenfassung

```text
Zwei gespeicherte Commits
          ↓ git log --oneline
Historie ansehen
          ↓ git show HEAD
Letzten Commit untersuchen
          ↓ README.md bearbeiten
Änderung im Arbeitsverzeichnis
          ↓ git diff
Nicht gestagte Änderung prüfen
          ↓ git add README.md
Änderung in der Staging Area
          ↓ git diff --staged
Nächsten Commit prüfen
          ↓ git commit
Dritter Commit
```

Du kannst jetzt gespeicherte Änderungen nachvollziehen und neue Änderungen **vor dem Commit gezielt kontrollieren**.

[Weiter: Branches →](./05-branches.md)
