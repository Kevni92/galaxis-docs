# Raumansichten und Flotteninteraktion

Status: Freigegeben

## Zweck

Dieses Dokument definiert die visuelle und interaktive Nutzung von Sternensystem- und Galaxieansicht. Es konkretisiert Auswahl, Kamera, Flottenbewegung, Kontextaktionen, Wissensdarstellung und den Übergang zu Kampf oder Kolonisierung.

## Sternensystemansicht

### Darstellung

- Sterne, Planeten, Monde, Asteroidengürtel, besondere Himmelskörper, Stationen, Schiffe und Flotten werden als dreidimensionale Objekte dargestellt.
- Die Kamera blickt standardmäßig schräg von oben auf das System.
- Zoomen, Verschieben und begrenztes Drehen der Kamera verändern nur die Ansicht.
- Objektgrößen dürfen zur Lesbarkeit überzeichnet werden. Ein sichtbarer Planetendurchmesser ist keine Kollisions- oder Reichweitenregel.
- Umlaufbahnen dürfen als Orientierung dargestellt und animiert werden. Die Animation verändert keine autoritative Position, solange keine ausdrückliche Orbitalregel existiert.

### Fachliche Geometrie

Jedes lokal positionierte Objekt besitzt eine serverautoritative XY-Position innerhalb des Systems. Die 3D-Darstellung leitet daraus eine Szene ab.

```text
fachlich:     systemId + x + y
Darstellung:  x + y + visuelles z + Mesh + Animation
```

Nur `systemId`, `x` und `y` dürfen Bewegung, Entfernung, Sensorik, Abfangen oder Kampf beeinflussen. Visuelles `z`, Kamerawinkel und Meshgröße besitzen keine fachliche Wirkung.

## Auswahl

### Primärauswahl

Ein Primärklick oder die entsprechende Tastaturaktion:

1. wählt ein sichtbares Objekt,
2. markiert es in Szene und Outliner,
3. aktualisiert den Auswahlkontext,
4. öffnet bei Himmelskörpern und verwaltbaren Objekten das zugehörige modale Detailfenster.

Ein einfacher Hover darf eine kompakte Beschriftung zeigen, öffnet aber kein vollständiges Detailfenster.

### Mehrfachauswahl

Mehrfachauswahl ist nur für fachlich unterstützte Objektarten zulässig, insbesondere Flotten. Himmelskörperdetails bleiben auf ein primär ausgewähltes Objekt bezogen.

## Flottenauswahl

Bei ausgewählter Flotte zeigt die UI mindestens:

- Flottenname und Besitzer,
- Schiffe oder zusammengefasste Rollen,
- aktuellen Standort,
- aktiven Befehl und Warteschlange,
- Bewegungs-, Sensor- und Versorgungsstatus,
- vom Server angebotene Aktionen,
- sichtbare Route oder lokales Ziel.

Auswahl allein verändert keinen fachlichen Zustand.

## Lokale Bewegung

### Freier Zielpunkt

Ein Sekundärklick auf einen freien sichtbaren Punkt der Systemebene bereitet für die ausgewählte Flotte einen lokalen Bewegungsbefehl zu dieser XY-Position vor.

Vor der Bestätigung zeigt der Client, soweit vom Server bereitgestellt:

- Zielposition,
- geschätzte Route,
- Kampagnenzeit bis zur Ankunft,
- bekannte Risiken,
- mögliche Konflikte mit der aktuellen Warteschlange.

Der Client versetzt die Flotte erst, nachdem der Server den Befehl angenommen hat. Eine angezeigte Bewegung zwischen bestätigten Zuständen ist Interpolation und keine fachliche Fortschreibung.

### Warteschlange

Eine modifizierte Sekundäraktion, standardmäßig `Shift` plus Sekundärklick, darf einen Auftrag an die Flottenwarteschlange anhängen. Der Server prüft jeden Folgeauftrag vor seinem tatsächlichen Start erneut.

