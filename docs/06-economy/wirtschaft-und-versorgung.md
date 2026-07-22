# Wirtschaft und Versorgung

Status: Freigegeben

## Zweck

Dieses Dokument definiert Ressourcen, Produktionsketten, Lagerung, Bedürfnisse, Versorgung, Transport, Handel, Reichshaushalt, Unterhalt und Defizitfolgen.

## Güter und Ressourcen

Jedes wirtschaftliche Gut besitzt mindestens:

- stabile ID,
- Kategorie,
- Lagereinheit,
- Transportierbarkeit,
- Erzeugungs- und Verbrauchsregeln,
- optionale Haltbarkeit oder Lagergrenze,
- fachliche Verwendung.

Neue Güter werden nur aufgenommen, wenn sie eine eigenständige strategische Entscheidung erzeugen. Optisch unterschiedliche Varianten ohne eigene Funktion bleiben ein Gut.

## Güterkategorien

Das MVP benötigt wenige klare Kategorien:

- **Grundversorgung:** unmittelbar für Bevölkerung und Koloniebetrieb benötigt.
- **Rohstoffe:** natürliche oder primär gewonnene Inputs.
- **Industriegüter:** verarbeitete Inputs für Bau, Schiffe und Anlagen.
- **Energie oder Betriebsmittel:** laufender Betrieb von Produktion und Infrastruktur.
- **Spezialgüter:** Forschung, Militär oder besondere Projekte.
- **Finanzmittel:** abstrakte, reichsweit verrechenbare Zahlungs- und Haushaltsgröße.

Der konkrete Güterkatalog wird als statische Datendefinition geführt und kann balanciert werden, ohne das Wirtschaftsmodell zu ändern.

## Produktion

Eine Produktionseinheit besitzt:

- Eingaben pro Produktionsperiode,
- Ausgaben pro Produktionsperiode,
- Arbeitskräftebedarf,
- Versorgungs- und Infrastrukturbedarf,
- maximale Kapazität,
- Priorität,
- Status und Effizienz.

Produktion wird serverseitig in Kampagnenzeit ausgewertet. Inputs werden vor Outputs gebucht. Fehlen Inputs, Arbeitskräfte oder Versorgung, wird die Leistung nach einer dokumentierten Regel reduziert oder gestoppt.

## Produktionsketten

Produktionsketten entstehen aus expliziten Input-Output-Beziehungen. Der Server muss Zyklen zulassen können, darf daraus aber keine Güter durch Rundung oder Auswertungsreihenfolge erzeugen.

Innerhalb eines Auswertungszeitpunkts gilt eine stabile Reihenfolge:

1. verfügbare Bestände und reservierte Mengen bestimmen,
2. Grundversorgung und geschützte Prioritäten bedienen,
3. Produktion nach Priorität und proportionaler Zuteilung ausführen,
4. Outputs einlagern,
5. Unterhalt und Verluste buchen,
6. Kennzahlen und Warnungen aktualisieren.

Technische Batchgrößen dürfen das fachliche Ergebnis nicht verändern.

## Lagerung und Reservierung

Bestände werden je Lagerort und Gut geführt. Ein Lager besitzt Kapazität, aktuellen Bestand, reservierte Menge und verfügbare Menge.

- Bau- oder Handelsaufträge dürfen Güter reservieren.
- Reservierte Güter stehen anderen Vorgängen nicht zur Verfügung.
- Überfüllung wird verhindert oder erzeugt eine ausdrücklich definierte Verlustregel.
- Negative Bestände sind unzulässig.
- Transfers buchen Quelle und Ziel atomar über einen Transportvorgang.

Finanzmittel können reichsweit geführt werden; physische Güter bleiben grundsätzlich standortgebunden.

## Bedürfnisse und Versorgung

Bedürfnisse werden in wenigen verständlichen Stufen geführt:

1. Überleben und Grundversorgung,
2. regulärer Lebensstandard,
3. Komfort- oder Luxusbedarf.

Jede Bevölkerungsgruppe erzeugt einen Bedarf pro Kampagnenzeit. Der Versorgungsgrad ergibt sich aus geliefertem und benötigtem Gut, getrennt nach relevanter Bedarfskategorie.

Grundversorgung hat standardmäßig höhere Priorität als Komfortverbrauch. Der Spieler darf Reserven und Prioritäten setzen, aber eine manuelle Einzelverteilung ist nicht erforderlich.

## Mangelzustände

Mangel wirkt gestuft und mit nachvollziehbaren Ursachen:

- kurzfristiger Engpass erzeugt Warnungen und reduzierte Leistung,
- anhaltender Mangel senkt Wachstum, Zufriedenheit und Produktivität,
- schwerer Mangel kann Bevölkerung, Anlagen und Stabilität schädigen,
- irreversible Folgen benötigen angemessene Vorwarnung.

Ein einzelner technischer Tick ohne Bestand darf keine unverhältnismäßige Katastrophe auslösen. Folgen orientieren sich an Dauer und Schwere.

## Interner Transport

Physische Güter werden zwischen Kolonien über bekannte, nutzbare Routen transportiert. Ein Transportauftrag enthält Quelle, Ziel, Gut, Menge, reservierte Kapazität, Route, Start, Ankunft und Status.

