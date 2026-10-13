# 05 – JSON

[← Zurück: HTTP-Methoden und Statuscodes](./04-http-methoden-statuscodes.md) | [Weiter: APIs und REST →](./06-api-rest.md)

Im vorherigen Unterkapitel hast du gesehen, wie CashFlow eine Transaktion anlegen oder abrufen könnte.

Aber **wie sehen die Daten aus**, die Frontend und Backend dabei austauschen?

Ein sehr häufig verwendetes Datenformat dafür ist **JSON**.

JSON steht für:

```text
JavaScript Object Notation
```

Du musst dafür noch kein JavaScript beherrschen. In diesem Kapitel lernst du zunächst, JSON **zu lesen und selbst aufzuschreiben**.

## Ein einfaches JSON-Objekt

Stell dir vor, das CashFlow-Backend liefert diese Transaktion:

```json
{
  "id": 1,
  "title": "Supermarkt",
  "amount": 4590,
  "type": "expense"
}
```

Das Beispiel ist ein **JSON-Objekt**.

Es enthält Informationen über eine Ausgabe:

- `id` – die Kennnummer,
- `title` – eine Beschreibung,
- `amount` – den Betrag,
- `type` – die Art der Transaktion.

Wie zuvor vereinbart, geben wir Beträge in unseren CashFlow-Beispielen in **Cent** an: `4590` steht für **45,90 €**.

## Schlüssel und Werte

Ein JSON-Objekt besteht aus **Schlüssel-Wert-Paaren**.

Nehmen wir einen kleinen Ausschnitt:

```json
{
  "title": "Supermarkt",
  "amount": 4590
}
```

Hier bedeutet:

```text
"title"       → Schlüssel
"Supermarkt"  → Wert

"amount"      → Schlüssel
4590          → Wert
```

Der **Doppelpunkt `:`** trennt Schlüssel und Wert. Ein **Komma `,`** trennt mehrere Paare voneinander.

Die **geschweiften Klammern `{ }`** umschließen das Objekt.

> **Merke:** In gültigem JSON müssen die Schlüssel eines Objekts in **doppelten Anführungszeichen** stehen.

## Häufige JSON-Datentypen

### String – Text

```json
{
  "title": "Bäckerei"
}
```

`"Bäckerei"` ist ein **String**, also Text.

### Number – Zahl

```json
{
  "amount": 650
}
```

`650` ist eine **Zahl**. Sie steht in JSON **ohne** Anführungszeichen.

### Boolean – Wahrheitswert

```json
{
  "recurring": false
}
```

Ein **Boolean** kann nur `true` oder `false` sein. Die Schreibweise ist kleingeschrieben und ohne Anführungszeichen.

Das Beispiel könnte bedeuten, dass es sich **nicht** um eine regelmäßig wiederkehrende Transaktion handelt. Eine Funktion für regelmäßige Buchungen planen wir hier noch nicht.

### Null – Kein Wert

```json
{
  "note": null
}
```

`null` bedeutet hier, dass **kein Wert** angegeben ist. Es ist nicht dasselbe wie der Text `"null"`.

### Array – Eine Liste

```json
{
  "categories": ["Lebensmittel", "Wohnen", "Freizeit"]
}
```

Ein **Array** ist eine geordnete Liste von Werten. Es steht in **eckigen Klammern `[ ]`**.

### Objekt – Zusammengehörige Eigenschaften

Objekte können auch in anderen Objekten stehen:

```json
{
  "transaction": {
    "id": 1,
    "title": "Supermarkt"
  }
}
```

Das innere Objekt gehört zum Schlüssel `"transaction"`.

## Arrays von Objekten

Eine API liefert häufig nicht nur eine Transaktion, sondern **mehrere**.

Beispielsweise könnte CashFlow mit einer Liste antworten:

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

Das äußere `[ ]` kennzeichnet ein **Array**. Darin befinden sich **zwei Objekte**.

Achte auf `"type"`:

```text
expense → Ausgabe
income  → Einnahme
```

Diese Begriffe sind **von unserer geplanten Anwendung festgelegte Werte**. JSON selbst schreibt nicht vor, wie wir Transaktionen benennen.

## JSON ist ein Datenformat, keine Programmiersprache

JSON dient dazu, Daten strukturiert aufzuschreiben und zwischen Programmen auszutauschen. Es ist **keine Programmiersprache**, mit der du Abläufe oder Funktionen definierst.

Bei einer HTTP-Response könnte unser Backend zum Beispiel mitteilen:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

Der zugehörige **Response-Body** könnte diese Daten enthalten:

```json
{
  "id": 1,
  "title": "Supermarkt",
  "amount": 4590
}
```

Der Header `Content-Type: application/json` bedeutet: **Der Body enthält JSON-Daten.**

