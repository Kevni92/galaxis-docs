# Spieler-, AI- und Reichsübernahmemodell

Status: Review

## Zweck

Dieses Dokument definiert, wie ein Reich durch einen menschlichen Spieler oder eine AI kontrolliert wird und wie ein Controllerwechsel abläuft. Es beschreibt keine konkrete AI-Implementierung.

## Begriffe

- **Reich:** fachliche Spielentität mit eigenem Zustand, Wissen, Befehlen und Beziehungen.
- **Controller:** autorisierte Instanz, die für ein Reich fachliche Befehle auswählt und erteilt.
- **Spielercontroller:** Controller, dessen Entscheidungen von einem menschlichen Spieler stammen.
- **AI-Controller:** Controller, dessen Entscheidungen durch ein automatisiertes System ausgewählt werden.
- **Controllerwechsel:** autoritative Änderung, welcher Controller neue Befehle für ein Reich erteilen darf.
- **Eigentum:** dauerhafte Zuordnung eines Accounts oder Kampagnenteilnehmers, sofern ein Kampagnentyp dies vorsieht. Eigentum und aktive Kontrolle sind getrennte Begriffe.

## Grundregeln

- Jedes aktive Reich besitzt zu einem Zeitpunkt höchstens einen primären Controller.
- Der Server speichert die autoritative Controllerzuordnung.
- Spieler- und AI-Controller verwenden dieselben fachlichen Befehle.
- Jeder Befehl wird unabhängig vom Controllertyp nach denselben Voraussetzungen und Regeln validiert.
- Ein Controller erhält nur Informationen, die dem Wissen seines Reiches entsprechen.
- Ein Controllerwechsel verändert weder Spielwerte noch Regeln des Reiches.

## Controllerarten

### Spielercontroller

Ein Spielercontroller darf Befehle für das zugeordnete Reich erteilen, solange:

- die Zuordnung gültig ist,
- die Kampagne den Spieler zur Kontrolle berechtigt,
- keine Übergabe oder Sperre aktiv ist.

Das Schließen des Clients beendet die Zuordnung nicht automatisch.

### AI-Controller

Ein AI-Controller darf dieselben veröffentlichten Befehlstypen verwenden wie ein Spielercontroller.

Interne Ziele, Bewertungen oder Pläne der AI sind keine Spielregeln. Sie dürfen die Auswahl gültiger Befehle beeinflussen, aber keine Validierung umgehen oder geheime Informationen bereitstellen.

Inhalte unter `ideas/`, einschließlich möglicher LLM-Ansätze, sind für dieses Modell nicht verbindlich.

### Kein aktiver Befehlsgeber

Ein Reich kann vorübergehend keinen neuen Befehlsgeber besitzen, wenn dies durch einen Kampagnentyp ausdrücklich vorgesehen ist. Bereits angenommene Befehle und autorisierte Routinen laufen weiter.

Dieser Zustand darf nicht stillschweigend durch einen Verbindungsabbruch entstehen.

## Befehle und laufende Vorgänge beim Controllerwechsel

Ein Controllerwechsel löscht keine bereits autoritativ angenommenen Befehle.

Es gilt:

- laufende Befehle behalten Status, Kosten und Abschlusszeitpunkt,
- Befehlswarteschlangen bleiben bestehen,
- der neue Controller darf Befehle nur nach deren normalen Regeln ändern oder abbrechen,
- bereits eingetretene Ergebnisse werden nicht zurückgesetzt,
- laufende Verträge, Verpflichtungen und Konflikte bleiben gültig,
- der Wechsel selbst erzeugt keine kostenlosen Abbrüche oder Rückerstattungen.

## Strategische Ziele und Automatisierung

Strategische Ziele, Prioritäten und Automatisierungsregeln werden getrennt von einzelnen Befehlen gespeichert.

Bei einem Wechsel von AI zu Spieler:

- stoppt die AI, neue Entscheidungen für das Reich zu erzeugen,
- bestehende gültige Befehle bleiben erhalten,
- aktive Prioritäten und Automatisierungen werden dem Spieler angezeigt,
- der Spieler kann sie nach ihren normalen Regeln bestätigen, ändern oder deaktivieren.

Bei einem Wechsel von Spieler zu AI:

- bleiben bestehende gültige Befehle erhalten,
- erhält die AI nur die freigegebenen Reichsinformationen,
- kann die AI bestehende Prioritäten berücksichtigen,
- darf die AI keine vom Spieler nicht autorisierten geheimen Metainformationen verwenden.

## Übernahmebericht

Ein neuer Controller erhält einen autoritativen Übernahmebericht. Dieser soll mindestens enthalten:

- aktuellen Zustand und wichtigste Veränderungen des Reiches,
- laufende und wartende Befehle,
- aktive Prioritäten, Routinen und Automatisierungen,
- wirtschaftliche Engpässe und unmittelbare Risiken,
- bekannte diplomatische Verpflichtungen und Konflikte,
- wichtige kürzlich getroffene Entscheidungen,
- offene oder zeitkritische Vorgänge.

Der Bericht darf nur Informationen enthalten, die das Reich selbst kennt.

