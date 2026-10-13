# 11 – Praxisworkflow

[← Zurück: .gitignore und sensible Daten](./10-gitignore-sicherheit.md) | [Weiter: Wissenscheck →](./12-wissenscheck.md)

Bisher hast du die einzelnen Git-Befehle kennengelernt: Du hast Änderungen geprüft, Commits erstellt, Branches angelegt, einen Konflikt gelöst und Änderungen zwischen lokalen Repositories ausgetauscht.

Jetzt verbinden wir diese Schritte zu einem **vollständigen Arbeitsablauf**. So ähnlich wird später auch die Entwicklung unserer App **CashFlow** organisiert.

Wir verwenden weiterhin **nur deine lokalen Übungsrepositories**. Du brauchst kein Firmen-GitLab und musst noch kein JavaScript programmieren.

## Lernziele

Nach diesem Unterkapitel kannst du:

- aus einer kleinen Anforderung eine nachvollziehbare Änderung machen,
- den Hauptbranch vor einer neuen Aufgabe prüfen und aktualisieren,
- eine Änderung auf einem Feature-Branch vorbereiten und committen,
- deinen Branch auf das lokale Remote pushen,
- eine Merge-Request-Beschreibung entwerfen und die Änderung überprüfen,
- den Feature-Branch lokal zusammenführen und den Hauptbranch synchronisieren,
- erklären, welche Schritte später über GitLab stattfinden.

## 1. Unsere Ausgangssituation

Du arbeitest mit den Repositories aus den bisherigen Unterkapiteln:

```text
webentwicklung/
├── git-uebung/             ← deine erste Arbeitskopie
├── git-uebung-kopie/       ← zweite Arbeitskopie aus Kapitel 07
└── git-uebung-remote.git/  ← gemeinsames lokales Repository
```

Wir bearbeiten **ausschließlich `git-uebung/`**. Das zweite Arbeitsverzeichnis benötigen wir in dieser Übung nicht.

Du solltest Kapitel 07 und 10 abgeschlossen haben. Falls dein Git-Status noch Änderungen oder einen laufenden Merge anzeigt, kläre das mit deiner betreuenden Person, bevor du weitermachst.

> **Sicherheit:** Führe die folgenden Befehle nicht im Tutorial-Repository und nicht in einem Firmenprojekt aus. Verwende keine echten Zugangsdaten oder Finanzdaten.

## 2. Das fiktive Issue

Stell dir vor, für CashFlow gibt es folgende Anforderung:

```text
Issue #12 – CashFlow-Konzept dokumentieren

Als neues Teammitglied möchte ich kurz nachlesen können,
was CashFlow ist und welche Funktionen später geplant sind.

Akzeptanzkriterien:
- Es gibt eine Datei cashflow-konzept.md.
- Die Datei beschreibt CashFlow in wenigen eigenen Sätzen.
- Sie nennt mindestens zwei geplante Funktionen.
- Die Änderung wird auf einem eigenen Feature-Branch erstellt.
```

Das ist **nur ein Übungs-Issue**. Du musst es nicht in GitLab anlegen. Später kann dieselbe Vorgehensweise für echte Aufgaben verwendet werden.

Warum eine Markdown-Datei statt Anwendungscode? Du sollst hier **Git üben**, nicht gleichzeitig neue JavaScript-Konzepte lernen.

## 3. Schritt 1 – Den Ausgangszustand prüfen

Öffne `git-uebung/` in VS Code und überprüfe:

```bash
git status
git branch --show-current
```

Wechsle, falls nötig, auf `main`:

```bash
git switch main
```

Aktualisiere `main` aus unserem **lokalen Übungs-Remote**:

```bash
git pull --ff-only
```

Mit `--ff-only` erlaubst du in dieser Übung nur ein Fast-Forward. Falls das nicht möglich ist, bricht Git ab. Prüfe dann den Zustand, statt wahllos andere Befehle auszuprobieren.

> **Merke:** Vor einer neuen Aufgabe prüfen wir, auf welchem Branch wir arbeiten und ob ungespeicherte Änderungen vorhanden sind.

## 4. Schritt 2 – Feature-Branch erstellen

Für unser Übungs-Issue verwenden wir den Branch-Namen:

```text
feature/12-cashflow-konzept
```

Erstelle ihn und wechsle direkt darauf:

```bash
git switch -c feature/12-cashflow-konzept
```

