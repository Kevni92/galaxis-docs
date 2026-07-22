# A0 lokal mit Codex umsetzen

Status: Arbeitsanleitung

Ziel: Milestone **A0 – Technisches Fundament** im Repository `Kevni92/galaxis-server` schrittweise lokal umsetzen.

## 1. Grundregel

Codex bearbeitet nicht den gesamten A0-Milestone in einem einzigen unübersichtlichen Auftrag. Jedes Server-Issue erhält einen eigenen Branch und einen kleinen überprüfbaren PR.

Die einzige Ausnahme ist der initiale Bootstrap des Docs-Submodules, weil `AGENTS.md` das Lesen der eingebundenen Dokumentation verlangt.

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
- CMake,
- ein C++20-fähiger Compiler,
- vcpkg oder die im Repository dokumentierte Bootstrapmethode,
- Docker Desktop beziehungsweise Docker Engine mit Compose,
- GitHub CLI `gh`, sofern Codex Issues und PRs direkt lesen oder erstellen soll.

Unter Windows ist Visual Studio 2022 mit C++-Toolchain der primäre lokale Compiler. Die CI verwendet zusätzlich Linux, damit keine unbemerkte Windows-Abhängigkeit entsteht.

## 4. Empfohlene Issue-Reihenfolge

```text
#1  Technologiestack und Architekturgrenzen
#2  Repository-Basis und Docs-Submodule
#8  deterministische Zeit-, Zufalls- und ID-Provider
#3  Konfiguration, Logging und Health
#4  PostgreSQL und Migrationen
#5  REST-Kern und Fehlerformat
#9  Balancing-Loader, Schema und Hash
#6  Accounts und Registrierung
#7  Bearer-Sessions
#10 OpenAPI-Contract-Tests
#11 lokale Gesamtumgebung und CI-Gate
```

Die Reihenfolge weicht absichtlich von der Nummerierung ab. Zeit, Zufall und IDs werden früh abstrahiert, bevor spätere Module versehentlich direkte Systemzugriffe einführen.

## 5. Startprompt für Codex

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

Arbeite in einem eigenen Branch. Halte Domain, Application, Infrastructure und Transport getrennt. Aktualisiere die betroffenen README-Navigationen. Führe die laut TESTING.md erforderlichen Prüfungen aus und dokumentiere ehrlich, welche Tests tatsächlich gelaufen sind.

Am Ende:
1. fasse die Änderungen zusammen,
2. nenne alle ausgeführten Tests und Ergebnisse,
3. nenne offene Risiken oder Folgearbeiten,
4. committe die Änderung bewusst,
5. öffne einen Draft-PR mit Feature-ID GAL-PLATFORM-STACK-001 und Links auf Issue #1 sowie die maßgeblichen Docs.
```

Für die weiteren Issues wird nur die Issue-Nummer und Feature-ID angepasst. Codex muss jedes Mal die im Issue genannten Quellen erneut prüfen.

## 6. Erwartetes Ergebnis je A0-Issue

### Issue #1

- dokumentierte Modulgrenzen,
- Buildzielstruktur,
- keine Fachlogik,
- keine versteckten alternativen Bibliotheksentscheidungen.

### Issue #2

- `docs/` als echtes Git-Submodule,
- CMake-, Preset- und vcpkg-Basis,
- minimales Server- und Testbinary,
- README für frischen Checkout,
- Modul-READMEs.

### Issue #8

- injizierbare Clock-, Random- und ID-Interfaces,
- Fakeimplementierungen,
- Tests ohne Sleep,
- keine globale Zufallsquelle.

### Issue #3

- validierte Konfiguration,
- strukturiertes Logging,
- Liveness und Readiness,
- geordneter Shutdown.

### Issue #4

- PostgreSQL über Docker Compose,
- libpqxx-Adapter,
- transaktionaler Migrationsrunner,
- Integrationstest gegen isolierte Datenbank.

### Issue #5

- `/api/v1`-Router,
- JSON- und Content-Type-Prüfung,
- Request-Kontext,
- einheitliches Fehlerformat,
- definierte Grenzwerte.

### Issue #9

- Balancingmanifest,
- Schema- und Referenzprüfung,
- kanonischer Hash,
- immutable Runtimekonfiguration.

### Issue #6

- Accountmodell,
- Registrierung,
- Argon2id-Passworthash,
- Accountpersistenz,
- keine Geheimnisse in Logs oder Antworten.

### Issue #7

- opake Bearer-Tokens,
- nur gehashte Tokens in PostgreSQL,
- Login, Sessionprüfung und Logout,
- Auth-Middleware.

### Issue #10

- OpenAPI-Contract-Tests gegen Docs,
- Schema- und Fehlerantwortprüfung,
- CI-Abweichung führt zum Fehlschlag.

### Issue #11

- dokumentierter Gesamtstart,
- Build-, Unit-, Integration- und Contract-Gate,
- A0-Smoke-Skript,
- GitHub Actions im vorgesehenen Zeitkorridor.

## 7. Definition of Done für A0

A0 ist nicht abgeschlossen, nur weil der Server kompiliert. Erforderlich sind:

- Registrierung, Login, Sessionprüfung und Logout über echte HTTP-Endpunkte,
- PostgreSQL-Persistenz und idempotente Migrationen,
- definierte Health-Endpunkte,
- Balancingversion und Hash,
- keine Klartextpasswörter oder Klartexttokens in der Datenbank,
- reproduzierbarer Start nach frischem Checkout,
- Unit-, Integrations- und Contract-Tests,
- minimaler Client-E2E gemäß `galaxis-client#6`,
- Abschlussprüfung im Docs-Umbrella #115.

## 8. Was Codex in A0 ausdrücklich nicht tun soll

- keine Kampagne oder Galaxie erzeugen,
- keinen Planeten oder Koloniezustand anlegen,
- keine Schiffe implementieren,
- keine WebSockets einführen,
- kein umfangreiches Adminsystem bauen,
- keine E-Mail-Verifikation oder Passwort-Reset-Funktion ergänzen,
- keine UI im Serverrepository ablegen,
- keine fachlichen Werte im C++-Code hart verdrahten,
- keine großen Sammel-PRs über mehrere unabhängige Issues erstellen.

## 9. Übergang zu A1

Nach Abschluss von A0 beginnt A1 mit `galaxis-server#12`. Vorher wird geprüft:

1. Docs-Issue #128 ist abgeschlossen.
2. Alle A0-Server-Issues sind abgeschlossen.
3. Alle A0-Client-Issues sind abgeschlossen.
4. A0-E2E läuft nach frischem Checkout.
5. Das Docs-Umbrella #115 bestätigt das Gate.

Erst danach wird die erste Kampagne und damit der Heimatplanet implementiert.
