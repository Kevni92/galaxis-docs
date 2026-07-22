# Server-first Implementierungsroadmap für Galaxis

Status: Verbindliche Implementierungsplanung

Datum: 2026-07-22

Zentrales GitHub-Issue: #114

## 1. Ziel und Vorgehensmodell

Galaxis wird zunächst vom Server aus aufgebaut. Die fachliche Simulation, Persistenz, Berechtigungen, Balancingdaten und REST-Verträge entstehen vor der jeweils dazugehörigen Benutzeroberfläche.

**Server-first bedeutet nicht clientlos.** Jede Alpha liefert einen kleinen vertikalen Schnitt, der über den echten Server bedienbar und als End-to-End-Ablauf testbar ist. Der Client wird zunächst funktional und bewusst schlicht umgesetzt. Visuelle Qualität und Bedienkomfort werden spiralförmig ausgebaut, sobald die zugrunde liegenden Abläufe stabil sind.

Die Reihenfolge innerhalb einer Alpha lautet grundsätzlich:

```text
Fach- und OpenAPI-Vertrag
        ↓
Domainmodell und Zustandsmaschinen
        ↓
Persistenz und Transaktionen
        ↓
Applicationfälle und REST-Adapter
        ↓
Headless-/Integrationsszenario
        ↓
minimaler Clientablauf
        ↓
End-to-End-Demo und Alpha-Gate
```

## 2. Verbindliche Prinzipien

1. Der Server ist für Zustand, Zeit, Wissen, Zufall, Berechtigungen und Validierung autoritativ.
2. Spieler und AI verwenden später dieselben fachlichen Befehle.
3. Domaincode hängt nicht von Fastify, TypeBox, JSON, PostgreSQL, Kysely, Node-I/O oder UI ab.
4. Jede Alpha enthält Persistenz, Fehlerzustände und Tests; diese werden nicht auf einen späteren Aufräummilestone verschoben.
5. OpenAPI wird vor unabhängiger Client-/Serverarbeit konkretisiert.
6. Balancingwerte liegen versioniert und serverseitig vor.
7. Jede Alpha besitzt genau eine sichtbare Abnahmedemo.
8. Eine spätere Alpha darf bereits intern vorbereitete Daten besitzen, diese aber nicht unkontrolliert an den Client freigeben.
9. Keine Alpha beginnt mit einer großen UI-Neugestaltung. Erst der funktionale Schnitt, danach spiralförmige Verbesserung.
10. Änderungen bleiben kleine PRs mit einer klaren Feature-ID.
11. TypeScript-Typen ersetzen keine Laufzeitvalidierung externer Daten.
12. Die gemeinsame Sprache von Client und Server erlaubt keine gemeinsame clientseitige Fachlogik; der Server bleibt die einzige autoritative Wahrheit.

## 3. Repository- und GitHub-Modell

### `galaxis-docs`

Enthält:

- Alpha-Umbrellas und projektübergreifende Abnahmegates,
- Fachquellen und Designentscheidungen,
- OpenAPI-Verträge,
- Balancingziele und Referenzszenarien,
- diese Roadmap.

### `galaxis-server`

Enthält:

- TypeScript-Domain- und Applicationlogik,
- Persistenz,
- Fastify-REST-Adapter,
- Accounts und Sessions,
- Simulation, Zeit und Zufall,
- Balancingdaten und Headless-Szenarien,
- serverseitige Tests.

### `galaxis-client`

Enthält:

- Desktop-Webclient,
- OpenAPI-basierte Typen und REST-Anbindung,
- Ansichten und Interaktionen,
- clientseitige Zustände ohne eigene Spielregeln,
- kritische Playwright-Demos.

### GitHub Projects

Ein GitHub Project kann manuell als Kanban- oder Zeitachsenansicht ergänzt werden. Es ist jedoch nicht die einzige Planungsquelle. Issues, Milestones, Feature-IDs und diese Roadmap bleiben verbindlich und können von ChatGPT und Codex direkt bearbeitet werden.

