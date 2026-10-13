# 08 – GitLab-Grundlagen

[← Zurück: Remote, Push und Pull](./07-remote-push-pull.md) | [Weiter: Issues und Merge Requests →](./09-issues-merge-requests.md)

In den letzten Kapiteln hast du **Git** auf deinem Rechner verwendet. In Kapitel 07 hast du sogar mehrere lokale Repositories miteinander verbunden und Änderungen mit `push`, `fetch` und `pull` ausgetauscht.

**GitLab** ergänzt Git um eine Oberfläche und Werkzeuge für die Zusammenarbeit im Team. Hier schauen wir uns die wichtigsten Begriffe an. Du musst dich dafür **noch nicht in eurem Firmen-GitLab einrichten** und auch keine Änderungen an einem echten Teamprojekt durchführen. Das üben wir später in der Praxis.

## Lernziele

Nach diesem Kapitel kannst du:

- den Unterschied zwischen **Git** und **GitLab** erklären,
- ein **GitLab-Projekt** von seinem **Git-Repository** unterscheiden,
- erklären, wofür Gruppen, Mitglieder und Rollen verwendet werden,
- die Begriffe **Default Branch** und **geschützter Branch** einordnen,
- verstehen, warum Teams mit **Merge Requests** arbeiten,
- erkennen, welche Informationen GitLab zu einem Commit zeigt,
- grob erklären, wozu eine **CI/CD-Pipeline** dient.

## 1. Git und GitLab – was ist der Unterschied?

**Git** ist das Versionsverwaltungssystem, das du über Befehle wie `git status`, `git commit` und `git push` kennengelernt hast.

**GitLab** ist eine Plattform, auf der Teams Git-Repositories gemeinsam verwalten und ihre Arbeit organisieren können.

```text
Git auf deinem Rechner                 GitLab
┌──────────────────────┐               ┌───────────────────────────┐
│ Dateien bearbeiten   │               │ Gemeinsames Repository   │
│ Commits erstellen    │ ── push ──→   │ Issues und Merge Requests│
│ Branches verwalten   │ ←─ fetch ──   │ Reviews und Pipelines     │
└──────────────────────┘               └───────────────────────────┘
```

Du kennst das Prinzip schon aus Kapitel 07: Dort war das gemeinsame Repository ein **lokaler Ordner**. Bei GitLab liegt es normalerweise auf einem Server und ist über die Plattform erreichbar.

> **Merke:** Ein Commit entsteht zunächst mit Git. GitLab macht die gemeinsame Arbeit mit diesen Commits und Branches leichter. GitLab ersetzt Git nicht.

## 2. Was ist ein GitLab-Projekt?

In GitLab findet die Arbeit normalerweise in einem **Projekt** statt.

Ein Projekt kann unter anderem enthalten:

- ein Git-Repository mit Dateien, Branches und Commits,
- **Issues** für Aufgaben und Fehler,
- **Merge Requests** für vorgeschlagene Codeänderungen,
- Mitglieder und ihre Berechtigungen,
- Konfiguration und Ergebnisse automatischer **Pipelines**,
- weitere Dokumentation.

Ein **Git-Repository** ist also ein wichtiger **Bestandteil** eines GitLab-Projekts. Das Projekt bietet zusätzliche Funktionen rund um das Repository.

### Was ist eine Gruppe?

GitLab kann mehrere Projekte in **Gruppen** organisieren. Beispielsweise könnte ein Team eine Gruppe besitzen, unter der verschiedene Anwendungen liegen.

Das ist nur ein mögliches Organisationsmodell. Wie Projekte und Gruppen in eurem Unternehmen angeordnet sind, besprechen wir später.

## 3. Repository, Branches und Commits in GitLab

Im Repository eines GitLab-Projekts kannst du typischerweise finden:

- Projektdateien und Ordner,
- vorhandene Branches,
- die Historie der Commits,
- Tags, mit denen beispielsweise bestimmte Stände markiert werden.

Bei einem Commit lassen sich in GitLab häufig die **Commit-Nachricht**, der **Autor**, der **Zeitpunkt** und die **Änderungen (Diff)** ansehen.