## Kontextaktionen auf Objekten

Ein Sekundärklick auf ein sichtbares Objekt öffnet ein Kontextmenü bezogen auf:

- ausgewählte Flotte oder Auswahlgruppe,
- Zielobjekt,
- reichsspezifisches Wissen,
- aktuellen diplomatischen Zustand,
- Reichweite, Fähigkeiten und Versorgung,
- laufende Befehle und Warteschlange.

Mögliche Aktionen sind beispielsweise:

- hierhin fliegen,
- Orbit oder lokalen Ankerpunkt ansteuern,
- erkunden,
- beobachten,
- kolonisieren,
- transportieren oder entladen,
- eskortieren,
- angreifen oder abfangen,
- reparieren oder versorgen,
- Details öffnen.

Die Existenz und Verfügbarkeit einer Aktion wird nicht allein im Client aus Objektarten kombiniert. Der Server oder ein serverautoritativ abgeleiteter Vertrag liefert:

- stabile Action-ID,
- lokalisierten Textschlüssel,
- aktiviert oder deaktiviert,
- sichtbaren Deaktivierungsgrund,
- Vorschau auf Kosten, Dauer und erwartbare Folge,
- den daraus entstehenden Befehlstyp.

## Planet und Kolonisierung

Ein Primärklick auf einen bekannten Planeten öffnet sein modales Detailfenster. Ein Sekundärklick bei ausgewählter Flotte kann zusätzlich Kontextaktionen anbieten.

`Kolonisieren` wird nur angeboten oder aktiviert, wenn der Server mindestens bestätigt:

- Planet und erforderliche Eigenschaften sind ausreichend bekannt,
- Ziel ist erreichbar und territorial zulässig,
- die Flotte besitzt die benötigte Kolonisierungsfähigkeit,
- Ressourcen, Bevölkerung und Kapazitäten genügen,
- keine ausschließende Konkurrenzsituation vorliegt.

Vor der Erteilung öffnet ein Bestätigungsdialog mit Voraussetzungen, Kosten, Dauer, Risiken und erwartbarem Koloniezustand. Das Planetendetail selbst bleibt ein lesendes modales Fenster, bis ein fachlicher Befehl ausgelöst wird.

## Feindliche Flotten und Kampfbeginn

Eine sichtbare feindliche Flotte kann abhängig von Wissen, Diplomatie und Haltung als Ziel verwendet werden.

Ein Kampf beginnt serverseitig, wenn:

- feindliche Flotten sich auf der autoritativen lokalen XY-Ebene innerhalb der definierten Begegnungs- oder Gefechtsreichweite befinden,
- Kriegs-, Zugangs- und Haltungsregeln eine Auseinandersetzung zulassen oder erzwingen,
- mindestens eine Seite angreift, abfängt oder nicht erfolgreich ausweichen kann.

Der Client darf einen Kampf nicht allein aufgrund optischer Nähe starten. Er zeigt bekannte Sensor-, Abfang- oder Gefechtsbereiche nur aus Serverdaten an.

Flottenhaltungen können beispielsweise `passiv`, `defensiv`, `abfangen`, `aggressiv` und `ausweichen` umfassen. Ihre genaue Wirkung wird im Flottenfachkonzept festgelegt.

## Galaxieansicht

Die Galaxieansicht zeigt ausschließlich freigegebene:

- Sternensysteme,
- Systemnamen oder zulässige Bezeichnungen,
- Verbindungen,
- Reichsgebiete und bekannte Kontrolle,
- Flottenpositionen oder Signaturen,
- Reiseziele und Routen.

Ein Primärklick wählt ein System und öffnet bei Bedarf ein modales Systemdetail. Ein Sekundärklick bei ausgewählter Flotte öffnet Aktionen wie:

- hierhin fliegen,
- Route planen,
- System erkunden,
- patrouillieren,
- eskortieren,
- Systemdetails öffnen.

