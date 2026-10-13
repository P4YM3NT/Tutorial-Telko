# 05 – Branches

[← Zurück: Historie und Unterschiede](./04-log-diff.md) | [Weiter: Merge und Konflikte →](./06-merge-konflikte.md)

In Kapitel 04 hast du die Änderungen in deinem Repository `git-uebung` untersucht und einen **dritten Commit** erstellt. Jetzt lernst du, wie du an einer neuen Änderung arbeiten kannst, **ohne sie sofort in den Hauptbranch zu übernehmen**.

Dafür verwenden wir **Branches**.

> **Wichtig:** Wir arbeiten weiterhin ausschließlich lokal in `git-uebung`. Du brauchst weder einen GitLab-Zugang noch Kenntnisse über die spätere CashFlow-Implementierung.

## Was ist ein Branch?

Ein **Branch** ist ein benannter Entwicklungszweig. Technisch verweist er auf einen Commit und bewegt sich mit neuen Commits weiter.

Du kannst dir das vereinfacht so vorstellen: Bis jetzt hast du drei Commits erstellt, und dein Hauptbranch `main` zeigt auf den neuesten davon.

```text
A ── B ── C
          ↑
         main
```

Wir erstellen von dort aus einen zweiten Branch namens `feature/git-exercise`:

```text
A ── B ── C
          ↑
          ├── main
          └── feature/git-exercise
```

**Beide Branches zeigen zunächst auf denselben Commit.** Es entsteht nicht automatisch eine zweite Kopie deines Projektordners.

Wenn du auf dem neuen Branch einen Commit erstellst, entwickelt er sich weiter:

```text
A ── B ── C ── D
          ↑     ↑
         main   feature/git-exercise
```

Der neue Commit `D` gehört zu unserem Feature-Branch. `main` zeigt weiterhin auf `C`.

## 1. Deinen aktuellen Branch prüfen

Öffne `git-uebung` in VS Code und führe aus:

```bash
git status
git branch
```

Bei unserer Übung sollte `main` der aktuelle Branch sein. Git markiert ihn in der Ausgabe von `git branch` mit einem Stern:

```text
* main
```

Alternativ zeigt dir dieser Befehl nur den aktuellen Branchnamen:

```bash
git branch --show-current
```

**Prüfe vor dem nächsten Schritt**, dass dein Arbeitsverzeichnis sauber ist (`working tree clean`). Wenn dort noch Änderungen angezeigt werden, kläre zuerst, was du damit machen möchtest. Bei einem Branchwechsel können ungespeicherte Änderungen sonst für Verwirrung sorgen oder den Wechsel verhindern.

> **Falls dein Hauptbranch anders heißt:** Wir haben ihn in Kapitel 02 mit `git init -b main` angelegt. Falls diese Option auf deinem Rechner nicht unterstützt wurde, kann dein Branch beispielsweise `master` heißen. Verwende in den folgenden Befehlen dann deinen tatsächlichen Hauptbranchnamen.

## 2. Einen neuen Branch erstellen und direkt darauf wechseln

Erstelle den Übungsbranch:

```bash
git switch -c feature/git-exercise
```

Der Befehl kombiniert zwei Schritte: **Branch erstellen** und **auf diesen Branch wechseln**.

Überprüfe das Ergebnis:

```bash
git branch
```

Beispiel:

```text
  main
* feature/git-exercise
```

Der Stern zeigt, auf welchem Branch du gerade arbeitest.

**Merke:** Der neue Branch enthält zunächst dieselben drei Commits wie `main`. Erst durch neue Änderungen und Commits unterscheiden sich die beiden Branches.

## 3. Auf dem Feature-Branch arbeiten

Erstelle in `git-uebung` eine neue Datei namens:

```text
branch-notizen.md
```

Schreibe einen kurzen Text hinein, zum Beispiel:

```md
# Meine Branch-Übung

Diese Datei entsteht auf meinem Feature-Branch.
```

Speichere die Datei und prüfe:

```bash
git status
```

Git sollte die neue Datei als `untracked` anzeigen. Das kennst du bereits aus Kapitel 02.

Stage **nur diese Datei** und committe sie:

```bash
git add branch-notizen.md
git commit -m "Add branch exercise notes"
```

Prüfe danach:

```bash
git status
git log --oneline
```

Auf dem Feature-Branch solltest du nun **vier Commits** sehen: die drei bisherigen und den neuen Commit für `branch-notizen.md`.

## 4. Zwischen Branches wechseln

Wechsle zurück auf den Hauptbranch:

```bash
git switch main
```

Schau im VS-Code-Explorer nach: Die Datei `branch-notizen.md` sollte auf `main` **nicht mehr vorhanden** sein. Sie ist aber nicht verloren gegangen – sie wurde auf dem Feature-Branch committed.

Prüfe die Historie:

```bash
git log --oneline
```

Auf `main` sind weiterhin nur die **drei bisherigen Commits** erreichbar.

Wechsle danach zurück:

```bash
git switch feature/git-exercise
```

Jetzt sollte `branch-notizen.md` wieder erscheinen, und `git log --oneline` zeigt auch den vierten Commit.

