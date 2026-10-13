# 05 – Browser und Developer Tools

[← Zurück: Git](./04-git.md) | [Weiter: Installation prüfen →](./06-setup-pruefen.md)

Webanwendungen werden in einem Browser ausgeführt.

Für das Tutorial benötigst du einen aktuellen Browser, zum Beispiel:

- Google Chrome,
- Mozilla Firefox,
- Microsoft Edge.

Andere moderne Browser können ebenfalls funktionieren.

## Warum brauchen Entwickler Browser-Werkzeuge?

Browser besitzen eingebaute Entwicklungswerkzeuge.

Sie heißen je nach Browser zum Beispiel:

```text
Developer Tools
```

oder kurz:

```text
DevTools
```

Damit können wir später untersuchen:

- welche HTML-Elemente auf einer Seite vorhanden sind,
- welche CSS-Regeln angewendet werden,
- welche JavaScript-Ausgaben entstehen,
- welche HTTP-Anfragen eine Anwendung sendet,
- welche Fehler auftreten.

## Developer Tools öffnen

In vielen Browsern kannst du die Developer Tools mit folgender Taste öffnen:

```text
F12
```

Alternativ funktioniert häufig:

```text
Strg + Umschalt + I
```

auf Windows und Linux.

Auf macOS ist es je nach Browser typischerweise:

```text
Cmd + Option + I
```

Du kannst die Developer Tools auch über das Browser-Menü öffnen.

## Wichtige Bereiche

Für den Anfang reichen drei Bereiche.

### Elements

Hier kannst du die HTML-Struktur einer Webseite untersuchen.

Je nach Browser kann der Bereich auch anders heißen, zum Beispiel:

```text
Inspector
```

### Console

Die Console zeigt unter anderem:

- JavaScript-Ausgaben,
- Warnungen,
- Fehlermeldungen.

Später verwenden wir dort zum Beispiel:

```js
console.log('Hallo Webentwicklung!')
```

### Network

Im Bereich **Network** können wir sehen, welche Anfragen der Browser an Server sendet.

Später werden dort zum Beispiel Anfragen wie diese sichtbar:

```text
GET /api/tasks
POST /api/tasks
```

Was diese Anfragen bedeuten, lernst du im nächsten Kapitel über die Grundlagen des Webs.

## Kleine Übung

1. Öffne eine beliebige Webseite.
2. Öffne die Developer Tools.
3. Suche den Bereich **Console**.
4. Suche den Bereich **Network**.
5. Lade die Webseite neu.

Im Network-Bereich sollten jetzt mehrere Einträge erscheinen.

Du musst diese Einträge noch nicht verstehen.

Es reicht zunächst, wenn du weißt, wo du sie später findest.

## Browser und Node.js

JavaScript kann an zwei für uns wichtigen Orten ausgeführt werden:

```text
Browser
→ JavaScript im Frontend

Node.js
→ JavaScript außerhalb des Browsers
```

Später werden wir JavaScript in beiden Umgebungen verwenden.

## Checkliste

- [ ] Ich habe einen aktuellen Browser installiert.
- [ ] Ich kann die Developer Tools öffnen.
- [ ] Ich finde den Bereich Console.
- [ ] Ich finde den Bereich Network.
- [ ] Ich weiß grob, dass Browser und Node.js beide JavaScript ausführen können.

Im letzten Abschnitt prüfen wir die komplette Entwicklungsumgebung.

[Weiter: Installation prüfen →](./06-setup-pruefen.md)
