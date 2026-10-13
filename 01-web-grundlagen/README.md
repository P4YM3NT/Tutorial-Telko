# 01 – Web-Grundlagen

Willkommen im Kapitel **Web-Grundlagen**.

Bevor wir selbst Frontends und Backends entwickeln, schauen wir uns an, wie eine Webanwendung grundsätzlich funktioniert.

In diesem Kapitel geht es noch nicht darum, möglichst viel Code zu schreiben. Wichtig ist zunächst, dass du ein gutes mentales Modell davon bekommst, was zwischen Browser, Server und später auch einer Datenbank passiert.

## Unser Lernprojekt: CashFlow

Im Laufe dieses Tutorials entwickelst du deine eigene Webanwendung namens **CashFlow** – ein kleines **Personal Finance Dashboard**.

Mit CashFlow wirst du später fiktive Einnahmen und Ausgaben erfassen, verwalten und in einem Dashboard auswerten können. Zum Beispiel möchtest du dir alle Ausgaben eines Monats anzeigen lassen oder nach Kategorien filtern.

Dafür kommen im Laufe des Tutorials verschiedene Technologien zum Einsatz. Wir lernen sie Schritt für Schritt kennen und erweitern damit dieselbe Anwendung.

**Noch musst du CashFlow nicht programmieren.** In den Web-Grundlagen verwenden wir die App zunächst nur als Beispiel, um zu verstehen, wie Browser, Backend und Datenbank zusammenspielen.

> **Wichtig:** Wir verwenden im gesamten Tutorial ausschließlich erfundene Finanzdaten. Du benötigst keine echten Konto- oder Zahlungsdaten.

## Lernziele

Nach diesem Kapitel kannst du:

- den Unterschied zwischen Client und Server erklären,
- beschreiben, was Frontend und Backend sind,
- den Aufbau einer URL grob erklären,
- erklären, was ein HTTP-Request und eine HTTP-Response sind,
- wichtige HTTP-Methoden unterscheiden,
- häufige HTTP-Statuscodes einordnen,
- erklären, was JSON ist,
- beschreiben, was eine API ist,
- REST als grundlegenden API-Stil einordnen,
- HTTP-Anfragen in den Browser Developer Tools untersuchen.

## Kapitelübersicht

1. [Client, Server, Frontend und Backend](./01-client-server.md)
2. [URL, Domain und Port](./02-url-domain-port.md)
3. [HTTP, Request und Response](./03-http-request-response.md)
4. [HTTP-Methoden und Statuscodes](./04-http-methoden-statuscodes.md)
5. [JSON](./05-json.md)
6. [APIs und REST](./06-api-rest.md)
7. [HTTP im Browser untersuchen](./07-browser-devtools-network.md)
8. [Praxis und Wissenscheck](./08-praxis-wissenscheck.md)

## Das große Bild

Stell dir vor, du öffnest CashFlow und möchtest deine Transaktionen sehen.

Eine mögliche spätere Fullstack-Anwendung funktioniert vereinfacht so:

```text
┌────────────────────────┐
│ CashFlow im Browser    │
│ Frontend (Vue/Quasar)  │
└───────────┬────────────┘
            │ Anfrage: „Zeige meine Transaktionen“
            ▼
┌────────────────────────┐
│ CashFlow-Backend       │
│ (Node.js / Express)    │
└───────────┬────────────┘
            │ Daten abfragen
            ▼
┌────────────────────────┐
│ Datenbank (PostgreSQL) │
└───────────┬────────────┘
            │ Ergebnis zurückgeben
            ▼
┌────────────────────────┐
│ CashFlow-Backend       │
└───────────┬────────────┘
            │ Antwort mit Transaktionen
            ▼
┌────────────────────────┐
│ CashFlow im Browser    │
└────────────────────────┘
```

Das ist ein **vereinfachtes Beispiel**, noch kein Programm, das du jetzt ausführen sollst.

In diesem Kapitel konzentrieren wir uns zunächst auf die Kommunikation zwischen Browser und Server. Die Datenbank behandeln wir später ausführlich.

> **Merke:** Du musst noch nicht jedes Detail auswendig kennen. Wichtig ist, dass du verstehst, welche Rolle die einzelnen Teile einer Webanwendung spielen.

[Weiter: Client, Server, Frontend und Backend →](./01-client-server.md)
