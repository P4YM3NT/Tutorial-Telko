# 06 – Merge und Konflikte

[← Zurück: Branches](./05-branches.md) | [Weiter: Remote, Push und Pull →](./07-remote-push-pull.md)

In Kapitel 05 hast du auf `feature/git-exercise` eine neue Datei erstellt und committed. Dein Hauptbranch `main` kennt diese Änderung noch nicht. Jetzt lernst du, wie du **zwei Branches zusammenführst** und was passiert, wenn Git dabei nicht automatisch entscheiden kann, welche Änderung gelten soll.

> **Wichtig:** Wir arbeiten weiterhin nur in deinem lokalen Übungsrepository `git-uebung`. Du benötigst dafür weder GitLab noch Zugriff auf ein Firmenprojekt. Verwende die folgenden Befehle nicht unüberlegt in einem anderen Repository.

## Lernziele

Nach diesem Kapitel kannst du:

- erklären, was ein Merge ist,
- eine Änderung von einem Feature-Branch nach `main` übernehmen,
- einen **Fast-Forward-Merge** erkennen,
- verstehen, warum Merge-Konflikte entstehen,
- einen Konflikt in einer Textdatei erkennen und auflösen,
- mit `git status` einen laufenden Merge überprüfen,
- erklären, wann `git merge --abort` sinnvoll ist.

## 1. Was bedeutet Merge?

Mit einem **Merge** führst du die Entwicklungsstände zweier Branches zusammen.

Nach Kapitel 05 sieht die Historie vereinfacht so aus:

```text
A ── B ── C ── D
          ↑     ↑
         main   feature/git-exercise
```

Der vierte Commit `D` enthält deine Datei `branch-notizen.md`. Um diese Änderung in `main` zu übernehmen, wechselst du zunächst **auf den Zielbranch** und führst dort den Merge aus.

## 2. Deinen ersten Merge durchführen

Öffne dein Repository `git-uebung` im Terminal.

Prüfe zuerst:

```bash
git status
git branch
```

Das Arbeitsverzeichnis sollte sauber sein. Die beiden Branches `main` und `feature/git-exercise` sollten vorhanden sein. Falls dein Hauptbranch anders heißt, verwende im Folgenden seinen tatsächlichen Namen.

Wechsle auf `main`:

```bash
git switch main
```

Führe den Feature-Branch zusammen:

```bash
git merge feature/git-exercise
```

Wenn du die vorherigen Kapitel wie vorgesehen bearbeitet hast, sollte Git den Merge **ohne Konflikt** durchführen.

Prüfe das Ergebnis:

```bash
git status
git log --oneline --graph --decorate --all
```

Öffne außerdem den Explorer in VS Code. Die Datei `branch-notizen.md` sollte jetzt auch auf `main` vorhanden sein.

**Merke:** Der Befehl `git merge feature/git-exercise` führt die Änderungen dieses Branches **in deinen aktuell ausgecheckten Branch** zusammen – nicht umgekehrt.

## 3. Was ist ein Fast-Forward-Merge?

Weil `main` seit dem Abzweigen des Feature-Branches keinen eigenen neuen Commit erhalten hat, kann Git den Zeiger von `main` einfach zum neueren Commit bewegen.

```text
Vorher:

A ── B ── C ── D
          ↑     ↑
         main   feature/git-exercise

Nachher:

A ── B ── C ── D
                ↑
                main
                feature/git-exercise
```

Das heißt **Fast-Forward**. Dabei ist kein zusätzlicher Merge-Commit notwendig.

> Ein Merge führt nicht immer zu einem neuen Commit. Das hängt unter anderem davon ab, wie sich die beiden Branches seit ihrer Trennung entwickelt haben.

Du kannst den inzwischen zusammengeführten Übungsbranch **optional** löschen:

```bash
git branch -d feature/git-exercise
```

`-d` löscht nur den lokalen Branch-Zeiger und prüft normalerweise, ob seine Änderungen zusammengeführt wurden. Der Inhalt des Commits bleibt über `main` erhalten.

## 4. Wann entsteht ein Merge-Konflikt?

Stell dir vor, zwei Personen ändern dieselbe Zeile einer Datei unterschiedlich:

**Branch A:**

```text
Status: in Bearbeitung
```

**Branch B:**

```text
Status: abgeschlossen
```

Git kann dann nicht immer wissen, welche Formulierung richtig ist. Ein solcher Fall kann zu einem **Merge-Konflikt** führen.

Das heißt nicht, dass Git kaputt ist. Git braucht eine Entscheidung von dir.