Das kennst du bereits aus der Kommandozeile:

| Git-Befehl | Vergleichbare Information in GitLab |
|---|---|
| `git branch` | Vorhandene Branches |
| `git log` | Commit-Historie |
| `git show` oder `git diff` | Änderungen an Dateien |

Die GitLab-Oberfläche ist eine weitere Möglichkeit, diese Informationen zu betrachten. Die genauen Menübezeichnungen können je nach Version unterschiedlich sein.

## 4. Projektmitglieder und Rollen

Nicht jedes Teammitglied darf automatisch alles in einem GitLab-Projekt tun.

Über **Mitglieder**, **Rollen** und **Berechtigungen** lässt sich festlegen, wer beispielsweise:

- Quellcode lesen,
- Änderungen auf bestimmte Branches pushen,
- Merge Requests erstellen,
- Änderungen zusammenführen,
- Projekteinstellungen verändern darf.

Welche Aktion tatsächlich erlaubt ist, hängt unter anderem von der jeweiligen Rolle und den Projekteinstellungen ab.

**Wichtig:** Diese GitLab-Rollen sind etwas anderes als die Benutzerrollen, die wir eventuell später für die CashFlow-App selbst entwickeln. Hier geht es um die Zusammenarbeit **am Quellcode**, nicht um Zugriffsrechte innerhalb der fertigen App.

## 5. Default Branch und geschützte Branches

### Default Branch

Der **Default Branch** ist der voreingestellte Hauptbranch eines Projekts. Er heißt häufig:

```text
main
```

Er kann in anderen Projekten auch anders heißen. Beim Arbeiten mit Git solltest du deshalb nicht ungeprüft davon ausgehen, dass der Hauptbranch immer `main` heißt.

### Geschützte Branches

GitLab kann Branches schützen und festlegen, **wer dorthin pushen oder Änderungen zusammenführen darf**.

Das ist besonders für den Hauptbranch sinnvoll. Ein Team kann damit zum Beispiel einen Ablauf vorsehen, bei dem eine Änderung erst geprüft werden muss, bevor sie in den Hauptbranch gelangt.

```text
Feature-Branch
      ↓
Änderung nach GitLab pushen
      ↓
Merge Request erstellen
      ↓
Änderung prüfen (Review)
      ↓
In den Hauptbranch mergen
```

Ein geschützter Branch bedeutet nicht, dass dort niemals Änderungen ankommen. Es bedeutet, dass **bestimmte Regeln für Änderungen** gelten können.

> **Beispiel CashFlow:** Später könnte eine neue Funktion wie „Transaktionen nach Kategorie filtern“ auf `feature/category-filter` entwickelt werden. Erst nach einer Prüfung wird sie in den Hauptbranch übernommen. **Die Funktion programmieren wir hier noch nicht.**

## 6. Was sind Issues und Merge Requests?

Diese Begriffe lernst du im nächsten Unterkapitel ausführlich kennen. Für den Anfang reicht:

- **Issue:** Beschreibt eine Aufgabe, einen Fehler oder eine gewünschte Verbesserung.
- **Merge Request (MR):** Schlägt vor, Änderungen aus einem Branch in einen anderen zu übernehmen. Andere können die Änderungen ansehen und Feedback geben.

Beispiel für CashFlow:

```text
Issue:
"Transaktionen sollen nach Kategorie filterbar sein."

Branch:
feature/category-filter

Merge Request:
"Kategorie-Filter ergänzen"
```

Ein Merge Request ist **nicht bereits der Merge selbst**. Er ist zunächst der Vorschlag, die Änderungen zu übernehmen.

## 7. Was ist eine Pipeline?

GitLab kann bei Ereignissen wie einem Push oder einem Merge Request automatisch festgelegte Arbeitsschritte ausführen. Eine solche Abfolge heißt **Pipeline**.

Typische Schritte können sein:

```text
Lint    → Code auf bestimmte Regeln prüfen
Test    → Automatische Tests ausführen
Build   → Anwendung für die Ausführung vorbereiten
Deploy  → Anwendung bereitstellen
```

