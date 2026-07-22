# Forschung und Technologien

Status: Review

## Zweck

Dieses Dokument definiert Forschungsressourcen, Fortschritt, Technologiestruktur, Auswahl, Voraussetzungen, Effekte, Spezialisierung, Technologietransfer und Aufholmechanismen.

## Forschungsleistung

Forschungsleistung ist eine reichsweite, nach Forschungsbereich aufschlüsselbare Leistung. Sie entsteht aus aktiven Forschungseinrichtungen, qualifizierten Arbeitskräften, Versorgung, Ereignissen und dokumentierten Modifikatoren.

Forschungsleistung ist kein physisches Lagergut. Nicht verwendete Leistung wird grundsätzlich nicht unbegrenzt gespeichert. Ausnahmen benötigen eine ausdrückliche Regel.

## Forschungsbereiche

Das MVP verwendet wenige stabile Forschungsbereiche, beispielsweise:

- Physik und Energie,
- Gesellschaft und Verwaltung,
- Biologie und Umwelt,
- Ingenieurwesen und Industrie,
- Raumfahrt und Militär.

Die endgültigen Bezeichnungen und Zuordnungen sind Datenkonfiguration. Eine Technologie kann einen Hauptbereich und optionale Nebenbereiche besitzen.

## Forschungsprojekt

Ein Forschungsprojekt besitzt mindestens:

- stabile Technologie-ID,
- benötigte Gesamtleistung,
- Forschungsbereich,
- Voraussetzungen,
- aktuellen Fortschritt,
- zugewiesene Leistung,
- Start- und Abschlusszeitpunkt oder Prognose,
- Status: verfügbar, aktiv, pausiert, abgeschlossen oder gesperrt.

Fortschritt wird serverseitig in Kampagnenzeit berechnet und bleibt beim Pausieren oder Wechsel erhalten, sofern die Technologie keine ausdrücklich definierte Verfallsregel besitzt.

## Parallelität

Das MVP unterstützt standardmäßig ein aktives Hauptprojekt pro Reich. Zusätzliche parallele Projekte können durch Technologien, besondere Einrichtungen oder Kampagneneffekte freigeschaltet werden.

Bei mehreren Projekten verteilt der Spieler die Forschungsleistung über Prioritäten oder Anteile. Die Summe der Zuweisungen darf die verfügbare Leistung nicht überschreiten.

## Technologiestruktur

Technologien bilden einen gerichteten, azyklischen Voraussetzungen-Graphen. Zyklen in zwingenden Voraussetzungen sind unzulässig.

Jede Technologie definiert:

- Voraussetzungen,
- sichtbare Kategorie und Stufe,
- Forschungskosten,
- Effekte und Freischaltungen,
- Wiederholbarkeit,
- Geheimhaltungs- oder Entdeckungsregeln, falls relevant.

Ein klassischer Baum darf visuell verwendet werden; fachlich maßgeblich ist der Graph.

## Sichtbarkeit und Auswahl

Der Spieler sieht grundsätzlich alle Technologien, deren Existenz sein Reich kennen darf. Gesperrte Technologien zeigen bekannte Voraussetzungen, sofern deren Geheimhaltung keinen spielerischen Zweck besitzt.

Das MVP setzt auf planbare Auswahl statt zufällig angebotener Karten. Zufall darf besondere Alternativen oder seltene Technologien aufdecken, aber nicht den grundlegenden Fortschritt eines Reiches unkontrollierbar machen.

## Voraussetzungen

Voraussetzungen können umfassen:

- abgeschlossene Technologien,
- Reichs- oder Koloniezustände,
- bekannte Anomalien oder Ereignisse,
- Mindestleistung in einem Bereich,
- besondere Ressourcen oder Projekte.

Voraussetzungen werden beim Start geprüft. Fallen nicht dauerhafte Voraussetzungen später weg, wird das Projekt nach einer dokumentierten Regel pausiert oder fortgesetzt. Bereits abgeschlossene Technologien werden nicht stillschweigend verloren.

## Technologieeffekte

Zulässige Effektarten sind insbesondere:

- Freischaltung neuer Gebäude, Schiffe, Bezirke oder Befehle,
- Verbesserung bestehender Kapazitäten oder Effizienzen,
- Veränderung klar benannter Formeln oder Grenzen,
- Freischaltung neuer Informationen oder Erkundungsmöglichkeiten,
- neue Automatisierungs- und Verwaltungsoptionen,
- neue diplomatische oder wirtschaftliche Handlungen.

Jeder Effekt besitzt eine eindeutige fachliche Zielgröße. Allgemeine undurchsichtige Prozentboni ohne sichtbare Ursache sollen vermieden werden.

## Wiederholbare Technologien

Wiederholbare Technologien sind nur zulässig, wenn:

- jede Stufe einen klaren Effekt besitzt,
- Kosten und Skalierung begrenzt oder nachvollziehbar wachsen,
- sie keine endlose Pflichtsteigerung als einzigen Endgame-Inhalt erzeugen,
- maximale Stufe oder abnehmender Nutzen dokumentiert ist.

Das MVP benötigt keine wiederholbaren Technologien.

## Forschungsschwerpunkte

Ein Reich kann einen oder mehrere Forschungsschwerpunkte festlegen. Ein Schwerpunkt:

- erhöht die Priorität oder Effizienz eines Bereichs,
- ist sichtbar und änderbar,
- besitzt gegebenenfalls eine Übergangszeit,
- darf andere Bereiche nicht vollständig unspielbar machen,
- soll eine langfristige Reichsidentität unterstützen.

Schwerpunkte beeinflussen Planung, nicht die fachliche Gültigkeit von Technologien.

## Spezialisierung

Spezialisierung entsteht aus wiederholten Entscheidungen, Einrichtungen und abgeschlossenen Technologien. Sie soll alternative starke Wege ermöglichen, aber keine dauerhaft unaufholbare frühe Fehlentscheidung erzeugen.

Ein Wechsel darf Kosten oder Zeit benötigen. Bereits erworbene Freischaltungen bleiben grundsätzlich erhalten; aktive Schwerpunktboni können wechseln.

## Technologietransfer

Technologie kann zwischen Reichen nur über ausdrücklich definierte Mechanismen übertragen werden:

- Forschungsabkommen,
- Lizenz oder Handel,
- gemeinsames Projekt,
- Ereignis,
- Spionage aus einem späteren System.

Transfer kann vollständige Freischaltung, Fortschrittsbonus oder Kostensenkung gewähren. Er darf nie eine Technologie vermitteln, deren zwingende Nutzungsvoraussetzungen das empfangende Reich nicht erfüllen kann, ohne dies sichtbar zu kennzeichnen.

## Aufholen

Aufholmechanismen sollen Rückstand reduzieren, ohne führende Reiche automatisch zu bestrafen. Mögliche Quellen:

- geringere Kosten für weit verbreitete bekannte Technologien,
- Bonus durch Kontakte und Forschungsabkommen,
- schnellere Grundlagenforschung,
- Zugang zu älteren Lizenztechnologien.

Der Bonus wird aus für das Reich bekannten und fachlich erlaubten Informationen berechnet. Verborgene fremde Technologien werden nicht offengelegt.

## Forschungswechsel und Abbruch

Beim Wechsel bleibt Fortschritt gespeichert. Reservierte Spezialressourcen werden nach dokumentierten Verbrauchsregeln behandelt. Ein abgeschlossener Forschungsschritt wird atomar ausgewertet: Kosten und Voraussetzungen prüfen, Technologie abschließen, Effekte aktivieren, Ereignis und Rückmeldung erzeugen.

## Rückkehrbericht

Der Rückkehrbericht zeigt:

- abgeschlossene Technologien,
- neu verfügbare wichtige Technologien,
- pausierte oder blockierte Projekte,
- Veränderungen der Forschungsleistung,
- Transferangebote und gemeinsame Projekte,
- erwartete nächste Abschlüsse.

## Anforderungen an Client und Server

### Client

Der Client muss Voraussetzungen, Kosten, Fortschritt, Zuweisung, Effekte, Schwerpunkt und Gründe für Sperren oder Pausen darstellen.

### Server

Der Server muss den Voraussetzungen-Graphen validieren, Fortschritt deterministisch berechnen, Leistung begrenzen, Abschlüsse atomar auswerten und alle Effekte gegen bekannte Zielgrößen anwenden.

## Offene Balancingfragen

1. Welche Forschungsbereiche gehören zum MVP?
2. Welche Technologien bilden den kleinsten spielbaren Graphen?
3. Wie stark dürfen Schwerpunkte und Aufholboni wirken?
4. Welche Transferformen gehören bereits zum MVP?
5. Werden parallele Projekte im MVP freigeschaltet?

## Akzeptanzkriterien

- Forschung wird als zeitabhängiger, serverautoritärer Fortschritt modelliert.
- Technologien bilden einen azyklischen Voraussetzungen-Graphen.
- Auswahl ist grundsätzlich planbar und nicht von zufälligen Karten abhängig.
- Effekte besitzen eindeutige fachliche Ziele.
- Transfer und Aufholen respektieren Wissen und Voraussetzungen.
- Pausieren oder Wechseln löscht keinen Fortschritt.

## Verwandte Dokumente

- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
- [Planeten und Kolonien](../04-planets/planeten-und-kolonien.md)
- [Erkundung und Informationsstände](../02-galaxy/erkundung-und-informationsstaende.md)
