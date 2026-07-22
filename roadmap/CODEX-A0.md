# A0 lokal mit Codex umsetzen

Status: Arbeitsanleitung

Ziel: Milestone **A0 – Technisches Fundament** im Repository `Kevni92/galaxis-server` schrittweise mit einem TypeScript-/Node.js-Server umsetzen.

## 1. Grundregel

Codex bearbeitet nicht den gesamten A0-Milestone in einem einzigen unübersichtlichen Auftrag. Jedes Server-Issue erhält einen eigenen Branch und einen kleinen überprüfbaren PR.

Die einzige Ausnahme ist der initiale Bootstrap des Docs-Submodules, weil `AGENTS.md` das Lesen der eingebundenen Dokumentation verlangt.

Der Server wird vollständig in TypeScript umgesetzt. Alte C++-, CMake-, vcpkg-, Boost-, libpqxx-, libsodium- oder Catch2-Vorgaben sind durch [Decision 0005](../decisions/0005-a0-server-technologiestack.md) ersetzt.

## 2. Repository vorbereiten

```bash
git clone https://github.com/Kevni92/galaxis-server.git
cd galaxis-server

git submodule add https://github.com/Kevni92/galaxis-docs.git docs
git submodule update --init --recursive
```

Falls `.gitmodules` und `docs/` bereits vorhanden sind:

```bash
git submodule update --init --recursive
```

Danach lesen:

```text
AGENTS.md
docs/AGENTS.md
docs/WORKFLOW.md
docs/TESTING.md
docs/SOURCE-CODE.md
docs/decisions/0005-a0-server-technologiestack.md
docs/roadmap/IMPLEMENTATION-ROADMAP.md
```

Vor der ersten eigentlichen Implementierung wird der Submodule-Bootstrap entweder als sehr kleiner vorbereitender Commit festgehalten oder in Server-Issue #2 übernommen. Danach gelten die normalen Issue- und PR-Regeln.

## 3. Voraussetzungen auf dem lokalen Rechner

Erforderlich:

- Git,
- Node.js 24 LTS in der im Repository festgelegten Patchversion,
- Corepack,
- `pnpm`, über das Repository beziehungsweise Corepack festgelegt,
- Docker Desktop beziehungsweise Docker Engine mit Compose,
- GitHub CLI `gh`, sofern Codex Issues und PRs direkt lesen oder erstellen soll.

Initial:

```bash
corepack enable
node --version
pnpm --version
```

Die Versionen müssen später mit `.node-version`, `package.json#engines` und `packageManager` übereinstimmen. Globale npm-Pakete dürfen keine versteckte Voraussetzung sein.

## 4. Verbindlicher TypeScript-Stack

Codex verwendet für A0:

- Node.js 24 LTS,
- TypeScript strict und ESM,
- pnpm,
- Fastify,
- TypeBox an Transport- und Konfigurationsgrenzen,
- Pino,
- PostgreSQL,
- `pg` und Kysely,
- versionierte SQL-Migrationen,
- `argon2` mit Argon2id,
- Node.js `crypto` für Sessiontokens und Hashes,
- Vitest,
- Fastify `inject()`,
- Testcontainers für PostgreSQL-Integrationstests,
- ESLint, Prettier und Architekturprüfung über `dependency-cruiser` oder eine gleichwertige festgelegte Lösung.

Codex darf nicht ohne neue Docs-Entscheidung auf NestJS, Prisma, SQLite oder einen C++-Server ausweichen.

## 5. Empfohlene Issue-Reihenfolge

```text
#1  TypeScript-Technologiestack und Architekturgrenzen
#2  Repository-Basis und Docs-Submodule
#8  deterministische Zeit-, Zufalls- und ID-Provider
#3  Konfiguration, Logging und Health
#4  PostgreSQL und Migrationen
#5  Fastify-REST-Kern und Fehlerformat
#9  Balancing-Loader, Schema und Hash
#6  Accounts und Registrierung
#7  Bearer-Sessions
#10 OpenAPI-Contract-Tests
#11 lokale Gesamtumgebung und CI-Gate
```

