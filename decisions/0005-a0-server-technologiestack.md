# 0005 – A0-Servertechnologiestack und Architekturgrenzen

Status: angenommen

Datum: 2026-07-22

## Kontext

`galaxis-server` ist zu Beginn praktisch leer. A0 soll eine reproduzierbare technische Grundlage schaffen, auf der die serverautoritative und deterministische Simulation schrittweise aufgebaut werden kann.

Der Server wird vollständig mit **TypeScript auf Node.js** umgesetzt. Die gemeinsame Sprache mit dem Webclient vereinfacht Werkzeugwahl, OpenAPI-Integration, lokale Entwicklung und Codex-Arbeit. Daraus folgt ausdrücklich nicht, dass Client und Server dieselbe Fachlogik teilen: Der Server bleibt autoritativ und die Domain bleibt unabhängig von HTTP, Datenbank und UI.

Die Wahl betrifft zunächst Entwicklung und Alpha-Phase. Einzelne Bibliotheken dürfen später nur durch eine neue dokumentierte Entscheidung und mit nachgewiesener Vertrags-, Persistenz- und Testkompatibilität ersetzt werden.

## Entscheidung

### Laufzeit und Sprache

- Node.js **24 LTS** als Serverlaufzeit.
- Die genaue Patchversion wird im Repository über `.node-version` und `package.json#engines` festgelegt.
- TypeScript im Strict-Modus als einzige produktive Serversprache.
- ECMAScript Modules; kein gemischtes CommonJS-/ESM-Projekt.
- `pnpm` über Corepack als Paketmanager; `pnpm-lock.yaml` ist verbindlich.
- `tsc` übernimmt Typprüfung und Produktionsbuild; `tsx` darf für lokale Entwicklungs- und Werkzeugskripte verwendet werden.
- Keine produktive Ausführung direkt aus untypisiertem JavaScript.

### HTTP, Schema und OpenAPI

- Fastify als HTTP-Adapter.
- TypeBox mit Fastify-Type-Provider für Request-, Response- und Konfigurationsschemas an technischen Grenzen.
- Fastify/Pino für strukturiertes Logging und Request-Korrelation.
- OpenAPI unter `contracts/openapi/` bleibt die maschinenlesbare Vertragsquelle.
- Route-Schemas müssen zum freigegebenen OpenAPI-Vertrag passen; TypeScript-Typen allein ersetzen keine Laufzeitvalidierung.
- WebSockets sind für A0 bis A3 keine Voraussetzung. Aktualisierungen verwenden zunächst REST und später den dokumentierten Changes-Endpunkt.

### Persistenz

- PostgreSQL als persistente Datenbank.
- `pg` als PostgreSQL-Treiber.
- Kysely als typisierter Query-Builder im Infrastrukturadapter.
- Versionierte SQL-Dateien und ein kleiner TypeScript-Migrationsrunner im Repository.
- Datenbanktypen oder Kysely-Typen dürfen nicht in Domainobjekte durchsickern.
- Docker Compose stellt die lokale PostgreSQL-Entwicklungsinstanz bereit.

### Sicherheit

- `argon2` mit Argon2id für Passworthashing.
- Node.js `crypto` für kryptografisch sichere Sessiontokens und Hashes.
- Sessiontokens werden nur einmal im Klartext ausgegeben; gespeichert wird ausschließlich ein geeigneter Tokenhash.
- Kryptografischer Zufall und deterministischer Simulationszufall sind getrennte Ports und Implementierungen.
- Secrets werden weder geloggt noch in Fehlerantworten aufgenommen.

### Tests und Qualität

- Vitest als primäres Testframework.
- Fastify `inject()` für schnelle HTTP-Integrationstests ohne echten Netzwerkport.
- Testcontainers für PostgreSQL-Integrationstests, sofern Docker verfügbar ist.
- ESLint mit TypeScript-Regeln und Prettier für statische Qualität und Formatierung.
- `dependency-cruiser` oder eine gleichwertige explizite Regelprüfung sichert Architekturgrenzen und verhindert Zyklen.
- CI führt mindestens Formatprüfung, Linting, Typprüfung, Unit-Tests, Integrationstests, Contract-Tests und Produktionsbuild aus.

### Architekturgrenzen

Der Server wird mindestens in folgende Verantwortungsbereiche getrennt:

```text
transport/http
    ↓
application
    ↓
domain

infrastructure/database ── implementiert Ports aus application/domain
infrastructure/config
infrastructure/logging
infrastructure/balancing
app/composition-root
```

Es gilt:

1. `domain` kennt weder Fastify, JSON-Schemas, PostgreSQL, Kysely, Umgebungsvariablen noch Dateisystemzugriffe.
2. `application` orchestriert Anwendungsfälle und Transaktionsgrenzen, enthält aber keine HTTP- oder SQL-Details.
3. `transport/http` validiert und übersetzt HTTP/JSON in Application-Aufrufe und Ergebnisse zurück.
4. `infrastructure` implementiert technische Ports, darf aber keine neue Spielregel definieren.
5. `app/composition-root` verdrahtet Module und Lifecycle, enthält aber keine Fachlogik.
6. Zeit, IDs und Simulationszufall werden injiziert. Domaincode verwendet weder `Date.now()`, `new Date()`, `Math.random()` noch `crypto.randomUUID()` direkt.
7. Kryptografischer Zufall für Authentifizierung wird getrennt vom seedbaren Simulationszufall behandelt.
8. Produktive Balancingwerte werden validiert, unveränderlich und versioniert geladen.
9. `any`, unvalidierte Type Assertions und ungeprüfte externe Daten sind an Domain- und Applicationgrenzen nicht zulässig.
10. Gemeinsame TypeScript-Sprache bedeutet nicht gemeinsamen Laufzeitcode zwischen Client und Server. Fachlogik bleibt serverseitig.

## Begründung

TypeScript ermöglicht eine schnelle, durchgängig typisierte Umsetzung von REST-Vertrag, Server und Client. Fastify bietet einen kleinen, testbaren HTTP-Adapter mit guter TypeScript- und Schemaunterstützung. PostgreSQL ist von Beginn an für Accounts, Sessions, Kampagnen und konkurrierende Schreibvorgänge geeignet. Kysely hält SQL sichtbar und typisiert, ohne die Domain an ein umfangreiches ORM zu koppeln.

Die Architektur verhindert, dass REST, Persistenz oder UI-Anforderungen zur fachlichen Wahrheit werden. Derselbe Domain- und Applicationcode kann später ohne HTTP-Server für Headless-Balancingläufe verwendet werden.

Node.js 24 ist zum Entscheidungszeitpunkt eine unterstützte LTS-Linie. Der konkrete Patchstand wird im Repository festgeschrieben und kontrolliert aktualisiert.

## Betrachtete Alternativen

### C++-Server

C++ wäre für maximale Simulationsleistung geeignet, erhöht für die frühe Alpha aber Build-, Abhängigkeits- und Integrationsaufwand. Da der Nutzer TypeScript auch auf dem Server verwenden möchte, wird C++ nicht als A0-Stack eingesetzt. Leistungsengpässe müssen zuerst gemessen werden; isolierte native Module bleiben später möglich, ohne die Serverarchitektur zu ändern.

### NestJS

NestJS bietet starke Strukturvorgaben, Decorators und Dependency Injection. Für A0 wurde Fastify direkt gewählt, weil dadurch Frameworkmagie und zusätzliche Abstraktionsschichten geringer bleiben. Domain- und Applicationstruktur werden explizit im Repository definiert.

### Prisma

Prisma bietet komfortable Generierung und Migrationen. Für Galaxis wurde Kysely mit sichtbaren SQL-Migrationen gewählt, damit komplexe Simulationstransaktionen, Abfragen und Migrationsschritte transparent bleiben und kein ORM-Modell zur Domainquelle wird.

### SQLite als Startdatenbank

SQLite wäre lokal einfacher, bildet konkurrierende Sessions, Transaktionen und den späteren Mehrbenutzerbetrieb aber nur eingeschränkt ab. Eine spätere Migration würde genau in der frühen Persistenzphase zusätzliche Arbeit erzeugen.

### WebSocket von Beginn an

Für Login, Heimatplanet und die ersten Bewegungsabläufe ist REST-Polling ausreichend. WebSocket würde A0 vergrößern, ohne die erste spielbare Schleife zu verbessern.

## Folgen

### Positive Folgen

- Client und Server verwenden dieselbe Sprache und Werkzeugfamilie.
- OpenAPI-Typen und Laufzeitschemas können eng aufeinander abgestimmt werden.
- Codex erhält eine eindeutige und schnell lokal ausführbare A0-Basis.
- Domain- und Simulationstests benötigen keinen Webserver und keine echte Datenbank.
- Balancingläufe können denselben Application- und Domaincode verwenden.
- Lokale Windows-, Linux- und CI-Ausführung verwenden denselben Node-/pnpm-Workflow.

### Verpflichtungen und Risiken

- TypeScript-Typen schützen nicht vor unvalidierten Netzwerk-, Datei- oder Datenbankdaten; Laufzeitvalidierung bleibt Pflicht.
- CPU-intensive Simulation darf den Node-Event-Loop nicht unkontrolliert blockieren. Langläufe müssen messbar, chunkbar und später bei Bedarf in Worker Threads ausführbar sein.
- Zahlendarstellung, Ganzzahligkeit, Rundung und deterministischer Zufall müssen ausdrücklich getestet werden.
- Paket- und Node-Versionen werden gepinnt; unkontrollierte Floating-Versionen sind nicht zulässig.
- Architekturgrenzen müssen automatisiert geprüft werden, weil TypeScript technisch beliebige Imports erlauben würde.