Prüfe mit `git branch --show-current`, ob du auf dem richtigen Branch bist.

Der Name zeigt, **wofür** die Änderung gedacht ist. In echten Teams können andere Namenskonventionen gelten.

## 5. Schritt 3 – Die Änderung umsetzen

Erstelle im Ordner `git-uebung/` eine neue Datei:

```text
cashflow-konzept.md
```

Die Datei soll enthalten:

1. eine Überschrift mit dem Namen **CashFlow**,
2. eine kurze Beschreibung der geplanten Personal-Finance-App in deinen eigenen Worten,
3. eine Liste mit mindestens zwei späteren Funktionen, zum Beispiel Einnahmen und Ausgaben erfassen oder Transaktionen filtern.

Du musst dafür weder die App bauen noch eine bestimmte Musterformulierung übernehmen.

## 6. Schritt 4 – Änderungen prüfen und committen

Bevor du einen Commit erstellst, prüfe:

```bash
git status
```

Da du eine **neue, noch nicht verfolgte Datei** angelegt hast, zeigt `git diff` deren Inhalt zunächst normalerweise **nicht**. Das ist ein wichtiger Unterschied zu einer bereits verfolgten, geänderten Datei.

Füge die neue Datei deshalb **gezielt** zur Staging Area hinzu:

```bash
git add cashflow-konzept.md
```

Prüfe die Änderungen, die im Commit landen sollen:

```bash
git diff --staged
git status
```

Kontrolliere:

- Ist die richtige Datei enthalten?
- Erfüllt sie die Akzeptanzkriterien des Issues?
- Sind versehentlich andere Dateien gestaged?
- Enthält sie ausschließlich ungefährliche Beispieldaten?

Erstelle anschließend einen Commit mit einer passenden Nachricht:

```bash
git commit -m "Document CashFlow concept"
```

Prüfe deinen neuesten Commit:

```bash
git log -1 --oneline
```

## 7. Schritt 5 – Feature-Branch pushen

In Kapitel 07 hast du das lokale Repository `git-uebung-remote.git` als `origin` eingerichtet. Dort veröffentlichst du jetzt deinen Feature-Branch:

```bash
git push -u origin feature/12-cashflow-konzept
```

Damit liegen die Commits deines Feature-Branches auch im **gemeinsamen lokalen Übungsrepository**. `main` wurde dadurch **noch nicht** verändert.

Prüfe bei Bedarf mit `git branch -r`, welche Remote-Branches Git kennt.

## 8. Schritt 6 – Merge Request als Entwurf vorbereiten

In einem echten GitLab-Projekt würdest du nun einen **Merge Request** eröffnen. Wir schreiben für diese Übung lediglich einen Entwurf an einem Ort deiner Wahl, zum Beispiel in deinen Notizen.

Notiere:

```text
Source Branch: feature/12-cashflow-konzept
Target Branch: main
```

Verwende diese Struktur:

```markdown
## Was wurde geändert?

## Warum?

## Wie wurde getestet?
```

Beschreibe **nur Prüfungen, die du tatsächlich durchgeführt hast**, als getestet. Weitere sinnvolle Prüfungen kannst du ausdrücklich als *noch geplant* kennzeichnen.

> **Wichtig:** Ein Branch-Push erstellt bei unserem lokalen Bare Repository **keinen** GitLab-Merge-Request. Diesen Arbeitsschritt simulieren wir bewusst nur auf Papier beziehungsweise in einer Notiz.

## 9. Schritt 7 – Die Änderung wie bei einem Review prüfen

Betrachte den Unterschied zwischen dem Hauptbranch und deinem Feature-Branch:

```bash
git diff main...feature/12-cashflow-konzept
```

Die drei Punkte bedeuten hier vereinfacht: Zeige die Änderungen, die seit dem gemeinsamen Ausgangspunkt auf dem Feature-Branch entstanden sind.

Prüfe die Änderung anhand der Akzeptanzkriterien. Ein Review fragt nicht nur, **ob** eine Datei geändert wurde, sondern **ob die Anforderung sinnvoll erfüllt ist**.

Falls du einen Fehler entdeckst, korrigiere die Datei auf dem Feature-Branch, prüfe sie erneut, erstelle einen weiteren Commit und pushe ihn. Ein späterer GitLab-Merge-Request würde solche zusätzlichen Commits automatisch anzeigen.

## 10. Schritt 8 – Lokal zusammenführen

