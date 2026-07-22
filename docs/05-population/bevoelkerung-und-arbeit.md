# Bevölkerung und Arbeit

Status: Freigegeben

## Zweck

Dieses Dokument definiert das Bevölkerungsmodell, Wachstum, Rückgang, Migration, Arbeitskräfte, Qualifikationen, Beschäftigung und sichtbare Kennzahlen.

## Bevölkerungsgruppe

Bevölkerung wird nicht als einzelne Person, sondern als aggregierte Bevölkerungsgruppe modelliert. Eine Gruppe besitzt mindestens:

- stabile ID,
- Koloniezugehörigkeit,
- Spezies oder Herkunft,
- Bevölkerungsmenge,
- relevante Eigenschaften,
- Beschäftigungsstatus,
- bekannte Bedürfnisse und Zufriedenheit,
- optional rechtliche oder gesellschaftliche Zugehörigkeit.

Gruppen mit gleichen fachlich relevanten Eigenschaften dürfen zusammengeführt werden. Aufteilung und Zusammenführung müssen Mengenerhaltung und nachvollziehbare Rundung gewährleisten.

## Bevölkerungsmenge

Die Menge wird serverseitig als deterministisch berechenbarer Wert geführt. Darstellung darf gerundet sein; Befehle und Berechnungen verwenden den autoritativen Wert.

Eine Gruppe darf nicht durch Rundungsfehler negativ werden oder Bevölkerung erzeugen. Änderungen werden mit Ursache und Zeitraum protokollierbar berechnet.

## Wachstum und Rückgang

Natürliches Wachstum hängt mindestens ab von:

- vorhandener Bevölkerung,
- Bewohnbarkeit und Umwelt,
- Wohn- und Versorgungskapazität,
- Grundbedürfnissen,
- Gesundheit und Sicherheit,
- dokumentierten Spezies- oder Technologieeffekten.

Rückgang kann durch Mangel, Krankheit, Krieg, Evakuierung, Migration oder anhaltende Überlastung entstehen. Extreme Folgen benötigen Vorwarnungen und sind im Rückkehrbericht sichtbar.

Wachstum wird in Kampagnenzeit berechnet und darf bei Offline-Nachholung nicht von der technischen Schrittgröße abhängen.

## Migration

Migration verschiebt Bevölkerung zwischen geeigneten Kolonien. Sie erzeugt keine neue Bevölkerung.

Migration benötigt:

- bekannte und erreichbare Quelle und Ziel,
- verfügbare Transportkapazität oder eine später definierte passive Verbindung,
- ausreichende Aufnahmefähigkeit,
- rechtliche und diplomatische Zulässigkeit,
- eine nachvollziehbare Ursache oder Spieleranweisung.

Das MVP unterstützt mindestens serverseitig angeordnete Umsiedlung. Freie automatische Binnenmigration kann später auf Attraktivität, Versorgung und Chancen reagieren, muss aber begrenzt und erklärbar bleiben.

## Arbeitsfähige Bevölkerung

Nicht jede Bevölkerungseinheit steht vollständig als Arbeitskraft zur Verfügung. Arbeitsfähigkeit wird aus Bevölkerungsmenge und fachlich definierten Anteilen abgeleitet. Kinder, Versorgungstätigkeiten, Krankheit oder andere nicht verfügbare Anteile können später berücksichtigt werden, sofern sie eine erkennbare Entscheidung erzeugen.

Für das MVP genügt ein aggregiertes Erwerbspotenzial je Bevölkerungsgruppe. Individuelle Lebensläufe werden nicht simuliert.

## Arbeitsplätze

Bezirke, Gebäude und andere Einrichtungen stellen Arbeitsplätze nach Typ und Qualifikationsanforderung bereit.

Ein Arbeitsplatz besitzt:

- Arbeitgeber oder Anlage,
- benötigte Arbeitskraftart oder Qualifikation,
- maximale Stellen,
- Priorität,
- Produktionswirkung bei Teilbesetzung,
- Mindestbesetzung, sofern erforderlich.

Arbeitsplätze erzeugen nur bei aktiver Anlage und ausreichender Versorgung eine produktive Beschäftigung.

## Qualifikationen

Qualifikation wird in wenigen klaren Kategorien geführt, beispielsweise allgemeine, technische, wissenschaftliche oder administrative Arbeitskraft. Eine Kategorie muss unterschiedliche Einsatzmöglichkeiten oder Ausbildungsentscheidungen erzeugen.

