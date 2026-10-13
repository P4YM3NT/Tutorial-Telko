# 03 – Staging und Commits

[← Zurück: Repository, Status und Änderungen](./02-repository-status.md) | [Weiter: Historie und Unterschiede →](./04-log-diff.md)

Im vorherigen Kapitel hast du im Ordner `git-uebung` ein lokales Git-Repository angelegt. Darin liegt bereits eine `README.md`, die Git noch als **untracked** anzeigt.

Jetzt lernst du, wie du Änderungen **gezielt für einen Commit auswählst** und in der lokalen Git-Historie speicherst.

> **Wichtig:** Verwende weiterhin ausschließlich dein eigenes Repository `git-uebung`. Du brauchst dafür weder GitLab noch JavaScript-Vorkenntnisse.

## Drei Schritte, die du unterscheiden solltest

```text
Datei in VS Code speichern
           ↓
Änderung liegt im Arbeitsverzeichnis
           ↓  git add
Änderung liegt in der Staging Area
           ↓  git commit
Änderung ist in der lokalen Git-Historie gespeichert
```

Ein **Commit** ist ein bewusst gespeicherter Projektstand. `git add` legt vorher fest, welche Änderungen in diesen Stand aufgenommen werden sollen.

## 1. Ausgangszustand prüfen

Öffne `git-uebung` in VS Code und führe im integrierten Terminal aus:

```bash
git status
```

Die Datei `README.md` sollte unter **Untracked files** erscheinen. Wenn sie dort nicht erscheint, prüfe, ob du den richtigen Ordner geöffnet hast und ob du sie im vorherigen Kapitel möglicherweise schon gestaged oder committed hast.

## 2. Die README stagen

Führe aus:

```bash
git add README.md
```

Prüfe anschließend erneut:

```bash
git status
```

Die Datei sollte nun unter **Changes to be committed** stehen. Git hat sie für den nächsten Commit vorgemerkt.

> **Merke:** `git add` erstellt noch **keinen** Commit. Es aktualisiert die Auswahl der Änderungen für den nächsten Commit.

## 3. Den ersten Commit erstellen

Wenn die richtige Datei gestaged ist, kannst du den ersten Commit erstellen:

```bash
git commit -m "Add Git exercise README"
```

Der Teil `-m` steht für die **Commit-Nachricht**. Sie beschreibt kurz, was gespeichert wurde.

Prüfe danach:

```bash
git status
```

Wenn seit dem Commit nichts geändert wurde, meldet Git sinngemäß, dass das Arbeitsverzeichnis sauber ist (`working tree clean`).

Du hast damit deinen **ersten lokalen Commit** erstellt. Auf GitLab wurde noch nichts hochgeladen.

## 4. Eine bereits verfolgte Datei verändern

Öffne `README.md` und ergänze einen neuen Satz, zum Beispiel darüber, was du mit Git bereits gelernt hast. Speichere die Datei.

Führe aus:

```bash
git status
```

Jetzt sollte `README.md` als **modified** erscheinen. Der Unterschied zu vorher: Die Datei wurde bereits mit deinem ersten Commit in Git aufgenommen und wird deshalb verfolgt.

Stage die Änderung erneut:

```bash
git add README.md
```

Anschließend prüfst du wieder den Status. Die Änderung ist jetzt für einen weiteren Commit vorgemerkt.

## 5. Eine gestagte Änderung zurücknehmen

Stell dir vor, du hast die README aus Versehen zu früh gestaged. Du möchtest den Inhalt aber **nicht löschen**, sondern nur noch nicht committen.

Verwende:

```bash
git restore --staged README.md
```

Überprüfe den Status. Die Datei sollte wieder als **modified**, aber nicht mehr als gestaged erscheinen.

Der geänderte Text bleibt dabei in deiner Datei erhalten. Du hast nur die Auswahl für den nächsten Commit zurückgenommen.

Wenn deine Änderung passt, kannst du sie erneut stagen und einen zweiten Commit erstellen:

```bash
git add README.md
git commit -m "Expand Git exercise README"
```

## 6. Mehrere Dateien gezielt auswählen

Mit `git add` kannst du auch mehrere Dateien auswählen:

```bash
git add README.md notizen.md
```

Das funktioniert, wenn die genannten Dateien tatsächlich vorhanden sind.