In einem Team würde nach Review und Freigabe häufig GitLab die Änderungen in den Zielbranch übernehmen. Wir führen den Merge **nur lokal im Übungsrepository** durch.

Prüfe zunächst, ob dein Arbeitsverzeichnis sauber ist:

```bash
git status
```

Wechsle auf `main`:

```bash
git switch main
```

Führe den Feature-Branch zusammen:

```bash
git merge feature/12-cashflow-konzept
```

Wenn `main` seit dem Erstellen des Feature-Branches unverändert geblieben ist, kann Git einen **Fast-Forward-Merge** durchführen. Falls ein Konflikt entsteht, nutze dein Wissen aus Kapitel 06 und bitte bei Bedarf um Unterstützung.

Überprüfe den Zustand:

```bash
git status
git log --oneline -5
```

Die Datei `cashflow-konzept.md` sollte jetzt auch auf `main` vorhanden sein.

Übertrage den aktualisierten Hauptbranch in dein **lokales** Übungs-Remote:

```bash
git push origin main
```

Erst jetzt enthält auch `main` im gemeinsamen Repository die neue Änderung.

### Optional: Aufräumen

Wenn der Branch vollständig in `main` zusammengeführt wurde und du ihn nicht mehr benötigst, kannst du den **lokalen** Branch löschen:

```bash
git branch -d feature/12-cashflow-konzept
```

Das Löschen des Remote-Branches behandeln wir hier nicht. Es ist für das Lernziel nicht notwendig.

## 11. Der gesamte Workflow

```text
Anforderung / Issue verstehen
             ↓
        main prüfen
             ↓
     Feature-Branch
             ↓
       Datei ändern
             ↓
   status + staged diff
             ↓
           Commit
             ↓
    Branch zum Remote
             ↓
     MR-Entwurf + Review
             ↓
       lokaler Merge
             ↓
       main pushen
```

In dieser Übung sind **Push und Merge echte Git-Operationen**. Der **Merge Request und das Review** werden nur simuliert. So trennen wir Git-Grundlagen und spätere Firmen-GitLab-Praxis sauber voneinander.

## Praxisaufgabe – Workflow erklären

Notiere die Antworten an einem Ort deiner Wahl:

1. Warum haben wir vor der Aufgabe zuerst `main` geprüft?
2. Weshalb wurde für das fiktive Issue ein Feature-Branch verwendet?
3. Warum war die neue Datei vor `git add` nicht im normalen `git diff` zu sehen?
4. Was zeigt `git diff --staged`?
5. Was ist der Unterschied zwischen dem Push des Feature-Branches und dem späteren Merge in `main`?
6. Warum gibt es in unserem lokalen Übungsrepository keinen echten Merge Request?
7. Woran erkennst du, dass die Änderung am Ende auf `main` angekommen ist?

## Wissenscheck

1. Welche Informationen sollte ein verständliches Issue enthalten?
2. Woran erkennst du vor einem Commit, welche Änderungen aufgenommen werden?
3. Was bewirkt `git push -u origin <branch>` grundsätzlich?
4. Warum führen wir Änderungen in Teams nicht immer direkt auf `main` aus?
5. Was ist der Unterschied zwischen einem Merge Request und einem Merge?
6. Was solltest du nach einem Review tun, wenn noch Änderungen nötig sind?
7. Was bedeutet ein Fast-Forward-Merge?
8. Welche Schritte aus diesem Unterkapitel wurden ohne GitLab wirklich ausgeführt und welche nur beschrieben?

## Abschluss-Checkliste

- [ ] Ich habe die Aufgabe in meinem lokalen `git-uebung`-Repository umgesetzt.
- [ ] Ich habe meinen Feature-Branch erstellt und einen Commit angelegt.
- [ ] Ich habe den Feature-Branch in das lokale Remote gepusht.
- [ ] Ich habe einen Merge-Request-Entwurf geschrieben und die Änderung überprüft.
- [ ] Ich habe den Branch lokal in `main` zusammengeführt.
- [ ] Ich habe `main` mit dem lokalen Remote synchronisiert.
- [ ] Ich kann die wichtigsten Schritte und ihren Zweck erklären.

Im letzten Unterkapitel überprüfst du dein Wissen und führst eine kleinere Aufgabe weitgehend selbstständig durch.

[Weiter: Wissenscheck →](./12-wissenscheck.md)
