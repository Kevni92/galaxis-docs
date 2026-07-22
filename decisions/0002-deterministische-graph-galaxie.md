# 0002 – Deterministische Graph-Galaxie mit reichsspezifischem Wissen

Status: angenommen

Datum: 2026-07-22

## Kontext

Galaxis benötigt eine räumliche Grundlage, die reproduzierbar erzeugt, deterministisch simuliert und asynchron ausgewertet werden kann. Gleichzeitig sollen Erkundung, Engstellen und territoriale Konflikte möglich sein, ohne verborgene Informationen an Clients oder AI-Systeme weiterzugeben.

## Entscheidung

1. Die Galaxie wird aus Seed, Generatorversion und Profil deterministisch erzeugt.
2. Sternensysteme bilden Knoten, interstellare Verbindungen bilden Kanten.
3. Koordinaten dienen der Darstellung, erlauben aber keine freie reguläre Bewegung ohne Verbindung.
4. Die erzeugte natürliche Struktur wird persistent gespeichert.
5. Wissen wird pro Reich geführt und von der serverseitigen Wahrheit getrennt.
6. Statisches Erkundungswissen und aktuelle Überwachung sind getrennt.
7. Spieler- und AI-Controller erhalten nur den Wissensstand ihres Reiches.
8. Anspruch, souveräner Besitz, militärische Kontrolle und Besetzung werden getrennt gespeichert.
9. Eine Flotte allein erzeugt keinen dauerhaften Besitz.

## Begründung

Ein Graph erzeugt verständliche Routen, strategische Engstellen und deterministisch prüfbare Bewegung. Reichsspezifisches Wissen ist Voraussetzung für Fog of War, faire AI und sichere REST-Ausgaben. Getrennte territoriale Zustände verhindern, dass kurzfristige militärische Präsenz automatisch Souveränität erzeugt.

## Betrachtete Alternativen

### Freie Bewegung anhand von Koordinaten

Sie erschwert Routenplanung, Reichweite, Sichtbarkeit und Grenzbildung erheblich.

### Vollständige Galaxie für jeden Controller

Dies widerspricht Fog of War und macht AI-Reichsübernahmen unfair.

### Ein einzelner Eigentumswert

Er kann Anspruch, Besitz und Besetzung nicht nachvollziehbar abbilden.

### Neugenerierung bei jedem Laden

Generatoränderungen könnten laufende Kampagnen verändern. Der Seed dient Reproduktion; die Kampagne verwendet persistente Daten.

## Positive Folgen

- reproduzierbare Kampagnen und Tests,
- verständliche Routen,
- einheitliches Fog of War,
- klare territoriale Zustände,
- sichere reichsspezifische REST-Ausgaben.

## Negative Folgen und Risiken

- hoher Validierungsbedarf für Generator und Startfairness,
- Generatorversion muss gespeichert werden,
- reichsspezifische Wissensstände erhöhen Speicher- und Testaufwand,
- besondere Bewegungsarten benötigen explizite Regeln.

## Betroffene Dokumente

- [Galaxiestruktur und Generierung](../docs/02-galaxy/galaxiestruktur-und-generierung.md)
- [Sternensysteme und Himmelskörper](../docs/02-galaxy/sternensysteme-und-himmelskoerper.md)
- [Erkundung und Informationsstände](../docs/02-galaxy/erkundung-und-informationsstaende.md)
- [Bewegung und Verbindungen](../docs/02-galaxy/bewegung-und-verbindungen.md)
- [Besitz und Kontrolle](../docs/02-galaxy/besitz-und-kontrolle.md)

## Ersetzt

keine

## Ersetzt durch

keine
