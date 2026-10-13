# 12 – Praxis und Wissenscheck

[← Zurück: Praxisworkflow](./11-praxisworkflow.md) | [Zurück zur Übersicht](./README.md)

Zum Abschluss von **02 – Git & GitLab** überprüfst du, ob du die wichtigsten Werkzeuge und Abläufe selbstständig anwenden und erklären kannst.

Dieses Kapitel besteht aus zwei Teilen:

1. **Abschlussaufgabe:** Eine kleine Änderung eigenständig mit Git bearbeiten.
2. **Wissenscheck:** Die wichtigsten Begriffe und Befehle mit eigenen Worten erklären.

**Wichtig:** Versuche die Aufgaben zuerst selbstständig zu lösen. Du darfst in den vorherigen Kapiteln nachschlagen. Notiere Antworten auf die Wissensfragen an einem Ort deiner Wahl, zum Beispiel auf Papier oder in einer eigenen Textdatei. Hier stehen **keine Musterlösungen**.

## Abschlussaufgabe – Eine neue CashFlow-Idee dokumentieren

Du nutzt weiterhin das lokale Repository `git-uebung` und das lokale Remote aus Kapitel 07. **Arbeite nicht im Tutorial-Repository und nicht im Firmen-GitLab.**

### Ausgangssituation

Das fiktive Team möchte die geplanten Kategorien von CashFlow dokumentieren. Eine Kategorie beschreibt, wofür eine Einnahme oder Ausgabe steht, beispielsweise Lebensmittel oder Gehalt.

### Dein Auftrag

Führe die folgenden Schritte möglichst eigenständig aus:

1. **Issue entwerfen:** Formuliere für diese kleine Änderung einen verständlichen Titel, eine kurze Beschreibung und mindestens **drei überprüfbare Akzeptanzkriterien**.
2. **Ausgangszustand prüfen:** Arbeite auf einem aktuellen `main` mit sauberem Arbeitsverzeichnis.
3. **Feature-Branch erstellen:** Wähle einen passenden, aussagekräftigen Namen.
4. **Datei bearbeiten:** Ergänze in `cashflow-konzept.md` einen Abschnitt **„Beispielkategorien“** mit mindestens drei unterschiedlichen, fiktiven Einnahmen- oder Ausgabenkategorien.
5. **Änderung prüfen:** Kontrolliere, welche Datei geändert wurde und welche Änderungen du in den nächsten Commit aufnehmen möchtest.
6. **Commit erstellen:** Verwende eine verständliche Commit-Nachricht.
7. **Feature-Branch pushen:** Übertrage deinen Branch in das lokale Übungs-Remote.
8. **Merge Request entwerfen:** Notiere Source Branch, Target Branch sowie die Abschnitte „Was wurde geändert?“, „Warum?“ und „Wie wurde getestet?“.
9. **Review vorbereiten:** Überprüfe deine Änderung anhand deiner Akzeptanzkriterien. Beschreibe mindestens eine tatsächliche Prüfung.
10. **Lokal mergen:** Übernimm die Änderung in `main`, überprüfe das Ergebnis und übertrage anschließend den aktualisierten `main`-Stand in dein lokales Remote.

Du bekommst diesmal **keine vollständige Befehlsliste**. Die notwendigen Befehle hast du in den vorherigen Unterkapiteln kennengelernt.

> **Falls `cashflow-konzept.md` fehlt:** Prüfe, ob du Kapitel 11 im richtigen Repository und Branch abgeschlossen hast. Bitte bei Bedarf deine betreuende Person um Hilfe, statt die Git-Historie zu überschreiben.

### Was du vorzeigen können solltest

- das formulierte Issue mit Akzeptanzkriterien,
- deine aktualisierte `cashflow-konzept.md`,
- den Commit und die Änderung in der Git-Historie,
- den Push des Feature-Branches in das lokale Remote,
- deinen Merge-Request-Entwurf,
- den aktualisierten Hauptbranch nach dem lokalen Merge.

Ein echter GitLab-Merge-Request ist **nicht** Bestandteil dieser Abschlussaufgabe. Wir üben die Plattform später mit eurem echten Workflow.

---

# Wissenscheck

Versuche die folgenden Fragen zunächst ohne Nachschlagen zu beantworten. Schreibe deine Antworten mit eigenen Worten auf und halte sie für das Abschlussgespräch bereit.

## Teil 1 – Git-Grundlagen

### Frage 1

Was ist Git und wofür verwenden wir es?

### Frage 2

Was ist ein Commit?

### Frage 3

