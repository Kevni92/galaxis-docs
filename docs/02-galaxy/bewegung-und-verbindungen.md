# Bewegung und räumliche Verbindungen

Status: Review

## Zweck

Dieses Dokument definiert die fachliche Grundlage für interstellare Bewegung und Routenplanung. Schiffsarten, Reichweiten und Kampfregeln werden in D6 konkretisiert.

## Grundmodell

Reguläre interstellare Bewegung erfolgt ausschließlich über bekannte und nutzbare Verbindungen zwischen Sternensystemen. Eine Route ist eine geordnete Folge solcher Verbindungen. Kartenkoordinaten bestimmen nicht allein die Erreichbarkeit.

## Verbindung

Jede Verbindung besitzt stabile ID, Endsysteme, Richtung, Grunddistanz oder Reisefaktor, Typ, reichsspezifischen Entdeckungsstand und aktuellen Nutzbarkeitszustand. Selbstverbindungen und ungültige Endpunkte sind unzulässig.

Das MVP benötigt mindestens einen regulären Verbindungstyp. Weitere Typen müssen Entdeckung, Nutzung, Reiseauswirkung und Sichtbarkeit ausdrücklich definieren.

## Nutzbarkeit

Eine Verbindung ist nutzbar, wenn sie bekannt und existent ist, die bewegte Entität alle Anforderungen erfüllt, der aktuelle Zustand die Nutzung erlaubt und Zugang, Diplomatie oder territoriale Regeln den Übergang nicht verbieten.

## Bewegungsbefehl

Ein Bewegungsbefehl enthält bewegte Entität, Ausgang, Ziel, Route oder serverseitige Routenauswahl, Annahmezeitpunkt und Status. Der Server prüft Controllerberechtigung, Standort, Verbindungen, Fähigkeiten, Route und Konflikte mit laufenden Befehlen.

## Routenwahl

Bestimmt der Server die Route, verwendet er eine dokumentierte Kostenfunktion aus Reisezeit, Gefahren, Zugangsrechten, Einschränkungen und Prioritäten. Bei Gleichstand gilt ein stabiler Tie-Breaker. Gleiche Eingaben müssen dieselbe Route ergeben.

## Reisezeit und Zustand

Jeder Abschnitt besitzt Start- und Zielzeitpunkt in Kampagnenzeit. Währenddessen ist die Flotte `unterwegs` und weder frei im Ausgangs- noch vollständig im Zielsystem verfügbar. Gespeichert werden Verbindung, Abfahrt, Ankunft und verbleibende Route.

## Änderungen nach Abfahrt

Ein bereits begonnener Abschnitt wird grundsätzlich nach den bei Start gültigen Regeln abgeschlossen. Noch nicht begonnene Folgeabschnitte werden vor ihrem Start neu geprüft. Wird die Route ungültig, wartet die Flotte im nächsten erreichten System oder verwendet eine ausdrücklich erlaubte Neuplanung.

## Abbruch und Umleitung

Eine laufende Teilstrecke wird nicht rückwirkend aufgehoben. Umleitung wirkt frühestens am nächsten fachlich zulässigen Entscheidungspunkt. Bereits entstandene Kosten und Risiken bleiben bestehen.

## Blockaden und unzugängliche Räume

Blockaden löschen keine Verbindung aus dem Graphen. Sie können Nutzung, Kampf, Risiko oder Routenempfehlung beeinflussen; Details folgen in D6. Der Client unterscheidet unbekannt, nicht erreichbar und derzeit gesperrt, soweit die Ursache bekannt ist.

## Sichtbarkeit und Offline-Fortschritt

Reisen werden nur bei ausreichender Sensorik sichtbar. Details können von bloßer Signatur bis zu Ziel und Ankunftszeit reichen. Bewegungen laufen während geschlossener Clients weiter. Offline-Nachholung verarbeitet Abschnitte und Ereignisse in stabiler Reihenfolge.

## Anforderungen an Client und Server

Der Client stellt bekannte, nutzbare und gesperrte Wege sowie serverbestätigte Routen und Zeiten dar. Der Server validiert Graph, Route und Befehl, speichert Reiseabschnitte und wertet Offline-Fortschritt deterministisch aus.

## Offene Folgefragen

1. Welche Verbindungstypen gehören zum MVP?
2. Welche Reichweiten-, Treibstoff- oder Versorgungssysteme gelten in D6?
3. Wie wirken Blockaden, Abfangen und Gefahren?
4. Welche lokalen Bewegungen innerhalb eines Systems benötigen Zeit?

## Akzeptanzkriterien

- Reguläre Bewegung ist an bekannte Graphverbindungen gebunden.
- Routenwahl und Tie-Breaker sind deterministisch.
- Begonnene und zukünftige Abschnitte sind getrennt geregelt.
- Offline-Fortschritt und Fog of War werden berücksichtigt.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Besitz und Kontrolle](besitz-und-kontrolle.md)
- [Flotten – Übersicht](../08-fleets/README.md)
