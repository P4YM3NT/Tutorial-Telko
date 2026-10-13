# 09 – Issues und Merge Requests

[← Zurück: GitLab-Grundlagen](./08-gitlab-grundlagen.md) | [Weiter: .gitignore und sensible Daten →](./10-gitignore-sicherheit.md)

In Kapitel 08 hast du gelernt, welche Aufgaben GitLab bei der Zusammenarbeit übernimmt. Jetzt schauen wir uns zwei wichtige Werkzeuge genauer an: **Issues** und **Merge Requests**.

Dabei bleiben wir zunächst bei **fiktiven Beispielen für CashFlow**. Du brauchst noch keinen Zugang zu einem Firmenprojekt und musst auch noch keine CashFlow-Funktion programmieren. Wie ihr GitLab im Unternehmen konkret verwendet, lernst du später in der Praxis.

## Lernziele

Nach diesem Kapitel kannst du:

- erklären, was ein Issue und ein Merge Request (MR) sind,
- aus einem Wunsch eine verständliche Aufgabe formulieren,
- **Akzeptanzkriterien** aufschreiben, die sich überprüfen lassen,
- den Zusammenhang zwischen Issue, Branch, Commit und Merge Request erklären,
- Source Branch und Target Branch unterscheiden,
- eine kurze MR-Beschreibung mit Testhinweisen verfassen,
- erklären, wozu Code Reviews und Nachbesserungen dienen.

## 1. Issues – Arbeit verständlich beschreiben

Ein **Issue** hält eine Aufgabe, einen Fehler oder eine Anforderung fest. Es beantwortet möglichst klar:

- **Was** soll geändert werden?
- **Warum** ist das sinnvoll?
- **Woran erkennen wir**, dass die Aufgabe erledigt ist?

### Beispiel: CashFlow nach Kategorien filtern

Stell dir vor, CashFlow zeigt bereits eine Liste mit fiktiven Einnahmen und Ausgaben an. Ein Benutzer möchte nur die Einträge der Kategorie „Lebensmittel“ sehen.

Ein mögliches Issue lautet:

```text
Titel:
Transaktionen nach Kategorie filtern

Beschreibung:
Als Benutzer möchte ich eine Kategorie auswählen können,
damit ich nur die passenden Transaktionen sehe.

Akzeptanzkriterien:
- Eine Kategorie kann ausgewählt werden.
- Es werden nur Transaktionen dieser Kategorie angezeigt.
- Der Filter kann zurückgesetzt werden, sodass wieder alle
  Transaktionen sichtbar sind.
```

Die drei Akzeptanzkriterien beschreiben **prüfbares Verhalten**. Sie schreiben noch nicht vor, wie das Programm intern aufgebaut sein muss.

> **Merke:** Ein gutes Issue muss nicht lang sein. Es muss verständlich machen, welches Ergebnis erwartet wird.

## 2. Was sind Akzeptanzkriterien?

**Akzeptanzkriterien** sind Bedingungen, anhand derer wir prüfen können, ob eine Anforderung erfüllt ist.

Wenig hilfreich wäre:

```text
- Der Filter soll gut funktionieren.
```

Besser ist eine überprüfbare Aussage:

```text
- Nach Auswahl der Kategorie "Lebensmittel" werden nur
  Transaktionen mit dieser Kategorie angezeigt.
```

So wissen Entwickler und Reviewer später, **was getestet werden soll**.

### Muss jedes Issue eine Benutzerbeschreibung enthalten?

Nein. Ein Issue kann auch einen Fehler, eine technische Aufgabe oder eine Dokumentationsänderung beschreiben. Die Formulierung „Als Benutzer möchte ich …“ ist nur eine hilfreiche Möglichkeit für Funktionen aus Benutzersicht.

## 3. Vom Issue zum Branch

Für Änderungen erstellen Teams häufig einen eigenen **Feature-Branch**. Das hast du in Kapitel 05 bereits praktisch ausprobiert.

