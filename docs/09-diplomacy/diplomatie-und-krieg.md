# Diplomatie, Verträge und Krieg

Status: Freigegeben

## Zweck

Dieses Dokument definiert Beziehungen zwischen Reichen, diplomatische Aktionen, Verträge, Bündnisse, Konflikte, Kriegsziele, Kriegsfortschritt und Friedensschlüsse.

## Diplomatischer Kontakt

Diplomatische Interaktion setzt einen fachlich bestätigten Kontakt voraus. Vor dem Erstkontakt können fremde Einheiten als unbekannter Akteur erscheinen.

Ein Kontaktstatus wird für jedes Reichspaar getrennt geführt:

- unbekannt,
- entdeckt, aber nicht kommunikationsfähig,
- Erstkontakt aktiv,
- diplomatischer Kontakt hergestellt,
- Kontakt abgebrochen oder blockiert.

Kontakt gibt keine vollständigen Informationen über Gebiet, Wirtschaft oder Militär frei.

## Beziehung

Eine Beziehung besteht nicht nur aus einem einzigen Meinungswert. Der Server führt nachvollziehbare Komponenten:

- Vertrauen,
- wahrgenommene Bedrohung,
- Kooperation,
- Konflikt und historische Verletzungen,
- vertragliche Bindung,
- bekannte Ansprüche und Grenzstreitigkeiten.

Eine zusammengefasste Haltung darf für Darstellung und AI verwendet werden, muss aber auf sichtbare Ursachen zurückführbar sein.

## Diplomatische Haltung

Ein Reich kann gegenüber einem anderen eine Haltung festlegen, beispielsweise freundlich, neutral, vorsichtig, rivalisierend oder feindlich.

Haltungen:

- steuern Empfehlungen und AI-Prioritäten,
- sind nicht automatisch gegenseitig,
- ersetzen keine Verträge oder Kriegszustände,
- dürfen nur dann öffentlich sein, wenn dies ausdrücklich vorgesehen ist.

## Diplomatische Aktion

Eine diplomatische Aktion ist ein serverautoritärer Befehl mit Absender, Empfänger, Typ, Inhalt, Voraussetzungen, Kosten, Frist und Status.

Mögliche Aktionen:

- Nachricht oder Absichtserklärung,
- Angebot oder Anfrage,
- Vertragsvorschlag,
- Handels- oder Forschungsabkommen,
- Garantie oder Bündnisanfrage,
- Forderung oder Ultimatum,
- Kündigung oder Vertragsänderung,
- Kriegserklärung,
- Friedensangebot.

Jede Aktion besitzt einen eindeutigen Lebenszyklus: vorbereitet, gesendet, zugestellt, angenommen, abgelehnt, zurückgezogen, abgelaufen oder gegenstandslos.

## Fristen und Abwesenheit

Angebote und Entscheidungen besitzen angemessene Fristen in Kampagnenzeit. Eine Frist darf nicht so kurz sein, dass der vorgesehene Check-in-Rhythmus regelmäßig unfaire automatische Ergebnisse erzeugt.

Bei Ablauf gilt eine vorab sichtbare Standardregel, in der Regel Ablehnung oder Fortbestand des bisherigen Zustands. Schweigen erzeugt nicht automatisch einen neuen belastenden Vertrag oder Kriegseintritt.

## Verträge

Ein Vertrag besitzt:

- stabile ID,
- beteiligte Reiche,
- Vertragstyp,
- Beginn und optionale Mindestlaufzeit,
- Rechte und Pflichten,
- Kündigungs- und Änderungsregeln,
- Status,
- Folgen bei Bruch,
- Sichtbarkeit.

Verträge wirken nur über ausdrücklich definierte Rechte und Pflichten. Ein allgemeiner Bündnisstatus gewährt keine nicht dokumentierten Sonderrechte.

## Vertragstypen des MVP

Das fachliche Grundmodell unterstützt mindestens:

### Nichtangriffspakt

Verpflichtung, keinen direkten Krieg zu beginnen. Er kann Kündigungsfrist und definierte Ausnahmen besitzen.

### Zugangsabkommen

Erlaubt bestimmte Bewegungs-, Versorgungs- oder Stationsrechte. Rechte werden einzeln benannt.

### Handelsabkommen

Ermöglicht vereinbarte Handelsrouten, Zahlungen oder Marktteilnahme.