## 4. Alpha-Übersicht

| Alpha | Sichtbares Ergebnis | Docs-Umbrella | Server-Milestone | Client-Milestone |
|---|---|---:|---:|---:|
| A0 | Registrierung, Login, Session und geschützte Testseite | #115 | `galaxis-server` #1 | `galaxis-client` #1 |
| A1 | Kampagne mit kolonisiertem Heimatplaneten | #116 | `galaxis-server` #2 | `galaxis-client` #2 |
| A2 | Erkundungsschiff bewegt sich im Heimatsternsystem | #117 | `galaxis-server` #3 | `galaxis-client` #3 |
| A3 | Erkundungsschiff deckt ein Nachbarsystem auf | #118 | `galaxis-server` #4 | `galaxis-client` #4 |
| A4 | zweite Kolonie gründen | #119 | `galaxis-server` #5 | `galaxis-client` #5 |
| A5 | Bevölkerung und Beschäftigung steuern | #120 | `galaxis-server` #6 | `galaxis-client` #6 |
| A6 | Gebäude, Güter und Versorgung betreiben | #121 | `galaxis-server` #7 | `galaxis-client` #7 |
| A7 | Technologie erforschen und Freischaltung nutzen | #122 | `galaxis-server` #8 | `galaxis-client` #8 |
| A8 | mehrere Flotten versorgen und reparieren | #123 | `galaxis-server` #9 | `galaxis-client` #9 |
| A9 | anderes Reich entdecken und Erstkontakt erleben | #124 | `galaxis-server` #10 | `galaxis-client` #10 |
| A10 | Vertrag und Handel abschließen | #125 | `galaxis-server` #11 | `galaxis-client` #11 |
| A11 | begrenzten Krieg und Raumkampf abschließen | #126 | `galaxis-server` #12 | `galaxis-client` #12 |
| A12 | Krise, Siegespfad und Kampagnenabschluss | #127 | `galaxis-server` #13 | `galaxis-client` #13 |

---

# 5. A0 – Technisches Fundament

## 5.1 Ziel

Nach einem frischen Checkout können TypeScript-Server, PostgreSQL und Client reproduzierbar gestartet werden. Ein Benutzer kann sich registrieren, anmelden, seine Session prüfen, eine geschützte Clientseite öffnen und sich abmelden.

A0 enthält noch keine Kampagne, kein Reich, keinen Planeten und keine Spielsimulation. Deterministische Provider und Balancing-Loader werden trotzdem bereits angelegt, damit spätere Systeme nicht auf globale Systemzeit oder Zufallsquellen zurückgreifen.

## 5.2 Verbindlicher Serverstack

Maßgeblich ist [Decision 0005](../decisions/0005-a0-server-technologiestack.md).

A0 verwendet:

- Node.js 24 LTS, genaue Patchversion im Repository gepinnt,
- TypeScript strict und ECMAScript Modules,
- pnpm über Corepack,
- Fastify,
- TypeBox an technischen Grenzen,
- Pino,
- PostgreSQL mit `pg` und Kysely,
- versionierte SQL-Migrationen,
- Argon2id über `argon2`,
- Node.js `crypto` für Sessiontokens und Hashes,
- Vitest, Fastify `inject()` und Testcontainers,
- ESLint, Prettier und automatisierte Architekturprüfung.

Der Server wird mindestens gegliedert in:

```text
src/app/composition-root
src/domain
src/application
src/infrastructure
src/transport/http
```

Domaincode verwendet weder `Date.now()`, `new Date()`, `Math.random()`, `crypto.randomUUID()`, Fastify, Kysely noch `process.env` direkt.

Weitere Quellen:

- Clientstack: [Decision 0006](../decisions/0006-alpha-client-technologiestack.md)
- OpenAPI-Arbeit: #128
- lokale Codex-Anleitung: [CODEX-A0.md](CODEX-A0.md)

## 5.3 Bootstrap vor dem ersten Codex-Issue