Nicht jedes Projekt führt alle Schritte aus. Welche Schritte existieren, hängt von der Konfiguration ab.

Eine Pipeline kann beispielsweise anzeigen, ob die Prüfungen **erfolgreich** waren oder **fehlgeschlagen** sind. Das kann einem Team vor dem Zusammenführen von Änderungen wichtige Hinweise geben.

**Noch nicht nötig:** Du musst jetzt keine Pipeline schreiben, starten oder konfigurieren. Das behandeln wir später beim Thema CI/CD.

## 8. Übung – Begriffe einem GitLab-Projekt zuordnen

Stell dir ein fiktives GitLab-Projekt für CashFlow vor. Du musst dafür **kein echtes GitLab-Projekt öffnen oder anlegen**.

Ordne die folgenden Aussagen jeweils dem passendsten Begriff zu:

**Begriffe:** Projekt, Repository, Issue, Merge Request, geschützter Branch, Pipeline

1. Hier werden die Dateien und die Git-Historie der Anwendung verwaltet.
2. Hier steht, dass ein Filter nach Kategorien ergänzt werden soll.
3. Hier schlägt ein Entwickler vor, seinen Feature-Branch in den Hauptbranch zu übernehmen.
4. Hier können Repository, Aufgaben, Mitglieder und weitere Werkzeuge zusammengefasst sein.
5. Hier wird geregelt, wer Änderungen direkt auf `main` übertragen darf.
6. Hier laufen beispielsweise automatische Tests.

Notiere deine Zuordnung an einem Ort deiner Wahl. Die Lösungen sind nicht in dieser Datei enthalten.

## 9. Kleine Denkaufgabe – Eine Änderung bei CashFlow

Stell dir folgenden Ablauf vor:

1. Für CashFlow wird eine neue Funktion gewünscht.
2. Ein Entwickler erstellt dafür einen Feature-Branch.
3. Der Entwickler committet seine Änderungen und pusht den Branch.
4. Anschließend erstellt er einen Merge Request.
5. Andere Teammitglieder prüfen die Änderung. Eine Pipeline führt automatische Tests aus.
6. Nach erfolgreicher Prüfung kann die Änderung in den Hauptbranch übernommen werden.

Beantworte mit eigenen Worten:

1. Wofür könnte das Issue in diesem Ablauf verwendet werden?
2. Warum wurde nicht direkt auf `main` entwickelt?
3. Was ist der Zweck des Merge Requests?
4. Was kann die Pipeline prüfen?
5. Bedeutet ein erfolgreicher Testlauf automatisch, dass die Änderung ohne menschliche Prüfung übernommen werden muss?

Hier geht es um **Verstehen und Erklären**, nicht um GitLab-Konfiguration oder Programmierung.

## Wissenscheck

1. Was ist der Unterschied zwischen Git und GitLab?
2. Was ist ein GitLab-Projekt?
3. Wie unterscheiden sich ein GitLab-Projekt und ein Git-Repository?
4. Wozu können Gruppen in GitLab dienen?
5. Welche Informationen kannst du zu einem Commit in GitLab finden?
6. Wofür sind Projektrollen und Berechtigungen da?
7. Was ist ein Default Branch?
8. Warum können Branches geschützt werden?
9. Was ist ein Issue?
10. Was ist ein Merge Request?
11. Was macht eine Pipeline grundsätzlich?
12. Sind GitLab-Projektrollen und Benutzerrollen in CashFlow dasselbe?

## Zusammenfassung

Git verwaltet unsere Versionshistorie. GitLab ergänzt Funktionen, mit denen Teams an einem Projekt zusammenarbeiten können:

```text
GitLab-Projekt
├── Repository (Dateien, Branches, Commits)
├── Issues (Aufgaben)
├── Merge Requests (Änderungen vorschlagen und prüfen)
├── Mitglieder und Berechtigungen
└── Pipelines (automatische Arbeitsschritte)
```

Du kennst jetzt die wichtigsten Begriffe. Im nächsten Kapitel sehen wir uns **Issues und Merge Requests** genauer an.

[Weiter: Issues und Merge Requests →](./09-issues-merge-requests.md)
