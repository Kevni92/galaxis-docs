# Erkundung und Informationsstände

Status: Freigegeben

## Zweck

Dieses Dokument definiert, welche Informationen ein Reich über Systeme, Himmelskörper, Verbindungen und fremde Aktivitäten besitzen kann und wie diese Informationen in Sternensystem- und Galaxieansicht dargestellt werden. Wissen wird pro Reich geführt und ist von der vollständigen serverseitigen Wahrheit getrennt.

## Grundsatz

Der Server kennt den autoritativen Zustand der Galaxie. Spieler- und AI-Controller erhalten ausschließlich Informationen, die ihr Reich durch Startwissen, Erkundung, Sensorik, Diplomatie oder Ereignisse erlangt hat.

Die 3D-Darstellung ist ebenfalls wissensgefiltert. Ein Objekt, dessen Existenz nicht bekannt ist, darf weder als Modell, Schatten, Orbitlinie, Picking-Fläche, Platzhalter noch über Objektanzahl oder Listenposition sichtbar werden.

## Wissenseintrag

Ein reichsspezifischer Wissenseintrag enthält mindestens:

- Objekt-ID,
- Wissensstufe,
- bekannte Eigenschaften,
- Informationsquelle,
- Zeitpunkt der letzten Bestätigung.

Einzelne Eigenschaften können unterschiedlich genau oder aktuell sein.

## Wissensstufen

### Unbekannt

Existenz und Lage sind nicht bekannt. Das System oder Objekt wird nicht angezeigt und kann nicht regulär als Ziel verwendet werden.

### Geortet

Position, grobe Sterninformationen und mindestens ein Zugang können bekannt sein. Planeten, Ressourcen und aktuelle Aktivitäten müssen noch unbekannt sein.

Ein geortetes System oder Objekt erscheint nur mit den tatsächlich freigegebenen Eigenschaften. Eine zulässige Bezeichnung wird gedämpft beziehungsweise dunkelgrau dargestellt. Ist der Name nicht bekannt, wird eine freigegebene neutrale Bezeichnung verwendet; der Client erfindet keinen kanonischen Namen.

### Erkundet

Die wesentliche statische Struktur ist bekannt: Sterne, entdeckte Planeten und Monde, natürliche Ressourcenobjekte und reguläre Verbindungen.

Bestätigte Namen erscheinen regulär, standardmäßig weiß. Bekannte Himmelskörper werden in der Sternensystemansicht dreidimensional gerendert und können ausgewählt werden.

### Überwacht

Aktuelle Sensorinformationen über dynamische Zustände liegen vor. Je nach Sensorqualität können Flotten, Anlagen, Besitz, Kontrolle, Aktivitäten, lokale Positionen und Bewegungsrichtungen sichtbar sein.

Erkundung bleibt bestehen; Überwachung kann verloren gehen.

### Veraltet

Veraltete Information ist keine eigene Grundstufe, sondern eine Kennzeichnung für nicht mehr aktuelle dynamische Daten. Die letzte bekannte Information bleibt sichtbar, zeigt aber Zeitpunkt und Unsicherheit eindeutig an.

## Eigenschaftsspezifisches Wissen

Die Wissensstufe ist nur eine Zusammenfassung. Ein Planet kann bekannt sein, während Bewohnbarkeit oder Ressourcen noch unbekannt sind. Eine Flotte kann erkannt sein, ohne Zusammensetzung oder Ziel zu kennen.

Unbekannte Werte dürfen nicht als Nullwerte erscheinen. Ein Planetendetailfenster zeigt nur bekannte Felder, kenntlich gemachte Schätzungen und ausdrücklich unbekannte Eigenschaften.

## Informationsquellen

Wissen kann entstehen durch:

- eigene Präsenz,
- Erkundungsbefehle,
- Sensoren,
- diplomatische Weitergabe,
- spätere Spionage,
- Ereignisse,
- öffentliche territoriale Änderungen.

Jede Quelle definiert Umfang, Genauigkeit und Aktualität.

## Erkundungsbefehl

Ein Erkundungsbefehl benötigt Kampagnenzeit. Der Server prüft Erreichbarkeit und Berechtigung, erzeugt beim Abschluss definierte Wissensgewinne und deckt Sonderinhalte nur bei erfüllten Bedingungen auf.

Teilinformationen bei Abbruch oder Scheitern müssen ausdrücklich definiert sein. Das bloße visuelle Anfliegen oder Zoomen auf ein Objekt erzeugt kein Wissen.

## Sensorik und veraltete Informationen

Sensoren liefern dynamische Informationen in einer fachlich definierten Reichweite. Fällt die Quelle weg, bleibt die letzte bekannte Information mit Beobachtungszeitpunkt erhalten und wird als veraltet markiert.

Statische bestätigte Informationen veralten nur, wenn das Objekt fachlich veränderbar ist.

Sensorreichweiten dürfen in der Raumansicht visualisiert werden, aber nur aus serverseitig freigegebenen Werten. Sichtbare Kreise oder Volumen sind keine eigenständige Regel.

## Verbindungen und unbekannte Wege

Eine Route kann unbekannt sein, obwohl beide Systeme bekannt sind. Reguläre ausgehende Verbindungen werden nach den Erkundungsregeln aufgedeckt. Verborgene Verbindungen benötigen eigene Bedingungen.

Nur bekannte Wege dürfen regulär geplant werden. Die Galaxieansicht darf keine verborgenen Kanten durch Layout, Abstand oder leere Anschlussstellen andeuten.