Im leeren Serverrepository fehlt zunächst das `docs/`-Submodule. Der einzige zulässige Schritt vor dem Lesen der Docs ist:

```bash
git submodule add https://github.com/Kevni92/galaxis-docs.git docs
git submodule update --init --recursive
```

Danach werden `AGENTS.md`, `docs/AGENTS.md`, `docs/WORKFLOW.md`, `docs/TESTING.md`, `docs/SOURCE-CODE.md`, Decision 0005 und diese Roadmap gelesen.

## 5.4 Empfohlene Serverreihenfolge

| Reihenfolge | Issue | Ergebnis |
|---:|---|---|
| 1 | `Kevni92/galaxis-server#1` | TypeScript-/Node-Stack und Architekturgrenzen |
| 2 | `Kevni92/galaxis-server#2` | pnpm-/TypeScript-Repositorybasis und Docs-Submodule |
| 3 | `Kevni92/galaxis-server#8` | injizierbare Zeit-, Zufalls- und ID-Provider |
| 4 | `Kevni92/galaxis-server#3` | Konfiguration, Pino, Health und Shutdown |
| 5 | `Kevni92/galaxis-server#4` | PostgreSQL, Kysely und SQL-Migrationen |
| 6 | `Kevni92/galaxis-server#5` | Fastify-REST-Kern und Fehlerformat |
| 7 | `Kevni92/galaxis-server#9` | Balancing-Manifest, TypeBox-Schema und Hash |
| 8 | `Kevni92/galaxis-server#6` | Account und Registrierung mit Argon2id |
| 9 | `Kevni92/galaxis-server#7` | Bearer-Sessions und Auth-Hook |
| 10 | `Kevni92/galaxis-server#10` | OpenAPI-Contract-Tests |
| 11 | `Kevni92/galaxis-server#11` | lokale Gesamtumgebung und CI-Gate |

Die Reihenfolge ist bewusst nicht strikt nach Issue-Nummer. Deterministische Provider werden früh eingeführt, bevor Infrastruktur oder spätere Domainmodule direkte Systemabhängigkeiten etablieren.

## 5.5 Clientreihenfolge

Der Client beginnt, sobald Health, REST-Fehlerformat und Auth-Vertrag stabil genug sind.

1. `galaxis-client#1` – Vite/Vue-App-Shell
2. `galaxis-client#2` – OpenAPI-Typen und REST-Client
3. `galaxis-client#3` – Session-Store und geschützte Routen
4. `galaxis-client#4` – Registrierung und Login
5. `galaxis-client#5` – Lade-, Fehler- und Verbindungszustände
6. `galaxis-client#6` – A0-End-to-End-Smoke

## 5.6 A0-Abnahmedemo

1. PostgreSQL starten.
2. Migrationen über pnpm-Skript ausführen.
3. TypeScript-Server starten.
4. Client starten.
5. Account registrieren.
6. Mit diesem Account anmelden.
7. Geschützte Sessionseite öffnen.
8. Session serverseitig prüfen.
9. Abmelden.
10. Erneuter Zugriff wird mit definiertem `401` abgewiesen.

## 5.7 A0-Gate

A0 ist abgeschlossen, wenn:

- Docs-Issue #128 abgeschlossen ist,
- Server-Issues #1 bis #11 abgeschlossen sind,
- Client-Issues #1 bis #6 abgeschlossen sind,
- frischer Checkout mit Node/pnpm gemäß README funktioniert,
- Migrationen idempotent laufen,
- Passwörter und Tokens nicht im Klartext gespeichert oder geloggt werden,
- Format, Lint, Typprüfung, Unit-, Integration-, Contract- und E2E-Tests grün sind,
- keine Gameplayregel in A0 eingeführt wurde.

---

# 6. A1 – Heimatplanet

## 6.1 Ziel

Ein neuer Spieler kann eine Singleplayer-Kampagne erstellen. Der Server erzeugt deterministisch eine minimale Galaxie, ein Startreich, ein bekanntes Heimatsystem, einen Heimatplaneten und eine aktive Kolonie mit Startbevölkerung und Grundversorgung. Der Client zeigt diesen Zustand an.

