# Zielgruppe und gewünschtes Spielerlebnis

Status: Review

## Zweck

Dieses Dokument beschreibt, für welche Spieler **Galaxis** gedacht ist und welche Nutzungssituation bei späteren Designentscheidungen berücksichtigt werden muss. Es legt keine konkreten Sitzungszeiten, UI-Abläufe oder Detailmechaniken fest.

## Primäre Zielgruppe

Galaxis richtet sich primär an Spieler, die:

- langfristige Strategie und den Aufbau eines eigenen Reiches mögen,
- Entscheidungen mit spürbaren mittel- und langfristigen Folgen bevorzugen,
- nicht dauerhaft online sein oder das Spiel ständig beobachten möchten,
- komplexe Zusammenhänge verstehen und gestalten wollen, ohne jede Routine einzeln verwalten zu müssen,
- kurze Lageprüfungen ebenso nutzen möchten wie längere Planungssitzungen,
- Wert auf eine nachvollziehbare Spielwelt, Reichsgeschichte und strategische Entwicklung legen.

Die primäre Zielgruppe soll Galaxis regelmäßig spielen können, ohne dass tägliche lange Sitzungen oder ständige Reaktionsbereitschaft erforderlich sind.

## Sekundäre Zielgruppe

Galaxis soll auch Spielern Raum geben, die intensiver planen und optimieren möchten. Diese Spieler können sich tiefer mit Wirtschaft, Flotten, Forschung, Diplomatie und langfristiger Reichsplanung beschäftigen.

Intensives Spielen soll zusätzliche Einsicht, bessere Planung und bewusstere Entscheidungen ermöglichen. Es darf jedoch nicht allein dadurch überlegen sein, dass ein Spieler das Spiel wesentlich häufiger kontrolliert oder Routinehandlungen fortlaufend manuell wiederholt.

## Nicht primär angesprochene Spieler

Galaxis richtet sich nicht primär an Spieler, die:

- reflexbasierte oder taktische Echtzeitsteuerung suchen,
- einen dauerhaften Aufmerksamkeits- und Anwesenheitswettbewerb erwarten,
- hauptsächlich durch häufiges Wiederholen kleiner Eingaben Fortschritt erzielen möchten,
- eine ausschließlich lineare oder sehr kurze Einzelspielerkampagne suchen,
- vollständige Kontrolle über jede kleinste Routinehandlung als zentralen Spielreiz benötigen.

Diese Abgrenzung schließt einzelne schnelle oder detailreiche Elemente nicht aus. Sie dürfen jedoch nicht die grundlegende Nutzungssituation des Spiels bestimmen.

## Gelegenheitsspiel und Intensivspiel

### Gelegenheitsspiel

Ein Gelegenheitsspieler soll nach einer Abwesenheit schnell erkennen können:

- was im Reich geschehen ist,
- welche Entscheidungen anstehen,
- welche Befehle noch laufen,
- welche Probleme dringend und welche nur langfristig relevant sind.

Eine kurze Spielsitzung soll einen sinnvollen Beitrag zur Entwicklung des Reiches leisten können. Die genaue Häufigkeit und Dauer solcher Sitzungen wird separat festgelegt.

### Intensivspiel

Ein Intensivspieler soll zusätzliche Zeit sinnvoll für folgende Tätigkeiten verwenden können:

- verschiedene langfristige Strategien vergleichen,
- Zusammenhänge und Prognosen analysieren,
- mehrere Reichsbereiche aufeinander abstimmen,
- Alternativen für Diplomatie, Forschung oder Expansion vorbereiten,
- vergangene Entwicklungen und zukünftige Risiken bewerten.

Mehr Spielzeit soll vor allem mehr Planungstiefe ermöglichen, nicht bloß mehr notwendige Klicks.

## Gewünschte Balance zwischen Kontrolle und Automatisierung

Der Spieler soll die strategische Richtung seines Reiches kontrollieren. Dazu gehören insbesondere Ziele, Prioritäten, Spezialisierungen, bedeutende Befehle und Reaktionen auf neue Situationen.

Wiederkehrende oder eindeutig ableitbare Routinen sollen automatisierbar, delegierbar oder gebündelt darstellbar sein. Automatisierung darf keine verborgene zweite Spielregel erzeugen und soll jederzeit verständlich machen, welche Vorgaben sie verfolgt.

Der genaue Umfang, die Konfiguration und die Grenzen der Automatisierung werden in späteren Fachbereichen festgelegt.

## Gewünschte Belastung des Spielers

Galaxis soll strategisch anspruchsvoll sein, aber keine dauerhafte Überwachung verlangen. Die Belastung soll vor allem aus bewussten Entscheidungen entstehen, nicht aus:

- ständigem Prüfen von Timern,
- wiederholten Bestätigungen ohne echte Wahl,
- versteckten oder schwer nachvollziehbaren Folgen,
- vermeidbarer Kleinstverwaltung,
- künstlichem Zeitdruck außerhalb ausdrücklich dafür vorgesehener Situationen.

Neue oder zurückkehrende Spieler sollen die aktuelle Lage ihres Reiches schrittweise verstehen können. Detailinformationen sollen verfügbar sein, ohne dass sie für jede grundlegende Entscheidung vollständig gelesen werden müssen.

## Konsequenzen für spätere Systeme

Aus dieser Zielgruppe ergeben sich folgende Anforderungen für spätere Fachkonzepte:

- Spielzustände und Veränderungen müssen verständlich zusammengefasst werden können.
- Laufende Befehle, Prioritäten und erwartbare Ergebnisse müssen sichtbar bleiben.
- Systeme müssen sowohl kurze Eingriffe als auch vertiefte Planung unterstützen.
- Routineaufgaben dürfen den strategischen Kern nicht verdrängen.
- Abwesenheit und Rückkehr müssen bei Zeitmodell, Ereignissen, Konflikten und Benachrichtigungen ausdrücklich berücksichtigt werden.
- Informationen sollen in Ebenen angeboten werden: zuerst entscheidungsrelevant, bei Bedarf detaillierter.
- AI- und Automatisierungssysteme müssen nachvollziehbare Ziele und Grenzen besitzen.

Diese Punkte sind Anforderungen an die spätere Ausgestaltung, aber noch keine vollständigen Regeln für die jeweiligen Systeme.

## Nicht durch dieses Dokument festgelegt

Dieses Dokument entscheidet noch nicht:

- wie häufig Spieler idealerweise einchecken,
- wie lang kurze oder lange Spielsitzungen konkret dauern,
- wie schnell die Spielzeit vergeht,
- welche Folgen eine längere Abwesenheit haben kann,
- welche Routinen im Einzelnen automatisiert werden,
- wie stark intensive Planung messbare Vorteile erzeugen darf,
- wie Einsteigerführung und konkrete Benutzeroberfläche aussehen.

Diese Fragen werden in den nachfolgenden D1-Issues und späteren Fachbereichen geklärt.

## Akzeptanzkriterien

- Die primäre Zielgruppe ist eindeutig benannt.
- Gelegenheitsspiel und Intensivspiel sind voneinander abgegrenzt.
- Die gewünschte Balance zwischen strategischer Kontrolle und Routineautomatisierung ist beschrieben.
- Konsequenzen für spätere Spielsysteme sind sichtbar.
- Konkrete Sitzungszeiten und Detailmechaniken werden nicht vorweggenommen.

## Verwandte Dokumente

- [Spielvision von Galaxis](game-vision.md)
- [Vision – Übersicht](README.md)
- [Gameplay – Übersicht](../01-gameplay/README.md)
