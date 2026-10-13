# 06 – APIs und REST

[← Zurück: JSON](./05-json.md) | [Weiter: HTTP im Browser untersuchen →](./07-browser-devtools-network.md)

In den bisherigen Unterkapiteln hast du HTTP-Requests, Statuscodes und JSON kennengelernt.

Jetzt verbinden wir diese Begriffe: **Wie können Frontend und Backend von CashFlow miteinander kommunizieren?**

Dafür stellt ein Backend häufig eine **API** bereit.

API steht für:

```text
Application Programming Interface
```

Auf Deutsch spricht man von einer **Programmierschnittstelle**.

Du musst noch keine API programmieren. Wir betrachten zunächst nur, wie sie aufgebaut sein könnte.

## Was ist eine API?

Eine API legt fest, **wie andere Programme mit einem System arbeiten können**. Eine Web-API kann zum Beispiel festlegen, über welche Adresse und mit welcher Methode das Frontend Daten anfordern darf.

Bei CashFlow möchte das Frontend die gespeicherten Transaktionen anzeigen.

Eine passende Anfrage könnte sein:

```http
GET /api/transactions
```

Das Backend könnte mit einer Liste von Transaktionen antworten.

Das Frontend muss dafür **nicht wissen**, wie das Backend intern programmiert ist oder wie es auf die Datenbank zugreift.

Es muss aber wissen:

```text
Welche Adresse rufe ich auf?
Welche HTTP-Methode verwende ich?
Welche Daten sende ich gegebenenfalls?
Welche Antwort kann zurückkommen?
```

> **Merke:** Eine API beschreibt die Schnittstelle. Eine Datenbank ist ein möglicher Ort, an dem das Backend Informationen speichert. Beides ist nicht dasselbe.

## API als Vertrag zwischen Frontend und Backend

Eine API kannst du dir vereinfacht als **Vertrag** zwischen zwei Programmen vorstellen.

Beispiel: Das CashFlow-Frontend fordert alle Transaktionen an.

**Request:**

```http
GET /api/transactions HTTP/1.1
Host: example.com
Accept: application/json
```

**Mögliche Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response-Body:**

```json
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

Die Beträge in CashFlow geben wir weiterhin in **Cent** an: `4590` bedeutet 45,90 €.

Das Frontend kann die Antwort lesen und die Transaktionen im Dashboard anzeigen.

Beachte: Diese API ist **ein Entwurf für unsere spätere Anwendung**. Die Adresse `example.com` dient hier nur zur Veranschaulichung; dort läuft nicht unser CashFlow-Backend.

## Was ist ein Endpoint?

Ein **Endpoint** ist ein bestimmter Zugangspunkt einer API. Bei HTTP-APIs betrachten wir dafür üblicherweise den **Pfad zusammen mit der HTTP-Methode**.

Unsere spätere CashFlow-API könnte zum Beispiel diese Endpoints anbieten:

```text
GET    /api/transactions
GET    /api/transactions/42
POST   /api/transactions
PATCH  /api/transactions/42
DELETE /api/transactions/42
```

Die Pfade beginnen hier mit `/api`, damit man die API-Endpunkte leicht von anderen Seiten der Anwendung unterscheiden kann. Das ist eine **Konvention**, keine zwingende HTTP-Regel.

## Was ist eine Ressource?

REST-orientierte APIs verwenden häufig den Begriff **Ressource**.

Eine Ressource ist etwas, mit dem unsere Anwendung arbeitet, zum Beispiel eine Transaktion.

```text
transactions
→ Sammlung aller Transaktionen

