# Sternensysteme und Himmelskörper

Status: Freigegeben

## Zweck

Dieses Dokument definiert die fachlichen Entitäten, die lokale Raumgeometrie und die grundlegende Darstellung innerhalb eines Sternensystems. Planetare Detailregeln, Kolonisierung und Entwicklung werden in D3 beschrieben.

## Sternensystem

Ein Sternensystem ist die kleinste reguläre räumliche Einheit für interstellare Bewegung, lokale Flottenbewegung, Erkundung und territoriale Zuordnung. Es besitzt mindestens:

- eine stabile ID,
- Galaxiekoordinaten und Region,
- eine begrenzte lokale XY-Ebene,
- mindestens einen Stern,
- natürliche Himmelskörper,
- interstellare Verbindungen,
- statische und dynamische Zustände.

Fachliche Beziehungen werden ausdrücklich über IDs gespeichert. Listenreihenfolgen, Kamerawinkel, sichtbare Objektgrößen und visuelle 3D-Höhen sind keine Spielregeln.

## Hierarchie

```text
Sternensystem
├── Stern oder Mehrfachsternsystem
├── Planet
│   └── Mond
├── Asteroidengürtel oder Ressourcenfeld
└── besonderes natürliches Objekt
```

Ein Mond gehört genau zu einem Planeten, ein Planet genau zu einem System. Eine physikalisch exakte Orbitalsimulation ist kein Bestandteil des MVP.

## Lokale Raumgeometrie

Jedes fachlich lokal positionierte Objekt besitzt innerhalb seines Systems eine autoritative zweidimensionale Position:

```text
systemId + x + y
```

Diese Position kann für lokale Bewegung, Entfernung, Sensorik, Abfangen, Begegnung und Kampf verwendet werden. Der Server validiert Koordinaten, Systemgrenzen und Positionsänderungen.

Eine visuelle Z-Koordinate, Neigung, Rotation, Orbitanimation oder Größenüberzeichnung wird ausschließlich durch den Client erzeugt und darf keine Entfernung, Reichweite, Kollisionsfläche oder Reisezeit beeinflussen.

## 3D-Sternensystemansicht

Bekannte natürliche und künstliche Objekte werden grundsätzlich dreidimensional gerendert:

- Sterne,
- Planeten,
- Monde,
- Asteroidengürtel und Ressourcenfelder,
- besondere Himmelskörper,
- Stationen und Außenposten,
- Schiffe und Flotten.

Die Kamera blickt standardmäßig schräg von oben auf das System. Zoomen, Verschieben, Fokussieren und begrenztes Drehen verändern nur die Darstellung.

Der Client darf visuelle Größen und Abstände für Lesbarkeit anpassen. Solche Anpassungen müssen erkennbar präsentational bleiben und dürfen keine fachliche Eigenschaft vortäuschen.

## Sterne

Ein System kann einen oder mehrere Sterne besitzen. Sternkategorien dürfen Umwelt, Energiegewinnung, Sensorik oder Ereignisse beeinflussen, müssen dann aber einen dokumentierten spielerischen Zweck besitzen. Reine optische Varianten erzeugen keine versteckten Effekte.

Ein Primärklick auf einen bekannten Stern wählt ihn aus und öffnet seine bekannten Details in einem modalen Fenster über der Systemansicht. Der Stern erhält keine eigenständige Vollbildseite.

## Planeten und Monde

Planeten und Monde besitzen stabile IDs, ihre Zugehörigkeit, grundlegende Kategorien, statische Generierungsmerkmale, lokale XY-Positionen und reichsspezifisch bekannte Eigenschaften. Bewohnbarkeit, Kolonisierung, Bezirke, Bevölkerung und Gebäude folgen in D3.

Ein Primärklick auf einen bekannten Planeten oder Mond wählt das Objekt aus und öffnet ein modales Detailfenster. Das Fenster kann Tabs für Übersicht, Kolonie, Bevölkerung, Versorgung und spätere Fachbereiche enthalten. Nicht bekannte oder nicht anwendbare Tabs werden nicht angeboten.

Ob Monde eigenständig kolonisiert werden können, wird in D3 entschieden.

## Asteroidengürtel und Ressourcenfelder

Diese Objekte sind keine Planeten. Sie können Rohstoffvorkommen, spätere Förderstandorte, Gefahren oder Ereignisse tragen. Existenz und Grundkategorie sind statisch; Abbau, Erschöpfung und künstliche Anlagen sind dynamisch.

Die 3D-Darstellung eines Gürtels oder Feldes ist eine visuelle Repräsentation. Seine fachliche Ausdehnung und Interaktionspunkte werden serverseitig definiert.

## Besondere Objekte

