# Flotten und Raumkampf

Status: Freigegeben

## Zweck

Dieses Dokument definiert Schiffe, Schiffstypen, Flottenbildung, lokale und interstellare Flottenbefehle, Raumkampf, Schäden, Reparatur, Verluste, Versorgung und Reichweite. Es legt außerdem das fachliche Modell fest, das die Stellaris-artige Auswahl und Sekundäraktion in den Raumansichten abbildet.

## Schiff

Ein Schiff ist eine veränderliche, eindeutig identifizierte Entität. Es besitzt mindestens:

- stabile ID,
- Schiffstyp und Bauvariante,
- Besitzer,
- aktuellen Standort, lokale XY-Position oder Reiseabschnitt,
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
- aktuelles Sternensystem und lokale XY-Position oder interstellaren Reiseabschnitt,
- aktiven Befehl und Warteschlange,
- Haltung und Rückzugsregeln,
- zusammengefasste Reichweite, Geschwindigkeit, Sensorik und Kampfkraft.

Die langsamste oder am stärksten eingeschränkte Einheit kann die gemeinsame Bewegungsfähigkeit begrenzen. Die konkrete Aggregation wird deterministisch berechnet.

Die sichtbare 3D-Position einer Flotte wird aus ihrer autoritativen fachlichen Position abgeleitet. Modellgröße, Formation und visuelle Höhe verändern keine Reichweite oder Begegnungsbedingung.

## Flottenbildung

Schiffe können am selben fachlich zulässigen Standort zusammengelegt oder geteilt werden.

- Teilung und Zusammenlegung sind serverautoritativ.
- Schiffe dürfen nicht gleichzeitig mehreren Flotten angehören.
- Laufende Reiseabschnitte werden nicht beliebig geteilt.
- Ein aktiver Kampf kann Änderungen begrenzen.
- Neue Flotten erhalten eigene IDs und Befehlszustände.

Kommandokapazität kann die Größe oder Anzahl effizient geführter Flotten begrenzen, muss aber als sichtbare Reichs- oder Führungsressource definiert sein.

## Auswahl und Bedienung

Ein Primärklick auf eine sichtbare eigene Flotte oder die entsprechende Tastaturaktion wählt sie aus. Auswahl synchronisiert:

- Markierung in Sternensystem- oder Galaxieansicht,
- Outliner,
- Flottenpanel oder modales Flottendetail,
- sichtbare Route, Reichweiten und aktiven Befehl,
- Kontext für nachfolgende Sekundäraktionen.

Auswahl allein verändert keinen fachlichen Zustand.

Bei ausgewählter Flotte gilt:

- Sekundäraktion auf freien Raum bereitet lokale Bewegung zu einer XY-Position vor.
- Sekundäraktion auf einen Himmelskörper oder eine künstliche Entität öffnet ein Kontextmenü mit zulässigen Aktionen.
- Sekundäraktion auf ein Sternensystem in der Galaxieansicht öffnet interstellare Aktionen.
- Eine modifizierte Sekundäraktion kann einen Folgeauftrag an die Warteschlange anhängen.

Jede Interaktion besitzt eine gleichwertige Tastatur- und Listenalternative.

## Flottenbefehle

Das MVP benötigt mindestens:

- lokal bewegen,
- interstellar bewegen,
- erkunden,
- patrouillieren oder Position halten,
- eskortieren,
- transportieren,
- kolonisieren, sofern die Flotte dafür ausgerüstet ist,
- angreifen oder militärisch eingreifen,
- abfangen oder verfolgen,
- zurückziehen oder ausweichen,
- reparieren oder versorgen.

Jeder Befehl definiert Voraussetzungen, Ziel, Kosten, Start, Dauer, Abbruch, Ergebnis und sichtbare Rückmeldung. Spieler und AI verwenden dieselben Befehlstypen.

## Kontextaktionen

Ein Kontextmenü ist eine aktuelle serverautoritativ gefilterte Abbildung möglicher Befehle für Auswahl und Ziel.

Beispiele:

### Freier lokaler Punkt