transactions/42
→ einzelne Transaktion mit der ID 42
```

In anderen Anwendungen könnten Ressourcen etwa `users`, `products` oder `orders` heißen.

Für CashFlow konzentrieren wir uns hier auf **Transaktionen**. Die spätere Anmeldung und Benutzerverwaltung gehören zum Abschlussprojekt und müssen noch nicht umgesetzt werden.

## Was ist REST?

REST steht für:

```text
Representational State Transfer
```

REST ist ein **Architekturstil** für verteilte Systeme. Eine REST-orientierte HTTP-API orientiert sich unter anderem an Ressourcen und nutzt HTTP auf eine konsistente Weise.

Für den Einstieg reicht diese vereinfachte Vorstellung:

> **REST-orientiert** bedeutet bei unserer geplanten API: Wir verwenden aussagekräftige Ressourcenpfade, passende HTTP-Methoden und sinnvolle Statuscodes.

Diese Regeln allein beschreiben noch nicht alle REST-Prinzipien. Die Feinheiten sind für den Anfang nicht erforderlich.

### Unsere geplante CashFlow-API

| Aktion | Methode | Endpoint |
|---|---|---|
| Alle Transaktionen lesen | `GET` | `/api/transactions` |
| Eine Transaktion lesen | `GET` | `/api/transactions/42` |
| Eine Transaktion erstellen | `POST` | `/api/transactions` |
| Eine Transaktion teilweise ändern | `PATCH` | `/api/transactions/42` |
| Eine Transaktion löschen | `DELETE` | `/api/transactions/42` |

Die Bezeichnungen `GET`, `POST`, `PATCH` und `DELETE` kennst du bereits aus dem vorherigen HTTP-Kapitel.

## Ressourcen statt Verben in URLs

Oft ist es verständlicher, in API-Pfaden **Dinge statt Tätigkeiten** zu benennen.

Eher so:

```http
GET /api/transactions
```

als so:

```http
GET /api/getTransactions
```

Und eher:

```http
DELETE /api/transactions/42
```

als so:

```http
POST /api/deleteTransaction
```

Die HTTP-Methode beschreibt bereits einen wichtigen Teil der Aktion.

## Beispiel: Eine Ausgabe erstellen

Ein Benutzer trägt in CashFlow eine Ausgabe für die Bäckerei ein.

Das Frontend könnte den folgenden Request senden:

```http
POST /api/transactions
```

**Request-Body:**

```json
{
  "title": "Bäckerei",
  "amount": 650,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Das Backend prüft die Angaben und erstellt die Transaktion.

**Möglicher Statuscode:**

```text
201 Created
```

**Möglicher Response-Body:**

```json
{
  "id": 7,
  "title": "Bäckerei",
  "amount": 650,
  "type": "expense",
  "category": "Lebensmittel"
}
```

Die ID wird hier **vom Backend vergeben**. Unser Frontend muss sie beim Erstellen nicht selbst bestimmen.

Je nach API können die genaue Antwort und die enthaltenen Felder etwas anders aussehen.

## Beispiel: Eine Transaktion existiert nicht

Das Frontend fragt nach einer Transaktion, die nicht gespeichert ist:

```http
GET /api/transactions/999
```

**Möglicher Statuscode:**

```text
404 Not Found
```

**Möglicher Response-Body:**

```json
{
  "message": "Transaction not found"
}
```

Eine API kann auch Fehler als strukturierte Daten zurückgeben. Wichtig ist, dass das Frontend den Fehler nicht einfach als erfolgreiche Transaktion behandelt.

## Pfad und Query-Parameter in einer API

In Kapitel 02 hast du beides bereits kennengelernt.

Ein **Pfad** kann eine bestimmte Ressource bezeichnen:

```text
/api/transactions/42
```

Ein **Query-Parameter** kann beispielsweise eine Liste filtern:

```text
/api/transactions?type=expense
```

Die erste Adresse meint eine **einzelne Transaktion**. Die zweite könnte **alle Ausgaben** zurückgeben.

Die Filterfunktion ist hier noch ein Entwurf; wir programmieren sie später.

## Eine API ist nicht automatisch REST

Nicht jede API ist eine HTTP-API, und nicht jede HTTP-API erfüllt automatisch die REST-Prinzipien.

Für unser Tutorial konzentrieren wir uns auf eine **REST-orientierte HTTP-API**. Andere API-Stile behandeln wir hier nicht.

## Frontend und API in CashFlow

So könnte die Kommunikation später aussehen:

```text
┌────────────────────┐
│     CashFlow       │
│ Vue / Quasar       │
│ Frontend           │
└─────────┬──────────┘
          │ GET /api/transactions
          ▼
┌────────────────────┐
│    Express-API     │
│     Backend        │
└─────────┬──────────┘
          │ verarbeitet Anfrage
          │ (später: Datenbankzugriff)
          ▼
┌────────────────────┐
│    Express-API     │
│  JSON-Response     │
└─────────┬──────────┘
          │ 200 OK + JSON
          ▼
┌────────────────────┐
│     CashFlow       │
│     Frontend       │
└────────────────────┘
```

Du musst die technischen Details noch nicht bauen können. Wichtig ist zu verstehen, **wer wen anfragt und wer antwortet**.

## Kleine Übung 1 – CashFlow-Endpoints entwerfen

Entwirf Methode und Pfad für diese Aktionen. Orientiere dich an den Beispielen, ohne sie einfach abzuschreiben:

1. Alle Transaktionen abrufen.
2. Transaktion mit der ID `5` abrufen.
3. Eine neue Einnahme speichern.
4. Nur die Kategorie der Transaktion mit ID `5` ändern.
5. Transaktion mit ID `5` löschen.

## Kleine Übung 2 – API-Ablauf erklären

CashFlow zeigt folgende Meldung an:

```text
Die Transaktion konnte nicht gefunden werden.
```

Du erfährst, dass das Frontend `GET /api/transactions/999` gesendet und die API mit `404 Not Found` geantwortet hat.

Erkläre mit eigenen Worten:

1. Was hat das Frontend angefragt?
2. Was sagt der Statuscode aus?
3. Welcher Teil der Anwendung könnte die Fehlermeldung anzeigen?

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Notiere deine Antworten an einem Ort deiner Wahl; bei Bedarf darfst du nachschlagen.

1. Wofür steht die Abkürzung API?
2. Was regelt eine API zwischen Programmen?
3. Was ist ein Endpoint?
4. Was ist eine Ressource?
5. Was bedeutet REST für unsere spätere Anwendung vereinfacht?
6. Warum verwenden wir eher `/api/transactions` statt `/api/getTransactions`?
7. Wofür nutzen wir `/api/transactions/42`?
8. Worin unterscheidet sich `/api/transactions?type=expense` davon?
9. Muss das Frontend wissen, wie das Backend seine Daten speichert?
10. Ist jede HTTP-API automatisch REST?

[Weiter: HTTP im Browser untersuchen →](./07-browser-devtools-network.md)
