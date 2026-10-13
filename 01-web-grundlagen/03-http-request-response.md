# 03 – HTTP, Request und Response

[← Zurück: URL, Domain und Port](./02-url-domain-port.md) | [Weiter: HTTP-Methoden und Statuscodes →](./04-http-methoden-statuscodes.md)

Client und Server müssen sich darauf einigen, **wie** sie miteinander kommunizieren.

Im Web wird dafür sehr häufig **HTTP** verwendet.

HTTP steht für:

```text
Hypertext Transfer Protocol
```

In diesem Kapitel betrachten wir HTTP anhand unserer späteren Webanwendung **CashFlow**. Du musst dafür noch keine API programmieren.

## Was ist ein Protokoll?

Ein **Protokoll** beschreibt Regeln für die Kommunikation.

Vereinfacht gesagt:

> Beide Seiten müssen wissen, wie eine Anfrage aussieht und wie darauf geantwortet wird.

Bei HTTP sprechen wir vor allem von:

```text
Request  → Anfrage
Response → Antwort
```

## HTTP-Request

Ein **Request** ist eine Anfrage, die ein Client an einen Server sendet.

Beispiel aus CashFlow:

```text
Browser:
„Gib mir die Liste meiner Transaktionen.“
```

Ein passender Request könnte vereinfacht so aussehen:

```http
GET /api/transactions HTTP/1.1
Host: cashflow.example.com
Accept: application/json
```

Die Adresse `cashflow.example.com` ist nur ein **Beispiel**. Wir haben noch keinen CashFlow-Server eingerichtet.

Was bedeuten die Bestandteile?

```text
GET
→ HTTP-Methode

/api/transactions
→ angefragter Pfad

HTTP/1.1
→ HTTP-Version in diesem Beispiel

Host: cashflow.example.com
→ angesprochener Hostname

Accept: application/json
→ der Client kann eine JSON-Antwort akzeptieren
```

Welche Methoden es gibt, sehen wir uns im nächsten Unterkapitel genauer an.

## HTTP-Response

Der Server bearbeitet den Request und sendet eine **Response** zurück.

Für unsere CashFlow-Anfrage könnte eine stark vereinfachte Antwort so aussehen:

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "title": "Supermarkt",
    "amount": 4590,
    "type": "expense"
  },
  {
    "id": 2,
    "title": "Gehalt",
    "amount": 250000,
    "type": "income"
  }
]
```

Die Response enthält hier:

- einen **Statuscode** (`200 OK`),
- einen **Header** (`Content-Type: application/json`),
- einen **Body** (die Liste der Transaktionen).

Die Darstellung mit eckigen Klammern und geschweiften Klammern heißt **JSON**. Das lernen wir im Unterkapitel `05-json.md` ausführlich kennen.

> **Hinweis:** Wir planen, Geldbeträge in CashFlow später in **Cent** zu speichern. Deshalb steht `4590` in diesem Beispiel für **45,90 €** und `250000` für **2.500,00 €**. Du musst dazu noch keine Berechnung programmieren.

## Der Ablauf

```text
┌──────────────────────┐
│ CashFlow im Browser  │
└──────────┬───────────┘
           │
           │ HTTP-Request
           │ GET /api/transactions
           ▼
┌──────────────────────┐
│ CashFlow-Backend     │
└──────────┬───────────┘
           │
           │ HTTP-Response
           │ 200 OK + Transaktionen
           ▼