Die Reihenfolge weicht absichtlich von der Nummerierung ab. Zeit, Zufall und IDs werden früh abstrahiert, bevor spätere Module direkte Zugriffe auf `Date.now()`, `new Date()`, `Math.random()` oder `crypto.randomUUID()` einführen.

## 6. Startprompt für Codex

Für das erste Issue kann folgender Auftrag verwendet werden:

```text
Arbeite im Repository Kevni92/galaxis-server an GitHub-Issue #1.

Lies zuerst vollständig:
- AGENTS.md
- docs/AGENTS.md
- docs/WORKFLOW.md
- docs/TESTING.md
- docs/SOURCE-CODE.md
- docs/decisions/0005-a0-server-technologiestack.md
- docs/roadmap/IMPLEMENTATION-ROADMAP.md
- das vollständige Issue #1 einschließlich Akzeptanzkriterien

Setze ausschließlich Issue #1 um. Erfinde keine Gameplayregeln und implementiere noch keine Authentifizierung, Datenbanktabellen oder Kampagnenlogik.

Der Serverstack ist Node.js 24 LTS mit TypeScript strict/ESM und pnpm. Halte domain, application, infrastructure, transport/http und app/composition-root getrennt. Domaincode darf Fastify, TypeBox, Kysely, pg, process.env, Date.now(), Math.random() und Node-spezifische I/O-APIs nicht direkt verwenden.

Arbeite in einem eigenen Branch. Aktualisiere die betroffenen README-Navigationen. Führe die laut TESTING.md erforderlichen Prüfungen aus und dokumentiere ehrlich, welche Tests tatsächlich gelaufen sind.

Am Ende:
1. fasse die Änderungen zusammen,
2. nenne alle ausgeführten Tests und Ergebnisse,
3. nenne offene Risiken oder Folgearbeiten,
4. committe die Änderung bewusst,
5. öffne einen Draft-PR mit Feature-ID GAL-PLATFORM-STACK-001 und Links auf Issue #1 sowie die maßgeblichen Docs.
```

Für die weiteren Issues werden Issue-Nummer und Feature-ID angepasst. Codex muss jedes Mal die im Issue genannten Quellen erneut prüfen.

## 7. Erwartete Repositorystruktur nach Issue #2

Die genaue Feinstruktur darf während #1 dokumentiert werden. Als verbindliche Mindeststruktur gilt:

```text
src/
├── app/
│   └── composition-root/
├── domain/
├── application/
├── infrastructure/
│   ├── balancing/
│   ├── config/
│   ├── database/
│   └── logging/
└── transport/
    └── http/

tests/
├── unit/
├── integration/
├── contract/
└── fixtures/

migrations/
scripts/
docs/                  # Git-Submodule
```

Sinnvolle Mindestdateien:

```text
package.json
pnpm-lock.yaml
tsconfig.json
tsconfig.build.json
eslint.config.js
prettier.config.js
.node-version
.env.example
docker-compose.yml
README.md
```

## 8. Erwartetes Ergebnis je A0-Issue

### Issue #1

- dokumentierter TypeScript-/Node-Stack,
- Modul- und Importgrenzen,
- Build-, Test- und Skriptstruktur,
- keine Fachlogik,
- keine konkurrierenden Frameworkentscheidungen.

### Issue #2

- `docs/` als echtes Git-Submodule,
- `package.json`, pnpm-Lockfile und TypeScript-Basis,
- minimales Server-Entrypoint und Testziel,
- ESLint, Prettier und Architekturprüfung,
- README für frischen Checkout,
- Modul-READMEs.

### Issue #8

