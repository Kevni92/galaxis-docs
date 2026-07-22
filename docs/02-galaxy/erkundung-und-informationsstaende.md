# Erkundung und Informationsstände

Status: Review

## Zweck

Dieses Dokument definiert, welche Informationen ein Reich über Systeme, Himmelskörper, Verbindungen und fremde Aktivitäten besitzen kann. Wissen wird pro Reich geführt und ist von der vollständigen serverseitigen Wahrheit getrennt.

## Grundsatz

Der Server kennt den autoritativen Zustand der Galaxie. Spieler- und AI-Controller erhalten ausschließlich Informationen, die ihr Reich durch Startwissen, Erkundung, Sensorik, Diplomatie oder Ereignisse erlangt hat.

## Wissenseintrag

Ein reichsspezifischer Wissenseintrag enthält mindestens Objekt-ID, Wissensstufe, bekannte Eigenschaften, Informationsquelle und Zeitpunkt der letzten Bestätigung. Einzelne Eigenschaften können unterschiedlich genau oder aktuell sein.

## Wissensstufen

### Unbekannt

Existenz und Lage sind nicht bekannt. Das System wird nicht angezeigt und kann nicht regulär als Ziel verwendet werden.

### Geortet

Position, grobe Sterninformationen und mindestens ein Zugang können bekannt sein. Planeten, Ressourcen und aktuelle Aktivitäten müssen noch unbekannt sein.

### Erkundet

Die wesentliche statische Struktur ist bekannt: Sterne, entdeckte Planeten und Monde, natürliche Ressourcenobjekte und reguläre Verbindungen.

### Überwacht

Aktuelle Sensorinformationen über dynamische Zustände liegen vor. Je nach Sensorqualität können Flotten, Anlagen, Besitz, Kontrolle und Aktivitäten sichtbar sein.

Erkundung bleibt bestehen; Überwachung kann verloren gehen.

## Eigenschaftsspezifisches Wissen

Die Stufe ist nur eine Zusammenfassung. Ein Planet kann bekannt sein, während Bewohnbarkeit oder Ressourcen noch unbekannt sind. Eine Flotte kann erkannt sein, ohne Zusammensetzung oder Ziel zu kennen. Unbekannte Werte dürfen nicht als Nullwerte erscheinen.

## Informationsquellen

Wissen kann durch eigene Präsenz, Erkundungsbefehle, Sensoren, diplomatische Weitergabe, spätere Spionage, Ereignisse oder öffentliche territoriale Änderungen entstehen. Jede Quelle definiert Umfang, Genauigkeit und Aktualität.

## Erkundungsbefehl

Ein Erkundungsbefehl benötigt Kampagnenzeit. Der Server prüft Erreichbarkeit und Berechtigung, erzeugt beim Abschluss definierte Wissensgewinne und deckt Sonderinhalte nur bei erfüllten Bedingungen auf. Teilinformationen bei Abbruch oder Scheitern müssen ausdrücklich definiert sein.

## Sensorik und veraltete Informationen

Sensoren liefern dynamische Informationen in einer fachlich definierten Reichweite. Fällt die Quelle weg, bleibt die letzte bekannte Information mit Beobachtungszeitpunkt erhalten und wird als veraltet markiert. Statische bestätigte Informationen veralten nur, wenn das Objekt fachlich veränderbar ist.

## Verbindungen und unbekannte Wege

Eine Route kann unbekannt sein, obwohl beide Systeme bekannt sind. Reguläre ausgehende Verbindungen werden nach den Erkundungsregeln aufgedeckt. Verborgene Verbindungen benötigen eigene Bedingungen. Nur bekannte Wege dürfen regulär geplant werden.

## Erstkontakt

Erstkontakt beginnt, wenn ein Reich eine fremde kontrollierte Entität ausreichend identifiziert. Vorher können Signaturen als unbekannter Akteur erscheinen. Der Kontaktstatus ist reichspaarbezogen; diplomatische Abläufe folgen in D7.

## Informationsaustausch

Geteilte Informationen behalten Quelle und Zeitpunkt. Vertragsende löscht historisches Wissen nicht, kann aber aktuelle Live-Sicht beenden. Fremde Berichte dürfen nicht als eigene Sensorbeobachtung erscheinen.

## Rückkehrbericht

Priorisiert werden neue Systeme und Verbindungen, abgeschlossene Erkundungen, Erstkontakte, relevante Grenzänderungen, verlorene Überwachung und stark veraltete kritische Informationen.

## Anforderungen an Client und Server

Der Client unterscheidet unbekannt, geortet, erkundet, überwacht und veraltet. Der Server verwaltet Wissen pro Reich, filtert REST-Ausgaben und Ereignisse, speichert Quellen und Zeitpunkte und verhindert Lecks über IDs oder Fehlermeldungen.

## Offene Folgefragen

1. Welche Sensorarten und Reichweiten existieren im MVP?
2. Welche Flottendetails sind je Sensorqualität sichtbar?
3. Welche Informationen dürfen diplomatisch geteilt werden?
4. Welche Erstkontaktphasen werden in D7 benötigt?

## Akzeptanzkriterien

- Wissen ist reichsspezifisch und von der Wahrheit getrennt.
- Statisches Erkundungswissen und aktuelle Überwachung sind getrennt.
- Dynamische Informationen können veralten.
- Spieler und AI unterliegen demselben Fog of War.
- Unbekannte Inhalte werden weder direkt noch technisch offengelegt.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Sternensysteme und Himmelskörper](sternensysteme-und-himmelskoerper.md)
- [Bewegung und Verbindungen](bewegung-und-verbindungen.md)
- [Controller und Reichsübernahme](../03-empires/controller-und-reichsuebernahme.md)