┌──────────────────────┐
│ CashFlow im Browser  │
└──────────────────────┘
```

Der Browser **sendet den Request**. Das Backend **sendet die Response**.

Es handelt sich um zwei getrennte Nachrichten. Eine Response gehört jeweils zu einem Request.

## Header

**HTTP-Header** enthalten zusätzliche Informationen zu einer Anfrage oder Antwort.

Beispiele:

```text
Accept
Content-Type
Authorization
```

Zwei Header sind für den Einstieg besonders hilfreich:

| Header | Vereinfacht bedeutet er |
|---|---|
| `Accept: application/json` | Der Client gibt an, dass er JSON als Antwort akzeptieren kann. |
| `Content-Type: application/json` | Der Inhalt des zugehörigen Bodys ist JSON. |

Das ist ein wichtiger Unterschied: `Accept` sagt etwas darüber, **welche Antwortformate akzeptiert werden**, während `Content-Type` den **tatsächlichen Inhalt der jeweiligen Nachricht** beschreibt.

Den Header `Authorization` brauchen wir erst später, wenn wir uns mit Authentifizierung und Berechtigungen beschäftigen.

## Body

Der **Body** enthält, sofern vorhanden, den eigentlichen Inhalt einer HTTP-Nachricht.

Bei einer Response kann das beispielsweise eine Transaktion sein:

```json
{
  "id": 1,
  "title": "Supermarkt",
  "amount": 4590,
  "type": "expense"
}
```

Auch ein Request **kann** einen Body besitzen. Wenn CashFlow später eine neue Ausgabe anlegen soll, könnten im Request-Body zum Beispiel solche Daten stehen:

```json
{
  "title": "Bäckerei",
  "amount": 650,
  "type": "expense"
}
```

**Nicht jeder Request oder jede Response hat einen Body.** Insbesondere beim einfachen Abrufen von Daten mit `GET` wird normalerweise kein Request-Body benötigt.

## Request und Response sind getrennte Nachrichten

Ein häufiger Denkfehler am Anfang ist:

> „Der Browser greift einfach direkt auf die Datenbank zu.“

Für unsere geplante CashFlow-Anwendung ist stattdessen dieser Ablauf vorgesehen:

```text
Browser
   │
   │ HTTP-Request
   ▼
Backend
   │
   │ Datenbankabfrage
   ▼
PostgreSQL
   │
   │ Ergebnis
   ▼
Backend
   │
   │ HTTP-Response
   ▼
Browser
```

Der Browser kommuniziert also mit dem **Backend**. Das Backend übernimmt den Zugriff auf PostgreSQL.

**Wichtig:** Die Kommunikation zwischen Backend und Datenbank ist nicht einfach derselbe HTTP-Request, der vom Browser kam. Das sind unterschiedliche Schritte.

## HTTP ist zustandslos

HTTP wird häufig als **stateless**, also **zustandslos**, beschrieben.

Vereinfacht bedeutet das:

> Jeder Request ist zunächst eine eigene Anfrage. Der Server erhält nicht automatisch den gesamten Zusammenhang früherer Requests.

Wenn eine Anwendung Informationen über mehrere Anfragen hinweg benötigt, sind zusätzliche Mechanismen möglich, zum Beispiel **Sessions** oder **Tokens**.

Für dieses Kapitel musst du diese Begriffe noch nicht verstehen. Das wird später im Zusammenhang mit Login und Benutzerverwaltung wichtig.

## HTTP und HTTPS

Du hast bereits zwei Schreibweisen kennengelernt:

```text
http://
https://
```

Bei **HTTPS** wird die Kommunikation zwischen Client und Server verschlüsselt übertragen. Das schützt die übertragenen Informationen vor dem einfachen Mitlesen auf dem Übertragungsweg.

Für Webanwendungen mit persönlichen Daten wie CashFlow ist HTTPS besonders wichtig. Es ersetzt aber keine sichere Anmeldung oder korrekte Berechtigungsprüfung.

## Kleine Übung 1 – Bestandteile zuordnen

Ordne diese vier Bestandteile den passenden Kategorien zu:

```text
GET /api/transactions
200 OK
Content-Type: application/json
{"title":"Supermarkt","amount":4590}
```

Kategorien:

```text
HTTP-Methode und Pfad
Status
Header
Body
```

Notiere deine Zuordnung. Du brauchst keinen Code auszuführen.

## Kleine Übung 2 – Den Ablauf erklären

Stell dir vor, du öffnest CashFlow und klickst auf **„Transaktionen anzeigen“**.

Erkläre in **drei bis fünf Sätzen**:

1. Wer sendet den Request?
2. An wen wird er gesendet?
3. Wer sendet die Response?
4. Welche Daten könnten im Response-Body stehen?
5. Greift der Browser dabei direkt auf PostgreSQL zu?

Formuliere den Ablauf mit deinen eigenen Worten.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Du kannst deine Antworten an einem Ort deiner Wahl notieren und bei Bedarf nachschlagen.

1. Was ist HTTP?
2. Was ist ein Request?
3. Was ist eine Response?
4. Welche Informationen können Header enthalten?
5. Was ist der Unterschied zwischen `Accept` und `Content-Type`?
6. Was befindet sich typischerweise im Body?
7. Hat jeder HTTP-Request einen Body?
8. Kommuniziert unser späteres CashFlow-Frontend direkt mit PostgreSQL?
9. Was bedeutet es vereinfacht, dass HTTP zustandslos ist?
10. Was ist der wichtigste Unterschied zwischen HTTP und HTTPS?

[Weiter: HTTP-Methoden und Statuscodes →](./04-http-methoden-statuscodes.md)