Zu unserem CashFlow-Issue könnte ein Branch so heißen:

```text
feature/category-filter
```

Ein Team kann zusätzlich die Issue-Nummer im Branch-Namen verwenden:

```text
feature/42-category-filter
```

Die Nummer `42` ist hier nur ein Beispiel. Welche Namensregeln gelten, hängt vom Projekt ab.

Auf dem Branch werden Änderungen entwickelt und **lokal committed**. Erst durch `push` werden die Commits zum gemeinsamen Remote übertragen. Den Unterschied hast du in Kapitel 07 kennengelernt.

## 4. Was ist ein Merge Request?

Ein **Merge Request** (kurz **MR**) ist ein Vorschlag, Änderungen aus einem Branch in einen anderen zu übernehmen.

```text
Source Branch: feature/category-filter
Target Branch: main
```

- **Source Branch:** Hier liegen die vorgeschlagenen Änderungen.
- **Target Branch:** Hier sollen die Änderungen später ankommen.

Ein Merge Request ist **noch kein Merge**. Er bietet zuerst die Gelegenheit, Änderungen anzusehen, zu besprechen und zu prüfen.

## 5. Der typische Ablauf

```text
Issue beschreiben
       ↓
Feature-Branch erstellen
       ↓
Änderungen umsetzen
       ↓
Änderungen prüfen und committen
       ↓
Branch pushen
       ↓
Merge Request erstellen
       ↓
Code Review / gegebenenfalls Pipeline
       ↓
Änderungen bei Bedarf nachbessern
       ↓
Merge in den Zielbranch
```

Eine Pipeline **kann** automatische Prüfungen ausführen, wenn das Projekt entsprechend eingerichtet ist. Du musst Pipelines hier weder erstellen noch konfigurieren; das folgt in einem späteren CI/CD-Kapitel.

## 6. Eine hilfreiche Merge-Request-Beschreibung

Eine kurze MR-Beschreibung sollte den Reviewer nicht raten lassen, worum es geht. Zum Beispiel:

```markdown
## Was wurde geändert?

- Kategorieauswahl für die Transaktionsliste ergänzt
- Zurücksetzen des Filters ermöglicht

## Warum?

Benutzer sollen ihre Ausgaben leichter nach Kategorien ansehen können.

## Wie wurde getestet?

- Kategorie "Lebensmittel" ausgewählt und Ergebnis geprüft
- Filter zurückgesetzt und vollständige Liste geprüft
```

Das ist ein **Beispiel**, kein Bericht über eine tatsächlich implementierte Funktion. Später müssen in einem echten MR natürlich die **wirklich durchgeführten Tests** stehen. Nicht getestete Dinge dürfen wir nicht einfach als getestet angeben.

## 7. Code Review und Feedback

Beim **Code Review** schaut sich ein anderer Entwickler die Änderung an. Typische Fragen sind:

- Erfüllt die Änderung die Akzeptanzkriterien?
- Ist der Code verständlich?
- Wurden erkennbare Fehlerfälle bedacht?
- Sind nur die beabsichtigten Dateien geändert worden?
- Wurde sinnvoll getestet?

Ein Review kann Fragen und Änderungsvorschläge enthalten. Das ist normaler Teil der Zusammenarbeit.

### Was passiert bei Nachbesserungen?

Wenn du Feedback erhältst, passt du deinen **Feature-Branch** an, prüfst die Änderung und erstellst weitere Commits. Durch einen erneuten `push` werden diese im bestehenden Merge Request sichtbar.

Ein typischer Ablauf ist:

```bash
git status
git diff
git add <datei>
git commit -m "Address review feedback"
git push
```

Das ist ein allgemeines Beispiel. Die konkrete Datei und die Commit-Nachricht hängen von der tatsächlichen Änderung ab.

## 8. Wann wird gemergt?

Wenn das Review abgeschlossen ist und die geltenden Projektregeln erfüllt sind, kann die Änderung in den Zielbranch übernommen werden. Ob die Person den Merge selbst durchführen darf, hängt von Berechtigungen und Projekteinstellungen ab.