### Forschungsabkommen

Ermöglicht definierte Forschungsboni, gemeinsame Projekte oder Technologietransfer.

### Verteidigungsbündnis

Definiert, unter welchen Bedingungen ein Angriff auf einen Partner Beistandspflichten auslöst. Der Eintritt erfolgt serverseitig nach den Vertragsbedingungen und nicht allein durch eine Clientmeldung.

Weitere Verträge benötigen einen eigenständigen Zweck und dürfen bestehende Typen nicht nur anders benennen.

## Vertragsänderung und Kündigung

Änderungen benötigen Zustimmung nach denselben Regeln wie ein neuer Vertrag. Kündigung kann sofort oder nach einer bekannten Frist wirksam werden.

Bereits entstandene Verpflichtungen bleiben bestehen, wenn der Vertrag dies vorsieht. Kündigung löscht keine laufenden Transporte, gemeinsamen Projekte oder Kriege ohne ausdrückliche Übergangsregel.

## Vertragsbruch

Ein Vertragsbruch ist ein autoritativ erkannter Verstoß gegen eine konkrete Pflicht. Er erzeugt:

- protokolliertes Ereignis,
- sichtbare Ursache für betroffene Reiche,
- definierte Beziehungs- oder Vertrauensfolgen,
- mögliche Kündigungs-, Sanktions- oder Kriegsmöglichkeiten.

Nicht jede negative Handlung ist automatisch Vertragsbruch; die verletzte Klausel muss benannt werden.

## Konflikt und Kriegserklärung

Ein Krieg ist ein eigener Zustand zwischen Kriegsseiten. Er beginnt durch gültige Kriegserklärung, Vertragsfolge oder ausdrücklich definiertes Ereignis.

Eine Kriegserklärung benötigt:

- Absender und Ziel,
- mindestens ein zulässiges Kriegsziel,
- bekannte Kosten oder politische Folgen,
- Wirksamkeitszeitpunkt,
- Behandlung bestehender Verträge,
- Bestimmung der anfänglichen Teilnehmer.

Überraschung ist möglich, aber die Simulation verwendet weiterhin autoritative Zeitpunkte und angemessene Schutzregeln des asynchronen Modells.

## Kriegsseiten und Teilnehmer

Ein Krieg besteht aus mindestens zwei Seiten. Reiche können durch Bündnisse, Garantien, Einladungen oder Ereignisse beitreten.

- Ein Reich gehört nicht gleichzeitig beiden Seiten an.
- Beitritt und Austritt sind protokolliert.
- Bündnisverpflichtungen werden als Angebote oder automatische Pflichten nach bekanntem Vertragstext ausgewertet.
- Controller- oder Online-Status beeinflusst keine Teilnahme.

## Kriegsziele

Ein Kriegsziel beschreibt die angestrebte, bei Frieden zulässige Veränderung, beispielsweise:

- Übertragung beanspruchter Systeme,
- Aufgabe von Ansprüchen,
- Reparations- oder Ressourcenleistung,
- Vertragsauflösung,
- politische oder diplomatische Konzession,
- begrenzte Demilitarisierung.

Ein Ziel benötigt Voraussetzungen, Umfang, Kosten, Fortschrittsquellen und maximal zulässige Friedensforderung. Vollständige Vernichtung ist kein Standardziel des MVP.

## Kriegsfortschritt

Kriegsfortschritt ist eine transparente Zusammenfassung aus dokumentierten Faktoren:

- erfüllte oder verteidigte Kriegsziele,
- militärische Kontrolle und Besetzung,
- Flottenverluste,
- wirtschaftliche Belastung,
- Dauer und Blockaden,
- bedeutende Ereignisse.

Er ist keine automatische Siegesbedingung, sondern begrenzt und erklärt mögliche Friedensforderungen. Einzelne Faktoren besitzen Obergrenzen, damit endloses Kämpfen oder kleine Gefechte nicht unbegrenzt skalieren.

## Kriegserschöpfung

Jedes beteiligte Reich kann eine sichtbare Kriegserschöpfung besitzen. Sie entsteht aus Dauer, Verlusten, Mangel, Besetzung und Belastung.

Hohe Erschöpfung kann Unterhalt, Bevölkerung, Stabilität und Friedensbereitschaft beeinflussen. Sie erzwingt nicht ohne Vorwarnung eine zufällige Kapitulation.

