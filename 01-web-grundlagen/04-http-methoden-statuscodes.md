# 04 – HTTP-Methoden und Statuscodes

[← Zurück: HTTP, Request und Response](./03-http-request-response.md) | [Weiter: JSON →](./05-json.md)

Im vorherigen Unterkapitel hast du gelernt, dass ein Browser **HTTP-Requests** an ein Backend sendet und darauf **HTTP-Responses** erhält.

Ein Request besitzt eine **HTTP-Methode**. Sie beschreibt, welche Art von Aktion der Client durchführen möchte. Eine Response besitzt einen **Statuscode**. Er beschreibt, wie die Anfrage verarbeitet wurde.

Wir betrachten beides anhand unserer späteren Anwendung **CashFlow**. Die API gibt es noch nicht – alle folgenden Endpunkte sind **Beispiele für unsere geplante Anwendung**. Du musst sie jetzt noch nicht programmieren.

## HTTP-Methoden

Bei Web-APIs begegnen uns besonders häufig diese Methoden:

```text
GET
POST
PUT
PATCH
DELETE
```

### GET – Daten abrufen

Mit `GET` fordert der Client Daten an.

```http
GET /api/transactions
```

CashFlow könnte damit eine Liste von Einnahmen und Ausgaben abrufen.

```http
GET /api/transactions/42
```

Hier könnte es um **eine einzelne Transaktion** mit der ID `42` gehen.

> **Merke:** `GET` soll Daten abfragen, nicht nebenbei eine Transaktion erstellen oder löschen.

### POST – Neue Daten anlegen

`POST` wird häufig verwendet, um eine neue Ressource zu erstellen.

```http
POST /api/transactions
```

Der Request könnte diesen **Body** enthalten:

```json
{
  "title": "Supermarkt",
  "amount": 4590,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Damit bitten wir das Backend, eine neue Ausgabe anzulegen.

**Wichtig für CashFlow:** Wir planen, Geldbeträge später als ganze Zahlen in **Cent** zu speichern. `4590` bedeutet daher **45,90 €**. Warum das sinnvoll ist, besprechen wir ausführlicher, wenn wir mit Geldbeträgen programmieren.

### PUT – Eine Ressource vollständig ersetzen

`PUT` wird in REST-orientierten APIs häufig verwendet, um eine Ressource vollständig durch eine neue Darstellung zu ersetzen.

```http
PUT /api/transactions/42
```

In einem solchen Fall könnten wir alle bearbeitbaren Eigenschaften der Transaktion senden:

```json
{
  "title": "Wocheneinkauf",
  "amount": 5990,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Wie genau `PUT` verwendet wird, hängt vom Vertrag der jeweiligen API ab.

### PATCH – Bestimmte Eigenschaften ändern

Mit `PATCH` lassen sich häufig **einzelne Eigenschaften** einer Ressource ändern, ohne alle anderen erneut zu senden.

```http
PATCH /api/transactions/42
```

Beispiel-Body:

```json
{
  "category": "Haushalt"
}
```

Damit möchten wir nur die Kategorie ändern. Titel, Betrag und Typ sollen erhalten bleiben.

**Unterschied vereinfacht:** `PUT` steht in unserer Beispiel-API für vollständiges Ersetzen, `PATCH` für teilweises Ändern.

### DELETE – Daten löschen

Mit `DELETE` fordern wir das Löschen einer Ressource an.

```http
DELETE /api/transactions/42
```

Hier soll die Transaktion mit der ID `42` gelöscht werden.

Gerade bei Finanzdaten wäre das eine Aktion, die unsere Anwendung später bewusst absichern oder bestätigen könnte. Wie solche Bestätigungen funktionieren, lernen wir erst bei der Umsetzung des Frontends.

## CRUD und HTTP

Im Zusammenhang mit Datenverwaltung wirst du oft den Begriff **CRUD** hören.

CRUD steht für:

```text
Create → Erstellen
Read   → Lesen
Update → Ändern
Delete → Löschen
```

Eine typische Zuordnung für CashFlow sieht so aus:

| CRUD | HTTP-Methode | CashFlow-Beispiel |
|---|---|---|
| Create | `POST` | `POST /api/transactions` |
| Read | `GET` | `GET /api/transactions` |
| Update | `PUT` oder `PATCH` | `PATCH /api/transactions/42` |
| Delete | `DELETE` | `DELETE /api/transactions/42` |

Diese Zuordnung ist eine **verbreitete Konvention**, aber nicht jede API muss exakt gleich aufgebaut sein.

## HTTP-Statuscodes

Die Antwort des Servers enthält einen **Statuscode**.

Zum Beispiel:

```text
200 OK
```

Anhand des Statuscodes erkennt der Client, ob eine Anfrage erfolgreich war oder welches Problem aufgetreten ist.

HTTP-Statuscodes sind nach ihren ersten Ziffern in Gruppen eingeteilt:

| Gruppe | Grobe Bedeutung |
|---|---|
| `1xx` | Information zum weiteren Ablauf |
| `2xx` | Erfolg |
| `3xx` | Umleitung oder weitere Schritte |
| `4xx` | Anfrage kann nicht wie gewünscht erfüllt werden |
| `5xx` | Fehler auf Serverseite |

Die Gruppen `1xx` und `3xx` musst du für unser Tutorial vorerst nicht im Detail kennen. Wir konzentrieren uns auf häufige Codes aus `2xx`, `4xx` und `5xx`.

### 200 OK – Anfrage erfolgreich

```http
GET /api/transactions
```

Eine mögliche Antwort:

```text
200 OK
```

Das Backend konnte die Anfrage erfolgreich bearbeiten und beispielsweise eine Liste von Transaktionen liefern.

### 201 Created – Neue Ressource erstellt

```http
POST /api/transactions
```

Eine mögliche Antwort nach dem erfolgreichen Speichern:

```text
201 Created
```

`201` passt häufig dann, wenn eine **neue** Transaktion angelegt wurde.

### 204 No Content – Erfolgreich, aber ohne Body

Nach einer erfolgreichen Löschanfrage könnte das Backend antworten:

```text
204 No Content
```

Die Anfrage war erfolgreich. Die Response enthält aber **keinen Body**.

### 400 Bad Request – Ungültige Anfrage

Stell dir vor, beim Anlegen einer Transaktion wird kein Titel angegeben:

```json
{
  "title": "",
  "amount": 4590,
  "type": "expense"
}
```

Wenn unsere API einen nicht leeren Titel verlangt, könnte sie mit folgendem Status antworten:

```text
400 Bad Request
```

**Wichtig:** `400` ist hier eine mögliche Entscheidung unseres API-Designs. Weitere spezielle Fehlercodes lernst du bei Bedarf später kennen.

### 401 Unauthorized – Nicht gültig angemeldet

```text
401 Unauthorized
```

Dieser Code bedeutet typischerweise, dass **gültige Authentifizierungsinformationen fehlen**.

Beispiel für eine spätere Ausbaustufe von CashFlow: Jemand möchte private Transaktionen abrufen, ist aber nicht angemeldet.

Trotz des Namens geht es hier um **Authentifizierung**: „Wer bist du?“

### 403 Forbidden – Zugriff nicht erlaubt

```text
403 Forbidden
```

Der Server verweigert den Zugriff, obwohl die Anfrage verstanden wurde.

Beispiel für eine spätere Ausbaustufe: Ein angemeldeter Benutzer versucht, auf Finanzdaten zuzugreifen, für die er keine Berechtigung hat.

Hier geht es um **Autorisierung**: „Darfst du das?“

> Für das aktuelle Tutorial musst du noch **keine Anmeldung oder Rechteverwaltung programmieren**. Wir lernen diese Statuscodes nur kennen, weil sie bei Webanwendungen wichtig sind. Login und Berechtigungen sind als Erweiterungen für das Abschlussprojekt geplant.

### 404 Not Found – Ressource nicht gefunden

```http
GET /api/transactions/99999
```

Falls es diese Transaktion nicht gibt, könnte das Backend so antworten:

```text
404 Not Found
```

### 500 Internal Server Error – Unerwarteter Serverfehler

```text
500 Internal Server Error
```

Der Server konnte eine Anfrage wegen eines unerwarteten internen Problems nicht erfolgreich bearbeiten.

Beispielsweise könnte bei der Verarbeitung der Transaktionen ein Fehler auftreten. Der Client kann daraus nicht automatisch die genaue technische Ursache ableiten.

## Ein Beispiel mit mehreren möglichen Ergebnissen

CashFlow möchte eine Ausgabe erstellen:

```http
POST /api/transactions
```

Mit dem Body:

```json
{
  "title": "Bäckerei",
  "amount": 650,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Je nach Verarbeitung könnten unterschiedliche Antworten zurückkommen:

| Situation | Möglicher Statuscode |
|---|---|
| Die neue Ausgabe wurde erstellt | `201 Created` |
| Pflichtfelder sind ungültig | `400 Bad Request` |
| Das Backend hat einen unerwarteten Fehler | `500 Internal Server Error` |

Die **gleiche HTTP-Methode** kann also zu **unterschiedlichen Statuscodes** führen.

## Nicht alles auswendig lernen

Für den Einstieg sind diese Codes besonders nützlich:

```text
200 OK
201 Created
204 No Content
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

> **Merke:** Wichtiger als Auswendiglernen ist, dass du den groben Zweck der Methode erkennst und den Statuscode einer Antwort einordnen kannst.

## Kleine Übung 1 – Welche HTTP-Methode?

Wähle eine passende HTTP-Methode für jede Aktion in CashFlow:

1. Alle Transaktionen anzeigen.
2. Eine neue Ausgabe speichern.
3. Nur die Kategorie der Transaktion mit ID `12` ändern.
4. Eine vorhandene Transaktion löschen.
5. Die Transaktion mit ID `12` abrufen.

Notiere für jede Aktion die Methode und, wenn du kannst, einen passenden API-Pfad.

## Kleine Übung 2 – Welcher Statuscode?

Welcher Statuscode passt in unserer Beispiel-API jeweils **am ehesten**?

1. Eine Transaktion wurde erfolgreich erstellt.
2. Die Transaktion mit ID `99999` wurde nicht gefunden.
3. Ein erforderlicher Titel ist leer.
4. Auf dem Server ist ein unerwarteter Fehler aufgetreten.
5. Eine Transaktion wurde erfolgreich gelöscht; das Backend liefert keinen Body zurück.
6. Jemand möchte private Daten abrufen, ist aber nicht angemeldet.
7. Jemand ist angemeldet, hat aber keine Berechtigung für die angefragten Daten.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Du kannst deine Antworten an einem Ort deiner Wahl notieren und bei Bedarf nachschlagen.

1. Wofür wird `GET` verwendet?
2. Wofür wird `POST` häufig verwendet?
3. Was ist der typische Unterschied zwischen `PUT` und `PATCH`?
4. Wofür steht CRUD?
5. Was bedeutet ein Statuscode aus dem Bereich `2xx`?
6. Was ist der Unterschied zwischen `201 Created` und `204 No Content`?
7. Wofür steht `404 Not Found`?
8. Was bedeutet `500 Internal Server Error`?
9. Wie unterscheiden sich `401 Unauthorized` und `403 Forbidden` vereinfacht?
10. Kann ein `POST`-Request je nach Ergebnis unterschiedliche Statuscodes zurückbekommen?

[Weiter: JSON →](./05-json.md)