## 6.2 Warum Galaxiegenerierung vor Planetenverwaltung kommt

Der Heimatplanet darf nicht als isolierter Datensatz erzeugt werden. Seine ID, sein Sternsystem, seine Lage, seine Verbindungen und sein Reichswissen gehören zur Galaxiewahrheit. Deshalb wird zuerst eine kleine deterministische Galaxie erzeugt und danach die Startposition daraus ausgewählt.

A1 benötigt noch keine große oder abschließend balancierte Galaxie. Der Generator muss aber bereits dieselben Invarianten verwenden, die A3 für interstellare Erkundung benötigt.

## 6.3 Umsetzung

Docs:

- Umbrella #116
- OpenAPI #129

Server:

1. `galaxis-server#12` – Kampagnen erstellen und auflisten
2. `galaxis-server#13` – minimale Startgalaxie
3. `galaxis-server#14` – Startreich und Controller
4. `galaxis-server#15` – Heimatsystem, Planet und Kolonie
5. `galaxis-server#16` – Startbevölkerung und Grundversorgung
6. `galaxis-server#18` – atomare Persistenz und Reload
7. `galaxis-server#17` – gefilterte A1-REST-Ressourcen
8. `galaxis-server#19` – Referenzszenario und Abnahmetest

Client:

1. `galaxis-client#7` – Kampagnenliste und Erstellung
2. `galaxis-client#8` – Kampagnenzustand und App-Shell
3. `galaxis-client#9` – Heimatsystemansicht
4. `galaxis-client#10` – Planet und Kolonie
5. `galaxis-client#11` – Navigation und Deep Links
6. `galaxis-client#12` – A1-End-to-End-Demo

## 6.4 A1-Gate

- gleicher Seed und gleiche Version ergeben denselben fachlichen Startzustand,
- unbekannte Nachbarsysteme werden nicht geleakt,
- Kampagne, Reich, Galaxie und Kolonie werden atomar persistiert,
- Startwerte stammen aus versionierten Balancingdaten,
- Server-Referenzszenario und Client-E2E sind grün.

---

# 7. A2 – Schiffe und lokales Sternensystem

## 7.1 Ziel

Das Startreich besitzt ein statisch definiertes Erkundungsschiff in einer Flotte. Der Spieler kann das Schiff sehen und innerhalb des Heimatsternsystems zu einem bekannten lokalen Navigationspunkt bewegen.

A2 enthält noch keinen Schiffsbau, keinen Kampf und keine interstellare Erkundung.

## 7.2 Umsetzung

Docs:

- Umbrella #117
- OpenAPI #130

Server:

1. `galaxis-server#20` – MVP-Schiffskatalog
2. `galaxis-server#21` – Ship-/Fleet-Aggregate
3. `galaxis-server#22` – Startflotte
4. `galaxis-server#23` – lokaler Bewegungsbefehl
5. `galaxis-server#24` – deterministische Reise
6. `galaxis-server#25` – REST-Ressourcen
7. `galaxis-server#26` – A2-Szenario

Client:

1. `galaxis-client#13` – lokale SVG-Systemkarte
2. `galaxis-client#14` – Schiff-/Flottenpanel
3. `galaxis-client#15` – Zielwahl und Befehl
4. `galaxis-client#16` – Reisefortschritt
5. `galaxis-client#17` – A2-End-to-End-Demo

## 7.3 A2-Gate

- Flotte besitzt konsistente Mitgliedschaft und Position,
- doppelte Command-ID erzeugt keine Doppelreise,
- Client schließt keine Reise selbst ab,
- normaler und nachgeladener Ablauf sind gleichwertig,
- A2-Headless- und E2E-Szenario sind grün.

---

# 8. A3 – Interstellare Erkundung

## 8.1 Ziel

