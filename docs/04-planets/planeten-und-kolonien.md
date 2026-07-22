# Planeten und Kolonien

Status: Freigegeben

## Zweck

Dieses Dokument definiert Planeten als nutzbare Lebensräume, den Lebenszyklus von Kolonien, planetare Entwicklung, Bezirke, Gebäude, Bauvorgänge sowie Spezialisierung und Verwaltung.

## Planet als fachliche Entität

Jeder Planet besitzt mindestens:

- stabile ID und Zugehörigkeit zu einem Sternensystem,
- Planetenkategorie,
- Größenklasse,
- Umwelt- und Gefahrenmerkmale,
- natürliche Ressourcenmerkmale,
- grundlegende Kapazitäten,
- reichsspezifisch bekannte Eigenschaften.

Planetenwerte werden serverseitig gespeichert. Grafische Größe oder Farbe erzeugt keine zusätzliche Regel.

## Planetenkategorien und Bewohnbarkeit

Eine Planetenkategorie beschreibt Umweltbedingungen, nicht automatisch die Eignung für jede Bevölkerung. Bewohnbarkeit wird aus Planeteneigenschaften und Anforderungen der betroffenen Spezies oder Bevölkerungsgruppe abgeleitet.

Bewohnbarkeit beeinflusst später insbesondere:

- Gründungsaufwand,
- Bevölkerungswachstum,
- Versorgung und Lebensqualität,
- notwendige Infrastruktur,
- Risiken und Unterhaltskosten.

Ein Planet darf grundsätzlich unbewohnbar, eingeschränkt bewohnbar oder regulär bewohnbar sein. Terraforming oder künstliche Lebensräume sind spätere Freischaltungen und keine Voraussetzung des MVP.

## Größe und Kapazitäten

Die Größenklasse begrenzt den langfristig nutzbaren Raum. Daraus werden getrennte Kapazitäten abgeleitet, beispielsweise:

- bewohnbare Kapazität,
- Bezirks- oder Flächennutzung,
- industrielle Belastbarkeit,
- natürliche Ressourcenpotenziale,
- ökologische oder infrastrukturelle Grenzen.

Kapazitäten sind keine beliebig erweiterbaren Bauplätze. Technologien und Entwicklung dürfen Grenzen verändern, müssen dies aber sichtbar und nachvollziehbar tun.

## Koloniegründung

Eine Koloniegründung ist ein serverautoritativ validierter Befehl. Voraussetzungen sind mindestens:

- bekanntes und erreichbares Ziel,
- ausreichende Bewohnbarkeit oder passende Sondertechnik,
- gültiger territorialer Zugang,
- verfügbare Gründungseinheit oder definierter Gründungsprozess,
- erforderliche Ressourcen und Bevölkerung,
- keine fachlich ausschließende Konkurrenzsituation.

Der Befehl bindet Kosten und benötigt Kampagnenzeit. Abbruch, Verlust der Gründungseinheit oder Änderung des Zugangs werden nach dem erreichten Fortschritt behandelt; bereits verbrauchte Leistungen werden nicht automatisch vollständig erstattet.

## Kolonielebenszyklus

Eine Kolonie durchläuft folgende Grundzustände:

1. **Geplant:** Befehl angenommen, Gründung noch nicht begonnen.
2. **Gründung:** Transport und Aufbau laufen.
3. **Außenposten:** dauerhaft präsent, aber wirtschaftlich und demografisch noch abhängig.
4. **Etablierte Kolonie:** besitzt stabile Bevölkerung, Grundversorgung und reguläre Verwaltung.
5. **Entwickelte Kolonie:** kann Spezialisierungen und größere Produktionsstrukturen tragen.
6. **Krise oder Rückgang:** wesentliche Voraussetzungen fehlen; Entwicklung und Bevölkerung können sinken.
7. **Aufgegeben oder verloren:** keine aktive eigene Kolonie mehr.

Zustandswechsel beruhen auf überprüfbaren Voraussetzungen. Eine Kolonie wird nicht allein durch Ablauf eines Timers etabliert, wenn Grundversorgung oder Bevölkerung fehlen.

## Planetare Entwicklung

Entwicklung beschreibt die langfristig aufgebaute Leistungsfähigkeit einer Kolonie. Sie entsteht durch Bevölkerung, Infrastruktur, stabile Versorgung, Gebäude, Forschung und Zeit.

Entwicklung darf nicht nur ein universeller Bonuswert sein. Sie wird über konkrete Kapazitäten und freigeschaltete Möglichkeiten sichtbar. Überlastung entsteht, wenn Bevölkerung, Gebäude oder Produktion dauerhaft oberhalb tragfähiger Kapazitäten liegen.

Folgen können sein:

- steigender Unterhalt,
- Versorgungsengpässe,
- sinkende Lebensqualität,
- verlangsamtes Wachstum,
- Schäden oder Rückgang bei anhaltender Krise.

## Bezirke und Flächennutzung

Bezirke bündeln großflächige Nutzung, beispielsweise Wohnen, Rohstoffgewinnung, Industrie, Forschung oder Versorgung. Ein Bezirk:

- belegt planetare Kapazität,
- besitzt Voraussetzungen,
- stellt Arbeitsplätze, Grundproduktion oder Bauplätze bereit,
- kann ausgebaut, umgewandelt oder stillgelegt werden.

Die konkrete Bezirksliste wird aus D4 und D5 abgeleitet. Neue Bezirksarten benötigen eine eigenständige strategische Funktion.

## Gebäude

Gebäude sind konkrete Anlagen innerhalb einer Kolonie. Jedes Gebäude besitzt:

- Typ und Stufe,
- Standort,
- Voraussetzungen,
- Baukosten und Bauzeit,
- laufenden Unterhalt,
- Arbeitskräfte- und Versorgungsbedarf,
- definierte Effekte,
- Zustand: geplant, im Bau, aktiv, deaktiviert, beschädigt oder im Abriss.

Effekte gelten nur, wenn die dafür definierten Betriebsbedingungen erfüllt sind.

## Bauvorgänge und Warteschlange

Das MVP verwendet pro Kolonie eine autoritative Bauwarteschlange. Ein Bauauftrag enthält Ziel, Kostenbindung, Start, Dauer, Status und Abbruchregeln.

- Der Server prüft Voraussetzungen beim Annehmen und vor wirksamen Zustandswechseln.
- Ressourcen werden nach einer dokumentierten Regel reserviert oder schrittweise verbraucht.
- Pause der Kampagne pausiert Bauzeiten; Client-Schließen nicht.
- Ausbau, Umbau und Abriss sind eigene Aufträge.
- Abbruch erstattet nur den fachlich noch nicht verbrauchten Anteil.

Spätere Technologien dürfen zusätzliche parallele Baukapazität ermöglichen, ohne das Grundmodell zu ersetzen.

## Spezialisierung

Eine Kolonie kann eine sichtbare strategische Spezialisierung erhalten, beispielsweise Versorgung, Rohstoffe, Industrie, Forschung, Militär oder gemischte Entwicklung.

Spezialisierung:

- setzt Prioritäten und verständliche Empfehlungen,
- kann dokumentierte Boni oder Verwaltungserleichterungen geben,
- verbietet andere Nutzungen nicht automatisch,
- darf keine verborgenen Produktionsregeln erzeugen,
- kann nach einer definierten Übergangszeit geändert werden.

## Verwaltung und Automatisierung

Der Spieler kontrolliert Ziele, Spezialisierung, große Bauaufträge und Prioritäten. Routinen dürfen delegiert werden, etwa:

- freie Arbeitskräfte nach Prioritäten verteilen,
- Gebäude bei fehlender Versorgung automatisch drosseln,
- definierte Mindestreserven schützen,
- wiederkehrende Reparaturen anstoßen,
- Warnungen und Vorschläge erzeugen.

Automatisierung darf nur veröffentlichte Befehle verwenden, benötigt klare Grenzen und muss ihre letzten Entscheidungen nachvollziehbar anzeigen.

## Aufgabe und Verlust

Eine Kolonie kann bewusst aufgegeben, evakuiert, zerstört oder durch Krieg verloren werden. Ein solcher Übergang behandelt mindestens:

- Bevölkerung und mögliche Evakuierung,
- laufende Aufträge,
- Gebäude und Ressourcen,
- territorialen Besitz,
- fremde oder verbleibende Einheiten,
- Rückkehrbericht und Protokollierung.

Eine kurzfristige Versorgungskrise löscht eine Kolonie nicht automatisch.

## Anforderungen an Client und Server

### Client

Der Client muss Planeteneigenschaften, Bewohnbarkeit, Kapazitäten, Koloniezustand, Bauwarteschlange, Spezialisierung, Engpässe und Automatisierung verständlich darstellen.

### Server

Der Server muss Gründung, Entwicklung, Kapazitäten, Bauaufträge, Zustände und Automatisierungsbefehle autoritativ validieren und in Kampagnenzeit auswerten.

## Offene Balancingfragen

1. Welche Planetenkategorien gehören zum MVP?
2. Welche konkreten Kapazitäten werden numerisch geführt?
3. Welche Bezirke und Gebäude bilden den kleinsten spielbaren Katalog?
4. Welche Zeit und Kosten gelten für Gründung und Zustandswechsel?
5. Welche Automatisierungsprofile werden zuerst angeboten?

## Akzeptanzkriterien

- Planeten, Kolonien, Bezirke und Gebäude sind eindeutig getrennt.
- Koloniegründung und Lebenszyklus besitzen nachvollziehbare Zustände.
- Entwicklung ist an konkrete Kapazitäten und Versorgung gebunden.
- Bauvorgänge sind serverautoritativ und offline-fähig.
- Spezialisierung und Automatisierung bleiben transparent.

## Verwandte Dokumente

- [Galaxie und Himmelskörper](../02-galaxy/sternensysteme-und-himmelskoerper.md)
- [Besitz und Kontrolle](../02-galaxy/besitz-und-kontrolle.md)
- [Bevölkerung und Arbeit](../05-population/bevoelkerung-und-arbeit.md)
- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