- hierhin fliegen,
- Position halten,
- Patrouillenpunkt setzen.

### Unkolonisierter Planet

- hierhin fliegen,
- Orbit ansteuern,
- erkunden,
- kolonisieren, wenn Fähigkeit und Voraussetzungen bestehen,
- Details öffnen.

### Eigener Planet oder eigene Station

- hierhin fliegen,
- reparieren,
- versorgen,
- Transport aufnehmen oder entladen,
- Details öffnen.

### Feindliche Flotte

- angreifen,
- abfangen,
- verfolgen,
- Abstand halten,
- beobachten,
- Details öffnen.

Der Client darf Aktionen nicht allein aus Schiffstypen und sichtbaren Zielmerkmalen freischalten. Der Server liefert oder bestätigt Action-ID, Aktivierung, sicheren Deaktivierungsgrund, Kosten, Dauer, Risiko und resultierenden Befehlstyp.

## Befehlswarteschlange

Eine Flotte besitzt höchstens einen aktiven Befehl und eine geordnete Warteschlange. Der Server prüft einen Folgeauftrag vor seinem tatsächlichen Start erneut.

Ein ungültiger Folgeauftrag wird mit Grund angehalten oder übersprungen, wenn der Spieler dies ausdrücklich als Verhalten gewählt hat. Die Warteschlange darf keine unbekannten Ziele oder Routen enthalten.

## Lokale Bewegung

Lokale Flottenbewegung findet auf der autoritativen XY-Ebene eines Systems statt. Ein Ziel kann eine freie Position oder ein definierter Objektanker sein.

Der Server bestimmt:

- gültigen Start und Zielpunkt,
- Route oder Segment,
- Geschwindigkeit,
- Start- und Ankunftszeit,
- mögliche Unterbrechungen,
- Zeitpunkt, an dem Begegnungs- oder Kampfregeln geprüft werden.

Der Client darf die Flotte zwischen bestätigten Zuständen visuell interpolieren, schließt die Bewegung aber niemals selbst ab.

## Interstellare Bewegung

Interstellare Bewegung folgt bekannten und nutzbaren Verbindungen. Ein Zielsystem kann in der Galaxieansicht über eine Kontextaktion gewählt werden. Route, Zugangsrechte, Versorgung und Folgeabschnitte werden serverseitig bestimmt oder validiert.

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

Reichweiten dürfen als Kreise oder Flächen in der 3D-Szene visualisiert werden, werden aber ausschließlich aus serverseitigen Werten abgeleitet.

## Flottenhaltungen

Eine Flotte besitzt eine sichtbare Haltung, die Begegnungen und automatische Reaktionen innerhalb veröffentlichter Regeln beeinflusst. Mindestens vorzusehen sind fachlich unterscheidbare Haltungen wie:

- `passiv`,
- `defensiv`,
- `abfangen`,
- `aggressiv`,
- `ausweichen`.

Eine Haltung ist kein geheimer AI-Modus. Sie definiert nachvollziehbar, ob eine Flotte bei feindlicher Annäherung wartet, ausweicht, verfolgt, abfängt oder einen Kampf auslöst.

Konkrete Reichweiten, Prioritäten und Umschaltfolgen werden im Balancing und in den Befehlsverträgen festgelegt.

## Sensor-, Abfang- und Gefechtsreichweite

Folgende Reichweiten bleiben getrennt:

- **Sensorreichweite:** bestimmt, ob und wie genau eine fremde Flotte sichtbar ist.
- **Abfang- oder Begegnungsreichweite:** bestimmt, ob eine Haltung eine Annäherung oder Verfolgung auslösen kann.
- **Gefechtsreichweite:** bestimmt, wann Flotten fachlich am selben Kampfstandort gelten und eine Kampfinstanz beginnen kann.
- **Waffenreichweite:** wirkt innerhalb einer Kampfinstanz auf Zielauswahl und Kampfwirkung.

Optische Nähe, Modellüberschneidung oder Kamerazoom sind keine Reichweitenregeln.

## Kampfbeginn

