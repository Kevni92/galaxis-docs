# Messgrößen und Qualitätsgrenzen

Status: Baseline v0.1

## Zweck

Balancing wird nicht anhand einzelner Bauchgefühle freigegeben. Dieses Dokument definiert Messgrößen, Zielkorridore und Warnsignale für Simulation und Playtests.

Messungen werden immer zusammen mit folgenden Metadaten gespeichert:

- Commit oder Build,
- Balancingversion,
- Szenarioversion,
- Simulationsseed,
- AI- oder Strategieprofil,
- Zeitprofil,
- Anzahl der Läufe,
- bekannte Abweichungen oder deaktivierte Systeme.

## Pacing-Metriken

| Kennzahl | Ziel für Baseline v0.1 |
|---|---:|
| Zeit bis erste relevante Erkundungsrückmeldung | 4–12 reale Stunden |
| Zeit bis erster Ausbau | 8–24 reale Stunden |
| Zeit bis erste Kolonie beauftragt | Tag 3–6 |
| Zeit bis erste Kolonie funktionsfähig | Tag 7–12 |
| Zeit bis erster Kontakt | Tag 4–12 |
| Zeit bis erste Technologie | Tag 2–4 |
| Beginn regelmäßiger Endgame-Dynamik | Woche 8–10 |
| formaler Kampagnenabschluss | Woche 10–14, Schwerpunkt Woche 12 |

Für automatisierte Läufe werden reale Zielzeiten über das Standard-Zeitprofil in Kampagnenzeit übersetzt.

## Stabilitätsmetriken

### Startreich

- Anteil der neutral gespielten Startreiche mit wirtschaftlichem Kollaps innerhalb der ersten 7 Tage: **unter 5 %**.
- Anteil der Startreiche ohne mindestens zwei sinnvolle Investitionsoptionen an Tag 1: **unter 10 %**.
- Anteil der Startreiche, die ohne neue Eingabe 72 Stunden vollständig handlungsunfähig werden: **unter 5 %**.

### Etabliertes Reich

- Anteil stabiler Reiche, die durch einen einzelnen normalen Engpass in eine irreversible Spirale geraten: **unter 10 %**.
- Median der essentiellen Reserve: **7 bis 14 Versorgungstage**.
- Median frei disponierbarer Überschuss: **10 bis 25 %**.
- Anteil dauerhaft unbesetzter notwendiger Stellen: normalerweise **unter 10 %**, Warnschwelle **20 %**.

## Aktivitäts- und Anwesenheitsmetriken

Balancing darf keine Klick- oder Anwesenheitsspirale erzeugen.

Zu messen sind:

- manuelle Entscheidungen pro realem Tag,
- notwendige Ansichtswechsel pro kurzer Sitzung,
- Zahl zeitkritischer Vorgänge,
- verpasster Wert durch einen statt vier Check-ins pro Tag,
- Zahl gleichartiger Wiederholungsaktionen,
- Anteil automatisch oder gebündelt verarbeitbarer Routinen.

Zielwerte:

- Median bedeutender manueller Entscheidungen: **1 bis 5 pro Tag**.
- Median bedeutender Ereignisentscheidungen: **höchstens 1 pro Tag**.
- Reiner Anwesenheitsvorteil von vier gegenüber einem Check-in pro Tag: im neutralen Vergleich **unter 10 %** bei zentralen Fortschrittsmetriken.
- Keine Kernaktion soll regelmäßig mehr als dreimal pro Sitzung identisch wiederholt werden müssen.

## Wirtschaftliche Metriken

- Produktion und Verbrauch je Gut und Zeiteinheit.
- Lagerreichweite in Versorgungstagen.
- Anteil reservierter gegenüber frei verfügbarer Mittel.
- Häufigkeit und Dauer von Mangelzuständen.
- Anteil verworfener Produktion wegen voller Lager.
- Transportauslastung und Transportverlust.
- Haushaltsanteile für Versorgung, Forschung, Expansion, Verwaltung und Militär.
- Zeit bis Erholung nach einem definierten Schock.

Warnsignale:

- Ein einzelnes Gut entscheidet in mehr als 70 % der neutralen Läufe allein über Erfolg oder Scheitern.
- Mehr als 25 % regulärer Produktion werden dauerhaft wegen Kapazitätsgrenzen verworfen.
- Ein Ressourcendefizit lässt sich durch eine triviale, immer gleiche Aktion ohne Opportunitätskosten lösen.
- Krieg finanziert sich im Mittel ohne Risiko vollständig selbst.

## Bevölkerungsmetriken

- natürliches Wachstum,
- Migration getrennt nach Quelle und Ziel,
- Beschäftigungsgrad,
- Qualifikationslücken,
- Versorgungsgrad,
- Dauer bis schwere Mangelfolgen,
- Erholungsdauer nach Versorgungskrise.

Warnsignale:

- Migration erzeugt oder vernichtet Bevölkerung.
- Eine Kolonie wächst trotz dauerhaft kritischer Grundversorgung normal weiter.
- Ein Populationstyp ist ohne sinnvolle Alternative in allen Produktionsbereichen optimal.
- Arbeitslosigkeit hat entweder keine erkennbare Folge oder führt sofort zur Unspielbarkeit.

