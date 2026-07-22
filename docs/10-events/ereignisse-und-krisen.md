# Ereignisse, Anomalien und Krisen

Status: Review

## Zweck

Dieses Dokument definiert das allgemeine Ereignissystem, Spielerentscheidungen, Ereignisfolgen, Anomalien sowie regionale und galaktische Krisen.

## Ereignisdefinition und Ereignisinstanz

Eine Ereignisdefinition ist statische Spieldatenbeschreibung. Eine Ereignisinstanz ist ein konkretes Auftreten in einer Kampagne.

Eine Definition enthält mindestens:

- stabile Definitions-ID und Version,
- Auslösebedingungen,
- zulässige Ziele,
- Sichtbarkeitsregeln,
- Schritte und Entscheidungen,
- mögliche Folgen,
- Wiederholungs- und Ausschlussregeln,
- Abbruch- und Abschlussbedingungen.

Eine Instanz enthält mindestens:

- stabile Instanz-ID,
- Definitionsversion,
- betroffene Kampagne und Entitäten,
- Auslösezeitpunkt,
- aktuellen Schritt und Status,
- bekannte Informationen je Reich,
- Entscheidungsfrist,
- gewählte oder automatisch angewandte Option,
- bereits ausgeführte Folgen.

## Deterministische Auslösung

Der Server prüft Ereignisbedingungen in einer stabilen Reihenfolge. Zufällige Auslösung verwendet ausschließlich serverseitigen, reproduzierbaren Zufall mit gespeichertem Kontext.

Ein Ereignis darf nicht mehrfach ausgelöst werden, nur weil derselbe Zeitraum technisch in kleineren Schritten verarbeitet wurde. Einmaligkeits- und Abklingregeln werden pro Kampagne, Reich oder Ziel gespeichert.

## Ereignisziele

Ereignisse können sich richten an:

- ein Reich,
- eine Kolonie oder Bevölkerungsgruppe,
- ein System oder Himmelsobjekt,
- eine Flotte oder einen Kampf,
- mehrere Reiche,
- die gesamte Kampagne.

Ziele werden über stabile IDs referenziert. Wird ein Ziel ungültig, greift eine definierte Abbruch-, Ersatz- oder Abschlussregel.

## Sichtbarkeit

Ein Ereignis darf nur Informationen anzeigen, die das betroffene Reich kennt oder durch das Ereignis ausdrücklich erfährt.

Es wird unterschieden zwischen:

- öffentlichem Ereignis,
- nur beteiligten Reichen bekanntem Ereignis,
- verborgenem Fortschritt,
- unbekannter Ursache mit sichtbarer Folge.

Verborgene Folgen dürfen existieren, müssen aber später durch beobachtbare Ursachen oder Entdeckungen nachvollziehbar werden. Technische IDs oder Optionen dürfen keine Geheimnisse vorwegnehmen.

## Ereignisschritte

Ein mehrstufiges Ereignis ist eine Zustandsmaschine. Jeder Schritt definiert:

- Eintrittsbedingungen,
- angezeigte Informationen,
- verfügbare Entscheidungen,
- Frist und Standardentscheidung,
- unmittelbare Folgen,
- nächsten Schritt oder Abschluss.

Bereits ausgeführte Schritte werden nicht erneut angewandt. Die Verarbeitung muss idempotent sein.

## Spielerentscheidungen

Eine Entscheidung ist ein fachlicher Befehl mit Instanz-ID und Options-ID. Der Server prüft:

- Controllerberechtigung,
- Wissen und Beteiligung,
- aktuellen Schritt,
- Voraussetzungen und Kosten,
- Frist,
- ob bereits entschieden wurde.

Optionen zeigen bekannte unmittelbare Folgen und bekannte Risiken. Unsichere oder verborgene Folgen werden als solche gekennzeichnet, nicht als exakte Werte vorgetäuscht.

## Fristen und Standardentscheidung

Entscheidungsfristen werden in Kampagnenzeit geführt und müssen zum Check-in-Rhythmus passen.

Bei Ablauf gilt eine in der Ereignisdefinition festgelegte Standardentscheidung. Sie soll grundsätzlich:

- den bisherigen Zustand erhalten,
- die defensivste zulässige Option wählen,
- oder den Vorgang ohne zusätzlichen Vorteil abbrechen.

Eine Standardentscheidung darf keine überraschende freiwillige Kriegserklärung, dauerhafte Gebietsabtretung oder unverhältnismäßige Ressourcenausgabe auslösen.

## Folgen

Ereignisfolgen werden atomar und ausschließlich über veröffentlichte fachliche Operationen angewandt. Mögliche Folgen sind:

- Ressourcen- oder Finanzbuchungen,
- Zustands- und Modifikatoränderungen,
- neue Befehle oder Projekte,
- Wissen und Entdeckungen,
- Beziehungen und Verträge,
- Bevölkerung, Kolonien oder Flotten,
- weitere Ereignisschritte.

Eine Folge muss Ziel, Betrag oder Zustand, Wirksamkeitszeitpunkt und Dauer eindeutig definieren. Ereignisse dürfen keine Validierungsregeln anderer Systeme umgehen.

## Wiederholbarkeit

Eine Ereignisdefinition legt fest, ob sie:

- einmal pro Kampagne,
- einmal pro Reich,
- einmal pro Ziel,
- nach Abklingzeit,
- oder unbegrenzt wiederholbar ist.

Wiederholbare Ereignisse benötigen Variation oder strategische Bedeutung und dürfen nicht als häufige belanglose Benachrichtigung auftreten.

## Anomalien

Eine Anomalie ist ein räumlich gebundenes besonderes Untersuchungsobjekt. Sie besitzt:

- stabile ID und Standort,
- Entdeckungsbedingungen,
- bekannte und verborgene Eigenschaften,
- Untersuchungsanforderungen,
- Fortschritt und Status,
- mögliche Risiken und Ergebnisse,
- Einmaligkeits- oder Konkurrenzregeln.

## Anomalieentdeckung und Untersuchung

Eine Anomalie kann durch Erkundung, Sensorik oder Ereignis sichtbar werden. Entdeckung gewährt nicht automatisch vollständiges Wissen.

Ein Untersuchungsbefehl benötigt geeignete Flotte, Forschung oder Ressourcen und Kampagnenzeit. Mehrstufige Untersuchung kann neue Optionen, Risiken und konkurrierende Teilnehmer erzeugen.

## Konkurrenz und Einmaligkeit

Ist eine Anomalie einzigartig oder verbrauchbar, bestimmt der Server den wirksamen Abschluss anhand autoritativer Zeitpunkte. Verlierende parallele Untersuchungen erhalten nur die nach ihren Regeln zulässigen Teilinformationen oder Erstattungen.

Der Client darf keinen sicheren exklusiven Anspruch anzeigen, bevor der Server ihn bestätigt.

## Regionale Krise

Eine regionale Krise betrifft einen begrenzten Teil der Galaxie und besitzt Phasen:

1. Vorzeichen und Entdeckung,
2. Ausbruch,
3. Eskalation,
4. mögliche Eindämmung oder Anpassung,
5. Abschluss und langfristige Folgen.

Beteiligte Reiche können unterschiedliche Informationen und Ziele besitzen. Krise und Gegenmaßnahmen verwenden bestehende Flotten-, Wirtschafts-, Forschungs- und Diplomatiesysteme.

## Galaktische Krise

Eine galaktische Krise ist ein Endgame-fähiger, kampagnenweiter Vorgang. Sie muss:

- ausreichend früh angekündigt oder entdeckbar sein,
- anhand der Kampagnenlage skalieren,
- mehrere sinnvolle Gegenstrategien zulassen,
- Beiträge verschiedener Reichstypen ermöglichen,
- Eskalation und Scheitern sichtbar machen,
- die vorherige Reichsentwicklung relevant halten.

Sie darf nicht als vollständig unabhängiges Minispiel sämtliche vorherigen Systeme entwerten.

## Skalierung

Krisenstärke wird aus vor Kampagnenstart bekannten Einstellungen und autoritativen Kampagnenkennzahlen abgeleitet, etwa Anzahl aktiver Reiche, Gesamtwirtschaft, Technologie, Flottenstärke und vergangene Dauer.

Skalierung wird bei definierten Phasenübergängen festgeschrieben oder begrenzt. Sie darf nicht jede Verbesserung der Spieler sofort vollständig neutralisieren.

## Zusammenarbeit und Wettbewerb

Krisen können gemeinsame Projekte, Beiträge, Informationsaustausch, militärische Ziele und diplomatische Entscheidungen erzeugen.

Beiträge werden transparent erfasst. Kooperation darf möglich sein, ohne alle bestehenden Konflikte automatisch zu beenden. Verrat oder konkurrierende Ziele benötigen ausdrückliche Regeln und sichtbare Risiken.

## Erfolg, Scheitern und Folgen

Eine Krise besitzt klare Erfolgs-, Teil- und Scheiterbedingungen. Folgen können regional unterschiedlich sein und wirken über bestehende Systeme.

Schwerwiegende irreversible Folgen benötigen Vorwarnungen und Reaktionsfenster. Das Ende einer Krise kann den Kampagnenabschluss auslösen, ersetzt aber nicht automatisch alle anderen Siegespfade.

## Rückkehrbericht

Priorisiert werden:

- neu ausgelöste zeitkritische Ereignisse,
- automatisch angewandte Standardentscheidungen,
- abgeschlossene oder gescheiterte Anomalien,
- Krisenphasen und Eskalation,
- Beiträge, Verluste und langfristige Folgen,
- neue Endgame- oder Siegsmöglichkeiten.

## Anforderungen an Client und Server

### Client

Der Client muss Ereignisschritte, Fristen, Voraussetzungen, bekannte Folgen, Unsicherheit, Anomaliefortschritt und Krisenphasen verständlich darstellen.

### Server

Der Server muss Definitionen versionieren, Instanzen als Zustandsmaschinen speichern, Auslösung und Zufall deterministisch auswerten, Entscheidungen validieren und Folgen idempotent anwenden.

## Offene Balancingfragen

1. Welche Ereignis- und Anomaliedefinitionen bilden den MVP-Katalog?
2. Welche Standardfristen gelten für Entscheidungen?
3. Welche regionalen und galaktischen Krisen werden zuerst umgesetzt?
4. Wie wird Krisenskalierung konkret begrenzt?
5. Welche Folgen dürfen verborgen bleiben und wann werden sie erklärt?

## Akzeptanzkriterien

- Definition und konkrete Instanz sind getrennt.
- Mehrstufige Ereignisse sind idempotente Zustandsmaschinen.
- Abwesenheit besitzt sichere, vorab sichtbare Standardentscheidungen.
- Anomalien haben Entdeckung, Untersuchung und Konkurrenzregeln.
- Krisen skalieren nachvollziehbar und verwenden bestehende Spielsysteme.
- Ereignisse umgehen keine fachliche Validierung.

## Verwandte Dokumente

- [Erkundung und Informationsstände](../02-galaxy/erkundung-und-informationsstaende.md)
- [Flotten und Raumkampf](../08-fleets/flotten-und-raumkampf.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
- [Endgame und Kampagnenabschluss](../11-campaign/endgame-und-abschluss.md)