Was zeigt dir `git status`?

## Teil 2 – Staging und Commits

### Frage 4

Was macht `git add app.js`?

### Frage 5

Was passiert bei `git commit -m "Document categories"`?

### Frage 6

Warum ist `git diff --staged` vor einem Commit nützlich?

## Teil 3 – Branches und Merge

### Frage 7

Wie erstellst du einen neuen Branch mit dem Namen `feature/category-examples` und wechselst direkt darauf?

### Frage 8

Warum verwenden Teams Feature-Branches?

### Frage 9

Was ist ein Merge-Konflikt und woran erkennst du ihn?

## Teil 4 – Remote

### Frage 10

Was ist der Unterschied zwischen `commit` und `push`?

### Frage 11

Was ist der Unterschied zwischen `fetch` und `pull`?

### Frage 12

Warum ist `origin` nicht automatisch ein GitLab-Server?

## Teil 5 – GitLab und Zusammenarbeit

### Frage 13

Was ist ein Issue?

### Frage 14

Was ist ein Merge Request, und warum ist er nicht dasselbe wie ein Merge?

### Frage 15

Warum sollte in vielen Teamprojekten nicht jeder direkt auf `main` pushen?

### Frage 16

Was würdest du nach einem Review tun, wenn jemand eine Änderung anfordert?

## Teil 6 – Sicherheit

### Frage 17

Solltest du eine `.env` mit echten Zugangsdaten committen? Begründe deine Antwort.

### Frage 18

Wofür verwenden wir `.gitignore`, und was passiert mit Dateien, die bereits von Git verfolgt werden?

---

# Kannst du den Workflow erklären?

Erkläre deiner betreuenden Person, warum diese Schritte in einem typischen Team sinnvoll sind:

```text
Issue verstehen
      ↓
main prüfen / aktualisieren
      ↓
Feature-Branch erstellen
      ↓
Änderung umsetzen
      ↓
status + diff prüfen
      ↓
add + commit
      ↓
Feature-Branch pushen
      ↓
Merge Request und Review
      ↓
Merge
      ↓
main aktualisieren
```

Erkläre außerdem, **welche Schritte du im lokalen Übungsrepository tatsächlich durchgeführt hast** und **welche wir für den späteren GitLab-Einsatz nur simuliert haben**.

## Abschluss-Checkliste

- [ ] Ich verstehe den Unterschied zwischen Git und GitLab.
- [ ] Ich kann ein lokales Repository erkennen und seinen Status prüfen.
- [ ] Ich kenne Arbeitsverzeichnis, Staging Area und Commit.
- [ ] Ich kann Änderungen gezielt stagen und committen.
- [ ] Ich kann `git diff`, `git diff --staged` und `git log` verwenden.
- [ ] Ich kann einen Feature-Branch erstellen, wechseln und zusammenführen.
- [ ] Ich kann einen Merge-Konflikt erkennen und weiß, wie ich vorgehe.
- [ ] Ich verstehe `push`, `fetch` und `pull`.
- [ ] Ich kann ein Issue mit überprüfbaren Akzeptanzkriterien formulieren.
- [ ] Ich kann Source Branch, Target Branch und Merge Request erklären.
- [ ] Ich weiß, was `.gitignore` leistet und wo seine Grenzen liegen.
- [ ] Ich weiß, dass Secrets und echte private Finanzdaten nicht in unsere Übungsrepositories gehören.
- [ ] Ich habe meine Abschlussaufgabe im lokalen Übungsrepository durchgeführt.

## Zusammenfassung

```text
Git                  → Versionsverwaltung
status               → aktuellen Zustand prüfen
add                  → Änderungen für den Commit vormerken
commit               → Änderungen lokal in der Historie speichern
log / diff           → Geschichte und Unterschiede untersuchen
branch               → Änderungen getrennt entwickeln
merge                → Entwicklungszweige zusammenführen
remote               → anderes Git-Repository
push / fetch / pull  → Änderungen zwischen Repositories austauschen
GitLab Issue         → Aufgabe oder Anforderung beschreiben
Merge Request        → Änderungen zur Prüfung und Übernahme vorschlagen
.gitignore           → nicht verfolgte Dateien und Ordner ignorieren
```

Ab jetzt sollen die praktischen Aufgaben der Tutorial-Reihe möglichst über einen nachvollziehbaren Git-Workflow bearbeitet werden. Den echten Firmen-GitLab-Ablauf üben wir später in der Praxis.

Im nächsten Kapitel folgen die **03 – JavaScript-Grundlagen**.
