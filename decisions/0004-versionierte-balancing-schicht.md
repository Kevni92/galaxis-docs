# 0004 – Versionierte Balancing-Schicht

Status: angenommen

Datum: 2026-07-22

## Kontext

Die freigegebenen Fachregeln des Galaxis-MVP definieren Entitäten, Zustände, Befehle, Verantwortlichkeiten und Invarianten. Für die Implementierung werden zusätzlich zahlreiche veränderliche Zahlen, Kurven, Wahrscheinlichkeiten, Katalogwerte und Pacingziele benötigt.

Werden diese Werte direkt in Fachtexte oder Quellcode eingemischt, entstehen widersprüchliche Quellen, schwer messbare Änderungen und problematische Savegame- oder Replayabweichungen.

## Entscheidung

Galaxis erhält eine eigenständige, versionierte Balancing-Schicht unter [`balancing/`](../balancing/README.md).

Es gilt:

1. Balancing steht unter Entscheidungen, Verträgen und Fachregeln.
2. Balancing darf Intensität, Dauer, Häufigkeit, Kosten und Grenzwerte ändern, aber keine Fachregel umdeuten.
3. Jede produktive Balancingkonfiguration besitzt Version und kanonischen Hash.
4. Kampagnen speichern ihre Balancing- und Katalogversion.
5. Laufende Kampagnen wechseln nicht unbemerkt auf neue Werte.
6. Produktive Werte liegen maschinenlesbar und serverautoritativ vor.
7. Der Client erhält nur darstellungs- und entscheidungsrelevante Werte.
8. Änderungen verwenden Zielmetriken, Referenzszenarien und Vorher-/Nachher-Vergleiche.
9. Statusstufen sind Entwurf, Baseline, Validiert, Release und Ersetzt.
10. Numerische Baselines dürfen geändert werden, ohne die Fachregel neu freizugeben, solange Bedeutung und Invarianten unverändert bleiben.

## Begründung

Balancingwerte ändern sich während Implementierung, Simulation und Playtests deutlich häufiger als Fachregeln. Eine getrennte Schicht ermöglicht schnelle, messbare Anpassung, ohne die fachliche Wahrheit zu verwässern.

Version und Hash machen Ergebnisse reproduzierbar. Die Speicherung je Kampagne verhindert, dass ein Wertupdate bestehende Spielstände stillschweigend verändert oder Replays unbrauchbar macht.

## Betrachtete Alternativen

### Werte direkt in Fachdokumenten

Vorteil: wenige Ordner und unmittelbarer Kontext.

Nachteile:

- häufige Zahlenänderungen erzeugen Rauschen in stabilen Fachquellen,
- Status und Beweisniveau sind schwer erkennbar,
- Implementierungsdaten bleiben trotzdem separat,
- unterschiedliche Kampagnenversionen sind schlecht abbildbar.

### Werte ausschließlich im Servercode

Vorteil: schnelle technische Umsetzung.

Nachteile:

- keine gemeinsame nachvollziehbare Quelle,
- Änderungen ohne Ziel oder Messnachweis,
- hoher Aufwand für Anpassung und Review,
- Gefahr widersprüchlicher Clientprognosen,
- schlechte Savegame- und Replaynachvollziehbarkeit.

### Externe Tabellen ohne Repositoryversionierung

Vorteil: einfache Bearbeitung für Designer.

Nachteile:

- schwer mit Code, Issues und Tests zu verknüpfen,
- unklare Historie und Freigabe,
- fehlende deterministische Zuordnung zu Builds,
- Risiko manueller Übertragungsfehler.

Eine spätere Tabellenoberfläche ist zulässig, wenn das versionierte Repositoryformat die autoritative Ausgabe bleibt.

## Positive Folgen

- klare Trennung zwischen Regel und Zahl,
- messbare Balancingänderungen,
- reproduzierbare Simulationen,
- belastbare Savegame- und Replayzuordnung,
- einfachere Automatisierung und Validierung,
- nachvollziehbare Release-Freigaben,
- gemeinsame Quelle für Server, Clientdarstellung und Tests.

## Negative Folgen und Risiken

- zusätzlicher Versions- und Validierungsaufwand,
- Datenmigrationen werden erforderlich,
- zu viele Parameter können Wechselwirkungen unübersichtlich machen,
- eine formale Datenstruktur kann falsche Sicherheit erzeugen, wenn Szenarien und Metriken fehlen,
- Balancing- und Fachänderungen müssen im Review sauber getrennt werden.

## Betroffene Dokumente

- [`balancing/README.md`](../balancing/README.md)
- [`balancing/data-format.md`](../balancing/data-format.md)
- [`balancing/workflow.md`](../balancing/workflow.md)
- [`balancing/metrics.md`](../balancing/metrics.md)
- [`WORKFLOW.md`](../WORKFLOW.md)
- [`TESTING.md`](../TESTING.md)
- [`DOCUMENTATION-STATUS.md`](../DOCUMENTATION-STATUS.md)

## Ersetzt

keine

## Ersetzt durch

keine