Besondere Objekte dürfen nur Spielwirkungen besitzen, wenn Entdeckung, Interaktionen, Risiken und Ergebnisse fachlich definiert sind. Dazu können Anomalien, stellare Überreste, verborgene Zugänge oder einzigartige Kampagnenobjekte gehören.

## Künstliche Objekte

Kolonien, Raumstationen, Außenposten und Flotten gehören nicht zur unveränderlichen natürlichen Struktur. Sie sind veränderliche Entitäten und verweisen auf System, lokale Position und gegebenenfalls Himmelskörper oder Objektanker.

## Auswahl und Kontextaktionen

- Primärauswahl fokussiert ein bekanntes Objekt und öffnet bei Himmelskörpern oder verwaltbaren Objekten das modale Detailfenster.
- Eine Sekundäraktion bei ausgewählter Flotte darf ein Kontextmenü mit zulässigen Aktionen für das Zielobjekt öffnen.
- Kontextaktionen können beispielsweise Bewegung, Erkundung, Beobachtung, Kolonisierung, Angriff, Reparatur oder Versorgung umfassen.
- Verfügbarkeit und Gründe werden serverautoritativ bestimmt.
- Jede räumliche Mausaktion benötigt eine gleichwertige Tastatur- oder Listenalternative.

## Bewegung innerhalb eines Systems

Auf der galaktischen Ebene ist ein System ein Knoten. Innerhalb des Systems bewegen sich Flotten auf der autoritativen XY-Ebene zu freien Zielpunkten oder fachlich definierten Objektankern.

Aus einer rein grafischen Orbitposition entsteht keine Reisezeit. Lokale Zielposition, Route, Geschwindigkeit und Ankunft werden serverseitig bestätigt.

## Namen und Sichtbarkeit

Der Server kennt die vollständige Struktur. Ein Reich kann ein System kennen, ohne alle Planeten, Eigenschaften oder besonderen Objekte entdeckt zu haben.

- Unbekannte Objekte werden nicht gerendert und sind nicht auswählbar.
- Geortete Objekte dürfen nur mit den freigegebenen groben Eigenschaften und gedämpfter Bezeichnung erscheinen.
- Erkundete Objekte erscheinen mit bestätigtem Namen und bekannter statischer Struktur.
- Überwachte Objekte können aktuelle dynamische Marker zeigen.
- Veraltete Informationen werden ausdrücklich als veraltet markiert.

Der Client darf unbekannte Inhalte nicht durch IDs, Objektanzahlen, Picking-Flächen, Schatten, Orbitlinien oder Listenreihenfolgen indirekt offenlegen.

## Anforderungen an Client und Server

### Client

Der Client:

- rendert bekannte Himmelskörper und künstliche Objekte dreidimensional,
- trennt fachliche XY-Position und visuelle 3D-Transformation,
- öffnet Objektdetails modal,
- synchronisiert Szene, Outliner und Auswahl,
- leitet keine Spielregel aus Grafik oder Kamera ab,
- bietet eine zugängliche alternative Objektliste.

### Server

Der Server:

- validiert Identitäten, Relationen, lokale Positionen und Systemgrenzen,
- trennt statische von dynamischen Daten,
- filtert alle Ausgaben nach Reichswissen,
- liefert nur zulässige Kontextaktionen,
- verhindert Informationslecks über Darstellungs- oder Interaktionsdaten.

## Offene Folgefragen

1. Welche Stern- und Planetenkategorien gehören zum MVP?
2. Welche Himmelskörper können kolonisiert werden?
3. Welche Ressourcenobjekte werden für D4 benötigt?
4. Welche besonderen Objekte gehören zum MVP?
5. Welche fachlichen lokalen Systemgrenzen und Objektanker gelten je Systemtyp?

## Akzeptanzkriterien

- Alle adressierbaren Objekte besitzen stabile Identitäten.
- Eltern-Kind-Beziehungen sind eindeutig.
- Statische natürliche Struktur und dynamische Kampagnenobjekte sind getrennt.
- Sterne, Planeten und weitere bekannte Himmelskörper werden in der Systemansicht dreidimensional gerendert.
- Fachliche lokale Bewegung verwendet ausschließlich serverseitige XY-Koordinaten.
- Visuelle Z-Höhe, Meshgröße und Animation erzeugen keine undokumentierte Regel.
- Planetendetails öffnen als modales Fenster über der Systemansicht.
- Verborgene Objekte und Eigenschaften werden weder direkt noch indirekt dargestellt.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Bewegung und Verbindungen](bewegung-und-verbindungen.md)
- [Planeten – Übersicht](../04-planets/README.md)
- [Raumansichten und Flotteninteraktion](../12-ui-ux/raumansichten-und-flotteninteraktion.md)
