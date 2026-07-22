# Endgame und Kampagnenabschluss

Status: Review

## Zweck

Dieses Dokument konkretisiert Endgame-Auslöser, Siegespfade, Kampagnenwertung, Niederlage, Abschlussbericht und optionales Nachspiel auf Grundlage der in D1 festgelegten Kampagnenstruktur.

## Eintritt ins Endgame

Das Endgame beginnt nicht ausschließlich zu einem festen Datum. Ein serverseitig bestimmter Endgame-Status kann ausgelöst werden, wenn mindestens eine konfigurierte Kombination erreicht ist:

- ausreichender Kampagnenfortschritt in realer oder Kampagnenzeit,
- ein großer Anteil der Galaxie ist erkundet oder politisch gebunden,
- mehrere Reiche erreichen fortgeschrittene Technologien oder Großprojekte,
- eine galaktische Krise wird ausgelöst,
- ein Reich beginnt einen angekündigten Siegespfad.

Der Eintritt wird kampagnenweit sichtbar angekündigt und verändert keine bestehenden Systeme durch ein separates Minispiel.

## Siegespfade

Das Fachmodell unterstützt mehrere gleichwertige Richtungen:

### Politischer Sieg

Ein Reich oder Bündnis erreicht eine anerkannte galaktische Führungs- oder Einigungsposition durch Verträge, Einfluss und Zustimmung.

### Wirtschaftlicher Sieg

Ein Reich vollendet ein galaxisweit relevantes Wirtschafts- oder Infrastrukturprojekt und kann dessen Unterhalt für eine bekannte Dauer sichern.

### Technologischer Sieg

Ein Reich schließt eine mehrstufige Spitzenforschung oder ein Großprojekt ab, dessen Fortschritt und Gegenmaßnahmen sichtbar sind.

### Militärischer Sieg

Ein Reich erreicht eine dominante, dauerhaft bestätigte strategische Stellung. Bloße kurzfristige Flottenstärke oder die Vernichtung eines einzelnen Gegners genügt nicht.

### Krisensieg

Ein Reich oder eine Koalition erfüllt entscheidende Beiträge zur Bewältigung einer galaktischen Krise. Beiträge anderer Reiche bleiben in der Wertung sichtbar.

Die konkrete Kampagne kann einzelne Pfade aktivieren oder deaktivieren. Voraussetzungen sind vor Kampagnenstart bekannt.

## Ankündigungsphase

Ein möglicher Sieg wird zunächst als `Sieg in Vorbereitung` angekündigt. Die Ankündigung enthält:

- Siegespfad und auslösendes Reich oder Bündnis,
- erfüllte und noch offene Bedingungen,
- frühesten möglichen Abschlusszeitpunkt,
- bekannte Gegenmaßnahmen,
- verbleibende Kampagnenzeit.

Die Ankündigungsphase muss mindestens einen angemessenen mehrfachen Check-in-Zeitraum umfassen. Ein Sieg darf nicht durch eine einzige unangekündigte Aktion sofort eintreten.

## Bestätigung eines Sieges

Nach Ablauf der Ankündigungsphase prüft der Server alle Bedingungen erneut. Ein Sieg wird nur bestätigt, wenn:

- der Pfad weiterhin gültig ist,
- keine zwingende Unterbrechung eingetreten ist,
- alle erforderlichen Projekte oder Zustände wirksam sind,
- der Abschluss atomar protokolliert werden kann.

Scheitert die Bestätigung, endet nur der aktuelle Versuch; bereits erreichte allgemeine Fortschritte bleiben nach ihren Regeln erhalten.

## Kampagnenwertung

Erreicht kein Reich bis zum konfigurierten Abschlussfenster einen eindeutigen Sieg, kann die Kampagne durch transparente Wertung abgeschlossen werden.

Bewertungskategorien sind vor Kampagnenstart bekannt und können umfassen:

- Bevölkerung und stabile Kolonien,
- wirtschaftliche Leistung und Versorgungssicherheit,
- Forschung und einzigartige Errungenschaften,
- diplomatische Stellung und Vertragserfüllung,
- militärische Sicherheit und erfüllte Kriegsziele,
- Erkundung, Anomalien und Krisenbeiträge,
- innere Stabilität und nachhaltige Entwicklung.

Jede Kategorie besitzt Obergrenzen oder abnehmenden Nutzen. Reine Reichsgröße oder Flottenstärke darf nicht allein alle anderen Wege übertreffen.

## Bündnissieg

Ein Siegespfad darf mehrere Reiche als Sieger anerkennen, wenn die Kampagneneinstellung dies erlaubt und die Zusammenarbeit vor Beginn der Bestätigungsphase wirksam war.

Kurzfristiger Beitritt nur zur Übernahme eines Sieges kann durch Mindestdauer, Beitragsanforderung oder Vertragsbedingungen verhindert werden.

## Niederlage eines Reiches

Ein Reich gilt erst als besiegt, wenn es dauerhaft keine eigenständige Handlungsfähigkeit mehr besitzt oder eine ausdrückliche Niederlagebedingung erfüllt.

Mögliche Kriterien:

- keine kontrollierbare Kolonie, territoriale Grundlage oder handlungsfähige Flotte,
- keine realistische Wiederherstellungsmöglichkeit innerhalb einer bekannten Frist,
- bestätigte Kapitulation oder Auflösung,
- kampagnenspezifisches Scheitern.

Einzelne verlorene Kolonien, Defizite oder schwere Kämpfe sind keine automatische Niederlage.

## Möglichkeiten nach Niederlage

Je Kampagnentyp kann ein Spieler:

- als Beobachter fortfahren,
- ein verfügbares AI-Reich übernehmen,
- einen ausdrücklich vorgesehenen Wiederaufbaupfad nutzen,
- die Kampagne mit persönlichem Abschlussbericht verlassen.

Beim Reichswechsel werden Wissen, Befehle und Vorteile nicht zwischen den Reichen übertragen.

## Ende der Kampagne

Beim formalen Abschluss wird ein unveränderlicher Ergebnisdatensatz erzeugt:

- Gewinner und Siegespfad oder Wertung,
- Abschlusszeitpunkt,
- Rangfolge und Kategorien,
- Zustand aller Reiche,
- bedeutende Krisen und Wendepunkte,
- Versionsangaben der maßgeblichen Regeln.

Nach dem Abschluss werden keine weiteren gewerteten Veränderungen mehr verbucht.

## Abschlussbericht

Der Bericht enthält mindestens:

- Verlauf der Kampagnenphasen,
- Entwicklung des eigenen Reiches,
- zentrale Entscheidungen und langfristige Ziele,
- Kolonien, Bevölkerung, Wirtschaft und Forschung,
- Diplomatie, Kriege und territoriale Veränderungen,
- wichtige Ereignisse, Anomalien und Krisen,
- Sieger, Wertung und Begründung,
- Zustand der Galaxie zum Abschluss.

Informationen anderer Reiche werden nur soweit offengelegt, wie die Kampagneneinstellung dies nach Ende erlaubt.

## Nachspiel

Eine Kampagne kann optional als ungewertetes Nachspiel fortgesetzt werden.

- Das offizielle Ergebnis bleibt unverändert.
- Der Zustand wird klar als `Nachspiel` gekennzeichnet.
- Neue Siege oder Wertungspunkte ändern den Abschluss nicht.
- Host oder Einzelspieler kann das Nachspiel pausieren oder beenden.
- Nicht unterstützte Endlossituationen dürfen durch dokumentierte technische Grenzen eingeschränkt werden.

## Krisen und Endgame

Eine galaktische Krise kann einen eigenen Krisensieg, Wertungsbeiträge oder eine gemeinsame Niederlage ermöglichen. Sie ersetzt jedoch nicht automatisch alle aktivierten Siegespfade.

Scheitert die Galaxie an einer ausdrücklich als existenziell definierten Krise, kann die Kampagne mit gemeinsamem Scheitern enden. Auslöser, Eskalation und letzte Gegenmaßnahmen müssen vorher sichtbar sein.

## Asynchronität

Für alle Abschlusszustände gilt:

- Online- oder Offline-Status beeinflusst keine Bedingung.
- Fristen laufen in Kampagnenzeit.
- Singleplayer-Pause stoppt Fristen.
- Sieg, Kapitulation oder irreversible Niederlage werden angekündigt, sofern Gegenmaßnahmen möglich sind.
- Rückkehrberichte priorisieren Endgame-Fortschritt und verbleibende Fristen.

## Anforderungen an Client und Server

### Client

Der Client muss Endgame-Status, aktive Siegespfade, Fortschritt, Gegenmaßnahmen, Wertung, Fristen, Niederlagerisiken und Abschlussbericht verständlich darstellen.

### Server

Der Server muss Auslöser, Fortschritt, Ankündigungsphasen, Bestätigung, Wertung und Ergebnisdatensatz autoritativ und atomar auswerten. Das offizielle Ergebnis wird nach Abschluss unveränderlich gespeichert.

## Offene Balancingfragen

1. Welche Siegespfade gehören in den ersten MVP-Katalog?
2. Wie lang ist die Ankündigungsphase im Standardprofil?
3. Welche Kategorien und Gewichtungen gelten für die Wertung?
4. Welche Kriterien definieren dauerhafte Handlungsunfähigkeit?
5. Welche Informationen werden nach Kampagnenende vollständig offengelegt?

## Akzeptanzkriterien

- Endgame-Eintritt und Siegesversuche werden angekündigt.
- Mehrere strategische Siegespfade sind möglich.
- Wertung ist transparent und nicht eindimensional.
- Niederlage erfordert dauerhafte Handlungsunfähigkeit oder klare Bedingung.
- Ergebnisdatensatz bleibt nach Abschluss unverändert.
- Nachspiel ist ungewertet und klar gekennzeichnet.
- Asynchronität und Reichsübernahme bleiben berücksichtigt.

## Verwandte Dokumente

- [Kampagnenstruktur](kampagnenstruktur.md)
- [Ereignisse und Krisen](../10-events/ereignisse-und-krisen.md)
- [Diplomatie und Krieg](../09-diplomacy/diplomatie-und-krieg.md)
- [Controller und Reichsübernahme](../03-empires/controller-und-reichsuebernahme.md)
