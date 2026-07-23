# 0007 – Client-UX, 3D-Raumdarstellung und Lokalisierung

Status: angenommen

Datum: 2026-07-23

Ersetzt: [0006 – Alpha-Clienttechnologiestack](0006-alpha-client-technologiestack.md)

## Kontext

Der Client soll nicht aus voneinander unabhängigen Vollbildseiten bestehen. Die häufigste Spielansicht ist eine räumliche Sternensystem- oder Galaxieansicht, über der einheitliche Fenster, Kontextmenüs und Detaildialoge geöffnet werden. Sterne, Planeten, Monde und andere Himmelskörper sollen räumlich verständlich und visuell hochwertig dargestellt werden, ohne daraus eine zweite clientseitige Physik- oder Simulationslogik abzuleiten.

Die frühere Entscheidung 0006 sah SVG als primäre Kartenlösung und keine 3D-Engine für A0 bis A3 vor. Das ist mit der nun festgelegten Ziel-UX nicht vereinbar.

## Entscheidung

### Clientstack

Für den Desktop-Webclient gilt:

- TypeScript,
- Vue 3 mit Composition API,
- Vite,
- Vue Router,
- Pinia,
- eine zentrale native-`fetch`-Abstraktion,
- aus OpenAPI generierte TypeScript-Typen,
- Vitest und Vue Test Utils,
- Playwright für kritische End-to-End-Abläufe,
- Three.js über eine kleine gekapselte Rendering-Schicht für Sternensystem- und Galaxieansicht,
- HTML, CSS und Vue-Komponenten für Topbar, Outliner, Fenster, Dialoge, Tabellen, Tooltips und Kontextmenüs,
- YAML-basierte Sprachdateien für alle sichtbaren Texte,
- ein strukturierter Begriffskatalog für rekursive Erklärungen in der UI.

Konkrete Bibliotheksversionen werden im Clientrepository fest gepinnt. Eine vollständige Game-Engine wird nicht eingeführt.

### 3D-Darstellung und 2D-Spielgeometrie

- Sterne, Planeten, Monde, Asteroidengürtel, besondere Himmelskörper, Stationen, Schiffe und Flotten werden in der Sternensystemansicht grundsätzlich dreidimensional gerendert.
- Die fachlich relevante lokale Bewegung findet ausschließlich auf einer autoritativen zweidimensionalen XY-Ebene statt.
- Eine visuelle Z-Koordinate, Objektneigung, Animation oder Größenüberzeichnung besitzt keine fachliche Wirkung.
- Der Server liefert stabile Identitäten, bekannte Eigenschaften sowie fachlich relevante Positionen und Zustände. Der Client darf keine Reichweite, Erreichbarkeit, verborgenen Objekte oder Reisezeit aus der Darstellung ableiten.
- Eine physikalisch exakte Orbital- oder Kollisionssimulation ist nicht Bestandteil des MVP.
- Die Galaxieansicht darf ebenfalls dreidimensional gerendert werden; ihre fachliche Bewegung bleibt an den autoritativen Systemgraphen und bekannte Verbindungen gebunden.

### Game Shell und Fenster

- Die Raumansicht bildet die permanente Arbeitsfläche einer laufenden Kampagne.
- Globale Werte und Kampagnenzeit stehen in einer Topbar.
- Hauptbereiche sind über ein linkes Zugriffsmenü und konfigurierbare Shortcuts erreichbar.
- Ein rechter Outliner fasst Planeten, Kolonien, Flotten und laufende Vorgänge zusammen.
- Normale Inhaltsbereiche öffnen als einheitliche modale Fenster über der Raumansicht.
- Fenster verwenden ein gemeinsames Größenraster, eine feste Titelzeile, Tabs, definierte Inhaltslayouts und einen einheitlichen Aktionsbereich.
- Planet-, Stern-, Flotten- und sonstige Objektdetails werden beim Auswählen in einem modalen Detailfenster dargestellt. Sie ersetzen die Raumansicht nicht durch eine eigene Vollbildseite.
- Vollbildansichten bleiben auf fachlich begründete Ausnahmen wie einen Technologiebaum oder eine großflächige Analyseansicht beschränkt.

### Auswahl und Befehle

