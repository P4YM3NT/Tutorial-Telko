# 02 – URL, Domain und Port

[← Zurück: Client und Server](./01-client-server.md) | [Weiter: HTTP, Request und Response →](./03-http-request-response.md)

Wenn du eine Webseite öffnest, gibst du meistens eine Adresse in den Browser ein oder klickst auf einen Link.

Zum Beispiel:

```text
https://example.com/products?id=42
```

Eine solche Adresse nennt man **URL**.

URL steht für:

```text
Uniform Resource Locator
```

Eine URL beschreibt, **unter welcher Adresse eine Ressource erreichbar ist**. Das kann zum Beispiel eine Webseite, ein Bild oder später eine Antwort unserer CashFlow-API sein.

## Vereinfachter Aufbau einer URL

Schauen wir uns eine Beispieladresse für unser späteres Projekt **CashFlow** an:

```text
https://cashflow.example.com:8443/api/transactions/42?details=true
```

Sie besteht aus verschiedenen Teilen:

| Bestandteil | Wert | Bedeutung |
|---|---|---|
| Protokoll | `https` | Wie kommuniziert wird |
| Domain | `cashflow.example.com` | Unter welchem Namen der Dienst erreichbar ist |
| Port | `8443` | Welcher Netzwerkdienst angesprochen wird |
| Pfad | `/api/transactions/42` | Welche Ressource angefragt wird |
| Query-Parameter | `details=true` | Zusätzliche Information zur Anfrage |

**Wichtig:** `cashflow.example.com` ist nur eine **ausgedachte Beispieladresse**. Dort läuft nicht unser Projekt. Auch der Port `8443` dient hier nur zur Veranschaulichung.

## Protokoll

Am Anfang einer Webadresse steht häufig:

```text
http://
```

oder:

```text
https://
```

Das beschreibt das verwendete Protokoll.

Für Webanwendungen verwenden wir **HTTP** beziehungsweise **HTTPS**.

Bei **HTTPS** wird die Kommunikation zwischen Browser und Server verschlüsselt. Gerade bei einer Anwendung, die später persönliche Finanzdaten verarbeitet, ist das wichtig.

Wie HTTP-Anfragen und -Antworten aufgebaut sind, schauen wir uns im nächsten Unterkapitel an.

## Domain

Beispiel:

```text
cashflow.example.com
```

Die Domain ist ein für Menschen lesbarer Name, unter dem ein Dienst erreichbar sein kann.

Computer kommunizieren im Netzwerk letztlich über **IP-Adressen**. Das **Domain Name System (DNS)** hilft dabei, einen Domainnamen der passenden IP-Adresse zuzuordnen.

Vereinfacht:

```text
cashflow.example.com
         │
         │ DNS
         ▼
IP-Adresse eines Servers
```

Wie DNS im Detail funktioniert, müssen wir für das Tutorial noch nicht wissen.

## Port

Auf einem Computer können mehrere Netzwerkdienste gleichzeitig laufen. Ein **Port** hilft dabei, diese Dienste voneinander zu unterscheiden.

Beispiel:

```text
http://localhost:3000
```

Hier ist:

```text
localhost → der eigene Rechner
3000      → der Port
```

Später könnten wir CashFlow lokal mit zwei getrennten Entwicklungsdiensten starten:

```text
Frontend:
http://localhost:9000

Backend:
http://localhost:3000
```

Diese Portnummern sind **nur Beispiele**. Welche Ports wir tatsächlich verwenden, hängt von der späteren Einrichtung ab.

> **Merke:** Ein Port gehört nicht zum Namen einer Datei oder eines Ordners. Er kennzeichnet einen Netzwerkdienst auf einem Rechner.

## Standardports

Bei HTTP und HTTPS steht der Port häufig nicht ausdrücklich in der URL.

Die üblichen Standardports sind:

```text
HTTP  → 80
HTTPS → 443
```

Wenn der jeweilige Standardport verwendet wird, muss er nicht in der URL stehen.

