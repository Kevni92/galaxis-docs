# Bewegung und räumliche Verbindungen

Status: Freigegeben

## Zweck

Dieses Dokument definiert die fachliche Grundlage für lokale Bewegung innerhalb eines Sternensystems sowie interstellare Bewegung und Routenplanung. Schiffsarten, Reichweiten, Haltungen und Kampfregeln werden in D6 konkretisiert.

## Räumliche Ebenen

Galaxis unterscheidet zwei fachliche Bewegungsebenen:

1. **lokale Systemebene:** autoritative zweidimensionale XY-Positionen innerhalb eines Sternensystems,
2. **interstellare Galaxieebene:** bekannte und nutzbare Verbindungen zwischen Sternensystemen.

Die 3D-Darstellung beider Ebenen ist eine Clientvisualisierung. Visuelle Höhe, Kameraperspektive und Meshgröße beeinflussen keine Route oder Reisezeit.

## Lokale Bewegung

Eine Flotte innerhalb eines Systems besitzt eine autoritative lokale Position. Ein lokaler Bewegungsbefehl kann adressieren:

- einen freien gültigen XY-Zielpunkt,
- einen bekannten lokalen Navigationsanker,
- einen fachlich definierten Anker eines bekannten Objekts, beispielsweise Orbit, Station oder Verbindungsausgang.

Der Befehl enthält mindestens bewegte Flotte, Ausgangssystem, Ziel, Annahmezeitpunkt und Status. Der Server prüft Controllerberechtigung, Standort, Bewegungsfähigkeit, Systemgrenzen, Zielwissen, laufende Befehle, Reichweite und bekannte Sperren.

## Bedienabbildung für lokale Bewegung

Bei ausgewählter Flotte kann der Client:

- über eine Sekundäraktion auf freien Raum einen XY-Zielvorschlag erzeugen,
- über eine Sekundäraktion auf ein Objekt zulässige Kontextaktionen abfragen,
- über eine modifizierte Aktion einen Folgeauftrag an die Warteschlange anhängen.

Diese Bedienung erzeugt zunächst nur einen Vorschlag. Die Flotte bewegt sich fachlich erst nach Annahme des serverautoritativen Befehls.

Eine zugängliche alternative Zielauswahl muss dieselben Ziele ohne präzise Mausbedienung anbieten.

## Lokale Route und Reisezeit

Der Server bestimmt für einen lokalen Bewegungsbefehl:

- verbindlichen Startpunkt,
- verbindlichen Zielpunkt,
- Route oder Bewegungssegment,
- Startzeit,
- Geschwindigkeit,
- erwartete Ankunft,
- Status und mögliche Unterbrechungsregeln.

Der Client darf zwischen bestätigten Positionen interpolieren. Diese Interpolation schließt keine Reise ab und darf bei neuer Serverantwort korrigiert werden.

## Reguläre interstellare Bewegung

Interstellare Bewegung erfolgt ausschließlich über bekannte und nutzbare Verbindungen zwischen Sternensystemen. Eine Route ist eine geordnete Folge solcher Verbindungen. Galaxiekoordinaten und sichtbare 3D-Abstände bestimmen nicht allein die Erreichbarkeit.

## Verbindung

Jede Verbindung besitzt stabile ID, Endsysteme, Richtung, Grunddistanz oder Reisefaktor, Typ, reichsspezifischen Entdeckungsstand und aktuellen Nutzbarkeitszustand. Selbstverbindungen und ungültige Endpunkte sind unzulässig.

Das MVP benötigt mindestens einen regulären Verbindungstyp. Weitere Typen müssen Entdeckung, Nutzung, Reiseauswirkung und Sichtbarkeit ausdrücklich definieren.

## Nutzbarkeit

Eine Verbindung ist nutzbar, wenn:

- sie bekannt und existent ist,
- die bewegte Entität alle Anforderungen erfüllt,
- der aktuelle Zustand die Nutzung erlaubt,
- Zugang, Diplomatie oder territoriale Regeln den Übergang nicht verbieten.

## Interstellarer Bewegungsbefehl

Ein interstellarer Bewegungsbefehl enthält bewegte Entität, Ausgangssystem, Zielsystem, Route oder serverseitige Routenauswahl, Annahmezeitpunkt und Status.

Ein Sekundärklick auf ein bekanntes System in der Galaxieansicht darf Aktionen wie `hierhin fliegen`, `Route planen` oder `erkunden` anbieten. Der Server prüft Controllerberechtigung, Standort, Verbindungen, Fähigkeiten, Versorgung, Route und Konflikte mit laufenden Befehlen.

## Routenwahl

Bestimmt der Server die Route, verwendet er eine dokumentierte Kostenfunktion aus Reisezeit, Gefahren, Zugangsrechten, Einschränkungen und Prioritäten. Bei Gleichstand gilt ein stabiler Tie-Breaker. Gleiche Eingaben müssen dieselbe Route ergeben.

## Reisezeit und Zustand

Jeder lokale oder interstellare Abschnitt besitzt Start- und Zielzeitpunkt in Kampagnenzeit. Währenddessen ist die Flotte `unterwegs` und nicht frei am Ausgangspunkt oder vollständig am Ziel verfügbar.

Gespeichert werden mindestens:

- Ausgang und Ziel,
- lokale Position oder Verbindung,
- Abfahrt,
- Ankunft,
- verbleibende Route,
- aktiver Befehl.

