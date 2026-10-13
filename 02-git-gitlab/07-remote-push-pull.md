# 07 – Remote, Push und Pull

[← Zurück: Merge und Konflikte](./06-merge-konflikte.md) | [Weiter: GitLab-Grundlagen →](./08-gitlab-grundlagen.md)

Bisher hast du in `git-uebung` **nur lokal** gearbeitet: Du hast Dateien verändert, Commits erstellt, Branches angelegt und einen Merge-Konflikt gelöst. Jetzt lernst du, wie mehrere Kopien eines Git-Repositories Änderungen austauschen.

In der Praxis liegt eine gemeinsame Kopie häufig auf einem Server, etwa in GitLab. **Für unsere Übungen benötigen wir aber weder GitLab noch einen Firmenzugang.** Wir richten auf deinem eigenen Rechner ein zweites Repository ein, das den gemeinsamen Speicherort simuliert.

> **Wichtig:** Verwende weiterhin ausschließlich deine Übungsordner. Gib keine Git-Befehle in einem echten Firmen- oder Tutorial-Repository ein, wenn du dir über ihre Wirkung unsicher bist.

## Lernziele

Nach diesem Kapitel kannst du:

- erklären, was ein **Remote-Repository** ist,
- verstehen, wofür der Name `origin` verwendet wird,
- zwischen `commit`, `push`, `fetch` und `pull` unterscheiden,
- ein Remote mit `git remote -v` untersuchen,
- einen lokalen Branch mit einem Remote-Branch verknüpfen,
- Änderungen aus einer anderen Repository-Kopie zunächst ansehen und anschließend übernehmen,
- prüfen, ob dein Arbeitsverzeichnis vor der Synchronisierung sauber ist.

## 1. Was ist ein Remote?

Ein **Remote** ist ein gespeicherter Verweis auf ein anderes Git-Repository. Dieses kann auf einem Server liegen – oder, wie in unserer Übung, in einem anderen Ordner auf demselben Rechner.

Vereinfacht:

```text
Dein Repository                 Gemeinsames Repository
    git-uebung/   ←── Git ──→    git-uebung-remote.git/
     (lokal)                        (hier ebenfalls lokal)
```

In einem Team würden andere Entwickler normalerweise über einen Server auf das gemeinsame Repository zugreifen. Wir simulieren diesen Ablauf lokal, damit du ihn ohne zusätzliche Zugänge lernen kannst.

### Was bedeutet `origin`?

`origin` ist **kein besonderer Server**. Es ist lediglich der übliche Name für ein Remote. Wenn du ein Repository klonst, legt Git meistens automatisch ein Remote namens `origin` an.

Mit diesem Befehl zeigst du die eingerichteten Remotes an:

```bash
git remote -v
```

Bei deinem bisherigen `git-uebung`-Repository ist vermutlich **noch kein Remote** eingetragen. Dann liefert der Befehl keine Ausgabe. Das ist kein Fehler.

## 2. Ein gemeinsames Übungsrepository anlegen

Wir erstellen nun das Repository, zu dem wir später Änderungen übertragen. Dafür verwenden wir ein **Bare Repository**. Dieses speichert Git-Historie und Branches, aber keinen normalen Arbeitsordner zum Bearbeiten von Dateien.

### Schritt 1: Deinen bisherigen Stand prüfen

Öffne `git-uebung` in VS Code und führe aus:

```bash
git status
git branch --show-current
git remote -v
```

Nach Kapitel 06 solltest du wieder auf `main` sein und ein sauberes Arbeitsverzeichnis haben. Falls Git noch einen laufenden Merge oder nicht commitete Änderungen meldet, **kläre das zuerst**, bevor du weitermachst.

Falls `git remote -v` bereits ein `origin` zeigt, füge nicht blind ein weiteres hinzu. Prüfe mit deiner betreuenden Person, ob du im richtigen Übungsrepository bist.

### Schritt 2: Den Übungsordner verlassen

Wechsle im Terminal **eine Verzeichnisebene nach oben**:

```bash
cd ..
```

Erstelle dort das gemeinsame Repository:

```bash
git init --bare --initial-branch=main git-uebung-remote.git
```

Die Option `--bare` sorgt dafür, dass das Repository nur für die Git-Verwaltung gedacht ist. `--initial-branch=main` legt `main` als vorgesehenen Hauptbranch fest.

Du solltest jetzt ungefähr diese Ordner haben:

```text
webentwicklung/
├── git-uebung/
└── git-uebung-remote.git/
```

Der übergeordnete Ordner kann auf deinem Rechner anders heißen.

> **Nicht verwechseln:** In `git-uebung` bearbeitest du Dateien. In `git-uebung-remote.git` bearbeitest du **keine** Projektdateien von Hand.

## 3. Remote eintragen und erstmals pushen

Wechsle zurück in dein Arbeitsrepository:

```bash
cd git-uebung
```

Hinterlege das neue gemeinsame Repository unter dem Namen `origin`:

```bash
git remote add origin ../git-uebung-remote.git
```

Prüfe die Verbindung:

```bash
git remote -v
```

Du solltest für `origin` einen Eintrag zum **Fetch** und einen zum **Push** sehen. Beide zeigen auf den gerade angelegten Ordner.

### Was macht `push`?

Ein **Commit** speichert Änderungen zunächst in deinem lokalen Repository. Mit **Push** überträgst du vorhandene lokale Commits in ein anderes Repository.

Übertrage deinen bisherigen Hauptbranch:

```bash
git push -u origin main
```

Dabei bedeutet:

- `origin`: das Ziel-Remote,
- `main`: der Branch, den du übertragen möchtest,
- `-u`: Git merkt sich für deinen lokalen Branch, welcher Remote-Branch normalerweise dazugehört (**Upstream**).

Danach genügt auf `main` oft:

```bash
git push
```

**Merke:** `git commit` und `git push` sind nicht dasselbe. Ein Commit ist zunächst lokal. Push macht passende Commits in einem anderen Repository verfügbar.

## 4. Eine zweite Arbeitskopie erstellen

Um Änderungen von „jemand anderem“ zu simulieren, klonst du das gemeinsame Repository ein zweites Mal.

Gehe dafür wieder eine Verzeichnisebene nach oben:

```bash
cd ..
```

Klonen bedeutet: Ein bestehendes Git-Repository wird als neue Arbeitskopie eingerichtet.

```bash
git clone git-uebung-remote.git git-uebung-kopie
```

Wechsle in die Kopie:

```bash
cd git-uebung-kopie
```

Prüfe:

```bash
git status
git remote -v
git log --oneline -3
```

Die Kopie enthält jetzt deine bisherigen Commits. Beim Klonen wurde normalerweise direkt das Remote `origin` eingerichtet.

Deine Ordner sehen jetzt ungefähr so aus:

```text
webentwicklung/
├── git-uebung/            ← erste Arbeitskopie
├── git-uebung-kopie/      ← zweite Arbeitskopie
└── git-uebung-remote.git/ ← gemeinsames Repository
```

**Beide Arbeitskopien sind voneinander getrennt.** Eine Änderung in `git-uebung-kopie` erscheint nicht automatisch in `git-uebung`.

## 5. Eine Änderung aus der zweiten Kopie pushen

Arbeite jetzt ausschließlich im Ordner `git-uebung-kopie`.

Erstelle die Datei `remote-notiz.md` und schreibe einen kurzen eigenen Satz hinein, der erklärt, was ein Remote ist. Speichere die Datei.

Anschließend:

```bash
git status
git add remote-notiz.md
git commit -m "Add remote exercise notes"
git push
```

Mit `git push` überträgst du diesen neuen Commit zum gemeinsamen Übungsrepository.

**Noch nicht in die erste Arbeitskopie wechseln und dort `pull` ausführen.** Zuerst untersuchen wir mit `fetch`, was sich geändert hat.

## 6. Änderungen mit `fetch` holen und ansehen

