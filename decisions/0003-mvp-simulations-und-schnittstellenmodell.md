# 0003 – MVP-Simulations- und Schnittstellenmodell

Status: angenommen

Datum: 2026-07-22

## Kontext

Die Fachbereiche Planeten, Bevölkerung, Wirtschaft, Forschung, Flotten, Diplomatie, Ereignisse und REST-Schnittstelle benötigen gemeinsame Leitentscheidungen, damit Client und Server ohne konkurrierende Zustände implementiert werden können.

## Entscheidung

Für das fachliche MVP gelten folgende systemübergreifende Entscheidungen:

1. Bevölkerung wird als aggregierte Bevölkerungsgruppen statt als Einzelpersonen simuliert.
2. Physische Güter bleiben standortgebunden; Finanzmittel und ausdrücklich definierte Kapazitäten dürfen reichsweit geführt werden.
3. Produktion, Forschung, Bau, Reise, Kampf und Ereignisse werden serverautoritativ in Kampagnenzeit ausgewertet.
4. Das MVP verwendet pro Kolonie eine Bauwarteschlange und standardmäßig ein aktives Hauptforschungsprojekt pro Reich.
5. Arbeitskräfte werden über transparente Prioritäten und stabile Tie-Breaker statt manueller Einzelzuweisung verteilt.
6. Flottenkämpfe verwenden diskrete, deterministisch reproduzierbare Kampfschritte und serverseitig kontrollierten Zufall.
7. Diplomatie, Verträge, Krieg und Frieden sind explizite Zustandsmaschinen und keine direkten Wertänderungen durch den Client.
8. Ereignisse und Krisen sind versionierte, idempotente Zustandsmaschinen und verwenden veröffentlichte fachliche Operationen.
9. Die Client-Server-Kommunikation verwendet versionierte REST-Ressourcen, reichsspezifische Zustände, idempotente Befehle und inkrementelle Änderungssynchronisation.
10. WebSockets oder ein lokales LLM sind keine Voraussetzung des fachlichen MVP.

## Begründung

Aggregation und klare Standortbindung halten die Simulation verständlich und performant. Serverautoritative Zustandsmaschinen ermöglichen Offline-Fortschritt, reproduzierbare Tests und spätere AI- oder Spielerübernahmen. Ein einheitlicher REST-Vertrag trennt Clientdarstellung von fachlicher Wahrheit und erlaubt robuste Wiederholung bei Verbindungsfehlern.

## Betrachtete Alternativen

### Individuelle Bevölkerungssimulation

Sie erhöht Datenmenge und Komplexität, ohne für das MVP genügend zusätzliche strategische Entscheidungen zu erzeugen.

### Globale Warenbestände

Sie würden Transport, Blockaden und räumliche Spezialisierung entwerten.

### Clientseitige Sofortausführung

Sie widerspricht dem serverautoritativen Modell und erschwert Offline-Fortschritt, Multiplayer und Betrugsschutz.

### Permanente WebSocket-Verbindung als Voraussetzung

Sie würde den Client stärker an eine dauerhafte Verbindung binden. REST mit Änderungsversionen und optionalem Long Polling genügt dem asynchronen Modell.

### Separate AI-Spielregeln

Sie würden Balancing, Tests und Reichsübernahmen inkonsistent machen.

## Positive Folgen

- klare fachliche Zuständigkeiten,
- reproduzierbare Simulation und Tests,
- robuste Offline- und Wiederholungsfähigkeit,
- gemeinsame Befehle für Spieler und AI,
- verständliche räumliche Wirtschaft und Logistik,
- REST-Vertrag kann direkt in OpenAPI überführt werden.

## Negative Folgen und Risiken

- Server benötigt persistente Zustandsmaschinen und Versionshistorie,
- numerisches Balancing muss viele Systeme gemeinsam berücksichtigen,
- aggregierte Modelle benötigen gute Erklärungen ihrer Ursachen,
- REST-Änderungssynchronisation erfordert Aufbewahrungs- und Konfliktregeln,
- deterministische Kämpfe benötigen kontrollierten Zufall und stabile Auswertungsreihenfolge.

## Betroffene Dokumente

- [Planeten und Kolonien](../docs/04-planets/planeten-und-kolonien.md)
- [Bevölkerung und Arbeit](../docs/05-population/bevoelkerung-und-arbeit.md)
- [Wirtschaft und Versorgung](../docs/06-economy/wirtschaft-und-versorgung.md)
- [Forschung und Technologien](../docs/07-research/forschung-und-technologien.md)
- [Flotten und Raumkampf](../docs/08-fleets/flotten-und-raumkampf.md)
- [Reichsverwaltung](../docs/03-empires/reichsverwaltung.md)
- [Diplomatie und Krieg](../docs/09-diplomacy/diplomatie-und-krieg.md)
- [Ereignisse und Krisen](../docs/10-events/ereignisse-und-krisen.md)
- [Endgame und Abschluss](../docs/11-campaign/endgame-und-abschluss.md)
- [REST API v1](../contracts/rest-api/galaxis-rest-v1.md)

## Ersetzt

keine

## Ersetzt durch

keine
