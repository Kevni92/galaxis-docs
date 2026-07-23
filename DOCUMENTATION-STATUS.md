# Dokumentationsstatus des Galaxis-MVP

Status: Freigegeben

Datum: 2026-07-23

## Bedeutung der Freigabe

Die fachliche Dokumentation des Galaxis-MVP ist vollständig genug, um konkrete Client-, Server-, Test-, OpenAPI- und UI-Arbeit abzuleiten. Die Freigabe bestätigt das fachliche Modell, nicht die Fertigstellung der Software.

Die fachlichen Regeln sind freigegeben. Numerische Werte, Formeln und Zielkorridore besitzen eine erste [Balancing-Baseline v0.1](balancing/README.md). Diese Baseline ist für die erste Implementierung verbindlich, aber noch nicht durch vollständige Simulation oder Playtests validiert.

Die UI-/UX-Grundlage ist mit Decision 0007 und `docs/12-ui-ux/` verbindlich festgelegt. Technische Detailversionen und konkrete Assets bleiben Umsetzungsaufgaben.

## Quellenpriorität

Bei Widersprüchen gilt:

1. angenommene Dateien unter [`decisions/`](decisions/README.md),
2. freigegebene Verträge unter [`contracts/`](contracts/README.md),
3. freigegebene Fachdokumente unter [`docs/`](docs/README.md),
4. freigegebene oder als Baseline gekennzeichnete Werte unter [`balancing/`](balancing/README.md),
5. sonstige Projekttexte,
6. Inhalte unter [`ideas/`](ideas/README.md) besitzen keine fachliche Wirkung.

## Milestone-Matrix

| Milestone | Maßgebliche Ergebnisse | Issues |
|---|---|---|
| D1 – Spielvision und Kernloop | Vision, Zielgruppe, Designprinzipien, Core Loop, Check-in, Zeit, Offline, Controller, Kampagne | #12–#20 |
| D2 – Galaxie und Sternensysteme | [Galaxie](docs/02-galaxy/README.md), Decision 0002 | #21–#25 |
| D3 – Planeten und Kolonien | [Planeten und Kolonien](docs/04-planets/planeten-und-kolonien.md) | #26–#30 |
| D4 – Bevölkerung und Wirtschaft | [Bevölkerung und Arbeit](docs/05-population/bevoelkerung-und-arbeit.md), [Wirtschaft und Versorgung](docs/06-economy/wirtschaft-und-versorgung.md) | #31–#36 |
| D5 – Forschung und Technologien | [Forschung und Technologien](docs/07-research/forschung-und-technologien.md) | #37–#41 |
| D6 – Flotten und Raumkampf | [Flotten und Raumkampf](docs/08-fleets/flotten-und-raumkampf.md) | #42–#47 |
| D7 – Reiche und Diplomatie | [Reichsverwaltung](docs/03-empires/reichsverwaltung.md), [Diplomatie und Krieg](docs/09-diplomacy/diplomatie-und-krieg.md) | #48–#53 |
| D8 – Ereignisse, Krisen und Endgame | [Ereignisse und Krisen](docs/10-events/ereignisse-und-krisen.md), [Endgame und Abschluss](docs/11-campaign/endgame-und-abschluss.md) | #54–#58 |
| D9 – REST-Schnittstellenanforderungen | [Galaxis REST API v1](contracts/rest-api/galaxis-rest-v1.md) | #59–#63 |
| D10 – Dokumentation vollständig | diese Prüf- und Freigabematrix | #64–#68 |
| UI/UX – Raumansichten und Bediengrundlage | [UI und UX](docs/12-ui-ux/README.md), [UI-Verträge](contracts/ui/README.md), Decision 0007 | querschnittlich |

## Vollständigkeitsprüfung

Der MVP beschreibt verbindlich:

- Identität, Zielgruppe und asynchronen Kernloop,
- Kampagnenzeit, Pause, Offline-Fortschritt und Rückkehrberichte,
- deterministische Galaxie, Erkundung, lokale und interstellare Bewegung, Besitz und Kontrolle,
- 3D-Sternensystem- und Galaxiedarstellung bei autoritativer XY- beziehungsweise Graphgeometrie,
- Planeten, modale Planetendetails, Kolonien, Bau und Verwaltung,
- Bevölkerung, Arbeit, Bedürfnisse, Güter, Produktion, Transport und Haushalt,
- Forschung, Technologieeffekte, Spezialisierung und Transfer,
- Schiffe, Flotten, freie lokale Zielpunkte, Kontextaktionen, Versorgung, Kampf, Schäden und Reparatur,
- Reiche, Controller, Beziehungen, Verträge, Krieg und Frieden,
- Ereignisse, Anomalien, Krisen, Endgame, Sieg und Niederlage,
- Game Shell, Fenster, Tabs, Shortcuts, Komponenten, Lokalisierung und Begriffskatalog,
- REST-Ressourcen, Zugriff, Zustandsabfragen, Kontextaktionen, Befehle, Fehler und Synchronisation.

## Widerspruchsprüfung

Die zentralen Invarianten sind konsistent:

- Der Server ist für Zeit, Zustand, Wissen, Zufall, Positionen, Kontextaktionen und Validierung autoritativ.
- Spieler und AI verwenden dieselben fachlichen Befehle.
- Der Client schließt keine Vorgänge selbstständig ab.
- Die 3D-Darstellung erzeugt keine eigene Physik oder Regelbasis.
- Fachliche lokale Bewegung verwendet ausschließlich serverseitige XY-Koordinaten.
- Physische Güter, Bevölkerung, Flotten und Anlagen bleiben standortgebunden.
- Wissen wird je Reich gefiltert; interne Wahrheit wird nicht an Client oder AI gegeben.
- Unbekannte Objekte werden nicht durch Rendering, Picking oder Kontextaktionen geleakt.
- Zustandsmaschinen und Offline-Nachholung müssen deterministisch und idempotent sein.
- Militärische Kontrolle, Besetzung und souveräner Besitz bleiben getrennt.
- Ereignisse, Diplomatie und REST-Befehle umgehen keine Fachvalidierung.
- Himmelskörperdetails werden modal dargestellt und ersetzen nicht die räumliche Arbeitsfläche.

Es wurden keine blockierenden Widersprüche zwischen den freigegebenen Dokumenten festgestellt. Decision 0006 ist ausdrücklich durch Decision 0007 ersetzt.

## Offene Fragen

Offene Abschnitte und Folgearbeiten betreffen überwiegend:

- empirische Validierung und Feintuning der Balancing-Baseline,
- konkrete produktive Kataloge von Gütern, Gebäuden, Technologien, Schiffen und Ereignissen,
- genaue lokale Systemgrößen, Bewegungsauflösung und Reichweitenwerte,
- konkrete 3D-Assets, Materialfamilien und Performancebudgets,
- genaue OpenAPI-Dateiaufteilung,
- spätere Erweiterungen außerhalb des MVP.

Diese Fragen ändern nicht das verbindliche Grundmodell. Jede Umsetzung muss Werte, Kataloge und technische Entscheidungen in eigenen Issues dokumentieren und gegen die freigegebenen Akzeptanzkriterien testen.

## Balancingstatus

Der Balancingbereich definiert:

- systemweite Pacing- und Stabilitätsziele,
- Formeln, Einheiten und Rundungsregeln,
- Fachbereichsbaselines,
- Messgrößen und Qualitätsgrenzen,
- ein versioniertes Datenformat,
- Referenzszenarien S01 bis S05,
- die Roadmap B1 bis B4.

Aktueller Status: **Baseline v0.1**. Noch offen sind produktive Datenkataloge und Serverdaten, automatisierte Simulation, Playtestvalidierung und Release-Freeze.

## Ableitbarkeit für Client

Aus den Dokumenten lassen sich mindestens folgende Clientbereiche ableiten:

- Kampagnen- und Rückkehrübersicht,
- permanente Game Shell mit Topbar, Zugriffsmenü und Outliner,
- 3D-Sternensystemansicht mit wissensgefilterten Himmelskörpern,
- 3D-Galaxieansicht mit Wissensständen und Graphverbindungen,
- modale Planet-, Kolonie-, Flotten- und Fachfenster,
- Flottenauswahl, freie XY-Zielpunkte, Objekt-Kontextaktionen, Reise und Kampfberichte,
- Kolonie-, Bevölkerungs-, Wirtschafts- und Forschungsansichten,
- Diplomatie, Verträge, Krieg und Frieden,
- Ereignisentscheidungen, Krisen- und Endgame-Übersichten,
- einheitliche Komponenten, Tabellen, Lade-, Konflikt- und Fehlerzustände,
- YAML-Lokalisierung und rekursive Begriffserklärungen.

## Ableitbarkeit für Server

Der Server kann in klar getrennte Domänen und Zustandsmaschinen aufgeteilt werden:

- Campaign/Time,
- Galaxy/Knowledge/LocalSpace,
- Empire/Controller,
- Planet/Colony,
- Population/Employment,
- Economy/Transport/Budget,
- Research,
- Fleet/Movement/Combat,
- Diplomacy/War,
- Events/Crisis/Endgame,
- REST/ContextAction/Command/ChangeLog.

Alle Zustandsänderungen sind über fachliche Befehle, Voraussetzungen, Zeitpunkte und Ergebnisse ableitbar.

## Ableitbarkeit für Tests

Verbindliche Testinvarianten sind mindestens:

- gleiche Ausgangslage und Eingaben ergeben dasselbe Ergebnis,
- Güter und Bevölkerung werden nicht durch Rundung oder Wiederholung erzeugt,
- unbekannte Informationen gelangen nicht an unberechtigte Reiche,
- Befehle sind idempotent und werden bei Wiederholung nicht doppelt ausgeführt,
- Offline-Nachholung entspricht regulärer Zeitverarbeitung,
- Controllerwechsel verändert keine laufenden Befehle oder Wissensstände,
- Besitz und Kontrolle wechseln nur durch erlaubte Operationen,
- Ereignisfolgen und Friedensschlüsse werden atomar angewandt,
- REST-Konflikte und Fehler liefern keine Informationslecks,
- 3D-Transformationen verändern keine fachlichen Positionen oder Reichweiten,
- Maus und Tastatur lösen dieselben fachlichen Aktionen aus,
- Planetendetails öffnen im gemeinsamen modalen Fenstersystem,
- Kontextaktionen werden vor Ausführung serverseitig erneut validiert.

## REST-, UI- und MVP-Freigabe

Der REST-Vertrag ist vollständig genug, um OpenAPI-v1-Spezifikationen und Contract-Tests für lokale Raumobjekte, Kontextaktionen und Bewegungsbefehle zu erstellen.

Die UI-Verträge sind vollständig genug, um Game Shell, 3D-Raumansichten, modale Details, Tastaturäquivalenz, Sprachdateien und Begriffspopovers in Client-Issues zu schneiden.

Konkrete Payload-Schemas müssen auf statische Datenkataloge der Implementierung verweisen, dürfen aber keine neue Fachlogik einführen.

Damit ist die fachliche Dokumentation des Galaxis-MVP einschließlich UI-/UX-Grundmodell freigegeben.