Das Erkundungsschiff kann über eine bekannte Verbindung zu einem zunächst unbekannten Nachbarsystem reisen. Nach Ankunft startet der Spieler einen Erkundungsauftrag. Beim serverseitigen Abschluss werden zulässige Systeminformationen reichsspezifisch freigegeben.

## 8.2 Umsetzung

Docs:

- Umbrella #118
- OpenAPI #131

Server:

1. `galaxis-server#27` – interstellares Verbindungs- und Routenmodell
2. `galaxis-server#28` – reichsspezifisches Wissen
3. `galaxis-server#29` – interstellarer Reisebefehl
4. `galaxis-server#30` – Erkundungsauftrag und Ergebnis
5. `galaxis-server#31` – Offline-Nachholung und Rückkehrbericht
6. `galaxis-server#32` – Galaxie- und Changes-REST
7. `galaxis-server#33` – A3-Szenario

Client:

1. `galaxis-client#18` – wissensgefilterte Galaxiekarte
2. `galaxis-client#19` – Route und Reisebefehl
3. `galaxis-client#20` – Erkundungsauftrag
4. `galaxis-client#22` – Changes-Synchronisierung
5. `galaxis-client#21` – Ergebnis und Rückkehrübersicht
6. `galaxis-client#23` – A3-End-to-End-Demo

## 8.3 A3-Gate

- interne Wahrheit und Reichswissen sind getrennt,
- unbekannte IDs und Objektzahlen werden nicht übertragen,
- Reise und Erkundung besitzen getrennte idempotente Zustände,
- Galaxie wird bei Erkundung nicht neu ausgewürfelt,
- normale und Offline-Nachholung liefern denselben Endhash,
- A3-Headless- und E2E-Szenario sind grün.

---

# 9. Spätere Alpha-Stufen

Für A4 bis A12 werden zunächst Umbrella-Issues und Milestones geführt. Konkrete Server- und Client-Issues werden jeweils erst detailliert, wenn die vorhergehende Alpha ihr Gate erreicht oder unmittelbar notwendige Verträge vorbereitet werden.

## A4 – Zweite Kolonie

Kolonisierungsmechanismus, Zielprüfung, Auftrag, Aufbauphase und zweite Kolonie in Navigation und Verwaltung.

## A5 – Bevölkerung und Arbeit

Bevölkerungsgruppen, Erwerbspotenzial, Qualifikation, Beschäftigungsprioritäten, natürliche Entwicklung, Migration und Produktivität.

## A6 – Wirtschaft, Gebäude und Versorgung

Güter, Gebäude, Bauaufträge, Produktion, Lager, Reservierung, Bedürfnisse, Mangel, Haushalt, Unterhalt und erste Transporte.

## A7 – Forschung und Technologien

Forschungsleistung, Auswahl, Voraussetzungen, Fortschritt, Abschluss, Freischaltungen, Spezialisierung und Aufholen.

## A8 – Flottenlogistik und Reparatur

Mehrere Flotten, Aufteilen, Zusammenführen, Reichweite, Versorgung, Schäden, Reparatur und Bergung.

## A9 – Andere Reiche und Erstkontakt

Mehrere Reiche, getrennte Controller und Wissensstände, Kontaktentdeckung, Bericht und einfache Beziehung.

## A10 – Diplomatie und Handel

Diplomatische Aktionen, Angebote, Verträge, Handelsbeziehungen, Wirkungen und Vertragsbruch.

## A11 – Konflikt und Raumkampf

Kriegserklärung, Flottenbegegnung, deterministischer Kampf mit kontrolliertem Zufall, Rückzug, Schäden, Verluste und Frieden.

## A12 – Ereignisse, Krise und Kampagnenabschluss

Ereigniszustandsmaschinen, Entscheidungen, Fristen, Krise, Gegenmaßnahmen, Siegespfade und Abschlussbericht.

---

# 10. Balancing-Zuordnung

Balancing-Issues behalten ihre B1–B4-Milestones. Diese Roadmap ordnet sie zusätzlich den Alphas zu.