## 5. Einen echten Konflikt vorbereiten

Wir erzeugen jetzt absichtlich einen Konflikt – ausschließlich in `git-uebung`.

### Schritt 1: Gemeinsame Ausgangsdatei auf `main`

Stelle sicher, dass du auf `main` bist und dein Arbeitsverzeichnis sauber ist:

```bash
git switch main
git status
```

Erstelle die Datei `konflikt-notizen.md` mit folgendem Inhalt:

```text
Status: offen
```

Speichere den gemeinsamen Ausgangszustand als Commit:

```bash
git add konflikt-notizen.md
git commit -m "Add conflict exercise file"
```

### Schritt 2: Änderung auf einem Feature-Branch

Erstelle einen neuen Branch:

```bash
git switch -c feature/merge-konflikt
```

Ändere in `konflikt-notizen.md` **nur die vorhandene Zeile** zu:

```text
Status: in Bearbeitung
```

Speichere und committe die Änderung:

```bash
git add konflikt-notizen.md
git commit -m "Update conflict status in feature"
```

### Schritt 3: Andere Änderung auf `main`

Wechsle zurück:

```bash
git switch main
```

Ändere **dieselbe Zeile** in `konflikt-notizen.md` diesmal zu:

```text
Status: abgeschlossen
```

Speichere und committe die Änderung:

```bash
git add konflikt-notizen.md
git commit -m "Update conflict status on main"
```

Nun haben beide Branches unterschiedliche neue Commits, die sich auf dieselbe Zeile beziehen.

## 6. Konflikt auslösen und untersuchen

Du befindest dich auf `main`. Starte jetzt den Merge:

```bash
git merge feature/merge-konflikt
```

Git sollte melden, dass `konflikt-notizen.md` einen Konflikt enthält. **Das ist in dieser Übung beabsichtigt.**

Prüfe den Zustand:

```bash
git status
```

Öffne anschließend `konflikt-notizen.md` in VS Code. Die Datei kann ungefähr so aussehen:

```text
<<<<<<< HEAD
Status: abgeschlossen
=======
Status: in Bearbeitung
>>>>>>> feature/merge-konflikt
```

Die Markierungen bedeuten:

- `<<<<<<< HEAD`: Beginn der Version aus deinem aktuellen Branch (`main`).
- `=======`: Trennt die beiden konkurrierenden Versionen.
- `>>>>>>> feature/merge-konflikt`: Ende der Version aus dem Branch, den du zusammenführen möchtest.

Diese Markierungen gehören **nicht** in die fertige Datei.

## 7. Konflikt selbstständig lösen

Jetzt entscheidest du, was am Ende in der Datei stehen soll.

1. Lies beide Änderungen aufmerksam.
2. Entscheide dich für eine sinnvolle endgültige Statuszeile. Du darfst eine der beiden Varianten auswählen oder eine eigene Formulierung verwenden.
3. Bearbeite `konflikt-notizen.md` so, dass **nur deine gewählte endgültige Zeile** darin steht.
4. Entferne alle Konfliktmarkierungen und speichere die Datei.
5. Prüfe mit `git status`, welche Datei noch als konfliktbehaftet gilt.

Wenn du die Datei fertig bearbeitet hast, markiere den Konflikt als aufgelöst:

```bash
git add konflikt-notizen.md
```

Prüfe erneut:

```bash
git status
```

Schließe den Merge mit einem Commit ab:

```bash
git commit -m "Resolve merge conflict"
```

Kontrolliere zum Schluss:

```bash
git status
git log --oneline --graph --decorate --all
```

Das Arbeitsverzeichnis sollte wieder sauber sein. Deine endgültige Datei darf keine Konfliktmarkierungen mehr enthalten.

> **Tipp:** VS Code kann beim Auflösen eines Konflikts Schaltflächen wie „Accept Current“, „Accept Incoming“ oder „Accept Both“ anbieten. Du kannst sie verwenden, solltest aber immer den endgültigen Dateiinhalt überprüfen. „Accept Both“ ergibt nicht automatisch einen sinnvollen Text.

## 8. Was ist ein Merge-Commit?

Anders als beim Fast-Forward haben sich in unserer Konfliktübung **beide Branches weiterentwickelt**.

Nach dem Auflösen sieht die Historie vereinfacht so aus:

```text
         E ──────── G
        /          / 
A ── D ─          /   ← main nach dem Merge
        \        /
         F ─────
```