Danach wird der Feature-Branch häufig gelöscht, wenn er nicht mehr benötigt wird.

> **Wichtig:** Ein grüner Pipeline-Status ist hilfreich, ersetzt aber nicht automatisch die inhaltliche Prüfung einer Änderung.

## 9. Übung – Ein Issue für CashFlow entwerfen

CashFlow soll später eine Suche in der Transaktionsliste erhalten.

**Anforderung:** Ein Benutzer soll Transaktionen anhand eines Textes im Titel finden können.

Erstelle **auf Papier oder in einer Textdatei** ein Issue mit:

1. einem verständlichen Titel,
2. einer kurzen Beschreibung aus Benutzersicht,
3. mindestens **drei überprüfbaren Akzeptanzkriterien**,
4. einem sinnvollen Branch-Namen.

Verwende noch keinen echten GitLab-Account und programmiere die Suche nicht. Es geht darum, eine Aufgabe präzise zu beschreiben.

## 10. Übung – Einen Merge Request vorbereiten

Stell dir vor, die Suche aus der vorherigen Aufgabe wurde auf einem Feature-Branch bereits umgesetzt. **Du musst dafür keinen Code schreiben.**

Erstelle einen Entwurf für die MR-Beschreibung mit diesen Überschriften:

```markdown
## Was wurde geändert?

## Warum?

## Wie wurde getestet?
```

Nenne mindestens zwei sinnvolle Tests, die man vor dem Merge durchführen **sollte**. Kennzeichne sie als **geplante Tests**, da du sie noch nicht ausgeführt hast.

Ergänze außerdem:

- einen möglichen Source Branch,
- einen möglichen Target Branch,
- eine kurze Erklärung, warum der Merge Request noch nicht bedeutet, dass die Änderung bereits gemergt wurde.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Notiere deine Antworten an einem Ort deiner Wahl.

1. Was ist ein Issue?
2. Welche Informationen sollte ein verständliches Issue enthalten?
3. Was sind Akzeptanzkriterien?
4. Warum sollten Akzeptanzkriterien überprüfbar formuliert sein?
5. Wie hängen ein Issue und ein Feature-Branch zusammen?
6. Was ist ein Merge Request?
7. Was bedeuten Source Branch und Target Branch?
8. Warum ist ein Merge Request noch kein Merge?
9. Wofür ist ein Code Review da?
10. Was passiert, wenn du nach einem Review weitere Commits pushst?
11. Was gehört in den Abschnitt „Wie wurde getestet?“?
12. Warum ist eine erfolgreiche Pipeline allein keine Garantie für korrekte Software?

## Abschluss-Checkliste

- [ ] Ich kann Issue und Merge Request unterscheiden.
- [ ] Ich kann ein Issue mit überprüfbaren Akzeptanzkriterien formulieren.
- [ ] Ich kann Source Branch und Target Branch erklären.
- [ ] Ich kann den Weg vom Issue bis zum Merge grob beschreiben.
- [ ] Ich habe ein CashFlow-Issue und eine MR-Beschreibung als Entwurf erstellt.
- [ ] Ich kann erklären, was bei einem Review passiert.
- [ ] Ich verstehe, dass wir den Firmen-GitLab-Workflow erst später praktisch üben.

## Zusammenfassung

```text
Issue         → Was soll erreicht werden?
Branch        → Wo entwickeln wir die Änderung?
Commit        → Welche Änderungen wurden gespeichert?
Merge Request → Welche Änderungen schlagen wir zur Übernahme vor?
Review        → Ist die Änderung nachvollziehbar und passend?
Merge         → Änderung wird in den Zielbranch übernommen
```

Als Nächstes lernen wir, warum bestimmte Dateien **nicht** in Git gehören und wie `.gitignore` dabei hilft.

[Weiter: .gitignore und sensible Daten →](./10-gitignore-sicherheit.md)
