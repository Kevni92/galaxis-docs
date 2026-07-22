# Dokumentationsstatus des Galaxis-MVP

Status: Freigegeben

Datum: 2026-07-22

## Bedeutung der Freigabe

Die fachliche Dokumentation des Galaxis-MVP ist vollständig genug, um konkrete Client-, Server-, Test- und OpenAPI-Arbeit abzuleiten. Die Freigabe bestätigt das fachliche Modell, nicht die Fertigstellung der Software.

Numerische Balancingwerte, konkrete Inhaltskataloge und technische Bibliotheksentscheidungen bleiben Umsetzungsaufgaben. Sie dürfen die hier festgelegten Zustände, Verantwortlichkeiten und Invarianten nicht stillschweigend verändern.

## Quellenpriorität

Bei Widersprüchen gilt:

1. angenommene Dateien unter [`decisions/`](decisions/README.md),
2. freigegebene Verträge unter [`contracts/`](contracts/README.md),
3. freigegebene Fachdokumente unter [`docs/`](docs/README.md),
4. sonstige Projekttexte,
5. Inhalte unter [`ideas/`](ideas/README.md) besitzen keine fachliche Wirkung.

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

## Vollständigkeitsprüfung

Der MVP beschreibt verbindlich:

- Identität, Zielgruppe und asynchronen Kernloop,
- Kampagnenzeit, Pause, Offline-Fortschritt und Rückkehrberichte,
- deterministische Galaxie, Erkundung, Bewegung, Besitz und Kontrolle,
- Planeten, Kolonien, Bau und Verwaltung,
- Bevölkerung, Arbeit, Bedürfnisse, Güter, Produktion, Transport und Haushalt,
- Forschung, Technologieeffekte, Spezialisierung und Transfer,
- Schiffe, Flotten, Befehle, Versorgung, Kampf, Schäden und Reparatur,
- Reiche, Controller, Beziehungen, Verträge, Krieg und Frieden,
- Ereignisse, Anomalien, Krisen, Endgame, Sieg und Niederlage,
- REST-Ressourcen, Zugriff, Zustandsabfragen, Befehle, Fehler und Synchronisation.

## Widerspruchsprüfung

Die zentralen Invarianten sind konsistent:

- Der Server ist für Zeit, Zustand, Wissen, Zufall und Validierung autoritativ.
- Spieler und AI verwenden dieselben fachlichen Befehle.
- Der Client schließt keine Vorgänge selbstständig ab.
- Physische Güter, Bevölkerung, Flotten und Anlagen bleiben standortgebunden.
- Wissen wird je Reich gefiltert; interne Wahrheit wird nicht an Client oder AI gegeben.
- Zustandsmaschinen und Offline-Nachholung müssen deterministisch und idempotent sein.
- Militärische Kontrolle, Besetzung und souveräner Besitz bleiben getrennt.
- Ereignisse, Diplomatie und REST-Befehle umgehen keine Fachvalidierung.

Es wurden keine blockierenden Widersprüche zwischen den freigegebenen Dokumenten festgestellt.

## Offene Fragen

Offene Abschnitte in Fachdokumenten betreffen überwiegend:

- numerische Balancingwerte,
- konkrete Kataloge von Gütern, Gebäuden, Technologien, Schiffen und Ereignissen,
- technische Algorithmen und Bibliotheken,
- genaue OpenAPI-Dateiaufteilung,
- spätere Erweiterungen außerhalb des MVP.

Diese Fragen sind keine offenen Grundsatzentscheidungen. Jede Umsetzung muss Werte und Kataloge in eigenen Issues dokumentieren und gegen die freigegebenen Akzeptanzkriterien testen.

## Ableitbarkeit für Client

Aus den Dokumenten lassen sich mindestens folgende Clientbereiche ableiten:

- Kampagnen- und Rückkehrübersicht,
- Galaxiekarte mit Wissensständen und Routen,
- Kolonie-, Bevölkerungs-, Wirtschafts- und Forschungsansichten,
- Flottenverwaltung, Reise und Kampfberichte,
- Diplomatie, Verträge, Krieg und Frieden,
- Ereignisentscheidungen, Krisen- und Endgame-Übersichten,
- einheitliche Lade-, Konflikt- und Fehlerzustände der REST-Kommunikation.

## Ableitbarkeit für Server

Der Server kann in klar getrennte Domänen und Zustandsmaschinen aufgeteilt werden:

- Campaign/Time,
- Galaxy/Knowledge,
- Empire/Controller,
- Planet/Colony,
- Population/Employment,
- Economy/Transport/Budget,
- Research,
- Fleet/Combat,
- Diplomacy/War,
- Events/Crisis/Endgame,
- REST/Command/ChangeLog.

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
- REST-Konflikte und Fehler liefern keine Informationslecks.

## REST- und MVP-Freigabe

Der REST-Vertrag ist vollständig genug, um eine OpenAPI-v1-Spezifikation und Contract-Tests zu erstellen. Konkrete Payload-Schemas müssen auf die statischen Datenkataloge der Implementierung verweisen, dürfen aber keine neue Fachlogik einführen.

Damit ist die fachliche Dokumentation des Galaxis-MVP freigegeben.