Wechsle zurück zur ersten Arbeitskopie:

```bash
cd ../git-uebung
```

Prüfe zunächst:

```bash
git status
```

Hole nun die aktuellen Informationen aus dem Remote:

```bash
git fetch origin
```

`fetch` holt neue Commits und aktualisiert Informationen über Remote-Branches, **ohne die Dateien deines aktuellen Arbeitsbranches automatisch zu ändern**.

Vergleiche deinen lokalen `main` mit dem Stand auf dem Remote:

```bash
git log --oneline main..origin/main
```

Dort sollte der neue Commit aus `git-uebung-kopie` zu sehen sein.

- `main` bezeichnet deinen lokalen Branch.
- `origin/main` bezeichnet deinen lokal gespeicherten Kenntnisstand über `main` auf `origin` (einen **Remote-Tracking-Branch**).

Prüfe im VS-Code-Explorer: Die Datei `remote-notiz.md` sollte in der ersten Arbeitskopie **noch nicht** vorhanden sein.

> **Merke:** `fetch` bedeutet: „Hole den aktuellen Stand, damit ich ihn untersuchen kann.“ Es übernimmt Änderungen nicht automatisch in deinen ausgecheckten Branch.

## 7. Änderungen mit `pull` übernehmen

Jetzt möchtest du den neuen Commit tatsächlich in deinen lokalen Branch `main` übernehmen.

```bash
git pull --ff-only
```

`pull` holt den Remote-Stand und integriert ihn in den aktuellen Branch. Mit `--ff-only` erlauben wir in unserer Übung **nur ein Fast-Forward**. Falls die Historien auseinanderlaufen, bricht Git ab, statt automatisch einen Merge-Commit zu erzeugen.

Überprüfe anschließend:

```bash
git status
git log --oneline -3
```

Jetzt sollte die Datei `remote-notiz.md` in `git-uebung` sichtbar sein.

### `fetch` und `pull` im Vergleich

```text
git fetch
    ↓
Neue Remote-Commits kennen und ansehen
    ↓
Eigener Arbeitsbranch bleibt unverändert

git pull
    ↓
Remote-Änderungen holen und integrieren
    ↓
Eigener Arbeitsbranch kann aktualisiert werden
```

**Wichtig:** `pull` ist nicht einfach ein Download einzelner Dateien. Git arbeitet mit Commits, Branches und ihrer gemeinsamen Historie.

## 8. Ein typischer Ablauf vor neuen Änderungen

Wenn du später auf einem gemeinsamen Repository arbeitest, kann dieser Ablauf sinnvoll sein:

```bash
git status
git switch main
git pull --ff-only
git switch -c feature/new-feature
```

Du prüfst zuerst deinen Zustand, bringst dann `main` auf den aktuellen Stand und erstellst anschließend einen neuen Feature-Branch.

Welche Regeln ein Team verwendet, kann sich unterscheiden. Eure konkreten Firmenabläufe behandeln wir **erst später in der Praxis**.

## 9. HTTPS und SSH – nur zur Einordnung

Ein echtes Remote kann statt eines lokalen Ordnerpfads beispielsweise eine URL besitzen:

```text
HTTPS: https://gitlab.example.com/team/project.git
SSH:   git@gitlab.example.com:team/project.git
```

Die Übertragung kann dann eine Authentifizierung benötigen. Welche Methode in eurem Unternehmen verwendet wird und wie man sie einrichtet, ist **nicht Teil dieser Übung**.

Hier benötigst du weder ein Passwort noch einen SSH-Schlüssel, weil unsere drei Repositories auf deinem Rechner liegen.

## 10. Häufige Probleme

**`fatal: not a git repository`**  
Du befindest dich wahrscheinlich im falschen Ordner. Prüfe deinen aktuellen Pfad und wechsle in `git-uebung` beziehungsweise `git-uebung-kopie`.

**`remote origin already exists`**  
Es gibt bereits ein Remote namens `origin`. Prüfe `git remote -v`, statt den Befehl einfach zu wiederholen.

