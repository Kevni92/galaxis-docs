# UI und UX

Dieser Bereich beschreibt die verbindliche Bedien- und Darstellungssprache von Galaxis. Er legt fest, wie die räumliche Hauptansicht, Fenster, Tabs, Shortcuts, Datenlayouts, Kontextaktionen, Lokalisierung und Begriffserklärungen zusammenwirken.

## Grundsatz

Die häufigste Ansicht einer laufenden Kampagne ist nicht eine Verwaltungsseite, sondern eine permanente Raumansicht. Das Sternensystem oder die Galaxie bleibt sichtbar, während Informationen und Befehle in einheitlichen Fenstern, Outlinern, Kontextmenüs und Popovers dargestellt werden.

Die 3D-Darstellung ist eine Visualisierung der serverautoritativen Welt. Sie bildet keine eigene Spielsimulation.

## Dokumente

- [Game Shell und Fenstersystem](game-shell-und-fenstersystem.md)
- [Raumansichten und Flotteninteraktion](raumansichten-und-flotteninteraktion.md)
- [Komponenten, Lokalisierung und Begriffskatalog](komponenten-lokalisierung-und-begriffskatalog.md)

## Verbindliche Leitlinien

1. Sternensystem- und Galaxieansicht bilden die räumliche Arbeitsfläche.
2. Sterne, Planeten und andere Himmelskörper werden in der Systemansicht dreidimensional gerendert.
3. Fachlich relevante lokale Geometrie bleibt zweidimensional und serverautoritativ.
4. Objekt- und Planetendetails öffnen als modale Fenster über der Raumansicht.
5. Alle normalen Inhaltsfenster folgen derselben Struktur und demselben Komponentenbestand.
6. Jeder Mausablauf besitzt eine gleichwertige Tastaturbedienung.
7. Sichtbare Texte stammen aus Sprachdateien; Fachbegriffe stammen aus einem strukturierten Katalog.
8. Der Client zeigt nur Informationen und Aktionen, die für das kontrollierte Reich freigegeben sind.
9. Farben, Animationen und 3D-Größe dürfen keine alleinige oder verborgene Bedeutung tragen.
10. Der jeweilige Alpha-Slice implementiert nur die benötigten Komponenten, aber niemals ein abweichendes UX-Grundmodell.

## Fachliche und technische Grenzen

- Fachliche Zustände, Befehle, Positionen, Reichweiten und Wissen werden in den jeweiligen Domänendokumenten und Verträgen definiert.
- Diese UI-Dokumente definieren Darstellung, Interaktion, Fokus, Navigation und Komponentenverwendung.
- Die technische Rendering- und Cliententscheidung steht in [Decision 0007](../../decisions/0007-client-ui-rendering-und-lokalisierung.md).
- Präzise Interaktionsverträge stehen unter [`contracts/ui/`](../../contracts/ui/README.md).

Zurück zur [Dokumentationsübersicht](../README.md).
