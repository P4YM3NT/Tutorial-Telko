# 04 – Git

[← Zurück: Node.js und npm](./03-nodejs-npm.md) | [Weiter: Browser und Developer Tools →](./05-browser-devtools.md)

Für die Versionsverwaltung unseres Codes verwenden wir **Git**.

Git hilft uns dabei, Änderungen an einem Projekt nachvollziehbar zu speichern.

Später können wir damit zum Beispiel herausfinden:

- welche Datei geändert wurde,
- was geändert wurde,
- wann eine Änderung vorgenommen wurde,
- wer eine Änderung vorgenommen hat.

Git wird in einem späteren Kapitel ausführlich erklärt.

Hier installieren und konfigurieren wir es zunächst nur.

## Git installieren

Lade Git von der offiziellen Website herunter:

https://git-scm.com/

Installiere die passende Version für dein Betriebssystem.

Wenn dein Ausbildungsbetrieb Git bereits vorkonfiguriert hat, kannst du diesen Schritt überspringen.

## Installation prüfen

Öffne nach der Installation ein neues Terminal und führe aus:

```bash
git --version
```

Wenn Git korrekt installiert ist, erscheint eine Ausgabe ähnlich wie:

```text
git version X.XX.X
```

Die konkrete Versionsnummer ist für dieses Tutorial nicht wichtig.

## Name und E-Mail-Adresse konfigurieren

Git speichert bei Änderungen, wer sie erstellt hat.

Dafür werden ein Name und eine E-Mail-Adresse hinterlegt.

Setze deinen Namen:

```bash
git config --global user.name "Max Mustermann"
```

Setze deine E-Mail-Adresse:

```bash
git config --global user.email "max.mustermann@example.com"
```

Ersetze die Beispielwerte durch deine eigenen Angaben beziehungsweise durch die Angaben, die in deinem Ausbildungsbetrieb verwendet werden sollen.

## Konfiguration prüfen

Mit folgendem Befehl kannst du die Git-Konfiguration anzeigen:

```bash
git config --global --list
```

Du solltest unter anderem Einträge für deinen Namen und deine E-Mail-Adresse sehen.

Zum Beispiel:

```text
user.name=Max Mustermann
user.email=max.mustermann@example.com
```

## Git und GitLab sind nicht dasselbe

Die Begriffe **Git** und **GitLab** werden am Anfang häufig verwechselt.

Vereinfacht:

```text
Git
→ Werkzeug für Versionsverwaltung

GitLab
→ Plattform für Git-Repositories und Zusammenarbeit
```

Git funktioniert auch ohne GitLab.

GitLab verwendet Git und ergänzt Funktionen wie:

- zentrale Repositories,
- Issues,
- Merge Requests,
- Code Reviews,
- CI/CD.

Diese Themen behandeln wir ausführlich im Kapitel **02 – Git & GitLab**.

## Repository klonen

Wenn du dieses Tutorial aus einem GitLab-Repository verwendest, hast du das Repository möglicherweise bereits geklont.

Ein Repository kann grundsätzlich mit folgendem Befehl kopiert werden:

```bash
git clone <repository-url>
```

Beispiel:

```bash
git clone https://gitlab.example.com/webentwicklung/tutorial.git
```

Die genaue Repository-Adresse hängt von eurem Projekt ab.

> Das Arbeiten mit `clone`, `commit`, `push`, Branches und Merge Requests behandeln wir später ausführlich. Du musst diese Befehle jetzt noch nicht beherrschen.

## Häufige Probleme

### `git` wurde nicht gefunden

Wenn eine Meldung erscheint, dass `git` nicht gefunden wurde:

1. Prüfe, ob Git installiert ist.
2. Schließe VS Code vollständig.
3. Starte VS Code erneut.
4. Öffne ein neues Terminal.
5. Führe `git --version` erneut aus.

### Falscher Name oder falsche E-Mail-Adresse

Du kannst die Werte jederzeit erneut setzen:

```bash
git config --global user.name "Neuer Name"
```

```bash
git config --global user.email "neue.mail@example.com"
```

## Checkliste

- [ ] Git ist installiert.
- [ ] `git --version` zeigt eine Versionsnummer.
- [ ] Mein Name ist in Git konfiguriert.
- [ ] Meine E-Mail-Adresse ist in Git konfiguriert.
- [ ] Ich kenne grob den Unterschied zwischen Git und GitLab.

Als Nächstes schauen wir uns den Browser und seine Entwicklungswerkzeuge an.

[Weiter: Browser und Developer Tools →](./05-browser-devtools.md)
