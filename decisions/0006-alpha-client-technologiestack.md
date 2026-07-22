# 0006 – Alpha-Clienttechnologiestack

Status: angenommen

Datum: 2026-07-22

## Kontext

Der Client soll die serverseitig implementierten Alpha-Schnitte möglichst früh bedienbar machen, ohne die Serverarbeit durch ein großes UI-Projekt zu blockieren. Dafür benötigt `galaxis-client` eine kleine, typisierte und gut testbare Basis.

## Entscheidung

Für A0 bis A3 gilt:

- TypeScript,
- Vue 3 mit Composition API,
- Vite,
- Vue Router,
- Pinia,
- native `fetch`-Abstraktion als zentraler REST-Client,
- aus OpenAPI generierte TypeScript-Typen,
- Vitest und Vue Test Utils,
- Playwright für wenige kritische End-to-End-Demos,
- SVG für die ersten System- und Galaxiekarten.

Der Client bleibt ein Desktop-Webclient. Eine spätere native Verpackung oder Mobile-App ist nicht Teil von A0 bis A3.

## Regeln

1. Der Server bleibt fachlich autoritativ.
2. Komponenten rufen `fetch` nicht direkt auf.
3. Clientzustände repräsentieren Serverantworten, Ladezustände und lokale Auswahl, aber keine unabhängige Spielsimulation.
4. Zulässige Befehle, Kosten, Dauer und Ergebnisse werden aus Serverdaten abgeleitet.
5. Typgenerierung ersetzt nicht die fachlichen Contract-Tests.
6. Karten verwenden servergelieferte Positionen und Wissensstände; der Client ergänzt keine verborgenen Objekte.
7. A0 bis A3 erhalten nur die UI, die für die jeweilige Abnahmedemo benötigt wird.

## Begründung

Vue, Pinia und Vite erlauben eine kleine, modulare Oberfläche und passen zu den bereits verwendeten Frontendwerkzeugen. TypeScript und OpenAPI-Typen reduzieren Vertragsabweichungen. SVG genügt für die frühen Karten, bleibt inspectable und benötigt keine 3D- oder Canvas-Engine.

## Nicht gewählt

- keine 3D-Engine in den frühen Alphas,
- kein Electron- oder Tauri-Paket in A0,
- kein WebSocket-Zwang,
- keine lokale Regel-Engine,
- kein umfassendes Designsystem vor dem ersten spielbaren Schnitt.

## Folgen

Die UI kann pro Alpha klein bleiben und parallel hinter dem Server entstehen. Spätere visuelle Überarbeitung darf Komponenten ersetzen, solange REST-Verträge, Zustandsgrenzen und E2E-Abläufe erhalten bleiben.

## Überprüfung

Die Entscheidung gilt als umgesetzt, wenn `Kevni92/galaxis-client#1` abgeschlossen ist und alle A0-Clienttests ohne direkte Duplizierung von Serverregeln laufen.