## Friedensangebot

Ein Friedensangebot enthält:

- beteiligte Seiten,
- vorgeschlagene Bedingungen,
- Kosten und zulässige Grenzen,
- Wirksamkeitszeitpunkt,
- Frist,
- Behandlung laufender Kämpfe, Besetzungen und Befehle.

Bedingungen werden gegen Kriegsziele, Fortschritt, Besitz und Verträge validiert. Ein Frieden kann bilateral oder für gesamte Seiten gelten, wenn der Kriegstyp dies erlaubt.

## Friedensschluss

Beim Wirksamwerden werden alle Folgen atomar angewandt:

1. Gebiets- und Anspruchsänderungen,
2. Zahlungen und Verpflichtungen,
3. neue oder beendete Verträge,
4. Ende oder Fortbestand von Besetzungen,
5. Zugangs- und Rückzugsregeln für Flotten,
6. Kriegsende und Berichte.

Laufende Kämpfe enden oder werden nach einer ausdrücklichen Übergangsregel abgewickelt. Fremde Flotten werden nicht teleportiert.

## Kapitulation und erzwungener Frieden

Eine Seite kann kapitulieren, wenn die Regeln dies erlauben. Erzwungener Frieden benötigt sehr klare, vorab sichtbare Bedingungen und angemessene Reaktionszeit. Offline-Status ist niemals Voraussetzung.

## Sichtbarkeit und Geheimhaltung

Kontakte, öffentliche Verträge, Kriege und anerkannte Gebietsänderungen können öffentlich sichtbar sein. Geheime Klauseln oder Verhandlungen sind nur beteiligten Reichen bekannt.

Der Client erhält keine internen AI-Bewertungen oder fremden Entscheidungsgründe, sofern sie nicht als diplomatische Erklärung veröffentlicht werden.

## AI und Spielerübernahme

AI verwendet dieselben diplomatischen Aktionen und Verträge. Bei Übernahme eines AI-Reiches zeigt der Bericht:

- aktive Verträge und Pflichten,
- offene Angebote und Fristen,
- Kriege, Ziele und Fortschritt,
- bekannte Beziehungsursachen,
- laufende Friedensverhandlungen,
- aktive diplomatische Prioritäten.

Interne AI-Pläne sind nicht bindend. Bereits gesendete Angebote und gültige Verträge bleiben bestehen.

## Anforderungen an Client und Server

### Client

Der Client muss Beziehungskomponenten, Verträge, Fristen, Pflichten, Kriegsziele, Fortschritt und mögliche Friedensfolgen verständlich darstellen.

### Server

Der Server muss Kontakte, Beziehungen, Aktionen, Verträge, Kriege und Frieden autoritativ verwalten, Fristen auswerten, Bedingungen validieren und Informationen nach Sichtbarkeit filtern.

## Offene Balancingfragen

1. Welche Beziehungskomponenten und Skalen gehören zum MVP?
2. Welche konkreten Vertragstypen werden zum Start angeboten?
3. Welche Kosten und Fristen gelten für Diplomatie und Kriegserklärung?
4. Wie werden Kriegsfortschritt und Erschöpfung numerisch gewichtet?
5. Welche Friedensbedingungen sind im MVP zulässig?

## Akzeptanzkriterien

- Kontakt, Beziehung, Haltung, Vertrag und Krieg sind getrennte Zustände.
- Diplomatische Angebote besitzen Fristen und sichere Standardfolgen.
- Verträge definieren konkrete Rechte, Pflichten und Bruchfolgen.
- Kriege besitzen Seiten, Ziele, Fortschritt und atomare Friedensschlüsse.
- Spieler und AI verwenden dieselben diplomatischen Befehle.
- Offline- oder Controllerstatus beeinflusst keine diplomatischen Rechte.

## Verwandte Dokumente

- [Reichsverwaltung](../03-empires/reichsverwaltung.md)
- [Controller und Reichsübernahme](../03-empires/controller-und-reichsuebernahme.md)
- [Besitz und Kontrolle](../02-galaxy/besitz-und-kontrolle.md)
- [Flotten und Raumkampf](../08-fleets/flotten-und-raumkampf.md)
- [Wirtschaft und Versorgung](../06-economy/wirtschaft-und-versorgung.md)
