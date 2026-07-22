# Sternensysteme und Himmelskörper

Status: Review

## Zweck

Dieses Dokument definiert die fachlichen Entitäten innerhalb eines Sternensystems. Planetare Detailregeln, Kolonisierung und Entwicklung werden in D3 beschrieben.

## Sternensystem

Ein Sternensystem ist die kleinste reguläre räumliche Einheit für interstellare Bewegung, Erkundung und territoriale Zuordnung. Es besitzt mindestens eine stabile ID, Kartenkoordinaten, eine Region, mindestens einen Stern, natürliche Himmelskörper, interstellare Verbindungen sowie statische und dynamische Zustände.

Fachliche Beziehungen werden ausdrücklich über IDs gespeichert. Grafische Positionen oder Listenreihenfolgen sind keine Spielregeln.

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

## Sterne

Ein System kann einen oder mehrere Sterne besitzen. Sternkategorien dürfen Umwelt, Energiegewinnung, Sensorik oder Ereignisse beeinflussen, müssen dann aber einen dokumentierten spielerischen Zweck besitzen. Reine optische Varianten erzeugen keine versteckten Effekte.

## Planeten und Monde

Planeten und Monde besitzen stabile IDs, ihre Zugehörigkeit, grundlegende Kategorien, statische Generierungsmerkmale und reichsspezifisch bekannte Eigenschaften. Bewohnbarkeit, Kolonisierung, Bezirke, Bevölkerung und Gebäude folgen in D3.

Ob Monde eigenständig kolonisiert werden können, wird in D3 entschieden.

## Asteroidengürtel und Ressourcenfelder

Diese Objekte sind keine Planeten. Sie können Rohstoffvorkommen, spätere Förderstandorte, Gefahren oder Ereignisse tragen. Existenz und Grundkategorie sind statisch; Abbau, Erschöpfung und künstliche Anlagen sind dynamisch.

## Besondere Objekte

Besondere Objekte dürfen nur Spielwirkungen besitzen, wenn Entdeckung, Interaktionen, Risiken und Ergebnisse fachlich definiert sind. Dazu können Anomalien, stellare Überreste, verborgene Zugänge oder einzigartige Kampagnenobjekte gehören.

## Künstliche Objekte

Kolonien, Raumstationen, Außenposten und Flotten gehören nicht zur unveränderlichen natürlichen Struktur. Sie sind veränderliche Entitäten und verweisen auf System oder Himmelskörper.

## Bewegung innerhalb eines Systems

Auf der galaktischen Ebene ist ein System ein Knoten. Spätere Systeme können lokale Ziele unterscheiden. Aus einer grafischen Orbitposition entsteht ohne ausdrückliche Regel keine Reisezeit.

## Sichtbarkeit

Der Server kennt die vollständige Struktur. Ein Reich kann ein System kennen, ohne alle Planeten, Eigenschaften oder besonderen Objekte entdeckt zu haben. Der Client darf unbekannte Inhalte nicht durch IDs, Objektanzahlen oder Reihenfolgen indirekt offenlegen.

## Anforderungen an Client und Server

Der Client muss natürliche und künstliche Objekte sowie bekannte und unbekannte Eigenschaften unterscheiden. Der Server validiert Identitäten und Relationen, trennt statische von dynamischen Daten und filtert alle Ausgaben nach Reichswissen.

## Offene Folgefragen

1. Welche Stern- und Planetenkategorien gehören zum MVP?
2. Welche Himmelskörper können kolonisiert werden?
3. Welche Ressourcenobjekte werden für D4 benötigt?
4. Welche besonderen Objekte gehören zum MVP?

## Akzeptanzkriterien

- Alle adressierbaren Objekte besitzen stabile Identitäten.
- Eltern-Kind-Beziehungen sind eindeutig.
- Statische natürliche Struktur und dynamische Kampagnenobjekte sind getrennt.
- Grafische Positionen erzeugen keine undokumentierten Regeln.
- Verborgene Eigenschaften können reichsspezifisch gefiltert werden.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Bewegung und Verbindungen](bewegung-und-verbindungen.md)
- [Planeten – Übersicht](../04-planets/README.md)