Die beiden Schreibweisen meinen daher im Normalfall denselben Zielport:

```text
https://example.com
https://example.com:443
```

## Pfad

Der **Pfad** bezeichnet eine bestimmte Ressource oder einen Bereich innerhalb eines Dienstes.

Für CashFlow könnten solche Pfade vorkommen:

```text
/api/transactions
/api/transactions/42
```

Eine mögliche Bedeutung wäre:

- `/api/transactions` – die Sammlung unserer Transaktionen,
- `/api/transactions/42` – eine einzelne Transaktion mit der ID `42`.

Was der Server unter einem bestimmten Pfad tatsächlich anbietet, legt die jeweilige Anwendung fest. Die Beispiele beschreiben unsere **geplante** API, die wir erst später entwickeln.

## Query-Parameter

Mit **Query-Parametern** können wir zusätzliche Informationen an eine URL anhängen.

Stell dir vor, du möchtest in CashFlow nur die Ausgaben eines bestimmten Monats sehen:

```text
https://cashflow.example.com/api/transactions?month=2026-10&type=expense
```

Die URL enthält:

```text
Pfad:
/api/transactions

Query-Parameter:
month=2026-10
type=expense
```

Das Fragezeichen `?` beginnt die Query-Parameter. Das Zeichen `&` trennt mehrere Parameter.

Query-Parameter eignen sich beispielsweise für:

- Filter,
- Sortierung,
- Suche,
- die Auswahl einer Seite bei langen Listen (Pagination).

**Pfad oder Query-Parameter?** Vereinfacht gesagt: Der Pfad bestimmt, **welche Ressource** angesprochen wird. Query-Parameter beschreiben häufig, **welche Auswahl oder Darstellung** davon gewünscht ist.

> **Wichtig:** Passwörter und andere Geheimnisse gehören nicht in eine URL. URLs können zum Beispiel im Browserverlauf oder in Serverprotokollen auftauchen.

## Was ist `localhost`?

Während der Entwicklung verwenden wir häufig:

```text
localhost
```

`localhost` bezeichnet den **eigenen Rechner**.

Wenn du später eine Adresse wie diese aufrufst:

```text
http://localhost:3000
```

versucht dein Browser, einen Dienst **auf deinem eigenen Rechner** über Port `3000` zu erreichen.

Das funktioniert nur, wenn dort tatsächlich ein passender Dienst läuft. `localhost` startet selbst keinen Server.

## Kleine Übung 1 – URL zerlegen

Zerlege diese **fiktive** CashFlow-Adresse:

```text
https://cashflow.example.com:8443/api/transactions/15?details=true
```

Bestimme:

1. Protokoll,
2. Domain,
3. Port,
4. Pfad,
5. Query-Parameter.

Notiere deine Antworten an einem Ort deiner Wahl.

## Kleine Übung 2 – Pfad oder Query-Parameter?

Stell dir vor, CashFlow verwendet folgende URL:

```text
https://cashflow.example.com/api/transactions?month=2026-10&type=expense
```

Beantworte mit eigenen Worten:

1. Welcher Teil ist der Pfad?
2. Welche zwei Query-Parameter sind enthalten?
3. Was könnte der Benutzer damit im Dashboard sehen wollen?
4. Was wäre anders, wenn du stattdessen `/api/transactions/15` aufrufst?

Du musst für diese Übungen **noch keinen Server starten und keinen Code schreiben**. Es geht nur darum, Adressen zu verstehen.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Wenn du nicht weiterkommst, darfst du in den vorherigen Abschnitten nachschlagen.

1. Was beschreibt eine URL?
2. Was ist eine Domain?
3. Wofür werden Ports verwendet?
4. Was bedeutet `localhost`?
5. Was ist der Unterschied zwischen Pfad und Query-Parametern?
6. Wofür steht das `?` in einer URL, und was macht das `&`?
7. Warum sollten keine Passwörter in einer URL stehen?

[Weiter: HTTP, Request und Response →](./03-http-request-response.md)