Ein Raumkampf beginnt, wenn:

- feindliche Flotten nach Kriegs-, Zugangs- und Haltungsregeln auf der autoritativen lokalen XY-Ebene innerhalb der definierten Gefechts- oder Begegnungsbedingung aufeinandertreffen,
- mindestens eine Seite angreift, abfängt oder nicht erfolgreich ausweichen kann,
- der Server Teilnehmer und Zeitpunkt autoritativ bestimmt.

Später eintreffende Flotten treten nach dokumentierten Verstärkungsregeln bei.

Eine feindliche Flotte in bloßer Sensorreichweite startet nicht automatisch einen Kampf. Sensorik, Abfangen und Gefecht bleiben getrennt.

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

Kämpfe und Reisen laufen während Abwesenheit weiter. Kritische bevorstehende Konflikte benötigen angemessene Vorwarnung, soweit das Reich sie erkennen kann.

Rückkehrberichte priorisieren Kämpfe, schwere Schäden, Verluste, abgebrochene Befehle, veränderte Kontrolle und automatische Reaktionen aus Flottenhaltungen.

## Anforderungen an Client und Server

### Client

Der Client muss:

- Schiffe und Flotten in System- und Galaxieansicht darstellen,
- Auswahl, Outliner und modale Flottendetails synchronisieren,
- Flottenzusammensetzung, Befehle, Route, Versorgung, Zustand, Haltung und Rückzug verständlich darstellen,
- freie lokale Ziele und Objektziele über Sekundäraktionen anbieten,
- Kontextaktionen aus serverautoritativen Daten darstellen,
- Reichweiten nur aus Serverwerten visualisieren,
- Kampfberichte verständlich anzeigen,
- eine gleichwertige Tastatur- und Listenbedienung bieten.

### Server

Der Server muss:

- Schiff, Flotte und lokale XY-Position autoritativ verwalten,
- Kontextaktionen und Befehle validieren,
- Bewegungs-, Begegnungs- und Kampfzustände deterministisch auswerten,
- Zufall kontrollieren,
- Schäden und Verluste buchen,
- Fog of War filtern,
- keine Berechtigung oder Information über Aktionslisten leaken.

## Offene Balancingfragen

1. Welche konkreten Schiffstypen und Module gehören zum MVP?
2. Wie wird Versorgungsreichweite numerisch bestimmt?
3. Welche Sensor-, Abfang-, Gefechts- und Waffenreichweiten gelten?
4. Wie wirken die einzelnen Flottenhaltungen und Prioritäten?
5. Welche Kampfrundenlänge und Zufallsverteilung gelten?
6. Wie funktionieren Blockaden, Verfolgung und Verstärkung genau?
7. Welche Schäden können außerhalb einer Werft repariert werden?

## Akzeptanzkriterien

- Schiffe, Flotten und Befehle sind getrennte Entitäten.
- Spieler und AI verwenden dieselben Flottenbefehle.
- Flotten besitzen autoritative lokale XY-Positionen.
- Eine ausgewählte Flotte kann freie Punkte und Objekte über ein einheitliches Kontextaktionsmodell adressieren.
- Reisen, Begegnungen und Kämpfe sind serverautoritativ und deterministisch reproduzierbar.
- Sensor-, Abfang-, Gefechts- und Waffenreichweite sind getrennt.
- Optische 3D-Nähe startet keinen Kampf.
- Versorgung begrenzt Einsätze ohne permanente Mikromanagementpflicht.
- Rückzug, Schäden, Reparatur und dauerhafte Verluste sind geregelt.
- Kampf überträgt nicht automatisch territorialen Besitz.

## Verwandte Dokumente

- [Bewegung und Verbindungen](../02-galaxy/bewegung-und-verbindungen.md)
- [Erkundung und Informationsstände](../02-galaxy/erkundung-und-informationsstaende.md)
- [Besitz und Kontrolle](../02-galaxy/besitz-und-kontrolle.md)
- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
- [Raumansichten und Flotteninteraktion](../12-ui-ux/raumansichten-und-flotteninteraktion.md)
