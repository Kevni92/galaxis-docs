# Flotten und Raumkampf

Status: Freigegeben

## Zweck

Dieses Dokument definiert Schiffe, Schiffstypen, Flottenbildung, Flottenbefehle, Raumkampf, Schäden, Reparatur, Verluste, Versorgung und Reichweite.

## Schiff

Ein Schiff ist eine veränderliche, eindeutig identifizierte Entität. Es besitzt mindestens:

- stabile ID,
- Schiffstyp und Bauvariante,
- Besitzer,
- aktuellen Standort oder Reiseabschnitt,
- strukturelle Integrität,
- Kampffähigkeit und zivile Funktionen,
- Versorgungszustand,
- Flottenzugehörigkeit,
- Status: im Bau, aktiv, beschädigt, außer Gefecht, zerstört oder ausgemustert.

## Schiffstypen und Rollen

Das MVP verwendet wenige klar unterscheidbare Rollen, beispielsweise:

- Erkundungsschiff,
- Transport- oder Kolonieschiff,
- leichte Kampfeinheit,
- schwere Kampfeinheit,
- Unterstützung oder Versorgung,
- ziviler Frachter.

Ein Typ benötigt einen eigenen strategischen Zweck. Varianten dürfen Werte und Module verändern, müssen aber innerhalb veröffentlichter Grenzen bleiben.

## Module und Ausrüstung

Ein Schiffstyp definiert erlaubte Modulplätze oder feste Komponenten. Module können Waffen, Verteidigung, Antrieb, Sensorik, Frachtraum oder Spezialfähigkeiten bereitstellen.

Die konkrete Modulbelegung wird beim Bau festgelegt. Änderungen benötigen Werft, Zeit und Ressourcen. Ein Modul darf nur dokumentierte Werte oder Befehle beeinflussen.

## Schiffsbau und Lebenszyklus

Schiffe werden durch geeignete Werften gebaut. Ein Bauauftrag reserviert Ressourcen, benötigt Kampagnenzeit und erzeugt erst bei Abschluss ein aktives Schiff.

Ausmusterung, Umbau und Reparatur sind eigene Vorgänge. Zerstörte Schiffe werden nicht wieder aktiviert; mögliche Bergung erzeugt getrennte Ressourcen oder Objekte.

## Flotte

Eine Flotte ist eine organisatorische Einheit aus einem oder mehreren Schiffen. Sie besitzt:

- stabile ID und Anzeigename,
- Besitzer und Controllerberechtigung,
- Schiffsmenge,
- aktuellen Standort oder Reiseabschnitt,
- aktiven Befehl und Warteschlange,
- Haltung und Rückzugsregeln,
- zusammengefasste Reichweite, Geschwindigkeit, Sensorik und Kampfkraft.

Die langsamste oder am stärksten eingeschränkte Einheit kann die gemeinsame Bewegungsfähigkeit begrenzen. Die konkrete Aggregation wird deterministisch berechnet.

## Flottenbildung

Schiffe können im selben fachlich zulässigen Standort zusammengelegt oder geteilt werden.

- Teilung und Zusammenlegung sind serverautoritativ.
- Schiffe dürfen nicht gleichzeitig mehreren Flotten angehören.
- Laufende Reiseabschnitte werden nicht beliebig geteilt.
- Ein aktiver Kampf kann Änderungen begrenzen.
- Neue Flotten erhalten eigene IDs und Befehlszustände.

Kommandokapazität kann die Größe oder Anzahl effizient geführter Flotten begrenzen, muss aber als sichtbare Reichs- oder Führungsressource definiert sein.

## Flottenbefehle

Das MVP benötigt mindestens:

- bewegen,
- erkunden,
- patrouillieren oder Position halten,
- eskortieren,
- transportieren,
- kolonisieren, sofern die Flotte dafür ausgerüstet ist,
- angreifen oder militärisch eingreifen,
- zurückziehen,
- reparieren oder versorgen.

Jeder Befehl definiert Voraussetzungen, Ziel, Kosten, Start, Dauer, Abbruch, Ergebnis und sichtbare Rückmeldung. Spieler und AI verwenden dieselben Befehlstypen.

## Befehlswarteschlange

Eine Flotte besitzt höchstens einen aktiven Befehl und eine geordnete Warteschlange. Der Server prüft einen Folgeauftrag vor seinem tatsächlichen Start erneut.

Ein ungültiger Folgeauftrag wird mit Grund angehalten oder übersprungen, wenn der Spieler dies ausdrücklich als Verhalten gewählt hat. Die Warteschlange darf keine unbekannten Ziele oder Routen enthalten.

## Reichweite und Versorgung

Flotteneinsatz wird durch ein nachvollziehbares Versorgungsmodell begrenzt. Das MVP verwendet eine von Versorgungsquellen abgeleitete Einsatzreichweite statt manueller Treibstoffeinheiten für jeden Flug.

Versorgungsquellen können sein:

- eigene Kolonien,
- geeignete Stationen oder Basen,
- Versorgungsschiffe,
- vertraglich nutzbare fremde Basen.

Jede Flotte besitzt einen Versorgungsstatus:

- versorgt,
- angespannt,
- unversorgt,
- kritisch.

Entfernung, Einsatzdauer, Schäden und feindliche Kontrolle können den Status verschlechtern. Folgen beginnen mit reduzierter Reparatur, Geschwindigkeit oder Kampffähigkeit und eskalieren erst bei anhaltender Unterversorgung.

## Kampfbeginn

Ein Raumkampf beginnt, wenn feindliche Flotten nach Kriegs-, Zugangs- und Haltungsregeln am selben Kampfstandort aufeinandertreffen und mindestens eine Seite den Kampf auslöst oder nicht ausweichen kann.

