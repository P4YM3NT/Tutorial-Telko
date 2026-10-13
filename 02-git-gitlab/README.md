# 02 – Git & GitLab

Willkommen im Kapitel **Git & GitLab**.

Im Installationskapitel hast du Git bereits eingerichtet. Jetzt lernst du, wie du Änderungen an einem Projekt nachvollziehbar speicherst und über GitLab mit anderen zusammenarbeitest.

Du brauchst dafür **noch keine JavaScript-Kenntnisse**. Wir üben Git zunächst mit einfachen Textdateien und kleinen, bereits bekannten JavaScript-Beispielen.

## Lernziele

Nach diesem Kapitel kannst du:

- erklären, wofür Git verwendet wird und wie es sich von GitLab unterscheidet,
- ein Repository erkennen, klonen oder für eine Übung neu anlegen,
- Änderungen mit `git status` und `git diff` überprüfen,
- Dateien gezielt mit `git add` stagen und mit `git commit` speichern,
- die Commit-Historie mit `git log` lesen,
- Branches erstellen, wechseln und einfache Merges verstehen,
- einen Merge-Konflikt erkennen und mit Unterstützung auflösen,
- die Unterschiede zwischen `fetch`, `pull` und `push` erklären,
- GitLab-Projekte, Issues und Merge Requests grundlegend verwenden,
- den Zweck von `.gitignore` erklären und sensible Daten aus Git heraushalten,
- einen einfachen Workflow vom Issue bis zum Merge Request durchlaufen.

## Kapitelübersicht

1. [Git verstehen](./01-git-verstehen.md)
2. [Repository, Status und Änderungen](./02-repository-status.md)
3. [Staging und Commits](./03-staging-commits.md)
4. [Historie und Unterschiede](./04-log-diff.md)
5. [Branches](./05-branches.md)
6. [Merge und Konflikte](./06-merge-konflikte.md)
7. [Remote, Push und Pull](./07-remote-push-pull.md)
8. [GitLab-Grundlagen](./08-gitlab-grundlagen.md)
9. [Issues und Merge Requests](./09-issues-merge-requests.md)
10. [.gitignore und sensible Daten](./10-gitignore-sicherheit.md)
11. [Praxisworkflow](./11-praxisworkflow.md)
12. [Wissenscheck](./12-wissenscheck.md)

## Git und GitLab – der Unterschied

```text
Git
→ Versionsverwaltung für Änderungen an deinem Projekt

GitLab
→ Plattform für die gemeinsame Arbeit mit Git-Repositories
```

Git kann auch ohne GitLab auf deinem Rechner verwendet werden. In eurem Unternehmen nutzt ihr GitLab zusätzlich für die Zusammenarbeit.

Ein typischer Ablauf sieht später so aus:

```text
Issue lesen
     ↓
Feature-Branch anlegen
     ↓
Dateien ändern und prüfen
     ↓
Änderungen committen
     ↓
Branch nach GitLab pushen
     ↓
Merge Request erstellen
     ↓
Review und gegebenenfalls Nachbesserung
     ↓
Merge
```

## Unser Lernprojekt CashFlow

Im Laufe des Tutorials entwickelst du **CashFlow**, eine Webanwendung zur Verwaltung fiktiver Einnahmen und Ausgaben.

Git wird uns dabei begleiten: Jede neue Funktion kann auf einem eigenen Branch entstehen und über einen Merge Request geprüft werden.

**Wichtig:** In diesem Kapitel bauen wir CashFlow noch nicht. Wir lernen den Git-Workflow zuerst in einem **separaten Übungsrepository**, damit du die Befehle ohne Risiko ausprobieren kannst.

Spätere Branch-Namen könnten zum Beispiel so aussehen:

```text
feature/transaction-list
feature/category-filter
fix/incorrect-total
```

Du musst jetzt noch nicht verstehen, wie diese Funktionen programmiert werden.

## Sicher üben

- Verwende für Git-Übungen ein eigenes Repository oder ein ausdrücklich dafür freigegebenes Firmenprojekt.
- Arbeite bei Teamprojekten nicht ohne Absprache direkt auf dem Hauptbranch.
- Prüfe mit `git status`, bevor du Änderungen übernimmst oder Befehle ausführst, die Dateien verändern.
- Committe keine Passwörter, Tokens oder echten Finanzdaten.
- Nutze für Fragen und Aufgaben die vorherigen Kapitel als Nachschlagewerk. Musterlösungen gehören nicht zum Studentenmaterial.

> **Merke:** Git soll dir helfen, Änderungen zu verstehen und nachzuvollziehen. Du musst nicht alle Befehle auswendig lernen – wichtig ist, ihren Zweck zu verstehen.

[Weiter: Git verstehen →](./01-git-verstehen.md)
