# Verbindliche Teststrategie für Galaxis

Diese Strategie gilt für `galaxis-client`, `galaxis-server` und spätere Umsetzungs-Repositories.

> **Grundregel:** Jede Änderung erhält die kleinsten Tests, die ihr tatsächliches Risiko zuverlässig abdecken. Teure System- und UI-Tests laufen nicht pauschal bei jeder kleinen PR.

## 1. Ziele

Tests müssen:

- fachliche Regeln zuverlässig absichern,
- schnell genug für häufige kleine PRs bleiben,
- Fehler möglichst nah an ihrer Ursache erkennen,
- deterministisch und reproduzierbar sein,
- teure End-to-End-Tests auf kritische Abläufe begrenzen.

## 2. Teststufen

### Lokal vor Commit

Zielzeit: **unter 30 Sekunden**.

- Formatierung und Linting,
- Typ- oder Compilerprüfung für betroffene Bereiche,
- betroffene Unit-Tests,
- gezielte Komponententests.

### Pull Request

Zielzeit: **2 bis 5 Minuten**.

- Build,
- Unit-Tests,
- relevante Komponenten- oder Integrationstests,
- Contract-Tests,
- nur wenige kritische Playwright-Smoke-Tests.

### Nach Merge auf `main`

- vollständige Unit- und Integrationstests,
- Client gegen echten Server,
- größere E2E-Suite,
- Persistenz- und Migrationsprüfungen.

### Nachtlauf oder manuell

- alle unterstützten Browser,
- vollständige Playwright-Suite,
- lange AI- und Simulationsläufe,
- Performance- und Speicherprüfungen,
- Savegame- und Kompatibilitätstests,
- visuelle Regressionen.

### Release

- vollständiger Systemtest,
- Upgrade bestehender Spielstände,
- Produktions-Build und Deployment-Test,
- manuelle Abnahme kritischer Abläufe.

## 3. Servertests

### Unit-Tests

Bevorzugt für:

- Spielregeln und Berechnungen,
- Befehlsvalidierung,
- Zustandsübergänge,
- Zeit- und Ressourcenmodelle,
- Kampf- und Reiseberechnungen,
- AI-Entscheidungslogik.

Unit-Tests dürfen keine echte Datenbank oder einen laufenden Webserver benötigen.

Simulation, Zeit und Zufall müssen injizierbar, steuerbar und reproduzierbar sein. Zufallstests verwenden feste Seeds.

### Integrationstests

Nur für tatsächliches Zusammenspiel, insbesondere:

- REST-Endpunkte,
- Datenbank und Persistenz,
- Laden und Speichern,
- mehrere Servermodule,
- Migrationen.

### Contract-Tests

Requests und Responses müssen gegen den freigegebenen REST-Vertrag geprüft werden. Vertragsabweichungen müssen früh fehlschlagen.

### Langzeittests

Große Galaxien, viele AI-Reiche oder simulierte Monate laufen nicht bei jeder PR, sondern nachts oder manuell.

## 4. Clienttests

### Unit-Tests

Bevorzugt für:

- Stores und Zustandslogik,
- Selektoren,
- Formatierungen,
- Validierungen,
- Mapping von REST-Daten,
- Fehlerbehandlung.

### Komponententests

Für einzelne Ansichten und Komponenten mit kontrollierten Testdaten. Ein echter Server ist dafür normalerweise nicht erforderlich.

### Contract- und Mock-Tests

Der Client entwickelt gegen den freigegebenen REST-Vertrag. Mock-Antworten müssen diesem Vertrag entsprechen.

### Playwright

Playwright ist nur für echte, kritische Nutzerabläufe vorgesehen, zum Beispiel:

- Kampagne öffnen,
- Sternensystem auswählen,
- Flotte auswählen,
- Befehl erteilen,
- sichtbare Bestätigung oder Fehlermeldung prüfen.

Nicht jede CSS-, Text- oder Komponentenänderung benötigt einen E2E-Test.

## 5. Playwright-Regeln für schnelle PRs

Auf Pull Requests gilt standardmäßig:

- nur Chromium,
- nur Desktop-Auflösung,
- kleine, feste Smoke-Suite,
- betroffene Tests, soweit zuverlässig ermittelbar,
- keine vollständige Browsermatrix,
- Screenshots, Traces und Videos nur bei Fehlern.

Firefox, WebKit, weitere Auflösungen und vollständige visuelle Tests laufen nach Merge oder nachts.

Ein neuer E2E-Test ist nur erforderlich, wenn ein neuer kritischer Nutzerablauf entsteht oder ein Fehler nicht sinnvoll auf niedrigerer Teststufe abgesichert werden kann.