Interstellare Bewegung folgt weiterhin ausschließlich bekannten und nutzbaren Graphverbindungen. Die visuelle Entfernung zwischen Sternen ist nicht allein entscheidend.

## Namen und Wissensdarstellung

- **Unbekannt:** Objekt wird nicht dargestellt und ist nicht auswählbar.
- **Geortet:** nur freigegebene grobe Darstellung; System- oder Objektname erscheint gedämpft beziehungsweise dunkelgrau.
- **Erkundet:** bekannte statische Struktur und bestätigte Namen erscheinen regulär, standardmäßig weiß.
- **Überwacht:** aktuelle dynamische Informationen und Aktivitätsmarker können erscheinen.
- **Veraltet:** letzte bekannte Information bleibt sichtbar, wird aber eindeutig als veraltet markiert.

Ein unbekannter Planet darf nicht als graue Kugel erscheinen, wenn bereits seine Existenz geheim ist. Graue Bezeichnungen gelten nur für tatsächlich freigegebene, aber noch nicht vollständig erkundete Objekte.

## Kamera und Orientierung

- Fokus auf ein Objekt bewegt die Kamera, nicht das Objekt.
- Der Spieler kann zur Flotte, zum Heimatplaneten oder zum ausgewählten System springen.
- Der Wechsel zwischen System- und Galaxieansicht erhält eine nachvollziehbare Auswahl, sofern das Objekt in beiden Ansichten sichtbar ist.
- Eine Schaltfläche und ein Shortcut stellen die Standardansicht wieder her.
- Optionales automatisches Kameranachführen darf jederzeit abgeschaltet werden.

## Tastatur- und Listenalternative

Alle sichtbaren Objekte müssen zusätzlich über eine zugängliche strukturierte Liste erreichbar sein.

- Pfeiltasten oder Listennavigation wählen Objekte.
- `Enter` öffnet Details.
- Eine Kontexttaste oder `Shift+F10` öffnet dieselben Kontextaktionen wie der Sekundärklick.
- Zielpunkte für freie Bewegung können über eine alternative Zielauswahl oder bekannte Navigationsanker gewählt werden, wenn präzise Mauspositionierung nicht möglich ist.
- Die 3D-Szene ist nicht die einzige Quelle für Namen, Status oder Befehle.

## Anforderungen an Client und Server

### Client

Der Client:

- rendert nur freigegebene Objekte,
- trennt Darstellung und fachliche XY-Geometrie,
- synchronisiert Szene, Outliner und Detailfenster,
- verwendet servergelieferte Kontextaktionen,
- interpoliert nur zwischen bestätigten Zuständen,
- bietet gleichwertige Tastatur- und Listenbedienung,
- öffnet Himmelskörperdetails modal.

### Server

Der Server:

- führt lokale Positionen und Bewegungen autoritativ,
- validiert freie Zielpunkte, Objektziele, Route, Reichweite und Fähigkeiten,
- liefert wissensgefilterte Objekte, Namen und Aktionen,
- entscheidet über Begegnung und Kampfbeginn,
- verarbeitet Befehle und Offline-Fortschritt deterministisch,
- verhindert Informationslecks über Auswahl, Aktionen oder Fehlergründe.

## Akzeptanzkriterien

- Sterne, Planeten und weitere Himmelskörper werden in der Systemansicht dreidimensional dargestellt.
- Lokale Bewegungs- und Kampfregeln verwenden ausschließlich die autoritative XY-Ebene.
- Ein Planet öffnet per Primärauswahl ein modales Detailfenster.
- Eine ausgewählte Flotte kann per Sekundäraktion einen freien Punkt oder ein Objekt als Ziel verwenden.
- Kontextaktionen werden nicht aus unbestätigter Clientlogik erfunden.
- Unbekannte Objekte und Namen werden nicht geleakt.
- Maus- und Tastaturabläufe führen zu denselben fachlichen Befehlen.
