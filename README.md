# Galaxis – Fachliche Dokumentation

Dieses Repository ist die verbindliche fachliche Quelle für das Spiel **Galaxis**.

Hier wird beschrieben, **wie das Spiel funktioniert**: Spielregeln, Entitäten, Befehle, Zustände, Wechselwirkungen und fachliche Anforderungen. Konkreter Client- oder Servercode gehört nicht in dieses Repository.

## Ziel der Dokumentation

Die Dokumentation soll:

- alle Spielmechaniken eindeutig und widerspruchsfrei beschreiben,
- als Grundlage für Issues in `galaxis-client` und `galaxis-server` dienen,
- von Menschen, Claude und Codex schnell verstanden werden,
- die spätere REST-Schnittstelle fachlich vorbereiten,
- Entscheidungen langfristig nachvollziehbar machen.

## Einstieg

- [Arbeitsregeln für KI-Agenten](AGENTS.md)
- [Dokumentationsübersicht](docs/README.md)
- [Dokumentationskonventionen](docs/conventions.md)
- [Glossar](glossary.md)
- [Fachliche Verträge](contracts/README.md)
- [Designentscheidungen](decisions/README.md)
- [Vorlagen](templates/README.md)

## Themenbereiche

| Bereich | Inhalt |
|---|---|
| [Vision](docs/00-vision/README.md) | Spielvision, Zielgruppe, Designprinzipien und Nicht-Ziele |
| [Gameplay](docs/01-gameplay/README.md) | Kernloop, Sitzungsablauf, Zeitmodell und Fortschritt |
| [Galaxie](docs/02-galaxy/README.md) | Galaxie, Sternensysteme, Himmelskörper und Erkundung |
| [Reiche](docs/03-empires/README.md) | Reiche, Regierung, Controller und Reichsverwaltung |
| [Planeten](docs/04-planets/README.md) | Planeten, Kolonien, Bezirke, Gebäude und Entwicklung |
| [Bevölkerung](docs/05-population/README.md) | Bevölkerung, Wachstum, Arbeit und Bedürfnisse |
| [Wirtschaft](docs/06-economy/README.md) | Ressourcen, Produktion, Handel und Unterhalt |
| [Forschung](docs/07-research/README.md) | Technologien, Forschungsauswahl und Freischaltungen |
| [Flotten](docs/08-fleets/README.md) | Schiffe, Flotten, Befehle, Bewegung und Kampf |
| [Diplomatie](docs/09-diplomacy/README.md) | Kontakte, Beziehungen, Verträge und Konflikte |
| [Ereignisse](docs/10-events/README.md) | Ereignisse, Anomalien, Entscheidungen und Krisen |
| [Kampagne](docs/11-campaign/README.md) | Kampagnenziele, Sieg, Niederlage und Endgame |

## Quellenpriorität

Bei Widersprüchen gilt folgende Reihenfolge:

1. angenommene Designentscheidung unter `decisions/`,
2. freigegebenes Fachdokument unter `docs/`,
3. freigegebener Vertrag unter `contracts/`,
4. Entwurf,
5. Issue oder Diskussion.

Widersprüche dürfen nicht stillschweigend aufgelöst werden. Sie müssen dokumentiert und als offene Entscheidung behandelt werden.