- injizierbare Clock-, Random- und ID-Ports,
- Produktions- und Fakeimplementierungen,
- Tests ohne Sleep,
- keine globale Simulationszufallsquelle,
- klare Trennung von Simulationszufall und kryptografischem Zufall.

### Issue #3

- validierte Konfiguration über TypeBox oder gleichwertig festgelegtes Schema,
- Pino-Logging,
- Liveness und Readiness,
- geordneter Shutdown.

### Issue #4

- PostgreSQL über Docker Compose,
- `pg`-Pool und Kysely-Adapter,
- transaktionaler SQL-Migrationsrunner,
- Integrationstest mit isolierter Datenbank oder Testcontainer.

### Issue #5

- Fastify-Server und `/api/v1`-Router,
- TypeBox-Validierung,
- Request-Kontext und Korrelations-ID,
- einheitliches Fehlerformat,
- definierte Body- und Timeoutgrenzen,
- HTTP-Tests über Fastify `inject()`.

### Issue #9

- validiertes Balancingmanifest,
- kanonische Serialisierung,
- SHA-256-Hash,
- unveränderliche Runtimekonfiguration,
- positive und negative Fixtures.

### Issue #6

- Account-Domainmodell,
- Repository-Port und PostgreSQL-Adapter,
- Registrierung,
- Argon2id Hash/Verify,
- keine Account-Enumeration oder Geheimnislogs.

### Issue #7

- opake Sessiontokens aus `crypto.randomBytes`,
- ausschließlich gehashte Tokens in PostgreSQL,
- Login, Sessionprüfung und Logout,
- Auth-Hook beziehungsweise Middleware ohne Kampagnenannahmen.

### Issue #10

- A0-OpenAPI als Testquelle,
- Request-/Response-Contract-Tests,
- Fehlerformatprüfung,
- Abweichungen blockieren CI.

### Issue #11

- `pnpm`-Skripte für Lint, Typecheck, Test, Build, Migration und Start,
- Docker-Compose-Gesamtumgebung,
- CI mit Node/pnpm-Cache,
- vollständiger A0-Smoke-Test.

## 9. Standardbefehle

Nach Issue #2 sollen möglichst folgende Befehle existieren:

```bash
pnpm install --frozen-lockfile
pnpm format:check
pnpm lint
pnpm typecheck
pnpm test
pnpm test:integration
pnpm test:contract
pnpm build
pnpm dev
```

Codex darf fehlende Skripte nicht stillschweigend überspringen. Ist ein Skript erst Gegenstand eines späteren Issues, muss dies im PR ausdrücklich genannt werden.

## 10. Architekturregeln für Codex

- Kein `any`, außer an technisch unvermeidbarer Stelle mit Begründung und lokaler Eingrenzung.
- Externe Daten werden zur Laufzeit validiert.
- Domaincode importiert keine Infrastruktur- oder Transportmodule.
- Fastify-Handler enthalten keine Fachlogik.
- Kysely-Zeilen werden über Mapper in Domain- oder Applicationtypen übersetzt.
- `process.env` wird nur im Konfigurationsadapter gelesen.
- Systemzeit und Zufall werden nur in den dafür vorgesehenen Produktionsadaptern gelesen.
- Fehler werden als definierte Application-/Domainfehler modelliert und erst im HTTP-Adapter übersetzt.
- Tests verwenden kontrollierte Zeit und Seeds; reale Wartezeiten sind zu vermeiden.
- CPU-intensive Simulationsschleifen dürfen später nicht unkontrolliert den Event Loop blockieren.

## 11. PR-Regel

Ein PR schließt genau ein Issue ab. Er enthält:

- Feature-ID,
- Link auf Server-Issue und Docs-Umbrella #115,
- gelesene maßgebliche Quellen,
- Änderung und klare Nicht-Ziele,
- tatsächlich ausgeführte Tests,
- bekannte Risiken,
- eventuell notwendige Folge-Issues.

A0 wird nicht in einem einzigen Sammel-PR umgesetzt.