**`git push` oder `git pull` weiß nicht, welchen Branch es verwenden soll.**  
Prüfe deinen Branch und ob ein Upstream eingerichtet ist. Beim ersten Push haben wir dafür `git push -u origin main` verwendet.

**`git pull --ff-only` bricht ab.**  
Möglicherweise haben sich beide Branches unabhängig verändert. Prüfe `git status` und die Historie. Erzwinge keine Synchronisierung und verwende hier insbesondere kein `push --force`.

## Praxisaufgabe – Zwei Arbeitskopien synchronisieren

Führe die Aufgaben mit **deinen drei lokalen Übungsordnern** durch. Du darfst die Erklärungen oben als Nachschlagewerk verwenden.

1. Überprüfe, welches Remote in `git-uebung` als `origin` eingetragen ist.
2. Erkläre, worin sich `git-uebung` und `git-uebung-remote.git` unterscheiden.
3. Erstelle in `git-uebung-kopie` einen weiteren kleinen Commit in einer **neuen Textdatei**, die du selbst benennst. Übertrage ihn zum gemeinsamen Repository.
4. Wechsle zu `git-uebung`. Führe zunächst nur `fetch` aus und untersuche, welche Commits auf `origin/main` neu sind.
5. Prüfe, ob deine neue Datei schon in `git-uebung` vorhanden ist.
6. Übernimm die Änderung anschließend mit `pull --ff-only` und prüfe die Datei erneut.
7. Erkläre anhand deiner Beobachtungen den Unterschied zwischen `fetch` und `pull`.

**Bitte keine direkten Änderungen im Ordner `git-uebung-remote.git` durchführen.**

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Notiere deine Antworten an einem Ort deiner Wahl.

1. Was ist ein Remote-Repository?
2. Kann ein Remote auch auf demselben Rechner liegen?
3. Was bedeutet `origin` typischerweise?
4. Was zeigt `git remote -v`?
5. Was ist der Unterschied zwischen `git commit` und `git push`?
6. Warum verwenden wir beim ersten Push häufig `-u`?
7. Was macht `git fetch`?
8. Was bedeutet `origin/main` in unserem Beispiel?
9. Was macht `git pull` zusätzlich zu `fetch`?
10. Warum ist `git status` vor `pull` und `push` sinnvoll?
11. Was bewirkt `--ff-only` bei unserem `pull`?
12. Warum ändern sich nach einem `push` nicht automatisch die Dateien in der anderen Arbeitskopie?

## Abschluss-Checkliste

- [ ] Ich kann den Unterschied zwischen lokalem und gemeinsamem Repository erklären.
- [ ] Ich habe ein lokales Bare Repository als Übungs-Remote angelegt.
- [ ] Ich habe `origin` eingerichtet und mit `git remote -v` überprüft.
- [ ] Ich habe meinen `main`-Branch erstmals gepusht.
- [ ] Ich habe eine zweite Arbeitskopie mit `git clone` erstellt.
- [ ] Ich habe aus dieser Kopie eine Änderung gepusht.
- [ ] Ich habe mit `fetch` eine Remote-Änderung untersucht, ohne sie sofort zu übernehmen.
- [ ] Ich habe die Änderung mit `pull --ff-only` übernommen.
- [ ] Ich kann den Unterschied zwischen `commit`, `push`, `fetch` und `pull` erklären.

## Zusammenfassung

```text
commit → Änderungen im eigenen Repository speichern
push   → eigene Commits zu einem anderen Repository übertragen
fetch  → neue Remote-Commits holen, ohne sie direkt zu integrieren
pull   → Remote-Commits holen und in den aktuellen Branch integrieren
```

Jetzt kennst du die Git-Seite der Zusammenarbeit. Im nächsten Unterkapitel schauen wir uns an, wie **GitLab** Repositories, Branches und Zusammenarbeit in einer Weboberfläche organisiert.

[Weiter: GitLab-Grundlagen →](./08-gitlab-grundlagen.md)
