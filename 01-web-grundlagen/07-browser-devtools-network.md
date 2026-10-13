# 07 – HTTP im Browser untersuchen

[← Zurück: APIs und REST](./06-api-rest.md) | [Weiter: Praxis und Wissenscheck →](./08-praxis-wissenscheck.md)

Bisher haben wir HTTP hauptsächlich anhand von Beispielen betrachtet.

Jetzt untersuchen wir **echte Netzwerk-Anfragen im Browser**. Dafür verwenden wir die **Developer Tools** (kurz **DevTools**), die du bereits bei der Installation kennengelernt hast.

In diesem Unterkapitel brauchst du **noch kein JavaScript zu programmieren** und auch noch kein CashFlow-Backend zu starten.

## Developer Tools öffnen

Öffne eine beliebige öffentlich erreichbare Webseite im Browser.

Die DevTools kannst du in vielen Browsern mit `F12` öffnen. Weitere häufige Tastenkombinationen sind:

```text
Windows / Linux: Strg + Umschalt + I
macOS:           Cmd + Option + I
```

Alternativ kannst du die Entwicklungswerkzeuge über das Browsermenü öffnen.

## Den Network-Tab verwenden

1. Öffne in den DevTools den Bereich **Network** (manchmal „Netzwerk“).
2. Lade die geöffnete Webseite **neu**.
3. Beobachte die Einträge, die erscheinen.

Einträge können beispielsweise Anfragen für HTML, CSS, JavaScript, Bilder oder API-Daten darstellen.

> **Wichtig:** Nicht jeder Eintrag ist eine Anfrage an eine API. Schon das Laden einer normalen Webseite verursacht Netzwerkaktivität.

## Welche Angaben werden angezeigt?

Je nach Browser kannst du Spalten wie diese sehen:

```text
Name
Status
Type
Method
Size
Time
```

Die Spalten lassen sich häufig ein- und ausblenden; ihre Namen unterscheiden sich teilweise zwischen Browsern.

- **Name:** Name der angefragten Ressource.
- **Status:** HTTP-Statuscode, sofern eine HTTP-Response vorliegt.
- **Type:** Art der Ressource, zum Beispiel Dokument, Skript oder Bild.
- **Method:** HTTP-Methode, etwa `GET`.
- **Size:** Übertragene oder angezeigte Größe; bei Cache-Nutzung kann die Anzeige abweichen.
- **Time:** Zeitangabe zur Anfrage.

## Einen Request genauer untersuchen

Klicke auf einen Eintrag im Network-Tab. In den Details findest du häufig mehrere Bereiche.

### Headers – Allgemeine Angaben

Unter **Headers** kannst du unter anderem suchen nach:

**Request URL**

```text
https://example.com/
```

**Request Method**

```text
GET
```

**Status Code**

```text
200
```

Der Statuscode kann je nach Webseite, Weiterleitung oder Situation anders ausfallen. Es ist also kein Fehler, wenn du nicht überall `200` siehst.

### Request Headers

Hier stehen Zusatzinformationen, die **der Client an den Server** gesendet hat.

Zum Beispiel kann ein Client mit `Accept` angeben, welche Antwortformate er bevorzugt.

### Response Headers

Hier stehen Zusatzinformationen, die **der Server an den Client** zurückgesendet hat.

Besonders interessant ist häufig:

```http
Content-Type: text/html
```

Das bedeutet, dass der Response-Body HTML enthält.

Bei einer JSON-API könnte stattdessen stehen:

```http
Content-Type: application/json
```

### Response und Preview

Hier kannst du häufig sehen, **welche Daten der Server zurückgegeben hat**.

Bei einer Webseite kann das HTML sein. Bei unserer späteren CashFlow-API könnte es ein JSON-Array sein:

```json
[
  {
    "id": 1,
    "title": "Supermarkt",
    "amount": 4590,
    "type": "expense"
  }
]
```

Dieses JSON ist **nur ein Beispiel**. Auf einer beliebigen Webseite wirst du nicht automatisch CashFlow-Daten finden.

## Unterschied zwischen Request und Response erkennen

In den DevTools findest du beide Seiten einer HTTP-Kommunikation:

```text
Request URL / Request Method
→ Wohin und auf welche Weise wurde angefragt?

Request Headers
→ Welche Zusatzinformationen hat der Client gesendet?

Status Code / Response Headers / Response
→ Was hat der Server geantwortet?
```

Das kennst du aus Kapitel 03 wieder. Jetzt kannst du es bei echten Anfragen beobachten.

## Filter im Network-Tab

Eine Seite kann viele Anfragen gleichzeitig auslösen. Mit Filtern wird die Liste übersichtlicher.

Typische Kategorien sind:

| Filter | Zeigt häufig |
|---|---|
| `Doc` oder `Document` | HTML-Dokumente |
| `JS` | JavaScript-Dateien |
| `CSS` | Stylesheets |
| `Img` | Bilder |
| `Fetch/XHR` | Anfragen, die oft aus Browser-JavaScript stammen |