Mit diesem Befehl werden Änderungen im aktuellen Verzeichnis und seinen Unterordnern berücksichtigt:

```bash
git add .
```

**Aber Vorsicht:** `git add .` kann auch Änderungen erfassen, die du gar nicht committen wolltest. Überprüfe deshalb vorher und nachher `git status`.

Gerade später bei CashFlow möchten wir vermeiden, versehentlich Konfigurationsdateien oder sensible Daten in einen Commit aufzunehmen.

## 7. Gute Commit-Nachrichten

Eine Commit-Nachricht sollte den Zweck einer Änderung verständlich beschreiben.

Wenig hilfreich:

```text
changes
stuff
fix
```

Besser:

```text
Add Git exercise README
Expand setup instructions
Fix typo in dashboard description
```

Die Beispiele zum Dashboard sind nur eine Vorschau auf CashFlow. **Die App selbst programmieren wir hier noch nicht.**

## 8. Warum kleine Commits sinnvoll sind

Ein Commit sollte möglichst **eine zusammengehörige Änderung** enthalten.

Statt einer Nachricht wie:

```text
Add login, change layout, rename files and update documentation
```

wären später mehrere passende Commits leichter zu verstehen und zu überprüfen.

Das hilft insbesondere bei der Fehlersuche und beim Code Review.

## Achtung: Änderungen verwerfen ist etwas anderes

Mit dem folgenden Befehl kann Git Änderungen an einer bereits verfolgten Datei im Arbeitsverzeichnis verwerfen:

```bash
git restore README.md
```

**Führe diesen Befehl jetzt nicht als Übung aus.** Dabei können Änderungen verloren gehen, die du noch nicht committed hast.

Unterscheide deshalb unbedingt:

| Befehl | Wirkung |
|---|---|
| `git restore --staged README.md` | Aus der Staging Area nehmen, lokale Dateiänderung behalten |
| `git restore README.md` | Nicht gestagte Änderungen an der Datei verwerfen |

## Praxisaufgabe – Zwei Commits in deinem Übungsrepository

Arbeite mit der `README.md` aus Kapitel 02 weiter. Du darfst die Erklärungen oben als Nachschlagewerk verwenden.

1. Prüfe mit Git, ob `README.md` noch **untracked** ist.
2. Nimm die Datei in die Staging Area auf und prüfe den neuen Status.
3. Erstelle einen ersten Commit mit einer verständlichen Nachricht.
4. Ergänze in `README.md` einen neuen Satz und speichere die Datei.
5. Prüfe, wie Git die Änderung jetzt bezeichnet.
6. Stage die Änderung, nimm sie anschließend **nur aus der Staging Area** zurück und vergewissere dich, dass dein neuer Satz noch vorhanden ist.
7. Stage die Änderung erneut und erstelle einen zweiten Commit mit einer passenden Nachricht.
8. Kontrolliere zum Schluss den Status des Repositories.

**Wichtig:** Behalte das Repository `git-uebung` und die beiden Commits. Im nächsten Kapitel untersuchen wir daran die Commit-Historie und die Unterschiede zwischen Dateiversionen.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten und notiere deine Antworten an einem Ort deiner Wahl.

1. Was macht `git add`?
2. Was speichert `git commit`?
3. Was ist die Staging Area?
4. Warum ist eine Datei nach dem ersten Commit bei einer erneuten Änderung `modified` statt `untracked`?
5. Was ist der Unterschied zwischen dem Speichern in VS Code und einem Git-Commit?
6. Was bewirkt `git restore --staged README.md`?
7. Warum ist `git restore README.md` mit Vorsicht zu verwenden?
8. Warum solltest du `git add .` nicht gedankenlos verwenden?
9. Woran erkennst du eine hilfreiche Commit-Nachricht?
10. Wurde mit deinen beiden Commits schon etwas zu GitLab hochgeladen?

## Zusammenfassung

```text
README.md (untracked)
       ↓ git add README.md
Staging Area
       ↓ git commit
Erster Commit
       ↓ README.md bearbeiten
README.md (modified)
       ↓ git add → git restore --staged → git add
Staging Area
       ↓ git commit
Zweiter Commit
```

Du kannst jetzt Dateien gezielt stagen, Änderungen wieder aus der Staging Area nehmen und lokale Commits erstellen.

[Weiter: Historie und Unterschiede →](./04-log-diff.md)