## Sternensystemansicht

Die Sternensystemansicht zeigt ausschließlich bekannte Objekte und Eigenschaften:

- unbekannte Himmelskörper erscheinen nicht,
- geortete Objekte erscheinen nur mit groben freigegebenen Merkmalen und gedämpfter Bezeichnung,
- erkundete Himmelskörper erscheinen mit bestätigtem Namen und bekannten statischen Eigenschaften,
- überwachte künstliche Objekte können aktuelle Position, Bewegung und Status zeigen,
- veraltete dynamische Informationen erhalten eine sichtbare Kennzeichnung.

Ein Klick auf einen sichtbaren Himmelskörper öffnet ein wissensgefiltertes modales Detailfenster. Der Dialog darf keine intern vorhandenen, aber unbekannten Tabs oder Felder verraten.

## Galaxieansicht

Die Galaxieansicht zeigt:

- bekannte Systeme,
- zulässige Systemnamen oder neutrale Bezeichnungen,
- bekannte Verbindungen,
- bekannte Reichsgebiete und Kontrolle,
- sichtbare Flotten oder Signaturen,
- bekannte Reise- und Erkundungsziele.

Die visuelle Farbe von Namen unterstützt den Wissensstand:

- gedämpft oder dunkelgrau für geortete, noch nicht vollständig erkundete Systeme,
- regulär beziehungsweise weiß für erkundete und bestätigte Systeme,
- zusätzliche Kennzeichnung für veraltete Informationen.

Farbe ist nicht die einzige Kennzeichnung; Symbol, Text oder Tooltip müssen den Zustand ebenfalls ausdrücken.

## Kontextaktionen und Wissen

Ein Kontextmenü darf nur Aktionen zeigen, deren Ziel und Existenz dem Reich ausreichend bekannt sind.

- `Hierhin fliegen` benötigt ein bekanntes und adressierbares Ziel.
- `Erkunden` darf bei georteten oder teilweise bekannten Zielen angeboten werden, wenn Flotte und Route zulässig sind.
- `Kolonisieren` darf keine unbekannte Bewohnbarkeit oder geheime Ausschlussursache offenlegen.
- Deaktivierungsgründe werden nur so genau dargestellt, wie das Reich die Ursache kennen darf.

## Erstkontakt

Erstkontakt beginnt, wenn ein Reich eine fremde kontrollierte Entität ausreichend identifiziert. Vorher können Signaturen als unbekannter Akteur erscheinen. Der Kontaktstatus ist reichspaarbezogen; diplomatische Abläufe folgen in D7.

## Informationsaustausch

Geteilte Informationen behalten Quelle und Zeitpunkt. Vertragsende löscht historisches Wissen nicht, kann aber aktuelle Live-Sicht beenden. Fremde Berichte dürfen nicht als eigene Sensorbeobachtung erscheinen.

## Rückkehrbericht

Priorisiert werden:

- neue Systeme und Verbindungen,
- neu bekannte Himmelskörper,
- abgeschlossene Erkundungen,
- Erstkontakte,
- relevante Grenzänderungen,
- verlorene Überwachung,
- stark veraltete kritische Informationen.

Meldungen verlinken auf die passende Galaxie- oder Sternensystemansicht und können das betroffene Objekt auswählen und sein modales Detailfenster öffnen.

## Anforderungen an Client und Server

### Client

Der Client:

- unterscheidet unbekannt, geortet, erkundet, überwacht und veraltet,
- rendert nur freigegebene 3D-Objekte,
- zeigt Namen und Eigenschaften entsprechend dem Wissensstand,
- filtert Detailfenster und Kontextaktionen,
- behandelt unbekannt, null und nicht anwendbar unterschiedlich,
- ergänzt keine verborgenen Objekte oder Eigenschaften.

### Server

Der Server:

- verwaltet Wissen pro Reich,
- filtert REST-Ausgaben, Kontextaktionen und Ereignisse,
- speichert Quellen und Zeitpunkte,
- liefert nur zulässige lokale Positionen und Bezeichnungen,
- verhindert Lecks über IDs, Fehler, Renderdaten oder Objektzählung.

## Offene Folgefragen

1. Welche Sensorarten und Reichweiten existieren im MVP?
2. Welche Flottendetails sind je Sensorqualität sichtbar?
3. Welche Informationen dürfen diplomatisch geteilt werden?
4. Welche Erstkontaktphasen werden in D7 benötigt?
5. Welche neutralen Bezeichnungen werden verwendet, wenn Existenz und Position, aber nicht der Eigenname bekannt sind?

## Akzeptanzkriterien

- Wissen ist reichsspezifisch und von der Wahrheit getrennt.
- Statisches Erkundungswissen und aktuelle Überwachung sind getrennt.
- Dynamische Informationen können veralten.
- Spieler und AI unterliegen demselben Fog of War.
- Unbekannte Inhalte werden weder direkt noch technisch oder visuell offengelegt.
- System- und Objektnamen zeigen ihren Wissensstand ohne ausschließlich auf Farbe angewiesen zu sein.
- Modale Detailfenster enthalten nur freigegebene Daten.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Sternensysteme und Himmelskörper](sternensysteme-und-himmelskoerper.md)
- [Bewegung und Verbindungen](bewegung-und-verbindungen.md)
- [Controller und Reichsübernahme](../03-empires/controller-und-reichsuebernahme.md)
- [Raumansichten und Flotteninteraktion](../12-ui-ux/raumansichten-und-flotteninteraktion.md)
