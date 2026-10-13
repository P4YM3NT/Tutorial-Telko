# 08 – Praxis und Wissenscheck

[← Zurück: HTTP im Browser untersuchen](./07-browser-devtools-network.md) | [Zurück zur Übersicht](./README.md)

Zum Abschluss von **01 – Web-Grundlagen** verbinden wir die wichtigsten Begriffe miteinander.

In diesem Kapitel sollst du zeigen, dass du erklären kannst, **wie die verschiedenen Teile einer Webanwendung zusammenarbeiten**.

> **Wichtig:** Bearbeite die Aufgaben möglichst eigenständig. Du darfst in den vorherigen Unterkapiteln nachschlagen. Die Antworten notierst du an einem Ort deiner Wahl. Programmieren musst du hier noch nicht.

## Das Gesamtbild: CashFlow

Später soll unser Personal Finance Dashboard ungefähr so arbeiten:

```text
┌────────────────────┐
│     CashFlow       │
│ Browser / Frontend │
│    Vue / Quasar    │
└─────────┬──────────┘
          │
          │ HTTP-Request
          │ GET /api/transactions
          ▼
┌────────────────────┐
│ CashFlow-Backend   │
│  Node.js / Express │
└─────────┬──────────┘
          │
          │ Datenbankabfrage
          ▼
┌────────────────────┐
│     PostgreSQL     │
│     Datenbank      │
└─────────┬──────────┘
          │
          │ Transaktionen
          ▼
┌────────────────────┐
│ CashFlow-Backend   │
└─────────┬──────────┘
          │
          │ HTTP-Response
          │ 200 OK + JSON
          ▼
┌────────────────────┐
│     CashFlow       │
│ Browser / Frontend │
└────────────────────┘
```

**Hinweis:** Das ist der geplante Aufbau unserer späteren Anwendung. CashFlow und seine API müssen dafür noch nicht existieren. In diesem Kapitel geht es um den **Ablauf**, nicht um die Implementierung.

## Praxisaufgabe 1 – Einen Request verstehen

Stell dir vor, CashFlow möchte eine bestimmte Transaktion anzeigen.

Gegeben ist dieser Request:

```http
GET /api/transactions/42 HTTP/1.1
Host: example.com
Accept: application/json
```

Beantworte:

1. Welche HTTP-Methode wird verwendet?
2. Welcher **Pfad** wird angefragt?
3. Welche Ressource könnte gemeint sein?
4. Welches Antwortformat akzeptiert der Client laut Header?
5. Ist `example.com` hier unsere tatsächlich laufende CashFlow-Anwendung?

## Praxisaufgabe 2 – Eine Response verstehen

Das Backend antwortet in unserem Beispiel mit:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response-Body:**