Der Server bestimmt Teilnehmer anhand eines autoritativen Zeitpunktes. Später eintreffende Flotten treten nach dokumentierten Verstärkungsregeln bei.

## Kampfinstanz

Ein Kampf ist eine serverseitige Zustandsmaschine mit:

- Teilnehmern und Seiten,
- Beginn und aktuellem Kampfschritt,
- Haltungen und Rückzugsschwellen,
- Zielauswahl,
- angewandten Schäden und Effekten,
- Verstärkungen,
- Ergebnis und Abschlusszeitpunkt.

Das MVP verwendet deterministische Kampfrunden oder diskrete Kampfschritte. Zufall wird ausschließlich über serverseitigen, reproduzierbaren Zufall mit gespeichertem Kontext ausgewertet.

## Zielauswahl und Kampfwirkung

Zielauswahl berücksichtigt nur bekannte und im Kampf verfügbare Ziele. Prioritäten können aus Rollen, Haltungen, Reichweite und Spielerbefehlen entstehen.

Kampfwirkung wird aus Waffen, Verteidigung, Zustand, Versorgung und dokumentierten Modifikatoren berechnet. Gleiche Ausgangslage, Befehle und Zufallsfolge ergeben dasselbe Ergebnis.

## Rückzug

Jede Seite kann eine Rückzugshaltung oder Schwelle festlegen. Rückzug benötigt einen zulässigen Zeitpunkt, eine erreichbare Route und gegebenenfalls Vorbereitungszeit.

Ein Rückzug ist kein sofortiges Verschwinden. Scheitert die Route oder wird die Flotte bewegungsunfähig, bleibt sie im Kampf. Erfolgreicher Rückzug erzeugt einen regulären Reiseabschnitt.

## Kampfende

Ein Kampf endet, wenn:

- nur noch eine kampffähige Seite verbleibt,
- alle Seiten erfolgreich abziehen,
- ein fachlich definierter Abbruchzustand eintritt.

Das Ergebnis enthält Verluste, Schäden, Rückzüge, Kontrolle, Bergungsobjekte und sichtbare Berichte. Besitzwechsel folgen nicht automatisch aus dem Kampfergebnis.

## Schäden

Schäden werden mindestens als strukturelle Integrität geführt. Optionale Komponenten- oder Systemschäden sind nur sinnvoll, wenn sie erkennbare Handlungsfolgen besitzen.

Zustände:

- einsatzfähig,
- beschädigt,
- schwer beschädigt,
- außer Gefecht,
- zerstört.

Beschädigung reduziert dokumentierte Fähigkeiten. Ein Schiff mit null Integrität ist zerstört und kann nicht durch gewöhnliche Reparatur zurückkehren.

## Reparatur und Bergung

Reparatur benötigt geeigneten Standort oder Reparaturfähigkeit, Ressourcen und Zeit. Feldreparatur darf nur begrenzt wirken.

Bergung kann nach Kämpfen Ressourcen, Informationen oder reparierbare Wracks erzeugen. Sie ist kein automatischer vollständiger Ersatz und benötigt einen eigenen Befehl.

## Verluste und Besatzung

Verluste werden dauerhaft verbucht und im Kampfbericht ausgewiesen. Sofern Besatzung als Bevölkerungs- oder Arbeitskraftressource relevant wird, muss D4 die Rückwirkung definieren. Das MVP kann Besatzung zunächst als Bestandteil des Schiffsbetriebs abstrahieren.

## Fog of War und Kampfberichte

Ein Reich erhält nur Informationen, die eigene Teilnehmer, Sensoren oder spätere Berichte liefern. Ein Kampfbericht unterscheidet bestätigte eigene Daten, beobachtete fremde Daten und Schätzungen.

## Offline-Fortschritt

Kämpfe und Reisen laufen während Abwesenheit weiter. Kritische bevorstehende Konflikte benötigen angemessene Vorwarnung, soweit das Reich sie erkennen kann. Rückkehrberichte priorisieren Kämpfe, schwere Schäden, Verluste, abgebrochene Befehle und veränderte Kontrolle.

## Anforderungen an Client und Server

### Client

Der Client muss Flottenzusammensetzung, Befehle, Route, Versorgung, Zustand, Rückzugshaltung und Kampfberichte verständlich darstellen.

### Server

Der Server muss Schiff und Flotte autoritativ verwalten, Befehle validieren, Bewegungs- und Kampfzustände deterministisch auswerten, Zufall kontrollieren, Schäden buchen und Fog of War filtern.

## Offene Balancingfragen

1. Welche konkreten Schiffstypen und Module gehören zum MVP?
2. Wie wird Versorgungsreichweite numerisch bestimmt?
3. Welche Kampfrundenlänge und Zufallsverteilung gelten?
4. Wie funktionieren Abfangen, Blockaden und Verstärkung genau?
5. Welche Schäden können außerhalb einer Werft repariert werden?

## Akzeptanzkriterien

- Schiffe, Flotten und Befehle sind getrennte Entitäten.
- Spieler und AI verwenden dieselben Flottenbefehle.
- Reisen und Kämpfe sind serverautoritativ und deterministisch reproduzierbar.
- Versorgung begrenzt Einsätze ohne permanente Mikromanagementpflicht.
- Rückzug, Schäden, Reparatur und dauerhafte Verluste sind geregelt.
- Kampf überträgt nicht automatisch territorialen Besitz.

## Verwandte Dokumente

- [Bewegung und Verbindungen](../02-galaxy/bewegung-und-verbindungen.md)
- [Erkundung und Informationsstände](../02-galaxy/erkundung-und-informationsstaende.md)
- [Besitz und Kontrolle](../02-galaxy/besitz-und-kontrolle.md)
- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
