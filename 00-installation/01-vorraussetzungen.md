# 01 – Voraussetzungen

[← Zurück zur Übersicht](./README.md) | [Weiter: Visual Studio Code →](./02-vscode.md)

Bevor wir Programme installieren, klären wir kurz, was du für dieses Tutorial benötigst.

## Hardware und Betriebssystem

Du benötigst einen Computer, auf dem du Programme installieren und Dateien bearbeiten kannst.

Das Tutorial ist grundsätzlich für die üblichen Desktop-Betriebssysteme geeignet:

- Windows
- macOS
- Linux

Die Darstellung einzelner Menüs oder Terminal-Befehle kann sich je nach Betriebssystem leicht unterscheiden.

## Internetzugang

Für die Einrichtung und für spätere Kapitel benötigst du einen Internetzugang.

Wir verwenden ihn unter anderem für:

- das Herunterladen von Entwicklungswerkzeugen,
- den Zugriff auf GitLab,
- das Installieren von JavaScript-Paketen,
- Dokumentation und Referenzen.

## Benutzerrechte

Für die Installation von Programmen können Administratorrechte erforderlich sein.

Wenn du einen verwalteten Firmenrechner verwendest und keine Programme installieren darfst, wende dich an die zuständige Person oder Abteilung.

## Was du noch nicht können musst

Für dieses Tutorial brauchst du keine Vorkenntnisse in:

- JavaScript,
- HTML,
- CSS,
- Datenbanken,
- Git,
- Linux,
- Vue,
- Node.js.

Die benötigten Grundlagen werden Schritt für Schritt eingeführt.

## Das Terminal

Während des Tutorials verwenden wir regelmäßig ein **Terminal**.

Ein Terminal ist ein Programm, in das wir Textbefehle eingeben können.

Beispiele:

```bash
node --version
```

oder:

```bash
git --version
```

Du musst diese Befehle nicht auswendig lernen.

> **Merke:** Wenn du einen neuen Befehl siehst, ist zunächst wichtiger zu verstehen, **was wir damit erreichen wollen**, als ihn auswendig zu kennen.

## Ordner für deine Projekte

Es ist hilfreich, einen festen Ordner für deine Lernprojekte anzulegen.

Zum Beispiel:

```text
webentwicklung/
```

Darin können später verschiedene Übungen und Projekte liegen:

```text
webentwicklung/
├── tutorial/
├── erste-uebung/
└── weitere-projekte/
```

Wo dieser Ordner liegt, kannst du selbst entscheiden.

Einen neuen Ordner kannst du mit folgenden Befehl erstellen:
```bash
# Ohne <>
mkdir <dein Ordnername>
```


> Um mit dem **Terminal** zu navigieren, guck gerne unten in **Tipps und Tricks** nach den Befehlen mit denen du dich im Terminal bewegen kannst ohne deine Maus benutzen zu müssen.


Typische Orte sind zum Beispiel:

```text
Dokumente/
```

oder ein eigener Entwicklungsordner wie:

```text
C:\dev\
```

beziehungsweise:

```text
~/dev/
```

## Tipps und Tricks

Um in deinem Terminal zwischen Ordnern hin und her zu navigieren, kannst du folgende Befehle nutzen:

```bash
# Mit diesem Befehl kannst du in einen Ordner navigieren, der in deinem jetzigen Ordner liegt
# Außerdem kannst du mit der Tabs-Taste durch die verfügbaren Ordner durchklicken
cd <Ordnername>

# Mit diesem Befehl, kannst du im Ordner zurück navigieren
cd ..
```

```bash
# Mit diesem Befehl kannst du dir die verfügbaren Ordner, die in deinem ausgewählten Ordner liegen, anzeigen
ls
```

## Checkliste

Bevor du weitermachst, sollte Folgendes möglich sein:

- [ ] Ich kann Programme auf meinem Rechner installieren oder weiß, an wen ich mich dafür wenden muss.
- [ ] Ich habe Zugriff auf das Internet.
- [ ] Ich weiß, wo ich meine Lernprojekte speichern möchte.

Als Nächstes installieren wir unseren Code-Editor.

[Weiter: Visual Studio Code →](./02-vscode.md)