Ausbildung oder Umschulung benötigt Zeit und gegebenenfalls Ressourcen. Fehlende Qualifikation kann Stellen unbesetzt lassen oder Effizienz senken, darf aber nicht durch verborgene Zufallsentscheidungen ausgeglichen werden.

## Beschäftigungszuweisung

Der Server weist verfügbare Arbeitskräfte anhand transparenter Prioritäten zu:

1. zwingende Grundversorgung und Überlebensfunktionen,
2. vom Spieler gesetzte Kolonieprioritäten,
3. explizite Gebäude- oder Sektorprioritäten,
4. stabile fachliche Tie-Breaker.

Der Spieler steuert Prioritäten, nicht einzelne Personen. Automatisierung darf nur diese veröffentlichten Regeln verwenden.

## Arbeitslosigkeit und unbesetzte Stellen

Arbeitslosigkeit und Personalmangel werden getrennt ausgewiesen.

- Arbeitslosigkeit: verfügbare Arbeitskräfte ohne Stelle.
- Personalmangel: offene Stellen ohne passende Arbeitskräfte.
- Qualifikationsmangel: Arbeitskräfte vorhanden, aber nicht geeignet.
- Inaktivität: Bevölkerung steht fachlich nicht als Arbeitskraft zur Verfügung.

Eine Kolonie kann gleichzeitig Arbeitslosigkeit in einer Gruppe und Personalmangel in einer anderen besitzen.

## Beschäftigungswechsel

Ändern sich Prioritäten, Bevölkerung oder Anlagen, wird die Zuweisung deterministisch neu berechnet. Ein Wechsel darf optional eine kurze Übergangs- oder Einarbeitungszeit besitzen, wenn dies später einen spielerischen Zweck erfüllt.

Laufende Produktionsperioden werden nicht doppelt gezählt. Der Server legt den Wirksamkeitszeitpunkt jeder Neuzuweisung fest.

## Zufriedenheit und Zugehörigkeit

Bevölkerungsgruppen dürfen einen aggregierten Zufriedenheits- oder Stabilitätszustand besitzen. Ursachen müssen sichtbar und auf wenige verständliche Kategorien begrenzt sein, etwa Versorgung, Wohnraum, Sicherheit, Rechte, Beschäftigung und Umwelt.

Konkrete politische Rechte oder Fraktionen werden in D7 oder einer späteren Erweiterung definiert. D4 benötigt keine vollständige Gesellschaftssimulation.

## Sichtbare Kennzahlen

Der Client zeigt mindestens:

- Gesamtbevölkerung und Veränderung,
- Bevölkerungsgruppen,
- Kapazität und Überlastung,
- Erwerbspotenzial,
- Beschäftigte, Arbeitslose und offene Stellen,
- Qualifikationsengpässe,
- Migration und wesentliche Ursachen,
- Warnungen bei Mangel oder starkem Rückgang.

Aggregierte Anzeigen müssen auf dieselben autoritativen Gruppen zurückführbar sein.

## Anforderungen an Client und Server

### Client

Der Client muss Ursachen von Wachstum, Rückgang, Migration und Beschäftigungsproblemen verständlich darstellen und Prioritäten statt Einzelzuweisungen anbieten.

### Server

Der Server muss Bevölkerungsmengen, Migration und Beschäftigung deterministisch berechnen, Mengenerhaltung gewährleisten, Prioritäten validieren und Offline-Fortschritt reproduzierbar auswerten.

## Offene Balancingfragen

1. Welche Qualifikationskategorien gehören zum MVP?
2. Welche Wachstums- und Migrationsraten sind angemessen?
3. Welche Bevölkerungsmerkmale sind spielerisch relevant?
4. Benötigt Beschäftigungswechsel eine Übergangszeit?
5. Welche Zufriedenheitsfolgen gehören bereits zum MVP?

## Akzeptanzkriterien

- Bevölkerung wird als aggregierte, stabile Gruppen modelliert.
- Wachstum, Rückgang und Migration sind mengen- und zeitkonsistent.
- Arbeitskräfte, Arbeitsplätze und Qualifikationen sind getrennt.
- Zuweisung erfolgt über sichtbare Prioritäten und stabile Tie-Breaker.
- Arbeitslosigkeit, Personalmangel und Qualifikationsmangel sind unterscheidbar.

## Verwandte Dokumente

- [Planeten und Kolonien](../04-planets/planeten-und-kolonien.md)
- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
- [Zeitmodell](../01-gameplay/zeitmodell.md)
