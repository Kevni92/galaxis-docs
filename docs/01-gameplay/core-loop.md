# Kern-Gameplay-Loop

Status: Freigegeben

## Zweck

Dieses Dokument beschreibt den übergeordneten Ablauf, durch den der Spieler sein Reich wiederholt bewertet, ausrichtet und weiterentwickelt. Detailmechaniken werden in späteren Fachbereichen definiert.

## Der Kernloop

```text
Lage erfassen
→ Ziele und Prioritäten setzen
→ Befehle erteilen
→ Simulation läuft weiter
→ Ergebnisse und Ereignisse auswerten
→ Strategie anpassen
```

## 1. Lage erfassen

Der Spieler erhält eine verständliche Zusammenfassung des aktuellen Reichszustands. Dazu gehören insbesondere:

- wesentliche Veränderungen seit der letzten Sitzung,
- laufende und abgeschlossene Befehle,
- Engpässe, Risiken und Chancen,
- neue Informationen über die Galaxie und andere Reiche,
- Entscheidungen, die Aufmerksamkeit benötigen.

Die Zusammenfassung muss zuerst das Entscheidungsrelevante zeigen und Detailinformationen bei Bedarf zugänglich machen.

## 2. Ziele und Prioritäten setzen

Der Spieler entscheidet, welche Entwicklung für das Reich aktuell wichtig ist. Ziele können verschiedene Zeithorizonte besitzen:

- **kurzfristig:** auf einen Engpass, ein Ereignis oder eine unmittelbare Gefahr reagieren,
- **mittelfristig:** eine Kolonie entwickeln, eine Flotte vorbereiten oder einen Forschungsschwerpunkt verfolgen,
- **langfristig:** das Reich wirtschaftlich, diplomatisch, technologisch oder militärisch ausrichten.

Ziele beschreiben die gewünschte Richtung. Sie ersetzen nicht die konkreten Befehle, können aber Automatisierung und spätere Entscheidungen steuern.

## 3. Befehle erteilen

Der Spieler löst Veränderungen ausschließlich über fachlich definierte Befehle aus. Ein Befehl muss:

- einen erkennbaren Zweck besitzen,
- vor der Annahme serverseitig validiert werden,
- Kosten, Voraussetzungen und erwartbare Folgen sichtbar machen können,
- einen nachvollziehbaren Status besitzen,
- bei zeitabhängiger Ausführung einen eindeutigen Start- und Ergebniszeitpunkt haben.

Menschliche und AI-Controller verwenden dieselben Befehlstypen.

## 4. Simulation läuft weiter

Nach der Befehlserteilung entwickelt sich die Spielwelt autoritativ weiter. Vorgänge können parallel ablaufen, sofern ihre Regeln dies erlauben.

Der Spieler muss nicht anwesend sein, damit gültige Befehle fortgesetzt oder abgeschlossen werden. Der Client ist eine Bedien- und Darstellungsschicht und keine Voraussetzung für die Simulation.

## 5. Ergebnisse und Ereignisse auswerten

Abgeschlossene Vorgänge erzeugen nachvollziehbare Ergebnisse. Neue Ereignisse können zusätzliche Entscheidungen, Risiken oder Möglichkeiten eröffnen.

Rückmeldungen müssen unterscheiden zwischen:

- erfolgreich abgeschlossenen Vorhaben,
- gescheiterten oder abgebrochenen Befehlen,
- automatisch behandelten Routinen,
- unerwarteten Veränderungen,
- Entscheidungen, die noch offen sind.

## 6. Strategie anpassen

Der Spieler vergleicht Ergebnisse mit den gesetzten Zielen und passt Prioritäten, Befehle oder langfristige Ausrichtung an. Damit beginnt der Loop erneut.

## Zeitebenen des Loops

### Operativer Loop

Reaktion auf aktuelle Informationen, Abschluss einzelner Befehle und kurzfristige Korrekturen.

### Entwicklungsloop

Aufbau und Abstimmung von Kolonien, Wirtschaft, Forschung, Flotten und Beziehungen über mehrere Sitzungen hinweg.

### Kampagnenloop

Langfristige Formung des Reiches, Umgang mit anderen Reichen sowie Fortschritt in Richtung Endgame und Kampagnenabschluss.

Alle späteren Systeme müssen mindestens einer dieser Ebenen zugeordnet werden können.

## Anforderungen an Client und Server

### Client

Der Client muss:

- Veränderungen seit der letzten Sitzung zusammenfassen,
- Ziele, Prioritäten, Befehle und Ergebnisse unterscheidbar darstellen,
- dringende Entscheidungen von langfristigen Hinweisen trennen,
- den Wechsel zwischen Übersicht und Details ermöglichen.

### Server

Der Server muss:

- Befehle autoritativ validieren,
- zeitabhängige Vorgänge unabhängig vom Client fortführen,
- Ergebnisse und relevante Ursachen protokollierbar machen,
- denselben Spielzustand für Spieler- und AI-Controller verwenden.

## Nicht durch dieses Dokument festgelegt

Dieses Dokument entscheidet noch nicht:

- konkrete Befehle einzelner Systeme,
- genaue Zeitgeschwindigkeit und Dauer von Vorgängen,
- konkrete UI-Ansichten,
- Anzahl oder Art möglicher Reichsziele,
- konkrete Ereignis- und Benachrichtigungsregeln.

## Akzeptanzkriterien

- Der Loop funktioniert ohne permanente Anwesenheit.
- Information, Zielsetzung, Befehl, Simulation und Rückmeldung sind getrennt.
- Kurz-, mittel- und langfristige Entscheidungen sind eingeordnet.
- Spätere Fachsysteme können in eine der Loop-Ebenen eingeordnet werden.

## Verwandte Dokumente

- [Spielvision von Galaxis](../00-vision/game-vision.md)
- [Zielgruppe und gewünschtes Spielerlebnis](../00-vision/zielgruppe-und-spielerlebnis.md)
- [Typische Spielsitzung und Check-in-Rhythmus](spielsitzung-und-check-in-rhythmus.md)