```json
{
  "id": 42,
  "title": "Supermarkt",
  "amount": 4590,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Beantworte:

1. War die Anfrage laut Statuscode erfolgreich?
2. Welches Datenformat enthält der Body?
3. Welche ID hat die Transaktion?
4. Handelt es sich um eine Einnahme oder eine Ausgabe?
5. Welchem Euro-Betrag entsprechen `4590` Cent?
6. Welcher Teil unserer Anwendung könnte die Informationen im Dashboard darstellen?

## Praxisaufgabe 3 – CashFlow-API entwerfen

Wir möchten unsere späteren **Transaktionen** über eine REST-orientierte HTTP-API verwalten.

Die Ressource heißt:

```text
transactions
```

Entwirf jeweils eine passende **HTTP-Methode und einen Pfad** für:

1. alle Transaktionen lesen,
2. Transaktion `7` lesen,
3. neue Transaktion erstellen,
4. nur den Titel von Transaktion `7` ändern,
5. Transaktion `7` löschen.

Zusatzfrage: Warum benötigen wir beim Erstellen nicht bereits eine Transaktions-ID im Pfad?

## Praxisaufgabe 4 – Statuscodes zuordnen

Ordne jeder Situation einen sinnvollen HTTP-Statuscode zu:

| Situation | Statuscode |
|---|---|
| Alle Transaktionen wurden erfolgreich gelesen | ? |
| Eine neue Transaktion wurde erstellt | ? |
| Ein Pflichtfeld ist ungültig | ? |
| Eine angefragte Transaktion wurde nicht gefunden | ? |
| Beim Backend ist ein unerwarteter Fehler aufgetreten | ? |
| Eine Transaktion wurde erfolgreich gelöscht; der Server sendet keinen Body zurück | ? |

Überlege außerdem: Würdest du für eine erfolgreiche Anfrage und eine nicht gefundene Ressource denselben Statuscode erwarten? Begründe kurz.

## Praxisaufgabe 5 – JSON selbst schreiben

Erstelle ein gültiges JSON-Objekt für diese fiktive Ausgabe:

```text
ID: 3
Titel: Kino
Betrag: 1450 Cent
Typ: expense
Kategorie: Freizeit
Regelmäßig: nein
```

Achte auf:

- doppelte Anführungszeichen bei Schlüsseln und Textwerten,
- richtige Datentypen,
- korrekte Kommas und Klammern.

Du kannst das JSON auf Papier notieren oder in VS Code eine Datei mit der Endung `.json` erstellen. Du musst dafür **noch kein JavaScript programmieren**.

## Praxisaufgabe 6 – Die Kommunikation im Browser beobachten

Nutze eine öffentliche Webseite ohne Anmeldung.

1. Öffne den **Network-Tab** in den Browser-DevTools.
2. Lade die Seite neu und wähle einen Request aus.
3. Notiere **Request URL**, **Request Method**, **Status Code** und den **Content-Type** der Response.
4. Erkläre, ob du hier eine normale Dokument-Anfrage oder eine Anfrage für andere Daten betrachtest.

Wenn dir ein bestimmter Eintragstyp nicht angezeigt wird, wähle einen anderen Request. Unterschiedliche Ergebnisse je nach Webseite sind normal.

## Wissenscheck

Versuche zunächst, die folgenden Fragen ohne Nachschlagen zu beantworten. Wenn du bei einer Frage nicht weiterkommst, nutze die vorherigen Kapitel als Nachschlagewerk.

### Grundlagen

1. Was ist ein Client?
2. Was ist ein Server?
3. Was ist der Unterschied zwischen Frontend und Backend?
4. Was bedeutet `localhost`?
5. Wofür wird ein Port verwendet?

### HTTP

6. Was ist ein HTTP-Request?
7. Was ist eine HTTP-Response?
8. Was ist ein Header?
9. Was ist ein Body?
10. Was ist der Unterschied zwischen HTTP und HTTPS?

### Methoden und Statuscodes

11. Wofür wird `GET` verwendet?
12. Wofür wird `POST` häufig verwendet?
13. Wofür wird `DELETE` verwendet?
14. Was bedeutet `200 OK`?
15. Was bedeutet `201 Created`?
16. Was bedeutet `400 Bad Request`?
17. Was bedeutet `404 Not Found`?
18. Was bedeutet `500 Internal Server Error`?

### JSON und APIs

19. Was ist JSON?
20. Was ist eine API?
21. Was ist ein Endpoint?
22. Was ist eine Ressource?
23. Was bedeutet REST für uns vereinfacht?

## Kannst du den gesamten Ablauf erklären?

Stell dir folgende Situation vor:

> Ein Benutzer öffnet CashFlow und möchte seine Ausgaben sehen. Das Frontend fragt die Transaktionen über die API an. Das Backend verarbeitet die Anfrage, liest später die Daten aus PostgreSQL und antwortet mit JSON. CashFlow zeigt die Daten im Browser an.

Erkläre deiner betreuenden Person **in eigenen Worten**:

1. Was macht das Frontend?
2. Welche Aufgabe hat das Backend?
3. Woher stammen die Transaktionsdaten später?
4. Wie gelangen die Daten zurück zum Frontend?
5. Warum braucht das Frontend dafür **keinen direkten Zugriff auf PostgreSQL**?

Du musst die Erklärung nicht perfekt formulieren. Entscheidend ist, dass du die Rollen und die Reihenfolge verstanden hast.

## Abschluss-Checkliste

Du bist bereit für das nächste Kapitel, wenn du diese Aussagen grundsätzlich erklären oder zeigen kannst:

- [ ] Ich unterscheide Client, Server, Frontend und Backend.
- [ ] Ich erkenne Protokoll, Domain, Port, Pfad und Query-Parameter in einer URL.
- [ ] Ich kann den Aufbau eines HTTP-Requests und einer Response grob erklären.
- [ ] Ich kenne die wichtigsten HTTP-Methoden und Statuscodes.
- [ ] Ich kann ein kleines JSON-Objekt lesen und selbst schreiben.
- [ ] Ich verstehe, was API, Endpoint, Ressource und REST-orientiert bedeuten.
- [ ] Ich kann einen HTTP-Request in den Browser-DevTools untersuchen.
- [ ] Ich kann den geplanten Datenfluss von CashFlow beschreiben.

## Zusammenfassung

In diesem Kapitel hast du gelernt:

```text
Client          → stellt Anfragen
Server          → verarbeitet Anfragen und antwortet
Frontend        → sichtbarer und interaktiver Teil
Backend         → serverseitige Verarbeitung
URL             → Adresse einer Ressource
HTTP            → Kommunikationsprotokoll
Request         → Anfrage
Response        → Antwort
HTTP-Methode    → beschreibt die Art der Anfrage
Statuscode      → beschreibt das Ergebnis
JSON            → strukturiertes Datenformat
API             → Schnittstelle zwischen Programmen
Endpoint        → konkreter Zugangspunkt einer API
REST            → Architekturstil für verteilte Systeme
Network-Tab     → HTTP-Kommunikation untersuchen
```

Du hast damit eine wichtige Grundlage geschaffen, um spätere Webanwendungen besser zu verstehen.

Im nächsten Hauptkapitel geht es mit **02 – Git & GitLab** weiter. Dort lernst du, wie wir Änderungen am Code verwalten und gemeinsam an Projekten arbeiten.

**Abgabe:** Besprich deine Antworten auf die Praxisaufgaben und den Wissenscheck mit deiner betreuenden Person. Zeige dabei auch, dass du im Network-Tab einen Request untersuchen kannst. Es ist nicht nötig, dafür bereits CashFlow-Code zu schreiben.