- Primärauswahl wählt ein bekanntes Objekt aus und synchronisiert Szene, Outliner und Detailfenster.
- Ein Sekundärklick auf einen freien Punkt bei ausgewählter Flotte bereitet einen lokalen Bewegungsbefehl zu dieser XY-Position vor.
- Ein Sekundärklick auf ein Objekt öffnet ein Kontextmenü mit den für Auswahl, Ziel, Wissen und aktuellem Zustand zulässigen Aktionen.
- Verfügbare Aktionen, deaktivierte Gründe, Kosten, Dauer und erwartbare Folgen werden aus Serverdaten oder einem serverautoritativen Aktionsvertrag abgeleitet.
- Der Client erfindet keine Befehlsberechtigung aus Schiffstyp, Zieltyp oder sichtbaren Werten.
- Jede Mausinteraktion besitzt eine gleichwertige Tastatur- und Listenalternative.

### Lokalisierung und Begriffskatalog

- Sichtbare Texte werden nicht direkt in Komponenten festgeschrieben.
- Sprachdateien verwenden stabile Schlüssel und erhalten ausschließlich explizite, typisierte Kontextwerte.
- Eine kleine sichere Formatierungsgrammatik unterstützt Zahlen, Prozente, Kampagnenzeit, Ressourcen, Hervorhebungen, Icons, Shortcuts und Verweise auf Spielbegriffe.
- Sprachdateien dürfen weder beliebiges HTML noch beliebige JavaScript-Ausdrücke ausführen.
- Fachbegriffe besitzen stabile Katalogschlüssel. Hover oder Tastaturfokus zeigt eine Kurzdefinition; ein fixiertes Popover kann rekursiv zu verwandten Begriffen navigieren, ohne mehrere schwebende Popups zu stapeln.

## Architekturregeln

1. Der Server bleibt für Zustand, Zeit, Wissen, Zufall, Berechtigungen, Befehle, lokale Positionen und Kampfzustände autoritativ.
2. Die Rendering-Schicht kennt Darstellungsobjekte, Kamera, Auswahl und Picking, aber keine eigene Spielsimulation.
3. Vue-Komponenten rufen weder Three.js noch `fetch` unkontrolliert direkt auf; beide Grenzen werden über klar definierte Adapter angesprochen.
4. Die Szene verwendet ausschließlich serverseitig freigegebene Objekte und Eigenschaften.
5. Clientprognosen werden als Prognose mit Datenstand gekennzeichnet und nach Serverantwort korrigiert.
6. Lokale Auswahl, Fensterzustand, Kamera und Hover sind Clientzustände; fachliche Position, Reise, Wissen und Befehle sind Serverzustände.
7. Reduzierte Bewegung, Skalierung der UI und eine nichtgrafische Objektliste müssen möglich sein.

## Nicht gewählt

- keine fachliche 3D-Physik,
- keine frei fliegenden Schiffe außerhalb der autoritativen XY-Ebene,
- keine Regelableitung aus Meshgröße, Orbitgrafik oder Kameraperspektive,
- keine vollständig clientseitige Pfad-, Kampf- oder Kolonisierungslogik,
- keine Fullscreen-Detailseite für jeden Planeten oder jede Flotte,
- kein unkontrolliertes HTML in Sprachdateien,
- keine verpflichtende WebSocket-Schnittstelle nur wegen der 3D-Darstellung.

## Folgen

- A1 führt die 3D-Sternensystemansicht und modale Himmelskörperdetails als Grundstruktur ein.
- A2 ergänzt Flottenauswahl, lokale XY-Bewegung, Kontextaktionen und Reisefortschritt.
- A3 ergänzt die wissensgefilterte Galaxieansicht und interstellare Kontextaktionen.
- A4 verwendet dieselbe Kontextaktion für Kolonisierung.
- A11 verwendet dieselbe lokale Geometrie für Begegnungs-, Abfang- und Kampfbeginn.
- Bestehende Client-Issues, OpenAPI-Schemas und Tests, die SVG, reine Navigationspunkte oder Vollbilddetails voraussetzen, müssen vor ihrer Umsetzung an diese Entscheidung angeglichen werden.

## Überprüfung

Die Entscheidung ist umgesetzt, wenn:

- Himmelskörper in der Sternensystemansicht über die gekapselte 3D-Schicht erscheinen,
- fachliche Bewegung und Reichweiten ausschließlich aus serverseitigen XY-Daten entstehen,
- ein Planet per Auswahl ein modales, tastaturbedienbares Detailfenster öffnet,
- Maus- und Tastaturbedienung dieselben fachlichen Befehle auslösen können,
- unbekannte Objekte nicht durch Rendering, Picking oder Bezeichnungen geleakt werden,
- sichtbare Texte und Begriffserklärungen vollständig aus der Lokalisierungs- und Katalogschicht stammen.
