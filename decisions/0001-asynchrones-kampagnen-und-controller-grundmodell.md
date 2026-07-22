# 0001 – Asynchrones Kampagnen- und Controller-Grundmodell

Status: angenommen

Datum: 2026-07-22

## Kontext

Galaxis soll langfristige strategische Tiefe bieten, ohne permanente Anwesenheit zu verlangen. Gleichzeitig müssen Singleplayer, spätere Spielerübernahmen von AI-Reichen, Offline-Fortschritt und zeitabhängige Befehle auf derselben fachlichen Grundlage funktionieren.

## Entscheidung

Für Galaxis gilt folgendes gemeinsames Grundmodell:

1. Der vorgesehene Nutzungsrhythmus ist ein sinnvoller täglicher Check-in ohne Anwesenheitspflicht.
2. Jede Kampagne besitzt eine serverautoritative Kampagnenzeit mit einem bei Kampagnenstart festgelegten Zeitprofil.
3. Im Singleplayer ist eine ausdrückliche Pause möglich; das Schließen des Clients pausiert die Kampagne nicht.
4. Gültige Befehle und die Simulation laufen während Abwesenheit weiter. Rückkehrinformationen werden serverseitig zusammengefasst.
5. Die Standardkampagne zielt auf ungefähr zwölf reale Wochen; ein sinnvoller Bereich liegt bei etwa acht bis sechzehn Wochen.
6. Spieler- und AI-Controller verwenden dieselben fachlichen Befehle und unterliegen denselben Spielregeln.
7. Controllerwechsel verändern weder laufende Befehle noch Reichszustand, Reichswissen oder Kampagnenzeit.

## Begründung

Dieses Modell verbindet die langfristige Entwicklung eines asynchronen Browser-Strategiespiels mit der strategischen Tiefe eines Weltraum-Grand-Strategy-Spiels. Es verhindert, dass der Client zur Voraussetzung für die Simulation wird, und ermöglicht spätere Multiplayer-Erweiterungen ohne zweite Regellogik.

Der tägliche Zielrhythmus gibt Balancing, Informationsmenge und Reaktionsfenstern eine gemeinsame Orientierung. Die Kampagnendauer ist lang genug für Reichsgeschichte und strategische Entwicklung, bleibt aber auf einen abgeschlossenen Fortschrittsbogen ausgerichtet.

## Betrachtete Alternativen

### Dauerhaft pausierender Singleplayer bei geschlossenem Client

Dies würde Offline-Fortschritt verhindern und das asynchrone Grundkonzept aufheben. Spätere AI-Reichsübernahmen und Multiplayer-Kampagnen würden eine abweichende Simulationslogik benötigen.

### Permanente Echtzeit ohne Singleplayer-Pause

Dies wäre technisch einheitlich, würde aber die Kontrolle über private Singleplayer-Kampagnen unnötig einschränken. Die ausdrückliche Pause kann als Kampagnenberechtigung umgesetzt werden, ohne das Zeitmodell zu verändern.

### Unterschiedliche Befehle oder Vorteile für AI-Reiche

Dies könnte kurzfristig einfacher wirken, würde aber Tests, Balancing, Reichsübernahmen und Nachvollziehbarkeit verschlechtern.

### Endlose Kampagne ohne formalen Abschluss

Dies würde langfristigen Fortschritt primär auf Wachstum und Ranglisten reduzieren. Ein ungefähr zwölfwöchiger Zielbogen ermöglicht Endgame, Rückblick und neue Kampagnen, während optionales ungewertetes Weiterspielen möglich bleibt.

## Positive Folgen

- Gemeinsame Grundlage für Singleplayer und späteren Multiplayer.
- Klare Anforderungen an Zeit, Persistenz, Rückkehrberichte und Befehlsausführung.
- AI-Reiche können ohne Regelwechsel von Spielern übernommen werden.
- Balancing kann auf einen bekannten Check-in- und Kampagnenrhythmus ausgerichtet werden.
- Client und Server können unabhängig gegen dieselben fachlichen Regeln getestet werden.

## Negative Folgen und Risiken

- Offline-Nachholung und deterministische Ereignisreihenfolge erhöhen die Anforderungen an den Server.
- Konflikte und irreversible Ereignisse benötigen sorgfältig gestaltete Reaktionsfenster.
- Ein Zeitprofil muss bei Kampagnenstart sinnvoll gewählt werden; spätere Änderungen sind aufwendig.
- Automatisierung und Rückkehrberichte werden für längere Abwesenheiten zu wichtigen Pflichtsystemen.
- Die angestrebte Kampagnendauer muss später durch Balancing bestätigt werden.

## Betroffene Dokumente

- [Spielvision](../docs/00-vision/game-vision.md)
- [Zielgruppe und Spielerlebnis](../docs/00-vision/zielgruppe-und-spielerlebnis.md)
- [Designprinzipien und Nicht-Ziele](../docs/00-vision/designprinzipien-und-nicht-ziele.md)
- [Kern-Gameplay-Loop](../docs/01-gameplay/core-loop.md)
- [Spielsitzung und Check-in-Rhythmus](../docs/01-gameplay/spielsitzung-und-check-in-rhythmus.md)
- [Zeitmodell](../docs/01-gameplay/zeitmodell.md)
- [Offline-Fortschritt und Abwesenheit](../docs/01-gameplay/offline-fortschritt-und-abwesenheit.md)
- [Controller und Reichsübernahme](../docs/03-empires/controller-und-reichsuebernahme.md)
- [Kampagnenstruktur](../docs/11-campaign/kampagnenstruktur.md)

## Ersetzt

keine

## Ersetzt durch

keine
