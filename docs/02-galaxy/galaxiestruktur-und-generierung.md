# Galaxiestruktur und Generierung

Status: Freigegeben

## Zweck

Dieses Dokument definiert die räumliche Grundstruktur einer Galaxis-Kampagne und die Anforderungen an ihre Erzeugung. Konkrete Zahlen für Systemanzahl, Dichte und Balancing werden später je Kampagnenprofil festgelegt.

## Grundmodell

Die Galaxie wird als zusammenhängender Graph modelliert:

- Sternensysteme sind Knoten.
- Interstellare Verbindungen sind Kanten.
- Koordinaten dienen Darstellung, regionaler Einordnung und Distanzberechnungen.
- Für reguläre interstellare Bewegung ist die Verbindung im Graphen maßgeblich, nicht eine frei gezeichnete Luftlinie.

Die räumliche Grundstruktur wird bei Kampagnenstart erzeugt und bleibt während der Kampagne stabil. Spätere Spielsysteme dürfen Zustände innerhalb dieser Struktur verändern, aber keine stillschweigende Neugenerierung der Galaxie auslösen.

## Generierungsprofil

Jede Kampagne besitzt ein Generierungsprofil. Es beschreibt mindestens:

- Größenklasse der Galaxie,
- angestrebte Systemdichte,
- Anzahl spielbarer Startreiche,
- Häufigkeit besonderer Regionen,
- gewünschte Verzweigung und Anzahl alternativer Routen,
- optionale Kampagneneinstellungen.

Konkrete Profile wie klein, mittel oder groß werden erst beim Balancing mit Zahlen belegt. Spielregeln sollen sich auf Profilmerkmale beziehen und nicht auf fest codierte Systemzahlen.

## Deterministische Erzeugung

Die Erzeugung muss reproduzierbar sein. Folgende Eingaben bestimmen das Ergebnis:

```text
Generierungs-Seed
+ Generatorversion
+ Generierungsprofil
+ freigegebene Kampagneneinstellungen
```

Gleiche Eingaben müssen dieselbe räumliche Struktur und dieselben statischen Himmelskörper erzeugen.

Nach erfolgreicher Erzeugung speichert der Server die vollständige Galaxie als autoritativen Kampagnenzustand. Eine Kampagne wird nicht bei jedem Laden erneut aus dem Seed aufgebaut. Seed und Generatorversion bleiben für Diagnose und Wiederholbarkeit gespeichert.

## Form und Regionen

Die Galaxie besitzt eine begrenzte, zusammenhängende Spielfläche. Systeme können zu Regionen oder Sektoren gruppiert werden. Regionen dienen Navigation, Inhaltsverteilung und späteren Gebietsregeln, bilden aber keine zusätzliche Besitzebene.

## Verbindungsstruktur

Für die reguläre Galaxie gelten folgende Invarianten:

- Jedes spielbare Startsystem gehört zum zusammenhängenden Hauptgraphen.
- Kein Startreich darf durch eine einzige unvermeidbare Sackgasse grundsätzlich handlungsunfähig sein.
- Wichtige Regionen sollen nach Möglichkeit über mehr als eine strategisch relevante Route erreichbar sein.
- Sackgassen und Engstellen sind erlaubt, müssen aber bewusst erzeugt werden.
- Unverbundene Sonderräume sind nur zulässig, wenn ein späteres System einen ausdrücklichen Zugang definiert.

Die Erzeugung muss unerreichbare reguläre Systeme, doppelte Verbindungen und ungültige Selbstverbindungen erkennen und ablehnen.

## Startpositionen

Jede spielbare Startposition muss mindestens:

- ein eindeutig bestimmtes Startsystem besitzen,
- Zugang zum Hauptgraphen haben,
- Raum für frühe Erkundung und Entwicklung bieten,
- keine unmittelbar unvermeidbare strategische Blockade enthalten,
- hinsichtlich früher Chancen innerhalb einer definierten Toleranz vergleichbar sein.

Vergleichbar bedeutet nicht vollständig symmetrisch. Unterschiedliche Umgebungen sind erwünscht, solange keine Startposition offensichtlich unspielbar oder strukturell überlegen ist.

## Statische und veränderliche Daten

Statisch sind Systemidentitäten, Koordinaten, natürliche Himmelskörper, grundlegende Verbindungen, Regionen und unveränderliche Generierungsmerkmale. Veränderlich sind Wissen, Kolonien, künstliche Objekte, Besitz, Kontrolle und aktuelle Zugänglichkeit.

## Validierung vor Kampagnenstart

Vor dem Start werden mindestens Zusammenhang, gültige Verbindungen, stabile IDs, Startpositionen, Profilkonformität und Reproduzierbarkeit geprüft. Bei Fehlern startet keine teilweise gültige Kampagne.

## Anforderungen an Client und Server

Der Client stellt nur freigegebene Systeme und Verbindungen dar und rekonstruiert keine vollständige Galaxie aus dem Seed. Der Server erzeugt, validiert, speichert und filtert die Struktur autoritativ.

## Offene Balancingfragen

1. Welche konkreten Größenprofile werden angeboten?
2. Welche Toleranzen gelten für vergleichbare Startpositionen?
3. Wie häufig dürfen Engstellen, Sackgassen und besondere Regionen auftreten?

## Akzeptanzkriterien

- Die Galaxie ist als deterministisch erzeugter, zusammenhängender Graph definiert.
- Seed, Generatorversion und Profil ermöglichen Reproduktion.
- Startpositionen werden anhand überprüfbarer Mindestbedingungen validiert.
- Statische Struktur und veränderlicher Kampagnenzustand sind getrennt.
- Der Client kann keine verborgene Galaxie lokal rekonstruieren.

## Verwandte Dokumente

- [Sternensysteme und Himmelskörper](sternensysteme-und-himmelskoerper.md)
- [Bewegung und räumliche Verbindungen](bewegung-und-verbindungen.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Besitz und Kontrolle](besitz-und-kontrolle.md)