> **Wichtig:** Git kann beim Branchwechsel Dateien im Arbeitsverzeichnis passend zum gewählten Branch ändern. Deshalb solltest du vor einem Wechsel immer `git status` prüfen. Git kann einen Wechsel ablehnen, wenn dabei lokale Änderungen überschrieben würden. Erzwinge den Wechsel in diesem Fall nicht, sondern prüfe zuerst die Meldung.

## 5. Die beiden Branches vergleichen

Mit folgendem Befehl siehst du die Commit-Historie über **alle Branches** hinweg:

```bash
git log --oneline --all --graph --decorate
```

Eine vereinfachte Ausgabe könnte so aussehen (deine Commit-IDs sind anders):

```text
* d4e5f6a (HEAD -> feature/git-exercise) Add branch exercise notes
* c3d4e5f (main) Document Git diff usage
* b2c3d4e Expand Git exercise README
* a1b2c3d Add Git exercise README
```

Du erkennst: Beide Branches teilen sich die ersten drei Commits, aber nur der Feature-Branch besitzt bereits den vierten Commit.

## 6. Wozu verwenden wir Branches?

Branches helfen uns dabei,

- neue Funktionen getrennt zu entwickeln,
- Fehlerbehebungen unabhängig vorzubereiten,
- Änderungen vor der Übernahme zu überprüfen,
- einen gemeinsamen Hauptbranch möglichst stabil zu halten.

Später könnten wir für **CashFlow** beispielsweise Branches mit solchen Namen verwenden:

```text
feature/transaction-list
feature/category-filter
fix/incorrect-total
```

Das sind **nur Beispiele für Namen**. Die Funktionen selbst programmieren wir noch nicht.

## 7. Verständliche Branch-Namen

Ein Branch-Name sollte erkennen lassen, **woran du arbeitest**.

Vergleiche:

```text
neu
```

mit:

```text
feature/transaction-filter
```

Der zweite Name ist aussagekräftiger. Welches Namensschema ein Team verwendet, kann unterschiedlich sein.

## 8. Was passiert mit einem fertigen Branch?

Wenn die Änderung auf dem Feature-Branch fertig ist, möchten wir sie häufig später in `main` übernehmen. Das heißt **Merge** und ist Thema des nächsten Kapitels.

Ein nicht mehr benötigter, bereits zusammengeführter lokaler Branch lässt sich beispielsweise mit `git branch -d` entfernen. **Führe das hier noch nicht aus.** Wir benötigen `feature/git-exercise` im nächsten Kapitel.

Git schützt dich normalerweise davor, einen nicht zusammengeführten Branch mit `-d` versehentlich zu löschen. Erzwingendes Löschen behandeln wir hier bewusst nicht.

## Praxisaufgabe – Mit zwei Branches arbeiten

Bearbeite die Aufgabe mit deinem bisherigen Repository `git-uebung`. Die Erklärungen oben darfst du als Nachschlagewerk verwenden.

1. Prüfe deinen aktuellen Branch und kontrolliere, dass das Arbeitsverzeichnis sauber ist.
2. Erstelle den neuen Branch `feature/git-exercise` und wechsle direkt darauf.
3. Erstelle `branch-notizen.md` mit einer Überschrift und einem selbst geschriebenen Satz über Branches.
4. Nimm nur diese Datei in die Staging Area auf und erstelle einen passenden Commit.
5. Prüfe, auf welchem Branch du bist und wie viele Commits du dort sehen kannst.
6. Wechsle auf `main`. Ist die neue Datei dort vorhanden? Wie viele Commits zeigt die normale Historie?
7. Wechsle zurück auf `feature/git-exercise`. Was hat sich geändert?
8. Vergleiche mit `git log --oneline --all --graph --decorate` die Historien beider Branches.

**Wichtig:** Lass `feature/git-exercise` und seinen Commit bestehen. Im nächsten Kapitel lernen wir, wie wir Branches zusammenführen. Du sollst die Änderung **noch nicht mergen**.

## Wissenscheck

Beantworte die Fragen in eigenen Worten und notiere deine Antworten an einem Ort deiner Wahl.

1. Was ist ein Git-Branch?
2. Zeigen `main` und ein neu erstellter Feature-Branch zunächst zwingend auf unterschiedliche Commits?
3. Wie siehst du, auf welchem Branch du gerade bist?
4. Was macht `git switch -c feature/git-exercise`?
5. Was macht `git switch main`?
6. Warum ist `git status` vor einem Branchwechsel hilfreich?
7. Warum siehst du `branch-notizen.md` auf `main` zunächst nicht?
8. Was passiert mit `main`, wenn du nur auf dem Feature-Branch einen neuen Commit erstellst?
9. Wofür eignet sich `git log --oneline --all --graph --decorate`?
10. Warum verwenden Teams aussagekräftige Branch-Namen?

## Zusammenfassung

```text
Drei Commits auf main
          ↓ git switch -c feature/git-exercise
Neuer Branch – noch derselbe Stand
          ↓ branch-notizen.md erstellen
          ↓ git add + git commit
Vierter Commit nur auf dem Feature-Branch
          ↓ git switch main
main zeigt weiterhin drei Commits
          ↓ git switch feature/git-exercise
Feature-Commit und Datei sind wieder sichtbar
```

Du kannst jetzt Branches erstellen, zwischen ihnen wechseln und verstehen, warum eine Änderung auf einem Feature-Branch nicht automatisch im Hauptbranch landet.

[Weiter: Merge und Konflikte →](./06-merge-konflikte.md)
