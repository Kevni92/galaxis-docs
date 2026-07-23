# Game Shell und Fenstersystem

Status: Freigegeben

## Zweck

Dieses Dokument definiert die dauerhaft sichtbare Kampagnenoberfläche und das einheitliche Fenstersystem. Einzelne Spielbereiche dürfen eigene Inhalte besitzen, aber keine abweichende Navigations- oder Fensterlogik einführen.

## Permanente Game Shell

Während einer laufenden Kampagne besteht die Oberfläche aus fünf stabilen Bereichen:

1. **Raumansicht:** Sternensystem oder Galaxie als zentrale Arbeitsfläche.
2. **Topbar:** Kampagnenzeit, Laufzustand und globale Ressourcen oder Kapazitäten.
3. **Zugriffsmenü links:** Hauptbereiche wie Reich, Kolonien, Flotten, Forschung und Diplomatie.
4. **Outliner rechts:** kompakte, gruppierte Übersicht über wichtige eigene Objekte und laufende Vorgänge.
5. **Fenster- und Meldungsebene:** modale Inhaltsfenster, Kontextmenüs, Tooltips, Begriffspopovers und Benachrichtigungen.

Die Raumansicht bleibt im Hintergrund erhalten, solange kein ausdrücklich definierter Vollbildmodus aktiv ist.

## Ansichtsebenen

### Sternensystemansicht

Die Sternensystemansicht ist die Standardarbeitsfläche für lokale Objekte und Flotten. Sterne, Planeten, Monde und andere bekannte Objekte werden dreidimensional gerendert. Die fachlich relevante Bewegung verwendet ausschließlich die serverseitige XY-Ebene.

### Galaxieansicht

Die Galaxieansicht zeigt bekannte Sternensysteme, bekannte Verbindungen, Reichswissen und zulässige Flottenziele. Sie kann dreidimensional gerendert werden, bleibt fachlich jedoch ein Graph aus Systemen und Verbindungen.

Der Wechsel zwischen beiden Ansichten muss jederzeit über einen sichtbaren Befehl und einen konfigurierbaren Shortcut möglich sein. Der Wechsel verändert keinen Spielzustand.

## Standardfenster

Normale Spielbereiche öffnen in einem zentralen modalen Fenster. Ein Standardfenster besitzt:

```text
Titelzeile
├── Titel und Kontext
├── optionaler Shortcut-Hinweis
├── Hilfe
└── Schließen

Tableiste

Inhaltsbereich
├── Zusammenfassung oder Status
├── einheitliche Abschnitte
├── Property-Grids, Tabellen oder Listen
└── optionale Detailtiefe

Aktionsbereich
├── Hinweise oder Validierungsgründe
├── sekundäre Aktionen
└── primäre Aktion
```

Standardfenster verwenden dieselbe Grundgröße und dieselben Innenabstände. Abweichungen sind nur für klar definierte kleine Dialoge, große Vergleichsfenster oder Vollbildansichten zulässig.

## Fensterklassen

### Standardfenster

Für Kolonie, Planet, Flotte, Reich, Forschungsauswahl, Diplomatie und vergleichbare Inhalte.

### Kleiner Dialog

Für Bestätigungen, Benennungen, Mengenangaben und klar begrenzte Auswahlentscheidungen. Kleine Dialoge dürfen kein eigenes Navigationssystem enthalten.

### Großes Fenster

Für datenreiche Vergleiche oder breite Tabellen, wenn ein Standardfenster den Inhalt nachweislich unlesbar machen würde.

### Vollbildansicht

Nur für Inhalte, deren räumliche oder strukturelle Gesamtübersicht den gesamten Arbeitsbereich benötigt, beispielsweise ein Technologiebaum oder eine umfangreiche Analyseansicht. Planet-, Stern-, Kolonie- und Flottendetails sind keine Vollbildansichten.

## Objektdetails

Ein Primärklick auf einen bekannten Himmelskörper oder ein künstliches Objekt wählt dieses aus. Die Details werden in einem modalen Standardfenster angezeigt.

Für einen Planeten bedeutet dies:

- Die 3D-Sternensystemansicht bleibt hinter dem Fenster sichtbar.
- Das Fenster zeigt Planetengrunddaten, bekannten Wissensstand und gegebenenfalls Kolonieinformationen.
- Inhaltliche Bereiche werden über Tabs wie `Übersicht`, `Kolonie`, `Bevölkerung`, `Versorgung` oder später `Gebäude` gegliedert.
- Nur Tabs mit fachlich vorhandenen und sichtbaren Daten werden angeboten.
- Die Auswahl des Planeten bleibt in der Szene und im Outliner markiert.
- Schließen des Fensters entfernt nicht zwingend die Auswahl.

Objektdetails dürfen nicht durch eine eigenständige Vollbildroute die räumliche Orientierung unterbrechen. Stabile Deep Links dürfen ein Objekt auswählen und sein Detailfenster direkt öffnen.