Das Frontend kann diese Daten später verarbeiten und im Dashboard anzeigen.

## JSON und JavaScript sehen ähnlich aus

Der Name JSON enthält zwar „JavaScript“. Trotzdem sind JSON und ein JavaScript-Objekt nicht dasselbe.

So könnte ein JavaScript-Objekt aussehen:

```js
const transaction = {
  id: 1,
  title: 'Supermarkt',
  amount: 4590
}
```

Und so dieselbe Information als JSON:

```json
{
  "id": 1,
  "title": "Supermarkt",
  "amount": 4590
}
```

Du musst die JavaScript-Schreibweise **noch nicht selbst verwenden**. Die Grundlagen von JavaScript lernen wir später.

Für den Moment ist wichtig:

- JSON ist ein **Datenformat**.
- In JSON stehen **Objektschlüssel in doppelten Anführungszeichen**.
- Für Strings verwendet JSON ebenfalls **doppelte Anführungszeichen**.
- JavaScript erlaubt an manchen Stellen andere Schreibweisen.

## JSON enthält keine Funktionen

Eine JavaScript-Funktion beschreibt eine ausführbare Aktion. JSON ist dafür nicht gedacht.

Darum kann JSON **Daten** wie Texte, Zahlen oder Listen enthalten, aber **keine Funktionen**.

Du musst noch nicht wissen, wie Funktionen in JavaScript geschrieben werden.

## Häufige JSON-Fehler

Bei JSON gibt es einige einfache Schreibregeln:

1. **Doppelte Anführungszeichen:** Schlüssel und Textwerte benötigen `"..."`.
2. **Kommas:** Zwischen Einträgen steht ein Komma, **hinter dem letzten Eintrag nicht**.
3. **Wahrheitswerte:** `true`, `false` und `null` werden kleingeschrieben und nicht in Anführungszeichen gesetzt.
4. **Kommentare:** Kommentare wie `// Hinweis` gehören **nicht** zu gültigem JSON.

Beispiel für **ungültiges** JSON:

```text
{
  title: 'Supermarkt',
  "amount": 4590,
}
```

In diesem Beispiel sind gleich mehrere Regeln verletzt. Welche, findest du in der Übung heraus.

## Kleine Übung 1 – JSON prüfen

Welche der beiden Varianten ist **gültiges JSON**? Begründe deine Antwort.

### Beispiel A

```json
{
  "title": "Bäckerei",
  "amount": 650,
  "type": "expense"
}
```

### Beispiel B

```text
{
  title: 'Bäckerei',
  "amount": 650,
  "type": "expense",
}
```

Notiere auch, **welche Fehler** du in der ungültigen Variante findest.

## Kleine Übung 2 – Eine CashFlow-Transaktion als JSON

Schreibe selbst ein JSON-Objekt mit diesen Informationen:

```text
ID: 5
Titel: Kino
Betrag in Cent: 1450
Typ: Ausgabe (expense)
Kategorie: Freizeit
Regelmäßig: nein
```

Achte auf die richtige Schreibweise von Texten, Zahlen und Wahrheitswerten.

## Kleine Übung 3 – Zwei Transaktionen

Erstelle ein JSON-**Array** mit genau zwei Transaktionen. Jede Transaktion soll `id`, `title`, `amount` und `type` enthalten.

Verwende diese fiktiven Angaben:

```text
1. Transaktion:
ID: 1
Titel: Gehalt
Betrag in Cent: 250000
Typ: income

2. Transaktion:
ID: 2
Titel: Bus-Ticket
Betrag in Cent: 320
Typ: expense
```

Du kannst die Antwort zunächst auf Papier oder in einer Textdatei notieren. Wenn du möchtest, erstelle zum Prüfen eine Datei mit der Endung `.json` in VS Code. Du musst dafür noch kein JavaScript ausführen.

## Wissenscheck

Beantworte die Fragen mit deinen eigenen Worten. Notiere die Antworten an einem Ort deiner Wahl; bei Bedarf darfst du nachschlagen.

1. Wofür verwenden wir JSON?
2. Was ist ein Schlüssel-Wert-Paar?
3. Welche Datentypen kommen in JSON vor?
4. Was ist der Unterschied zwischen `{ }` und `[ ]`?
5. Was ist ein JSON-Array aus Objekten?
6. Welche Anführungszeichen braucht gültiges JSON bei Texten und Objektschlüsseln?
7. Worin unterscheiden sich JSON und JavaScript-Objekte?
8. Darf ein JSON-Dokument eine Funktion enthalten?
9. Warum ist ein Komma hinter dem letzten Objekt-Eintrag problematisch?
10. Was sagt `Content-Type: application/json` über einen HTTP-Body aus?

[Weiter: APIs und REST →](./06-api-rest.md)