Transportkapazität kann durch zivile Schiffe, Infrastruktur oder abstrakte Logistikpunkte bereitgestellt werden. Das MVP darf eine abstrahierte Kapazität verwenden, solange Route, Zeit, Unterbrechung und Standortbindung erhalten bleiben.

## Handelsrouten

Eine Handelsroute ist eine wiederkehrende Transportvereinbarung. Sie definiert:

- Beteiligte und Zugang,
- Güter und Zielmengen oder Kapazitäten,
- Route,
- Preis- oder Tauschregel,
- Priorität,
- Laufzeit und Kündigung,
- Verhalten bei Mangel oder Unterbrechung.

Handel erzeugt keine Güter. Lieferung und Zahlung werden serverseitig nachvollziehbar gebucht. Verträge und diplomatische Rechte folgen in D7.

## Preise und Tausch

Das MVP verwendet keine vollständig simulierte galaktische Börse. Preise können durch Vertrag, feste Marktregel oder spätere regionale Märkte bestimmt werden.

Jede Preisbildung muss für den Spieler erklärbar sein und darf keine verborgenen Informationen über fremde Bestände offenlegen.

## Unterbrechungen und Blockaden

Wird eine Route unbrauchbar, bleibt der Auftrag mit Grund und letzter Position sichtbar. Bereits transportierte Güter werden nicht dupliziert. Mögliche Folgen sind Warten, Neuplanung, Rückkehr oder Verlust nach ausdrücklich definierten Regeln.

Blockaden und militärische Risiken folgen D6; Zugangsrechte und Vertragsbruch folgen D7.

## Reichshaushalt

Der Reichshaushalt führt mindestens:

- verfügbare Finanzmittel,
- regelmäßige Einnahmen,
- laufenden Unterhalt,
- reservierte Mittel,
- einmalige Kosten,
- erwarteten Saldo,
- bekannte zukünftige Verpflichtungen.

Einnahmen können aus Kolonien, Handel, Gebühren oder Ereignissen stammen. Unterhalt entsteht insbesondere durch Gebäude, Flotten, Verwaltung, Verträge und Projekte.

## Defizit und Reserven

Ein kurzfristig negativer Saldo ist nicht automatisch ein Fehler, solange Reserven vorhanden sind. Sind Zahlungsverpflichtungen nicht erfüllbar, greift eine gestufte Defizitregel:

1. Warnung und Nutzung verfügbarer Reserven,
2. Priorisierung zwingender Verpflichtungen,
3. Drosselung oder Deaktivierung nicht zwingender Leistungen,
4. steigende Nachteile bei anhaltendem Defizit,
5. keine stillschweigende Erzeugung negativer unbegrenzter Mittel.

Welche Verpflichtungen zwingend sind, wird je System festgelegt. Defizitfolgen müssen sichtbar und reversibel beginnen, bevor existenzielle Schäden eintreten.

## Wirtschaftliche Kennzahlen

Der Client zeigt mindestens:

- Produktion und Verbrauch je Gut,
- aktuelle und reservierte Bestände,
- Engpässe und Reichweite der Vorräte,
- Transportkapazität und unterbrochene Routen,
- Einnahmen, Unterhalt und erwarteten Saldo,
- Ursachen von Effizienzverlusten,
- Prioritäten und geschützte Reserven.

## Anforderungen an Client und Server

### Client

Der Client muss Flüsse, Bestände, Reservierungen, Mangelursachen, Transportstatus und Haushalt verständlich zusammenfassen und bei Bedarf bis zur verursachenden Anlage aufschlüsseln.

### Server

Der Server muss Gütererhaltung, Reservierungen, Produktion, Verbrauch, Transport und Finanzbuchungen autoritativ und deterministisch auswerten. Jeder Befehl wird gegen Wissen, Bestand, Kapazität und Berechtigung geprüft.

## Offene Balancingfragen

1. Welcher minimale Güterkatalog gehört zum MVP?
2. Welche Transportkapazitäten werden abstrakt oder als Schiffe modelliert?
3. Welche konkreten Mangelstufen und Defizitfolgen gelten?
4. Welche Lagerkapazitäten und Reservierungsregeln sind sinnvoll?
5. Benötigt das MVP regionale Märkte oder genügen Verträge?

## Akzeptanzkriterien

- Güter, Bestände, Reservierungen und Finanzmittel sind getrennt.
- Produktion erhält Güter und ist unabhängig von technischer Schrittgröße.
- Bedürfnisse und Mangel wirken gestuft und nachvollziehbar.
- Physische Güter bleiben standort- und transportgebunden.
- Haushalt und Defizite besitzen sichtbare, begrenzte Folgen.
- Handel erzeugt weder Güter noch geheime Informationen.

## Verwandte Dokumente

- [Planeten und Kolonien](../04-planets/planeten-und-kolonien.md)
- [Bevölkerung und Arbeit](../05-population/bevoelkerung-und-arbeit.md)
- [Bewegung und Verbindungen](../02-galaxy/bewegung-und-verbindungen.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