`E` und `F` stehen für die unterschiedlichen Änderungen auf den Branches. `G` ist der **Merge-Commit**, der beide Entwicklungswege zusammenführt. Die tatsächliche Darstellung in `git log` kann anders aussehen.

## 9. Einen Merge abbrechen

Manchmal möchtest du einen begonnenen Merge **nicht** abschließen. Solange ein Merge läuft, kannst du ihn häufig mit folgendem Befehl abbrechen:

```bash
git merge --abort
```

Damit versucht Git, den Zustand vor dem Merge wiederherzustellen.

**Führe diesen Befehl in unserer Übung nicht aus**, wenn du den Konflikt bereits erfolgreich aufgelöst hast. Wir lernen ihn hier nur als mögliche Reaktion auf einen laufenden, problematischen Merge kennen.

> **Vorsicht:** Wenn vor oder während des Merges weitere lokale Änderungen vorhanden sind, ist die Wiederherstellung nicht in jeder Situation problemlos möglich. Deshalb vor einem Merge immer `git status` prüfen.

## 10. Wie arbeiten Teams später damit?

In Teams werden Feature-Branches oft über **Merge Requests** geprüft und zusammengeführt. Das lernst du in den späteren GitLab-Unterkapiteln.

Für den Moment reicht es, wenn du einen lokalen Merge durchführen und verstehen kannst, warum ein Konflikt entstehen kann.

Bei **CashFlow** könnten später zwei Entwickler dieselbe Darstellung einer Transaktion ändern. Dann würden dieselben Git-Prinzipien gelten. CashFlow selbst programmieren wir hier noch nicht.

## Praxisaufgabe – Zeige, dass du einen Konflikt verstanden hast

Beantworte die Fragen anhand **deiner eigenen Übung**. Notiere deine Antworten an einem Ort deiner Wahl.

1. Warum konnte der erste Merge von `feature/git-exercise` nach `main` als Fast-Forward erfolgen?
2. Welche Datei hat im zweiten Teil einen Konflikt ausgelöst?
3. Welche zwei Änderungen standen sich gegenüber?
4. Welche endgültige Zeile hast du gewählt – und warum?
5. Wie hast du Git mitgeteilt, dass der Konflikt behoben wurde?
6. Woran erkennst du, dass der Merge abgeschlossen ist?
7. Was wäre der Unterschied zwischen `git merge --abort` und dem erfolgreichen Auflösen des Konflikts?

## Wissenscheck

1. Was bedeutet es, zwei Branches zu mergen?
2. Auf welchem Branch musst du stehen, wenn du `feature-x` **in `main`** übernehmen möchtest?
3. Was ist ein Fast-Forward-Merge?
4. Entsteht bei jedem Merge automatisch ein neuer Merge-Commit?
5. Warum kann ein Merge-Konflikt entstehen?
6. Was bedeuten `<<<<<<<`, `=======` und `>>>>>>>` in einer Konfliktdatei?
7. Warum müssen Konfliktmarkierungen vor dem Abschluss entfernt werden?
8. Wofür verwendest du `git add` beim Auflösen eines Konflikts?
9. Woran zeigt `git status`, dass ein Merge noch nicht abgeschlossen ist?
10. Wozu dient `git merge --abort`?

## Abschluss-Checkliste

- [ ] Ich habe meinen ersten Feature-Branch nach `main` gemerged.
- [ ] Ich kann erklären, warum dabei ein Fast-Forward möglich war.
- [ ] Ich habe in `git-uebung` absichtlich einen echten Merge-Konflikt ausgelöst.
- [ ] Ich habe beide widersprüchlichen Änderungen erkannt.
- [ ] Ich habe die Konfliktmarkierungen entfernt und den Merge abgeschlossen.
- [ ] Mein Arbeitsverzeichnis ist wieder sauber.
- [ ] Ich weiß, wann ich einen Merge abbrechen könnte.

## Zusammenfassung

```text
Feature-Branch fertig
        ↓
Auf Zielbranch wechseln
        ↓
git merge <feature-branch>
        ↓
Automatischer Merge möglich?
        ├── Ja → Ergebnis prüfen
        └── Nein → Konflikt ansehen
                     ↓
                  Datei korrigieren
                     ↓
                  git add
                     ↓
                  Merge-Commit abschließen
        ↓
git status prüfen
```

Im nächsten Kapitel lernst du, wie Git mit entfernten Repositories kommuniziert und worin sich `fetch`, `pull` und `push` unterscheiden.

[Weiter: Remote, Push und Pull →](./07-remote-push-pull.md)
