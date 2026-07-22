# Offline-Fortschritt und Abwesenheit

Status: Freigegeben

## Zweck

Dieses Dokument legt fest, wie sich eine Kampagne bei geschlossenem Client oder längerer Abwesenheit entwickelt und wie der Spieler anschließend informiert wird.

## Grundregel

Das Schließen des Clients stoppt die Simulation nicht. Solange die Kampagne nicht ausdrücklich pausiert ist, schreitet die Kampagnenzeit gemäß ihrem Zeitprofil weiter voran.

Der Online-Status eines Spielers ist keine Spielregel und darf weder Vorteile noch zusätzliche Nachteile auslösen.

## Was während der Abwesenheit weiterläuft

Während einer Abwesenheit dürfen insbesondere fortgesetzt werden:

- bereits angenommene Befehle,
- Bau-, Forschungs-, Reise- und Produktionsvorgänge,
- laufende wirtschaftliche und diplomatische Effekte,
- vorher konfigurierte Routinen und Prioritäten,
- Ereignisse und Zustandsübergänge nach ihren Fachregeln,
- Aktionen anderer Reiche und Controller.

Der konkrete Umfang wird in den jeweiligen Fachsystemen definiert.

## Keine automatische vollständige AI-Übernahme

Das Schließen des Clients oder eine normale Abwesenheit wechselt nicht automatisch den Controller des Reiches.

Stattdessen können später fachlich definierte Hilfen verwendet werden:

- stehende Befehle,
- Prioritäten,
- Grenzwerte,
- delegierte Routinen,
- ausdrücklich aktivierte Vertretungs- oder AI-Übernahme.

Eine vollständige AI-Übernahme erfordert einen sichtbaren Controllerwechsel gemäß dem Controller-Modell.

## Offene Entscheidungen während der Abwesenheit

Nicht jede Entscheidung darf die gesamte Simulation blockieren. Entscheidungen werden daher fachlich in drei Gruppen eingeordnet:

### Ohne Frist

Die Entscheidung bleibt offen, bis der Spieler oder Controller handelt. Andere unabhängige Vorgänge laufen weiter.

### Mit sicherem Standardverhalten

Ist eine Frist erforderlich, muss vorab ein dokumentiertes Standardverhalten gelten, beispielsweise Ablehnen, Beibehalten oder defensives Handeln. Der Standard darf keine versteckte optimale Entscheidung sein.

### Kritisch und unumkehrbar

Schwerwiegende irreversible Entscheidungen benötigen eine angemessene Vorwarnung und ein Reaktionsfenster. Ist keine faire Standardentscheidung möglich, muss das Fachsystem eine andere Schutz- oder Vertretungsregel vorsehen.

## Schutz vor unverhältnismäßigem Schaden

Galaxis garantiert nicht, dass eine abwesende Person keine Nachteile erleidet. Verpasste Chancen, veränderte Markt- oder Diplomatiesituationen und Handlungen anderer Reiche sind Teil einer fortlaufenden Welt.

Es gilt jedoch:

- Kurze Abwesenheit darf nicht regelmäßig zu vollständigem Kontrollverlust führen.
- Bedeutende Bedrohungen sollen möglichst früh erkennbar oder über stehende Regeln behandelbar sein.
- Ein einzelnes sehr kurzes reales Reaktionsfenster darf nicht allein über den Fortbestand eines Reiches entscheiden.
- Schutzmechanismen dürfen nicht stärker sein, nur weil ein Spieler bewusst offline geht.
- Online-Status darf anderen Spielern nicht als taktisch nutzbare Information offengelegt werden.

Konkrete Kriegs-, Belagerungs- und Niederlageregeln werden in späteren Fachbereichen festgelegt.

## Rückkehrbericht

Bei der Rückkehr erhält der Spieler eine serverseitig erzeugte Zusammenfassung seit seinem letzten bestätigten Informationszeitpunkt.

Der Rückkehrbericht enthält mindestens:

- vergangene reale Zeit und fortgeschrittene Kampagnenzeit,
- wesentliche Zustandsveränderungen,
- abgeschlossene, gescheiterte und abgebrochene Befehle,
- automatisch ausgeführte Routinen,
- bedeutende wirtschaftliche Veränderungen,
- neue Kontakte, Konflikte und Ereignisse,
- aktuell offene oder dringende Entscheidungen,
- Hinweise auf unerwartete Abweichungen von gesetzten Zielen.

Routinevorgänge werden zusammengefasst. Der Spieler muss bei Bedarf zu den zugrunde liegenden Details wechseln können.

## Informationszeitpunkt

Der Server speichert, bis zu welchem autoritativen Stand ein Controller die Rückkehrinformationen bestätigt hat. Das bloße Öffnen einer Verbindung darf wichtige Meldungen nicht unbemerkt als gelesen markieren.

## Längere Abwesenheit

Für längere Abwesenheiten sollen Spieler vorab mindestens eine der später fachlich ausgestalteten Möglichkeiten nutzen können:

- ausreichende Befehlswarteschlangen,
- strategische Prioritäten,
- automatisierte Routinegrenzen,
- ausdrückliche AI-Vertretung,
- ausdrückliche Kampagnenpause im Singleplayer.

Welche Möglichkeit verfügbar ist, hängt vom Kampagnentyp und den späteren Systemen ab.

## Missbrauchsschutz

Das Offline-Modell muss insbesondere verhindern:

- Schutz durch absichtliches Trennen der Verbindung,
- wiederholtes Zurücksetzen von Fristen durch erneutes Einloggen,
- doppelte Verarbeitung derselben Offline-Zeit,
- Manipulation durch lokale Uhrzeitänderung,
- Zugriff eines AI- oder Spielercontrollers auf Informationen außerhalb des Reichswissens.

## Anforderungen an Client und Server

### Client

Der Client muss:

- Abwesenheit und Simulation nicht gleichsetzen,
- Rückkehrinformationen priorisiert anzeigen,
- offene Entscheidungen von abgeschlossenen Meldungen trennen,
- vor einer ausdrücklichen Pause oder Controllerübergabe den Status klar anzeigen.

### Server

Der Server muss:

- Fortschritt unabhängig vom Client berechnen,
- Offline-Zeit höchstens einmal verarbeiten,
- Rückkehrinformationen aus autoritativen Änderungen erzeugen,
- Fristen und Standardverhalten nach den jeweiligen Fachregeln auswerten,
- Online-Status nicht als Spielregel verwenden.

## Akzeptanzkriterien

- Client-Schließen und ausdrückliche Pause sind klar getrennt.
- Laufende Befehle können ohne offenen Client fortgesetzt werden.
- Kritische Entscheidungen benötigen Frist, Standardverhalten oder Schutzregel.
- Rückkehrberichte sind aus autoritativen Änderungen ableitbar.
- Das Modell berücksichtigt Frustpotenzial und verhindert taktischen Logout-Schutz.

## Verwandte Dokumente

- [Zeitmodell, Geschwindigkeit und Pause](zeitmodell.md)
- [Typische Spielsitzung und Check-in-Rhythmus](spielsitzung-und-check-in-rhythmus.md)
- [Spieler-, AI- und Reichsübernahmemodell](../03-empires/controller-und-reichsuebernahme.md)
