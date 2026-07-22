# Reichsentität und Reichsverwaltung

Status: Freigegeben

## Zweck

Dieses Dokument definiert das Reich als zentrale politische und wirtschaftliche Entität, seine Identität, Gebiete, Verwaltungswerte, Lebenszyklus sowie die Einbettung von Spieler- und AI-Controllern.

## Reich

Ein Reich besitzt mindestens:

- stabile ID,
- Namen und optionale visuelle Identität,
- Kampagnenzugehörigkeit,
- aktuellen Lebenszyklusstatus,
- souverän besessene Systeme und Kolonien,
- bekannten Galaxiezustand,
- Finanzmittel, Forschung und reichsweite Kapazitäten,
- diplomatische Beziehungen und Verträge,
- Controllerzuordnung,
- freigegebene Verwaltungsprioritäten und Automatisierungen.

Anzeigename, Symbol und Farbe sind änderbare Präsentationswerte. Die ID bleibt stabil.

## Reichsidentität

Reichsidentität entsteht aus gewählten und entwickelten Eigenschaften, beispielsweise:

- gesellschaftlicher oder politischer Ausrichtung,
- Forschungs- und Wirtschaftsprofil,
- diplomatischer Haltung,
- historischen Entscheidungen,
- Spezialisierungen und langfristigen Zielen.

Eigenschaften müssen konkrete, sichtbare Auswirkungen oder narrative Bedeutung besitzen. Sie dürfen keine pauschalen versteckten AI-Sonderregeln erzeugen.

## Gebiet

Das Reichsgebiet wird aus souverän besessenen Systemen abgeleitet. Kolonien und Außenposten bilden territoriale Grundlagen nach den Regeln von D2 und D3.

Disjunkte Gebiete sind zulässig. Gebiet, Anspruch, militärische Kontrolle und Wissen bleiben getrennte Zustände.

## Reichsweite Ressourcen und Kapazitäten

Reichsweit geführt werden nur Werte, deren Standortbindung keinen eigenen spielerischen Zweck besitzt, insbesondere:

- Finanzmittel,
- bestimmte Verwaltungs- und Forschungskapazitäten,
- diplomatische oder politische Kapazitäten,
- bekannte strategische Kennzahlen.

Physische Güter, Bevölkerung, Flotten und Anlagen bleiben standortgebunden.

## Verwaltungskapazität

Verwaltungskapazität begrenzt die effiziente Steuerung eines wachsenden Reiches, ohne harte willkürliche Gebietsverbote zu erzeugen.

Belastung kann entstehen durch:

- Anzahl und Entfernung von Kolonien,
- Bevölkerung,
- besondere Verwaltungsaufgaben,
- besetzte oder instabile Gebiete,
- aktive Großprojekte und Verträge.

Kapazität entsteht durch Institutionen, Gebäude, Technologien und Entscheidungen. Überlastung wirkt gestuft, beispielsweise durch langsamere Verwaltung, höheren Unterhalt, geringere Automatisierungsqualität oder verzögerte Maßnahmen.

Der Spieler muss Ursachen, aktuelle Belastung, verfügbare Kapazität und erwartete Folgen sehen können.

## Reichsprioritäten

Ein Reich kann langfristige Prioritäten festlegen, etwa Expansion, Konsolidierung, Forschung, Wirtschaft, Verteidigung oder Diplomatie.

Prioritäten:

- steuern Empfehlungen und zulässige Automatisierung,
- beeinflussen keine Validierung durch geheime Regeln,
- sind für einen neuen Controller sichtbar,
- können nach einer dokumentierten Übergangsregel geändert werden,
- ersetzen keine konkreten Befehle.

## Verwaltungsebenen

Das MVP benötigt keine vollständige mehrstufige Bürokratiesimulation. Fachlich genügen:

- Reichsebene für Ziele, Haushalt, Forschung und Diplomatie,
- Kolonieebene für lokale Entwicklung und Produktion,
- Flottenebene für operative Befehle.

Regionen oder Sektoren können später als Bündelungs- und Automatisierungsebene ergänzt werden, ohne Eigentum oder Spielregeln zu duplizieren.

## Regierung und politische Eigenschaften

Eine Regierungsform kann Regeln für Prioritäten, Kapazitäten, Diplomatie oder Ereignisse beeinflussen. Das MVP benötigt mindestens eine neutrale Standardregierung. Weitere Regierungsformen dürfen erst ergänzt werden, wenn ihre Entscheidungen und Wechselwirkungen dokumentiert sind.

Regierungswechsel benötigt eine ausdrückliche Entscheidung oder ein Ereignis. Er verändert nicht rückwirkend Besitz, Wissen oder bereits angenommene Befehle.

## Reichslebenszyklus

Ein Reich besitzt folgende mögliche Zustände:

- `vorbereitet`: Kampagnenstart noch nicht wirksam,
- `aktiv`: regulär handlungsfähig,
- `eingeschränkt`: wesentliche Handlungsfähigkeit reduziert,
- `besiegt`: formale Niederlage eingetreten,
- `aufgelöst`: keine eigenständige Spielentität mehr,
- `Nachspiel`: Kampagne nach offiziellem Abschluss fortgesetzt.

Ein Reich wird nicht allein durch Verlust eines Systems oder eine kurzfristige Wirtschaftskrise besiegt. Niederlage folgt den Kampagnenregeln.

## Controller und Eigentum

Controller und Reich sind getrennt. Ein Reich kann von Spieler oder AI kontrolliert werden, ohne seine Spielregeln zu ändern.

- Jeder aktive Befehl wird unabhängig vom Controller gleich validiert.
- Ein Controllerwechsel erhält Befehle, Ziele, Wissen und Zustände.
- AI erhält nur Reichswissen und freigegebene Befehle.
- Ein Verbindungsabbruch ist keine automatische Übergabe.
- Übernahme und Rückgabe werden atomar und protokolliert ausgeführt.

Das maßgebliche Detailmodell steht in [Spieler-, AI- und Reichsübernahmemodell](controller-und-reichsuebernahme.md).

## Übernahmebericht

Ein neuer Spielercontroller erhält mindestens:

- Reichslage und wichtigste Veränderungen,
- Haushalt, Forschung und Versorgung,
- laufende Befehle und Projekte,
- Kolonien, Flotten und Risiken,
- diplomatische Verträge und Konflikte,
- Prioritäten und Automatisierungen,
- zeitkritische Entscheidungen.

Der Bericht enthält nur Wissen des Reiches und keine internen AI-Gedankenketten.

## AI-Berechtigungen

AI-Controller dürfen:

- veröffentlichte fachliche Befehle erteilen,
- Prioritäten und Automatisierungen innerhalb ihrer Berechtigung ändern,
- diplomatische Angebote nach denselben Regeln senden und beantworten,
- auf Ereignisse und Krisen reagieren.

AI-Controller dürfen nicht:

- Validierung umgehen,
- geheime fremde Informationen lesen,
- Spielwerte direkt verändern,
- alternative Kosten oder Zeiten verwenden,
- Verträge oder Kriege außerhalb veröffentlichter Befehle erzeugen.

Die konkrete AI-Implementierung bleibt außerhalb der Fachregeln. Inhalte unter `ideas/` sind nicht verbindlich.

## Auflösung und Nachfolge

Bei Auflösung eines Reiches müssen Besitz, Kolonien, Flotten, Verträge, Ansprüche, Bevölkerung und laufende Vorgänge ausdrücklich behandelt werden. Es gibt keine pauschale automatische Übertragung aller Entitäten an den Sieger.

Eine Nachfolgeentität erhält eine neue Reichs-ID, sofern sie fachlich ein neues Reich darstellt. Historische Beziehungen können verknüpft, aber nicht als Identität wiederverwendet werden.

## Sichtbare Kennzahlen

Der Client zeigt mindestens:

- Reichsidentität und Status,
- Gebiet und bekannte Ansprüche,
- Haushalt, Forschung und Verwaltungsbelastung,
- langfristige Prioritäten,
- aktive Verträge und Konflikte,
- aktuell kontrolliertes Reich,
- Warnungen und zeitkritische Vorgänge.

## Anforderungen an Client und Server

### Client

Der Client stellt Reichslage, Prioritäten, Kapazitäten, Controllerwechsel und Übernahmebericht dar und bestätigt kritische Übergaben bewusst.

### Server

Der Server verwaltet Reichsidentität, Zustände, Controller, Gebiet, Kapazitäten und Prioritäten autoritativ und verhindert Informationsvermischung zwischen Reichen.

## Offene Balancingfragen

1. Welche Verwaltungswerte gehören zum MVP?
2. Wie wird Verwaltungskapazität numerisch berechnet?
3. Welche Regierungsformen gehören zur ersten Version?
4. Welche Reichsprioritäten und Automatisierungen werden angeboten?
5. Welche Auflösungs- oder Nachfolgeregeln benötigt das MVP?

## Akzeptanzkriterien

- Reich, Gebiet, Controller und Account sind getrennte Begriffe.
- Physische lokale Ressourcen werden nicht pauschal reichsweit gemacht.
- Verwaltungsüberlastung wirkt gestuft und sichtbar.
- Controllerwechsel verändert keine Reichsregeln oder laufenden Befehle.
- AI unterliegt denselben Befehlen, Kosten, Zeiten und Wissensgrenzen.
- Reichslebenszyklus und Auflösung sind explizit geregelt.

## Verwandte Dokumente

- [Controller und Reichsübernahme](controller-und-reichsuebernahme.md)
- [Besitz und Kontrolle](../02-galaxy/besitz-und-kontrolle.md)
- [Planeten und Kolonien](../04-planets/planeten-und-kolonien.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
- [Kampagnenstruktur](../11-campaign/kampagnenstruktur.md)