## Tabs und Fokus

- `Tab` bewegt den Fokus in dokumentierter Reihenfolge durch die Bedienelemente des aktiven Fensters.
- Eine fokussierte Tableiste kann mit Pfeiltasten navigiert werden.
- `Enter` oder `Leertaste` aktiviert den fokussierten Tab.
- `Ctrl+Tab` und `Ctrl+Shift+Tab` dürfen zwischen Tabs wechseln, sofern keine Betriebssystem- oder Browserfunktion verletzt wird.
- Beim Tabwechsel bleibt der Fokus an einer nachvollziehbaren Stelle.
- Nicht sichtbare Tabinhalte dürfen keine fokussierbaren Elemente besitzen.
- `Escape` schließt das oberste schließbare Fenster oder Kontextmenü.
- Nach dem Schließen kehrt der Fokus zum auslösenden Objekt, Menüeintrag oder Outlinerpunkt zurück.

## Shortcuts

Shortcuts werden über stabile Action-IDs definiert und sind konfigurierbar. Komponenten prüfen keine fest codierten Tasten.

Beispiele:

```yaml
open_galaxy_view: G
open_system_view: S
open_empire: F2
open_research: F4
open_fleets: F6
close_window: Escape
```

Jede Shortcut-Aktion besitzt:

- eine lokalisierte Bezeichnung,
- eine Standardbelegung,
- eine mögliche alternative Belegung,
- Konfliktprüfung,
- sichtbare Darstellung in Tooltips und Menüs.

## Inhaltliches Grundmuster

Alle Inhaltsseiten und Tabs verwenden dieselbe Reihenfolge:

1. Kontext und wichtigste Aussage,
2. Status, Warnung oder Entscheidung,
3. kompakte Kerndaten,
4. Details und Ursachen,
5. Verlauf, Warteschlange oder verwandte Objekte,
6. Aktionen.

Daten mit Label und Einzelwert verwenden ein Property-Grid:

```text
Bevölkerung                 1.250.000
Koloniestatus               Etabliert
Grundversorgung             Stabil
Nahrungsreserve             34 Tage
Datenstand                  Kampagnenzeit 2842.05.17
```

Label stehen links, Werte rechts. Einheiten, Datenstand und Unsicherheit werden explizit angezeigt. Fehlende oder unbekannte Werte erscheinen nicht als `0`.

## Layering

Von unten nach oben gilt:

1. Raumansicht,
2. permanente Shell,
3. Hauptfenster,
4. kleiner Dialog über Hauptfenster,
5. Kontextmenü oder Tooltip,
6. kritische Systemmeldung.

Es darf nicht unbegrenzt eine Kette modaler Hauptfenster entstehen. Ein neues Hauptfenster ersetzt oder fokussiert das bisherige. Kleine Bestätigungsdialoge dürfen kurzfristig darüberliegen.

## Outliner

Der Outliner zeigt nur kompakte, handlungsrelevante Informationen. Er ist kein Ersatz für Detailfenster.

- Gruppen sind ein- und ausklappbar.
- Auswahl in Outliner und Raumansicht ist synchron.
- Doppelklick oder definierte Aktivierung fokussiert das Objekt in der Raumansicht.
- Ein Kontextmenü verwendet dieselben verfügbaren Aktionen wie das räumliche Objekt.
- Warnungen und Status sind nicht ausschließlich farbcodiert.

## Zustände

Jedes Fenster und jeder Inhaltsbereich unterstützt mindestens:

- `loading`,
- `loaded`,
- `empty`,
- `partial`,
- `stale`,
- `blocked`,
- `forbidden`,
- `not-found`,
- `error`.

Ein fehlender Wert, eine unbekannte Eigenschaft und ein tatsächlicher Nullwert werden unterschiedlich dargestellt.

## Anforderungen an die Umsetzung

- Fenster, Tabs, Fokus und Shortcuts werden zentral implementiert.
- Fachmodule setzen Inhalte aus gemeinsamen Komponenten zusammen.
- Sichtbare Texte stammen aus Sprachdateien.
- Detailfenster dürfen keine eigene REST- oder Befehlslogik umgehen.
- Raumansicht, Outliner und Fenster verwenden dieselbe stabile Objektauswahl.
- Alle wesentlichen Abläufe sind ohne präzise Mausbedienung erreichbar.

## Akzeptanzkriterien

- Planetendetails öffnen als modales Fenster über der 3D-Systemansicht.
- Standardfenster besitzen dieselbe erkennbare Struktur.
- Tabs sind vollständig per Tastatur bedienbar.
- Deep Links können Ansicht, Objekt und offenen Tab wiederherstellen.
- Schließen eines Fensters stellt einen nachvollziehbaren Fokus wieder her.
- Kein Fachmodul führt ohne neue Entscheidung ein eigenes Fenstersystem ein.
