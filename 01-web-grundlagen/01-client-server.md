# 01 – Client, Server, Frontend und Backend

[← Zurück zur Übersicht](./README.md) | [Weiter: URL, Domain und Port →](./02-url-domain-port.md)

Wenn du eine Webseite öffnest, arbeiten im Hintergrund oft mehrere Programme zusammen.

Die zwei wichtigsten Begriffe für den Anfang sind:

```text
Client
Server
```

## Was ist ein Client?

Ein **Client** ist ein Programm, das eine Anfrage an einen anderen Dienst stellt.

Bei Webanwendungen ist der Client häufig dein Browser.

Beispiele für Clients sind:

- ein Webbrowser,
- eine Smartphone-App,
- ein Desktop-Programm,
- ein anderes Backend.

Wenn du eine Webseite öffnest, kann dein Browser Daten von einem Server anfordern.

## Was ist ein Server?

Ein **Server** ist ein Programm, das Anfragen entgegennimmt und darauf antwortet.

Zum Beispiel:

```text
Browser:
„Gib mir die Startseite.“

Server:
„Hier ist die Startseite.“
```

Oder später bei unserem Lernprojekt **CashFlow**:

```text
Browser:
„Zeige mir meine Transaktionen.“

Server:
„Hier sind die angefragten Transaktionen.“
```

> **Merke:** Mit „Server“ kann im Alltag sowohl ein Rechner als auch ein darauf laufendes Programm gemeint sein. Hier sprechen wir vor allem über das Programm, das Anfragen beantwortet.

## Client und Server zusammen

Vereinfacht sieht die Kommunikation so aus:

```text
┌────────────┐
│   Client   │
│  Browser   │
└─────┬──────┘
      │
      │ Anfrage
      ▼
┌────────────┐
│   Server   │
└─────┬──────┘
      │
      │ Antwort
      ▼
┌────────────┐
│   Client   │
│  Browser   │
└────────────┘
```

Für diese Kommunikation verwenden Webanwendungen meistens **HTTP** oder **HTTPS**.

Was genau dahintersteckt, behandeln wir in einem späteren Abschnitt dieses Kapitels.

## Webseite oder Webanwendung – was ist der Unterschied?

Eine **Webseite** stellt oft hauptsächlich Informationen dar, zum Beispiel Öffnungszeiten oder einen Artikel.

Eine **Webanwendung** ermöglicht es dir zusätzlich, mit Funktionen zu arbeiten, etwa Daten zu erfassen, zu filtern oder zu ändern.

CashFlow ist eine Webanwendung: Du kannst später Ausgaben hinzufügen, bearbeiten und auswerten.

Die Grenze ist nicht immer eindeutig. Für den Einstieg reicht diese Unterscheidung.

## Was ist das Frontend?

Das **Frontend** ist der Teil einer Anwendung, mit dem Benutzer direkt interagieren.

Dazu gehören zum Beispiel:

- Texte,
- Buttons,
- Formulare,
- Tabellen,
- Navigation,
- Dialoge.

Bei CashFlow gehören etwa die **Transaktionsliste**, die **Monatsübersicht** und ein Button **„Ausgabe hinzufügen“** zum Frontend.

In unserem Tutorial bauen wir das Frontend später mit:

```text
JavaScript
Vue
Quasar
```

Das Frontend läuft bei klassischen Webanwendungen überwiegend im Browser.

## Statische und dynamische Inhalte

Nicht jeder Inhalt auf einer Seite muss jedes Mal neu berechnet oder vom Backend abgerufen werden.

- **Statisch:** Ein fester Titel wie „CashFlow“ bleibt gleich, solange niemand die Seite beziehungsweise den Code verändert.
- **Dynamisch:** Die Summe deiner Ausgaben kann sich ändern, wenn du eine Transaktion hinzufügst.

Dynamische Inhalte können im Browser berechnet oder vom Backend geliefert werden. **Dynamisch bedeutet also nicht automatisch, dass eine Datenbank benötigt wird.**

## Was ist das Backend?

Das **Backend** läuft normalerweise auf einem Server.

Es übernimmt zum Beispiel Aufgaben wie:

- Daten verarbeiten,
- Eingaben prüfen,
- Geschäftslogik ausführen,
- Daten aus einer Datenbank lesen,
- Daten in einer Datenbank speichern,
- Antworten an das Frontend senden.

In CashFlow könnte das Backend später überprüfen, ob der Betrag einer Transaktion gültig ist, und die Transaktion speichern.

In unserem Tutorial verwenden wir später:

```text
Node.js
Express
Joi
```

## Frontend und Backend zusammen

Beispiel: Jemand öffnet in CashFlow die Transaktionsübersicht.

```text
┌─────────────────────┐
│ Frontend im Browser │
│ Vue / Quasar        │
└──────────┬──────────┘
           │
           │ „Gib mir die Transaktionen“
           ▼
┌─────────────────────┐
│ Backend             │
│ Node.js / Express   │
└──────────┬──────────┘
           │
           │ Daten lesen
           ▼
┌─────────────────────┐
│ Datenbank           │
│ PostgreSQL          │
└─────────────────────┘
```

Das Backend bekommt die angefragten Daten von der Datenbank und schickt sie als Antwort an das Frontend. Dort werden sie angezeigt.

**Wichtig:** In unserer geplanten Anwendung greift das Frontend nicht direkt auf PostgreSQL zu. Das Backend übernimmt den Datenbankzugriff.

Das ist ein vereinfachter Überblick. Wir werden diese Architektur erst in späteren Kapiteln selbst umsetzen.

## Sind Client und Frontend dasselbe?

Nicht immer.

In vielen Webanwendungen ist der Browser gleichzeitig der Client und führt das Frontend aus.

Aber grundsätzlich sind die Begriffe unterschiedlich:

```text
Client
→ stellt Anfragen an einen Server

Frontend
→ sichtbarer und interaktiver Teil einer Anwendung
```

Ein Client muss also nicht zwingend ein grafisches Frontend besitzen.

## Sind Server und Backend dasselbe?

Auch diese Begriffe werden häufig ähnlich verwendet, bedeuten aber nicht exakt dasselbe.

```text
Server
→ Programm oder System, das Anfragen entgegennimmt

Backend
→ serverseitiger Teil unserer Anwendung
```

Für den Einstieg reicht es, wenn du weißt:

> In unserer späteren Fullstack-Anwendung kommuniziert das Frontend im Browser mit unserem Backend auf einem Server.

## Kleine Übung – Begriffe zuordnen

Ordne diese Bestandteile unserer späteren CashFlow-Anwendung zu:

```text
Browser mit geöffneter CashFlow-Seite
Express-Anwendung
Button „Ausgabe hinzufügen“
PostgreSQL
Anfrage „Zeige meine Transaktionen“
```

Mögliche Kategorien:

```text
Client
Frontend
Backend
Datenbank
Kommunikation
```

**Hinweis:** Ein Bestandteil kann zu mehr als einer Kategorie passen.

Notiere deine Zuordnung und begründe mindestens zwei deiner Entscheidungen mit eigenen Worten. Die Lösungen stehen nicht in diesem Kapitel.

## Kleine Übung – Statisch oder dynamisch?

Überlege dir bei den folgenden Inhalten, ob sie in CashFlow eher statisch oder dynamisch wären:

1. Der feste Seitentitel „CashFlow“.
2. Die Summe aller Ausgaben im ausgewählten Monat.
3. Die Transaktionsliste nach dem Hinzufügen einer neuen Ausgabe.

Begründe deine Antworten kurz. Du brauchst dafür noch keinen Code zu schreiben.

## Wissenscheck

Beantworte die Fragen mit eigenen Worten. Du kannst die Antworten an einem Ort deiner Wahl notieren und die bisherigen Abschnitte bei Bedarf noch einmal nachlesen.

1. Was ist ein Client?
2. Was ist ein Server?
3. Welche Aufgaben übernimmt ein Frontend?
4. Welche Aufgaben übernimmt ein Backend?
5. Warum braucht unsere geplante CashFlow-Anwendung mehrere Teile?
6. Was ist der Unterschied zwischen statischen und dynamischen Inhalten?
7. Greift das CashFlow-Frontend direkt auf PostgreSQL zu?

[Weiter: URL, Domain und Port →](./02-url-domain-port.md)
