# Zeitmodell, Geschwindigkeit und Pause

Status: Review

## Zweck

Dieses Dokument definiert das gemeinsame Zeitfundament für Simulation, Befehle, Ereignisse und Offline-Fortschritt.

## Autoritative Kampagnenzeit

Jede Kampagne besitzt genau eine serverautoritative **Kampagnenzeit**. Der Client zeigt diese Zeit an, bestimmt sie aber nicht.

Bei laufender Kampagne ergibt sich die Kampagnenzeit aus:

```text
vergangene reale Zeit × festgelegter Geschwindigkeitsfaktor der Kampagne
```

Der Geschwindigkeitsfaktor wird durch das bei Kampagnenstart gewählte Zeitprofil festgelegt. Das Standardprofil wird auf den vorgesehenen täglichen Check-in-Rhythmus abgestimmt. Konkrete Umrechnungswerte können beim Balancing festgelegt werden, ohne das Zeitmodell zu verändern.

## Zeitprofile

Eine Kampagne kann bei ihrer Erstellung ein unterstütztes Zeitprofil erhalten, beispielsweise entspannt, standard oder schnell.

Dabei gilt:

- Das Zeitprofil ist eine Kampagneneigenschaft.
- Es gilt einheitlich für alle Reiche und Controller der Kampagne.
- Es darf nach Kampagnenstart nicht beiläufig verändert werden.
- Eine spätere Änderung benötigt eine ausdrückliche Host- oder Administrationsaktion und muss protokolliert werden.
- Spielregeln und Dauern werden in Kampagnenzeit formuliert und nicht für jedes Profil neu definiert.

## Singleplayer-Pause

Im Singleplayer darf der Spieler die Kampagne ausdrücklich pausieren.

Während einer Pause:

- schreitet die Kampagnenzeit nicht fort,
- werden keine zeitabhängigen Vorgänge abgeschlossen,
- laufen keine Fristen ab,
- werden keine neuen zeitgesteuerten Ereignisse ausgelöst,
- bleiben bereits erteilte Befehle und Zustände erhalten.

Das Schließen des Clients ist **keine Pause**. Eine Pause muss bewusst ausgelöst und als Kampagnenzustand gespeichert werden.

## Geschwindigkeitsänderungen

Das grundlegende asynchrone Modell benötigt im MVP nur:

- `pausiert`,
- `laufend mit dem festgelegten Zeitprofil`.

Freies Beschleunigen oder Verlangsamen während einer laufenden Kampagne ist kein notwendiger Bestandteil des MVP. Eine spätere Singleplayer-Beschleunigung darf nur ergänzt werden, wenn sie deterministisch bleibt und keine zweite Regelbasis erzeugt.

## Späterer Multiplayer

In einer Kampagne mit mehreren menschlichen Spielern gilt:

- kein einzelner Spieler kann die Kampagne pausieren,
- das gemeinsame Zeitprofil gilt für alle,
- Controllerwechsel verändern die Kampagnenzeit nicht,
- Host- oder Administrationspausen müssen für alle sichtbar und protokolliert sein.

Damit verwendet Singleplayer dasselbe Zeitmodell; er besitzt lediglich zusätzliche Berechtigung zur ausdrücklichen Pause.

## Zeitabhängige Befehle

Jeder zeitabhängige Befehl besitzt mindestens:

- einen autoritativen Annahmezeitpunkt,
- einen Startzeitpunkt,
- eine Dauer oder einen Zielzeitpunkt,
- einen Status,
- eindeutig definierte Bedingungen für Abschluss, Abbruch oder Verzögerung.

Dauern werden in Kampagnenzeit angegeben. Der Client darf Abschlusszeiten berechnen und anzeigen, die verbindliche Auswertung erfolgt jedoch auf dem Server.

## Parallele Vorgänge

Mehrere Vorgänge dürfen parallel laufen, sofern ihre Fachregeln dies erlauben. Konflikte werden nicht durch zufällige Reihenfolge im Programm gelöst, sondern durch eine stabile Auswertungsordnung.

Für Vorgänge mit gleichem Zeitstempel verwendet der Server einen deterministischen Tie-Breaker, beispielsweise eine fortlaufende autoritative Ereignisnummer.

## Offline-Nachholung

War der Serverprozess im Singleplayer nicht aktiv, wird beim nächsten Start die seit dem letzten autoritativen Speicherzeitpunkt vergangene reale Zeit ermittelt und in Kampagnenfortschritt umgerechnet.

Dabei gilt:

- pausierte Zeit wird nicht nachgeholt,
- dieselbe Ausgangslage und derselbe Zeitabstand müssen dasselbe Ergebnis liefern,
- technische Verarbeitung in größeren Schritten darf das fachliche Ergebnis nicht verändern,
- alle relevanten Ergebnisse müssen für den Rückkehrbericht rekonstruierbar sein.

## Zeitstempel und Zeitzonen

Autoritative Zeitstempel werden unabhängig von der lokalen Zeitzone gespeichert. Lokale Darstellung ist Aufgabe des Clients. Sommerzeit oder eine Änderung der Geräteeinstellung darf die Simulation nicht beeinflussen.

## Fristen und Reaktionsfenster

Spielinterne Fristen werden grundsätzlich in Kampagnenzeit definiert. Eine Singleplayer-Pause stoppt daher auch diese Fristen.

Schwerwiegende irreversible Folgen benötigen angemessene Vorwarnung und Reaktionsfenster. Die konkrete Länge wird im jeweiligen Fachsystem festgelegt.

## Anforderungen an Client und Server

### Client

Der Client muss:

- Kampagnenzeit und Zustand `pausiert` oder `laufend` klar anzeigen,
- erwartete Abschlusszeitpunkte nachvollziehbar darstellen,
- veraltete lokale Zeitprognosen nach Serverantwort korrigieren,
- niemals allein durch die lokale Uhr Spielzustände abschließen.

### Server

Der Server muss:

- die einzige autoritative Kampagnenuhr führen,
- Pause und Zeitprofil persistent speichern,
- Ereignisse deterministisch ordnen,
- Offline-Nachholung reproduzierbar auswerten,
- Zeitänderungen und Administrationspausen protokollieren.

## Akzeptanzkriterien

- Singleplayer-Pause und Client-Schließen sind eindeutig voneinander getrennt.
- Alle Zeitprofile verwenden dieselben fachlichen Dauern in Kampagnenzeit.
- Das Modell ist auf späteren Multiplayer ohne zweite Simulationslogik übertragbar.
- Zeitabhängige Befehle und gleichzeitige Ereignisse sind deterministisch formulierbar.
- Offline-Nachholung kann unabhängig von der Verarbeitungsgeschwindigkeit reproduziert werden.

## Verwandte Dokumente

- [Typische Spielsitzung und Check-in-Rhythmus](spielsitzung-und-check-in-rhythmus.md)
- [Offline-Fortschritt und Abwesenheit](offline-fortschritt-und-abwesenheit.md)
- [Kern-Gameplay-Loop](core-loop.md)
