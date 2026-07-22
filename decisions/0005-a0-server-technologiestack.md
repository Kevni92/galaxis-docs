# 0005 – A0-Servertechnologiestack und Architekturgrenzen

Status: angenommen

Datum: 2026-07-22

## Kontext

`galaxis-server` ist zu Beginn praktisch leer. A0 soll eine reproduzierbare technische Grundlage schaffen, auf der die serverautoritative, deterministische Simulation schrittweise aufgebaut werden kann. Ohne frühe Festlegung der zentralen Werkzeuge würden die ersten Issues dieselben Entscheidungen mehrfach und widersprüchlich treffen.

Die Wahl betrifft zunächst die Entwicklungs- und Alpha-Phase. Einzelne Bibliotheken dürfen später ersetzt werden, aber nur durch eine neue dokumentierte Entscheidung und mit nachgewiesener Vertrags-, Persistenz- und Testkompatibilität.

## Entscheidung

### Sprache und Build

- C++20 als gemeinsamer Sprachstandard für MSVC und GCC/Clang.
- CMake mit versionierten `CMakePresets.json`-Presets.
- vcpkg im Manifestmodus für C++-Abhängigkeiten.
- keine globale Entwicklerinstallation als versteckte Buildvoraussetzung.

### Serveradapter und Daten

- Boost.Asio und Boost.Beast für den asynchronen HTTP-Adapter.
- nlohmann/json für JSON an der Transportgrenze.
- PostgreSQL als persistente Datenbank.
- libpqxx als PostgreSQL-Adapter.
- versionierte SQL-Dateien und ein kleiner kontrollierter Migrationsrunner im Repository.
- spdlog für strukturiertes Logging.
- libsodium für kryptografisch sichere Zufallswerte und Argon2id-Passworthashing.
- Catch2 als primäres C++-Testframework.
- Docker Compose für die lokale PostgreSQL-Entwicklungsinstanz.

### Clientvertrag

- REST über UTF-8 JSON gemäß `contracts/rest-api/`.
- OpenAPI unter `contracts/openapi/` wird die maschinenlesbare Vertragsquelle.
- WebSockets sind für A0 bis A3 keine Voraussetzung. Inkrementelle Aktualisierung verwendet zunächst REST-Polling und später den dokumentierten Changes-Endpunkt.

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
```

Es gilt:

1. `domain` kennt weder HTTP, JSON, PostgreSQL noch Umgebungsvariablen.
2. `application` orchestriert Anwendungsfälle und Transaktionen, enthält aber keine Transportdetails.
3. `transport` übersetzt HTTP und JSON in Application-Aufrufe und Ergebnisse zurück.
4. `infrastructure` implementiert technische Ports, darf aber keine neue Spielregel definieren.
5. Zeit, Zufall und IDs werden injiziert und niemals direkt im Domaincode aus Systemquellen gelesen.
6. `main` verdrahtet Komponenten, enthält aber keine Fachlogik.
7. Produktive Balancingwerte werden als immutable, versionierte Serverdaten geladen.

## Begründung

C++20 entspricht dem vorhandenen Entwicklerumfeld und genügt für modulare, deterministische Simulation ohne unnötige Compilerhürden. Boost.Asio/Beast hält den HTTP-Adapter klein und kontrollierbar, ohne die Domain an ein Webframework zu binden. PostgreSQL ist von Beginn an für Accounts, Sessions, Kampagnen und konkurrierende Schreibvorgänge geeignet. Die gewählten Bibliotheken sind weit verbreitet, plattformübergreifend und gut automatisiert testbar.

Die Architektur verhindert, dass REST, Persistenz oder UI-Anforderungen zur fachlichen Wahrheit werden. Dadurch kann dieselbe Simulation später headless für Balancingläufe verwendet werden.

## Betrachtete Alternativen

### Komplettes C++-Webframework

Ein Framework wie Drogon könnte Routing und Datenbankzugriff beschleunigen. Es wurde für A0 nicht gewählt, weil die Frameworkgrenzen leicht bis in Application und Domain durchdringen. Ein späterer Austausch des HTTP-Adapters bleibt möglich.

### SQLite als Startdatenbank

SQLite wäre lokal einfacher, bildet aber konkurrierende Sessions, Transaktionen und den späteren Mehrbenutzerbetrieb nur eingeschränkt ab. Eine spätere Migration würde genau in der frühen Persistenzphase zusätzliche Arbeit erzeugen.

### WebSocket von Beginn an

Für Login, Heimatplanet und die ersten Bewegungsabläufe ist REST-Polling ausreichend. WebSocket würde A0 vergrößern, ohne die erste spielbare Schleife zu verbessern.

## Folgen

### Positive Folgen

- Codex und Menschen erhalten eine eindeutige A0-Basis.
- Domain- und Simulationstests benötigen keinen Webserver und keine echte Datenbank.
- Balancingläufe können denselben Application- und Domaincode verwenden.
- lokales Windows- und CI-Linux-Build bleiben möglich.

### Negative Folgen

- Boost.Beast benötigt mehr Adaptercode als ein vollständiges Webframework.
- PostgreSQL und Docker erhöhen die lokale A0-Einrichtung.
- ein eigener kleiner Migrationsrunner muss gepflegt werden.

## Überprüfung

Die Entscheidung gilt als korrekt umgesetzt, wenn Server-Issue `Kevni92/galaxis-server#1` abgeschlossen ist und die in A0 angelegte Modulstruktur diese Abhängigkeitsrichtung technisch und dokumentarisch einhält.