## Forschungsmetriken

- Zeit je Technologieklasse,
- Abschlüsse je Kampagnenphase,
- Anteil ungenutzter Forschungsleistung,
- Häufigkeit von Forschungswechseln,
- technologische Streuung zwischen Reichen,
- Aufholgeschwindigkeit,
- Wert der Freischaltungen in Folgeentscheidungen.

Zielkorridore:

- 18 bis 30 bedeutende Abschlüsse pro Standardkampagne für ein aktives Reich.
- Kein neutrales Reich soll allein durch einen frühen Zufall dauerhaft mehr als eine vollständige Kampagnenphase zurückfallen.
- Eine Forschungsspezialisierung muss erkennbaren Vorteil und erkennbare Opportunitätskosten besitzen.

## Militärische Metriken

- Flottengröße und Unterhaltsanteil,
- Siegquote nach relativem Kampfwert,
- Gewinner- und Verliererverluste,
- Rückzugshäufigkeit,
- Vollvernichtungsquote,
- Reparatur- und Wiederaufbauzeit,
- Kriegsdauer,
- eroberter Wert gegenüber Kriegskosten,
- Anteil nicht kampfbedingter Verluste durch Logistik.

Qualitätsgrenzen:

- Bei etwa gleicher Ausgangsstärke liegt die Siegquote keiner Seite dauerhaft über 60 %, sofern Position und Doktrin neutral sind.
- Ein Verband mit ungefähr doppeltem effektiven Kampfwert gewinnt über viele neutrale Läufe deutlich häufiger, Zielwert **über 85 %**, aber nicht zwingend verlustfrei.
- Vollvernichtung bei annähernd ausgeglichenem Gefecht: **unter 10 %**.
- Begrenzter Krieg: Median **5 bis 14 reale Tage**.
- Wiederaufbau nach einer knappen Niederlage muss möglich sein, ohne bedeutungslos billig zu werden.

## Diplomatie- und Strategiemetriken

- Zahl und Dauer von Verträgen,
- Vertragsbruchquote,
- Anteil diplomatisch isolierter Reiche,
- Häufigkeit von Kriegen ohne erkennbares Ziel,
- Nutzen von Handel gegenüber Autarkie,
- Bildung dauerhafter Blöcke,
- Gegenmaßnahmen gegen dominante Reiche.

Eine Strategie gilt als dominant, wenn sie unter neutralen Startbedingungen über mehrere Seeds und Gegnertypen:

- in mehr als 60 % der Läufe den höchsten Gesamterfolg erzielt,
- keinen wesentlichen Gegenentwurf besitzt,
- und nicht mit proportional höherem Risiko oder Opportunitätskosten bezahlt wird.

## Endgame-Metriken

- Zeitpunkt des ersten ernsthaften Siegespfads,
- Zeitpunkt der Siegankündigung,
- verbleibende Gegenreaktionszeit,
- Anteil überraschender Abschlüsse ohne sichtbare Vorwarnung,
- Verteilung der Siegesrichtungen,
- Anteil formal beendeter Kampagnen,
- Dauer zwischen Endgame-Beginn und Abschluss.

Ziele:

- Endgame wird typischerweise Woche 8–10 relevant.
- Mehr als eine Siegesrichtung erreicht in einer Szenariomatrix realistische Erfolgschancen.
- Überraschende formale Abschlüsse ohne ausreichende Gegenreaktion: **unter 5 %**.

## Performance-Metriken

Balancingtests müssen auch technische Grenzen sichtbar machen:

- Simulationszeit je Kampagnentag,
- Speicher je Reich, Kolonie, Flotte und Ereignis,
- Größe des Änderungsprotokolls,
- Dauer der Offline-Nachholung,
- Datenmenge der REST-Synchronisation.

Performance darf nicht durch fachlich abweichende Abkürzungen erkauft werden.

## Statistikregeln

Berichte enthalten mindestens:

- Anzahl der Läufe,
- Mittelwert,
- Median,
- 10., 25., 75. und 90. Perzentil,
- Minimum und Maximum,
- Anteil außerhalb des Zielkorridors,
- Aufschlüsselung nach Strategieprofil und Seedgruppe.

Für seltene Ereignisse werden ausreichend viele Läufe oder gezielte Szenarien verwendet. Ein Mittelwert ohne Verteilung ist kein ausreichender Freigabenachweis.

## Freigabeampel

### Grün

- zentrale Metriken liegen im Zielkorridor,
- keine Erhaltungs- oder Determinismusverletzung,
- keine dominante Strategie ohne Gegenmaßnahme,
- bekannte Abweichungen sind gering und dokumentiert.

### Gelb

- einzelne Zielkorridore werden verfehlt,
- System bleibt spielbar und Ursache ist verstanden,
- Folge-Issue und Messplan existieren.

### Rot

- Fachinvariante verletzt,
- Ressourcen- oder Bevölkerungsduplizierung,
- Informationsleck,
- deterministisch nicht reproduzierbar,
- regelmäßige irreparable Spirale,
- eindeutig dominante triviale Strategie,
- Kampagne kann ihren Zielbogen nicht erreichen.

Ein roter Befund blockiert eine Validiert- oder Release-Freigabe.