Die Bezeichnungen können je nach Browser abweichen.

## Was bedeutet Fetch/XHR?

Eine Webanwendung muss nicht bei jeder Datenänderung die komplette Seite neu laden.

Browser-JavaScript kann dafür Anfragen im Hintergrund senden, zum Beispiel über die eingebaute Funktion `fetch()`.

Solche Anfragen findest du häufig unter **Fetch/XHR**.

Wenn CashFlow später die Transaktionen über eine API lädt, werden wir dort passende Einträge untersuchen können.

**Wichtig:** Wenn unter `Fetch/XHR` bei einer ausgewählten Webseite nichts erscheint, ist das nicht automatisch ein Fehler. Nicht jede Webseite sendet solche Anfragen.

## Was ist mit Cache?

Der Browser kann bestimmte Dateien zwischenspeichern. Das nennt man **Cache**.

Dadurch können bei einem erneuten Laden weniger Daten übertragen werden oder Einträge anders aussehen.

Für unsere erste Übung musst du den Cache **nicht verändern**. Es reicht, wenn du weißt, dass er die angezeigten Ergebnisse beeinflussen kann.

## Kleine Praxisaufgabe 1 – Einen echten Request finden

Nutze eine beliebige öffentliche Webseite ohne Anmeldung. Du musst keine persönlichen Daten eingeben.

1. Öffne die DevTools und den **Network-Tab**.
2. Lade die Seite neu.
3. Wähle einen Eintrag vom Typ **Document/Doc**, wenn möglich.
4. Suche die folgenden Angaben und notiere sie an einem Ort deiner Wahl:

```text
Request URL:
Request Method:
Status Code:
Content-Type (Response Header):
```

5. Erkläre, ob der angezeigte Inhalt eher **HTML** oder **JSON** ist.

Die Ergebnisse hängen von der ausgewählten Webseite ab. Es gibt hier deshalb nicht genau eine mögliche Kombination aus URL und Statuscode.

## Kleine Praxisaufgabe 2 – Anfragen unterscheiden

Untersuche die Liste im Network-Tab erneut:

1. Findest du einen Eintrag vom Typ `JS`, `CSS` oder `Img`? Notiere den Typ und den angezeigten Namen.
2. Stelle den Filter auf **Fetch/XHR**. Siehst du Einträge?
3. Erkläre, weshalb sich das Anzeigen einer HTML-Seite von einer späteren CashFlow-API-Anfrage unterscheiden kann.

Wenn kein passender Eintrag vorhanden ist, **notiere das einfach**. Es geht darum, das Werkzeug kennenzulernen, nicht eine bestimmte Anzahl von Requests zu finden.

## Verbindung zu CashFlow

Wenn wir später CashFlow programmieren, könnte im Network-Tab beispielsweise diese Anfrage auftauchen:

```http
GET /api/transactions
```

Dann kannst du untersuchen:

- Wurde der Request gesendet?
- Welche URL wurde aufgerufen?
- Welche HTTP-Methode wurde verwendet?
- Welchen Statuscode hat das Backend zurückgegeben?
- Enthält die Response die erwarteten Transaktionen?

So hilft der Network-Tab später bei der **Fehlersuche**.

## Typische Anfängerprobleme

**„Im Network-Tab steht gar nichts.“**

Prüfe, ob der Tab geöffnet war, als du die Seite neu geladen hast.

**„Ich finde keine JSON-Daten.“**

Normale Webseiten liefern oft HTML, Bilder oder Skripte. JSON ist nicht bei jedem Request zu erwarten.

**„Ich sehe einen anderen Statuscode als 200.“**

Auch Weiterleitungen oder fehlende Ressourcen können sichtbar sein. Versuche zunächst, den angezeigten Code einzuordnen.

**„Ein Request enthält sensible Daten.“**

Teile keine echten Zugangsdaten, Cookies oder Autorisierungswerte aus dem Network-Tab. Für die Übungen reichen URL, Methode, Statuscode und allgemeiner `Content-Type`.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Notiere deine Antworten an einem Ort deiner Wahl; bei Bedarf darfst du nachschlagen.

1. Wo findest du HTTP-Anfragen im Browser?
2. Weshalb solltest du nach dem Öffnen des Network-Tabs die Seite neu laden?
3. Was zeigt die **Request URL** an?
4. Was zeigt die **Request Method** an?
5. Was beschreibt der **Status Code**?
6. Was ist der Unterschied zwischen Request Headers und Response Headers?
7. Wo kannst du den Antwortinhalt häufig sehen?
8. Was bedeutet `Content-Type: application/json`?
9. Wofür ist der Filter **Fetch/XHR** nützlich?
10. Warum muss eine normale Webseite nicht zwingend JSON-Anfragen zeigen?
11. Wie kann der Network-Tab später bei der Fehlersuche in CashFlow helfen?

[Weiter: Praxis und Wissenscheck →](./08-praxis-wissenscheck.md)
