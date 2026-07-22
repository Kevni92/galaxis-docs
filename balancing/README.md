# Balancing

Status: Baseline v0.1

Dieser Ordner enthält die numerischen Zielwerte, Parameterkorridore, Formeln, Referenzszenarien und Messgrößen für **Galaxis**.

Balancing ist verbindlich für die jeweils gekennzeichnete Entwicklungsstufe, steht aber unter den fachlichen Regeln. Es darf verändern, **wie schnell**, **wie stark**, **wie häufig** oder **wie teuer** etwas ist. Es darf nicht verändern, **was** eine Entität, ein Zustand oder ein Befehl fachlich bedeutet.

## Abgrenzung

Balancing darf beispielsweise festlegen:

- Bau-, Reise-, Forschungs- und Reparaturdauer,
- Kosten, Erträge, Kapazitäten und Unterhalt,
- Wachstums-, Schadens- und Wahrscheinlichkeitswerte,
- Reaktionsfenster, Abklingzeiten und Grenzwerte,
- Zielkorridore für Kampagnenverlauf und strategische Vielfalt.

Balancing darf nicht:

- neue Spielregeln einführen,
- Berechtigungen oder Informationsgrenzen umgehen,
- Spieler und AI unterschiedlichen Regeln unterwerfen,
- serverautoritative Validierung ersetzen,
- Zustände oder Befehle umdeuten,
- Inhalte unter `ideas/` als beschlossen behandeln.

## Quellenrang

Bei einem Widerspruch gilt:

1. angenommene Designentscheidungen unter [`decisions/`](../decisions/README.md),
2. freigegebene Verträge unter [`contracts/`](../contracts/README.md),
3. freigegebene Fachregeln unter [`docs/`](../docs/README.md),
4. freigegebene oder als Baseline gekennzeichnete Werte unter `balancing/`,
5. sonstige Projekttexte,
6. Inhalte unter [`ideas/`](../ideas/README.md) besitzen keine fachliche Wirkung.

Ein Balancingwert, der einer höher priorisierten Quelle widerspricht, ist ungültig und muss korrigiert werden.

## Statusstufen

Jedes Balancingdokument oder jeder Datensatz verwendet eine dieser Stufen:

- **Entwurf:** noch nicht für Implementierung oder Vergleichstests verbindlich.
- **Baseline:** Startwert für Implementierung, Simulation und erste Playtests.
- **Validiert:** anhand definierter Szenarien und Messgrößen geprüft.
- **Release:** für einen konkreten Release-Kandidaten eingefroren.
- **Ersetzt:** nicht mehr verwenden; Nachfolger muss verlinkt sein.

`Baseline` bedeutet nicht „endgültig“. Eine Baseline darf gezielt geändert werden, benötigt aber Ziel, Messung und Änderungsnachweis.

## Dokumente

- [Systemweite Baseline-Ziele](baseline.md)
- [Formeln, Einheiten und Rundung](formulas-and-units.md)
- [Messgrößen und Qualitätsgrenzen](metrics.md)
- [Balancing-Datenformat](data-format.md)
- [Änderungs- und Freigabeworkflow](workflow.md)
- [Balancing-Roadmap](ROADMAP.md)
- [Änderungsprotokoll](CHANGELOG.md)
- [Referenzszenarien](scenarios/README.md)

## Fachbereiche

- [Kampagne und Pacing](domains/campaign-pacing.md)
- [Planeten und Kolonien](domains/planets-and-colonies.md)
- [Bevölkerung und Beschäftigung](domains/population-and-employment.md)
- [Wirtschaft und Versorgung](domains/economy-and-supply.md)
- [Forschung und Technologien](domains/research.md)
- [Flotten, Reisen und Raumkampf](domains/fleets-travel-and-combat.md)
- [Diplomatie, Ereignisse und Endgame](domains/diplomacy-events-and-endgame.md)

## Grundregeln

1. Erst Ziel und Messgröße, dann Zahl.
2. Formeln werden vor Einzelwerten stabilisiert.
3. Werte besitzen Einheit, Wertebereich und Herkunft.
4. Änderungen nennen Ausgangswert, neuen Wert und erwartete Wirkung.
5. Konservierte Größen dürfen durch Rundung weder erzeugt noch vernichtet werden.
6. Simulationsergebnisse werden mit Seed, Balancingversion und Szenarioversion gespeichert.
7. Eine einzelne Kennzahl darf nicht allein über Freigabe entscheiden.
8. Strategische Vielfalt ist wichtiger als mathematische Symmetrie.
9. Häufigeres Einloggen darf keinen reinen Anwesenheitsvorteil erzeugen.
10. Live- oder Telemetriedaten dürfen die Privatsphäre von Spielern nicht verletzen.

## Verantwortlichkeit

Das Docs-Repository definiert Ziele, Baselines und Freigabekriterien. Der Server implementiert und validiert die autoritativen Werte. Der Client stellt nur freigegebene, für Entscheidungen benötigte Werte und Prognosen dar.

Produktive Balancingdaten sollen später maschinenlesbar im Server-Repository liegen. Jede solche Datei verweist auf die zugehörige Quelle unter `balancing/` und besitzt eine explizite Balancingversion.