## 6. Auswahl nach Änderungstyp

| Änderung | Mindesttests in der PR |
|---|---|
| reine Dokumentation | Link- und Formatprüfung |
| Formatierung oder statischer Text | Linting, betroffene Komponentenprüfung |
| isolierte UI-Komponente | Unit- oder Komponententest |
| Client-Zustandslogik | Unit-Test |
| REST-Nutzung im Client | Unit-/Komponententest und Contract-Test |
| reine Serverberechnung | Unit-Test |
| Serverbefehl oder Zustandswechsel | Unit-Test, bei Bedarf Integrationstest |
| REST-Endpunkt | Unit-/Integrationstest und Contract-Test |
| Persistenz oder Migration | Integrationstest |
| neuer kritischer Gesamtprozess | zusätzlich ein Playwright-Smoke-Test |

Tests dürfen nicht allein anhand des Dateipfads übersprungen werden, wenn die Änderung ein höheres fachliches Risiko besitzt.

## 7. CI-Laufzeit begrenzen

- Alte CI-Läufe desselben PRs werden bei neuem Push abgebrochen.
- Abhängigkeiten und Build-Zwischenergebnisse werden sinnvoll gecacht.
- Unabhängige schnelle Jobs dürfen parallel laufen.
- Teure Tests werden nur durch betroffene Bereiche oder Risikomerkmale aktiviert.
- Ein zentraler Pflicht-Check läuft immer und fasst notwendige Ergebnisse zusammen.
- Sharding wird erst verwendet, wenn die Testlaufzeit den zusätzlichen Startaufwand rechtfertigt.

## 8. Flaky Tests

Ein Test darf nicht dauerhaft durch Retries „grün gerechnet“ werden.

Bei Flakiness muss:

1. der Test als instabil erkannt werden,
2. die Ursache untersucht werden,
3. Zeit-, Zufalls- oder Netzwerkabhängigkeit kontrollierbar gemacht werden,
4. der Test repariert oder vorübergehend klar isoliert werden.

## 9. Pull-Request-Nachweis

Jede PR nennt:

- ausgeführte Tests,
- Ergebnis,
- bewusst nicht ausgeführte Teststufen mit Begründung,
- bekannte Risiken.

Ein Agent darf nicht behaupten, Tests ausgeführt zu haben, wenn dies nicht erfolgt ist.

## 10. Zielzeiten

| Pipeline | Zielzeit |
|---|---:|
| lokale Schnelltests | unter 30 Sekunden |
| Docs-PR | unter 1 Minute |
| kleiner Client-PR | 2–4 Minuten |
| kleiner Server-PR | 2–5 Minuten |
| PR mit Playwright-Smoke | höchstens etwa 5 Minuten |
| vollständiger Main-Lauf | 5–10 Minuten |
| Nacht- und Release-Läufe | Laufzeit nach Umfang |

Wird ein normaler kleiner PR regelmäßig langsamer, muss zuerst die Testauswahl oder CI-Struktur verbessert werden, statt die längere Laufzeit stillschweigend zu akzeptieren.

## 11. Balancing- und Simulationstests

Balancingänderungen benötigen risikobasierte Nachweise gemäß [`balancing/workflow.md`](balancing/workflow.md).

### In jeder betroffenen Pull Request

- Daten- und Schemavalidierung,
- betroffene Formel-, Grenzwert- und Rundungstests,
- deterministische Wiederholung mit festen Seeds,
- Erhaltungstest für Bevölkerung, Güter, Schiffe oder andere konservierte Größen,
- kleine betroffene Referenzszenarien,
- Vorher-/Nachher-Vergleich mit identischen Eingaben,
- Prüfung von Balancingversion, Quellen und Changelog.

### Nach Merge oder nachts

- Coverage-Seeds,
- vollständige Strategieprofile,
- Langzeit- und Offline-Nachholung,
- Verteilungs- und Ausreißerbericht,
- Performance großer Kampagnen,
- Reproduction Seeds bekannter Fehler.

### Release

- alle Golden-, Coverage- und Reproduction-Seeds,
- vollständige Referenzszenariomatrix,
- Exploit- und Dominanzprüfung,
- Savegame-, Migrations- und Hashkompatibilität,
- eingefrorene Balancingversion mit Freigabebericht.

Ein Mittelwert allein reicht nicht. Berichte enthalten mindestens Median, relevante Perzentile, Anteil außerhalb des Zielkorridors und die verwendeten Seeds. Eine Baseline darf nicht als validiert oder releasefähig bezeichnet werden, wenn die in [`balancing/metrics.md`](balancing/metrics.md) geforderten Nachweise fehlen.