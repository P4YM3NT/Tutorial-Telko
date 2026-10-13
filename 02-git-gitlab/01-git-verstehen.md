# 01 – Git verstehen

[← Zurück zur Übersicht](./README.md) | [Weiter: Repository, Status und Änderungen →](./02-repository-status.md)

Git ist ein **Versionsverwaltungssystem**. Es hilft uns dabei, Änderungen an Dateien über die Zeit nachvollziehbar zu speichern.

## Warum brauchen wir Versionsverwaltung?

Stell dir vor, ein Projekt wird ohne Git entwickelt:

```text
projekt/
projekt-neu/
projekt-neu-final/
projekt-neu-final-wirklich/
projekt-neu-final-wirklich-2/
```

Schnell ist unklar, welche Version die aktuelle ist und was zwischen den Ordnern geändert wurde.

Mit Git verwenden wir stattdessen **ein Projekt** und speichern bewusst nachvollziehbare Zwischenstände.

Diese Zwischenstände heißen **Commits**.

## Ein Commit ist ein gespeicherter Projektstand

Ein einfaches Beispiel für unser späteres Lernprojekt CashFlow:

```text
Commit A: Erste Projektdateien
   ↓
Commit B: Beschreibung des Dashboards ergänzt
   ↓
Commit C: Schreibfehler korrigiert
```

Ein Commit gehört zur Git-Historie. Er besitzt unter anderem eine Kennung, einen Autor, einen Zeitpunkt und eine Nachricht, die den Zweck der Änderung beschreibt.

Die technischen Details lernst du in den nächsten Abschnitten.

## Git arbeitet zunächst lokal

Git kann auf deinem eigenen Rechner arbeiten, auch ohne eine Verbindung zu GitLab.

Du kannst beispielsweise:

- Änderungen prüfen,
- Commits erstellen,
- Branches anlegen,
- die Historie ansehen.

Erst für das Teilen und gemeinsame Bearbeiten von Änderungen kommt typischerweise ein **Remote-Repository**, etwa auf eurem Firmen-GitLab, dazu.

> **Merke:** Eine Datei in VS Code zu speichern oder einen Commit in Git zu erstellen bedeutet noch nicht, dass die Änderung automatisch auf GitLab liegt.

## Was ist ein Repository?

Ein **Repository** (kurz **Repo**) ist ein von Git verwaltetes Projekt.

Neben den normalen Projektdateien speichert Git seine internen Informationen üblicherweise im versteckten Verzeichnis:

```text
.git/
```

Diesen Ordner bearbeiten wir normalerweise nicht von Hand.

Für die Übungen verwenden wir später ein **eigenes Übungsrepository**. So musst du keine Änderungen am Tutorial-Repository selbst vornehmen.

## Drei wichtige Bereiche: Arbeitsverzeichnis, Staging Area und Repository

Vereinfacht kannst du dir den Ablauf so vorstellen:

```text
Arbeitsverzeichnis
   │  Datei bearbeiten und speichern
   ▼
Änderungen an Dateien
   │  git add
   ▼
Staging Area
   │  git commit
   ▼
Git-Repository (Commit-Historie)
```

### Arbeitsverzeichnis

Hier liegen die Dateien, die du in VS Code bearbeitest. Wenn du beispielsweise einen Satz in `README.md` änderst, ändert sich zunächst die Datei auf deinem Rechner.

### Staging Area

Die Staging Area ist eine Art **Auswahlbereich für den nächsten Commit**. Mit `git add` legst du fest, welche Änderungen Git für den nächsten Commit berücksichtigen soll.

### Git-Repository

Mit `git commit` speicherst du die ausgewählten Änderungen als neuen Commit in der lokalen Git-Historie.

Dabei gilt: `git add` und `git commit` sind unterschiedliche Schritte.

## Datei speichern, committen und pushen – drei unterschiedliche Dinge

| Aktion | Bedeutung |
|---|---|
| Datei in VS Code speichern | Aktualisiert die Datei auf deinem Rechner |
| `git add` | Merkt Änderungen für den nächsten Commit vor |
| `git commit` | Speichert diese Änderungen in deiner lokalen Git-Historie |
| `git push` | Überträgt lokale Commits später zu einem Remote-Repository |

`git push` verwenden wir erst in einem späteren Unterkapitel. Hier sollst du den Unterschied zunächst nur kennen.

## Kleine Übung – Den Ablauf verstehen

Ordne die folgenden Aktionen den passenden Bereichen oder Schritten zu:

```text
A – Eine Datei in VS Code verändern
B – git add README.md
C – git commit -m "Update README"
D – git push
```

Verwende diese Begriffe:

```text
Arbeitsverzeichnis
Staging Area
lokale Commit-Historie
Remote-Repository
```

Notiere deine Zuordnung an einem Ort deiner Wahl. Du musst dafür noch keine Befehle ausführen.

## Kleine Denkaufgabe – Was ist schon gespeichert?

Du änderst in CashFlow später eine Datei und speicherst sie in VS Code. Danach schließt du VS Code.

Beantworte mit eigenen Worten:

1. Ist deine Änderung jetzt auf deinem Rechner gespeichert?
2. Ist dadurch automatisch ein Git-Commit entstanden?
3. Ist die Änderung dadurch bereits in GitLab angekommen?
4. Welche Schritte fehlen, um sie später als Commit nach GitLab zu übertragen?

## Wissenscheck

Beantworte die Fragen möglichst ohne Nachschlagen. Wenn du nicht weiterkommst, darfst du die Erklärungen erneut lesen.

1. Was ist Git und wofür verwenden wir es?
2. Was ist ein Repository?
3. Was ist ein Commit?
4. Funktioniert Git auch ohne GitLab?
5. Was ist die Staging Area?
6. Was ist der Unterschied zwischen dem Speichern einer Datei und einem Commit?
7. Warum ist ein Commit nicht automatisch auf GitLab verfügbar?

## Zusammenfassung

```text
Datei verändern
      ↓
mit git add auswählen
      ↓
mit git commit lokal speichern
      ↓
später mit git push teilen
```

Als Nächstes legen wir ein Übungsrepository an und beobachten mit `git status`, wie Git neue und geänderte Dateien erkennt.

[Weiter: Repository, Status und Änderungen →](./02-repository-status.md)