## Übernahme eines AI-Reiches durch einen Spieler

Eine spätere Multiplayer-Kampagne kann einem Spieler erlauben, ein bisher AI-gesteuertes Reich zu übernehmen.

Die Übernahme muss:

1. durch den Server autorisiert werden,
2. einen eindeutig bestimmten Wirksamkeitszeitpunkt besitzen,
3. den bisherigen AI-Controller für neue Befehle deaktivieren,
4. bereits angenommene Befehle beibehalten,
5. einen Übernahmebericht erzeugen,
6. für andere betroffene Systeme protokolliert werden.

Die Übernahme darf dem Spieler keine Informationen aus zuvor kontrollierten oder beobachteten Reichen übertragen.

## Rückgabe oder Verlassen eines Reiches

Verlässt ein Spieler eine laufende Kampagne, darf das Reich nach einer kampagnenspezifischen Regel an einen AI-Controller übergeben werden.

Dabei gilt:

- ein bloßer Verbindungsverlust löst keine sofortige dauerhafte Rückgabe aus,
- eine bewusste Übergabe ist klar zu bestätigen,
- eine automatische Übergabe nach längerer Abwesenheit benötigt eine bekannte Frist,
- laufende Befehle bleiben erhalten,
- andere Spieler erhalten keine Information, die den Online-Status taktisch offenlegt,
- die Übergabe darf nicht als Schutz vor bereits laufenden Gefahren verwendet werden.

Konkrete Fristen und Rechte werden beim späteren Multiplayer-Konzept festgelegt.

## Singleplayer

Im Singleplayer kontrolliert der menschliche Spieler mindestens ein Reich; andere Reiche können durch AI-Controller gesteuert werden.

Der Singleplayer verwendet dieselbe Controllerzuordnung und dieselben Befehle wie eine spätere Multiplayer-Kampagne. Zusätzliche Singleplayer-Rechte wie das Pausieren der Kampagne gehören zum Kampagnentyp, nicht zum Spielercontroller selbst.

Ein später optionaler Wechsel auf ein anderes Reich muss als ausdrücklicher Controllerwechsel behandelt werden und darf keine Reichsinformationen vermischen.

## Späterer Multiplayer

Im Multiplayer können mehrere Reiche gleichzeitig jeweils eigene Spieler- oder AI-Controller besitzen.

Für jeden Wechsel gelten dieselben atomaren Regeln. Es darf keinen Zeitraum geben, in dem zwei primäre Controller widersprüchliche neue Befehle mit gleicher Berechtigung erteilen können.

Anfragen, die vor dem Wechsel abgesendet, aber erst danach beim Server eintreffen, werden anhand des autoritativen Annahmezeitpunkts und der dann gültigen Berechtigung bewertet.

## Protokollierung

Jeder Controllerwechsel muss mindestens protokollieren:

- betroffenes Reich,
- bisherigen und neuen Controllertyp,
- autorisierende Instanz,
- Wirksamkeitszeitpunkt,
- Grund oder Wechselart,
- Ergebnis der Übergabe.

Interne AI-Gedankenketten oder vollständige private Planungsdaten müssen nicht gespeichert werden. Fachliche Ziele, Befehle und sichtbare Begründungen können gespeichert werden, sofern sie für Spiel und Nachvollziehbarkeit erforderlich sind.

## Anforderungen an Client und Server

### Client

Der Client muss:

- das aktuell kontrollierte Reich eindeutig anzeigen,
- bei Übernahme einen priorisierten Bericht bereitstellen,
- bestehende Befehle und Automatisierungen sichtbar machen,
- Übergabe und Rückgabe bewusst bestätigen lassen,
- keine Befehle als angenommen darstellen, bevor der Server sie autorisiert hat.

### Server

Der Server muss:

- Controllerzuordnungen autoritativ verwalten,
- jeden Befehl gegen die aktuelle Zuordnung validieren,
- Controllerwechsel atomar durchführen,
- laufende Befehle unverändert erhalten,
- Reichswissen strikt vom Controller und dessen vorherigen Rollen trennen,
- Wechsel und Übergaben protokollieren.

## Akzeptanzkriterien

- Spieler- und AI-Controller verwenden dieselben fachlichen Befehle.
- Controllerwechsel verändern keine Spielregeln oder laufenden Vorgänge.
- AI-Pläne sind von autoritativen Befehlen getrennt.
- Eine AI-Reichsübernahme erzeugt einen begrenzten Übernahmebericht.
- Singleplayer und späterer Multiplayer verwenden dasselbe Grundmodell.
- Verbindungsabbruch und ausdrückliche Controllerübergabe sind getrennt.

## Verwandte Dokumente

- [Offline-Fortschritt und Abwesenheit](../01-gameplay/offline-fortschritt-und-abwesenheit.md)
- [Zeitmodell, Geschwindigkeit und Pause](../01-gameplay/zeitmodell.md)
- [Kampagnenstruktur, Dauer, Sieg und Niederlage](../11-campaign/kampagnenstruktur.md)
- [Arbeitsregeln für KI-Agenten](../../AGENTS.md)
