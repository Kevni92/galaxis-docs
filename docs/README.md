# Fachliche Dokumentation

Unter `docs/` wird beschrieben, wie Galaxis aus Sicht des Spiels funktioniert.

## Freigabestatus

Der vollständige MVP-Status und die Traceability stehen in [`DOCUMENTATION-STATUS.md`](../DOCUMENTATION-STATUS.md).

## Struktur

| Ordner | Zweck |
|---|---|
| `00-vision/` | Vision, Zielgruppe, Designprinzipien und Nicht-Ziele |
| `01-gameplay/` | Kernloop, Zeitmodell, Spielsitzung und Fortschritt |
| `02-galaxy/` | Galaxie, Systeme, Himmelskörper und Erkundung |
| `03-empires/` | Reiche, Controller, Regierung und Verwaltung |
| `04-planets/` | Planeten, Kolonien, Bezirke und Gebäude |
| `05-population/` | Bevölkerung, Wachstum, Arbeit und Bedürfnisse |
| `06-economy/` | Ressourcen, Produktion, Unterhalt und Handel |
| `07-research/` | Forschung, Technologien und Freischaltungen |
| `08-fleets/` | Schiffe, Flotten, Bewegung und Kampf |
| `09-diplomacy/` | Kontakte, Beziehungen, Verträge und Krieg |
| `10-events/` | Ereignisse, Anomalien, Entscheidungen und Krisen |
| `11-campaign/` | Kampagnenstruktur, Sieg, Niederlage und Endgame |
| `12-ui-ux/` | Game Shell, 3D-Raumansichten, Fenster, Komponenten, Lokalisierung und Begriffskatalog |

## Verbindliche Regeln

- Neue Dokumente folgen [den Dokumentationskonventionen](conventions.md).
- Wiederverwendbare Strukturen liegen unter [`templates/`](../templates/README.md).
- Zentrale Begriffe stehen im [Glossar](../glossary.md).
- Grundlegende Entscheidungen werden unter [`decisions/`](../decisions/README.md) festgehalten.
- Fachliche Verträge werden unter [`contracts/`](../contracts/README.md) abgeleitet.
- Die Raumdarstellung und das UI-Grundmodell folgen [Decision 0007](../decisions/0007-client-ui-rendering-und-lokalisierung.md).