## Änderungen nach Abfahrt

Ein bereits begonnener Abschnitt wird grundsätzlich nach den bei Start gültigen Regeln abgeschlossen. Noch nicht begonnene Folgeabschnitte werden vor ihrem Start neu geprüft.

Wird eine interstellare Route ungültig, wartet die Flotte im nächsten erreichten System oder verwendet eine ausdrücklich erlaubte Neuplanung. Wird ein lokales Objektziel ungültig, gilt die für den Befehl definierte Ersatz-, Warte- oder Abbruchregel.

## Abbruch und Umleitung

Eine laufende Teilstrecke wird nicht rückwirkend aufgehoben. Umleitung wirkt frühestens am nächsten fachlich zulässigen Entscheidungspunkt. Bereits entstandene Kosten und Risiken bleiben bestehen.

Eine neue Sekundäraktion kann abhängig von Befehl und Zustand eine Umleitung, einen Ersatz der Warteschlange oder einen Folgeauftrag bedeuten. Der Client muss diese Wirkung vor Bestätigung sichtbar machen.

## Kontextaktionen

Kontextaktionen kombinieren Auswahl, Ziel und aktuellen sichtbaren Zustand. Mögliche Bewegungs- oder Folgeaktionen sind unter anderem:

- zu Position bewegen,
- Objektanker ansteuern,
- System anfliegen,
- erkunden,
- patrouillieren,
- eskortieren,
- kolonisieren,
- angreifen oder abfangen,
- reparieren oder versorgen.

Der Client erfindet diese Aktionen nicht aus sichtbaren Objekttypen. Verfügbarkeit, Deaktivierungsgrund, Kosten, Dauer und resultierender Befehl werden serverautoritativ geliefert oder abgeleitet.

## Begegnung und Kampf

Lokale Bewegung kann Flotten innerhalb definierter Begegnungs-, Sensor-, Abfang- oder Gefechtsreichweiten bringen. Ein Kampf beginnt nur nach den fachlichen Regeln aus D6 und wird vom Server ausgelöst.

Optische Überschneidung von 3D-Modellen oder sichtbare Nähe auf dem Bildschirm ist keine Kampfbedingung.

## Blockaden und unzugängliche Räume

Blockaden löschen keine Verbindung aus dem Graphen. Sie können Nutzung, Kampf, Risiko oder Routenempfehlung beeinflussen. Der Client unterscheidet unbekannt, nicht erreichbar und derzeit gesperrt, soweit die Ursache bekannt ist.

Lokale Sperrzonen oder Gefahren benötigen eigene serverseitige Geometrie und dürfen nicht allein aus einer grafischen Fläche entstehen.

## Sichtbarkeit und Offline-Fortschritt

Reisen werden nur bei ausreichender Sensorik sichtbar. Details können von bloßer Signatur bis zu Position, Ziel und Ankunftszeit reichen.

Bewegungen laufen während geschlossener Clients weiter. Offline-Nachholung verarbeitet lokale Abschnitte, interstellare Abschnitte, Begegnungen und Ereignisse in stabiler Reihenfolge.

## Anforderungen an Client und Server

### Client

Der Client:

- stellt bekannte lokale Positionen, nutzbare Verbindungen, Routen und Zeiten dar,
- trennt 3D-Visualisierung und fachliche XY-Geometrie,
- versetzt eine Flotte nicht optimistisch,
- bietet Sekundäraktionen für freie Punkte und Objekte,
- zeigt Kontextaktionen und sichere Deaktivierungsgründe,
- bietet dieselben Ziele über Tastatur und alternative Liste.

### Server

Der Server:

- validiert lokale Positionen, Systemgrenzen, Graph, Route und Befehl,
- speichert lokale und interstellare Reiseabschnitte,
- liefert wissensgefilterte Kontextaktionen,
- entscheidet über Begegnung und Kampfbeginn,
- wertet Offline-Fortschritt deterministisch aus.

## Offene Folgefragen

1. Welche Verbindungstypen gehören zum MVP?
2. Welche Reichweiten-, Versorgungs- und Haltungsregeln gelten in D6?
3. Wie wirken Blockaden, Abfangen und Gefahren?
4. Welche lokalen Objektanker sind je Himmelskörper oder Anlage zulässig?
5. Welche fachliche Systemausdehnung und Bewegungsauflösung werden verwendet?

## Akzeptanzkriterien

- Lokale Bewegung verwendet serverautoritative XY-Ziele.
- Interstellare Bewegung ist an bekannte Graphverbindungen gebunden.
- Routenwahl und Tie-Breaker sind deterministisch.
- Begonnene und zukünftige Abschnitte sind getrennt geregelt.
- Die 3D-Darstellung erzeugt keine eigene Erreichbarkeit oder Kampfregel.
- Freie Zielpunkte und Objektziele können über ein einheitliches Befehlsmodell adressiert werden.
- Kontextaktionen werden serverautoritativ validiert.
- Offline-Fortschritt und Fog of War werden berücksichtigt.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Sternensysteme und Himmelskörper](sternensysteme-und-himmelskoerper.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Besitz und Kontrolle](besitz-und-kontrolle.md)
- [Flotten – Übersicht](../08-fleets/README.md)
- [Raumansichten und Flotteninteraktion](../12-ui-ux/raumansichten-und-flotteninteraktion.md)