| Alpha | Unmittelbar relevante Balancing-Issues |
|---|---|
| A0 | #98 Balancing-Manifest/Validator, #100 vollständige Baseline als übergreifendes Ziel |
| A1 | #83 Pacing, #84 Galaxiegröße/Startabstände, #85 Planet/Kolonie, #86 Startbevölkerung, #99 Szenariofixtures |
| A2 | #93 Schiffskosten, #94 Reisezeiten, #99 Fixtures, #101 Headless-Runner-Grundlage |
| A3 | #84 Startabstände, #94 interstellare Reise, #99 Fixtures, #101 Runner, #105 Offline-Äquivalenz |
| A4 | #85 Koloniegründung, #91 Haushalt/Defizit |
| A5 | #86 Bevölkerung/Migration, #87 Beschäftigung, #90 Mangelstufen |
| A6 | #88 Güterkatalog, #89 Produktion/Lager, #90 Versorgung, #91 Haushalt |
| A7 | #92 Forschung und Technologien |
| A8 | #93 Flottenkosten, #94 Logistik, #95 Schäden/Reparatur |
| A9 | #84 Galaxie-/Startverteilung, #96 Beziehungen und Erstkontaktwerte |
| A10 | #96 Diplomatie, Verträge, Krieg und Frieden |
| A11 | #93 bis #96 sowie B2-Simulationswerkzeuge #101 bis #105 |
| A12 | #97 Ereignisse/Krise/Endgame, B2 #101–#105, B3 #106–#109, B4 #110–#113 |

Balancing-Arbeitsweise je Alpha:

1. Nur notwendige Parameter implementieren.
2. Werte als Baseline markieren, nicht als Release behaupten.
3. Referenzfixture parallel zum Domainmodul erstellen.
4. Vorher-/Nachher-Läufe mit identischen Seeds verwenden.
5. Changelog, Version und Hash aktualisieren.
6. Keine Fachregel durch eine Zahl ersetzen oder umgehen.

---

# 11. PR- und Codex-Arbeitsweise

Codex bearbeitet grundsätzlich genau ein konkretes Issue pro Branch.

Empfohlene Branchbenennung:

```text
codex/a0-server-001-stack
codex/a0-server-002-repo
codex/a0-server-008-runtime
```

Vor jedem Issue:

1. `AGENTS.md` lesen.
2. Docs-Submodule aktualisieren.
3. Fachquellen und Entscheidungen aus dem Issue lesen.
4. Abhängigkeiten und offene Vorgänger prüfen.
5. Tests bestimmen.
6. kleinsten sinnvollen PR-Umfang festlegen.

Ein abgeschlossener PR enthält Feature-ID, Quellen, tatsächliche Tests, bekannte Risiken und aktualisierte Navigation. Folgeprobleme erhalten eigene Issues.

# 12. Fortschritts- und Alpha-Gates

Eine Alpha wird nicht allein dadurch abgeschlossen, dass alle Issues geschlossen sind. Das Umbrella-Issue prüft zusätzlich:

- reproduzierbare Demo nach frischem Checkout,
- echte Persistenz und Reload,
- definierte Fehler- und Berechtigungsfälle,
- Contract-Tests,
- Headless-/Integrationsszenario,
- minimalen Client-E2E,
- dokumentierten Balancingstand,
- keine roten bekannten Abweichungen.

Produktive Implementierung der nächsten Alpha beginnt erst, wenn das aktuelle Gate keine grundlegende Architektur- oder Datenmodelländerung mehr erwarten lässt.

# 13. Nächster konkreter Schritt

Der lokale Einstieg ist [CODEX-A0.md](CODEX-A0.md).

Begonnen wird mit:

1. Docs-Submodule bootstrapen.
2. `galaxis-server#1` mit TypeScript/Node.js umsetzen.
3. kleinen Draft-PR erstellen und prüfen.
4. danach `galaxis-server#2`, `#8` und die weitere A0-Reihenfolge abarbeiten.
5. Client A0 beginnen, sobald REST-Kern und Auth-Vertrag stabil sind.
