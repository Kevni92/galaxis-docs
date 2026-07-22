# Bevölkerung und Beschäftigung

Status: Baseline v0.1

Fachliche Grundlage: [`docs/05-population/`](../../docs/05-population/README.md)

## Ziel

Bevölkerung soll gleichzeitig Arbeitskraft, Verbraucher, langfristige Entwicklung und strategisch gebundener Standortwert sein. Wachstum darf nicht nur eine passive Exponentialkurve sein; Versorgung, Wohnraum, Sicherheit, Migration und Qualifikation müssen sichtbare Entscheidungen erzeugen.

## Populationsdarstellung

Balancingwerte gelten für aggregierte Populationseinheiten. Die konkrete Skalierung einer Einheit wird im Datenkatalog festgelegt und bleibt über eine Kampagne stabil.

Zu unterscheiden sind:

- Gesamtbevölkerung,
- erwerbsfähige Bevölkerung,
- verfügbare Arbeitskraft,
- beschäftigte Arbeitskraft,
- Qualifikationsgruppen,
- Migration,
- vorübergehend nicht verfügbare Gruppen.

Eine Personengruppe darf nicht gleichzeitig mehrfach als Arbeitskraft gezählt werden.

## Natürliches Wachstum

Für eine etablierte, gut versorgte Kolonie gilt als erste Zielrate:

- **0,5 bis 1,5 % pro realer Woche** im Standardprofil.

Eine junge Kolonie kann durch Aufbauprogramme und Altersstruktur zeitweise schneller wachsen. Dauerhaftes natürliches Wachstum oberhalb von **2 % pro Woche** benötigt eine deutliche Ursache und Prüfung gegen exponentielle Skalierung.

Einflussfaktoren:

- Grundversorgung,
- Wohn- und Infrastrukturkapazität,
- Gesundheit und Umwelt,
- Sicherheit und Stabilität,
- politische oder kulturelle Modifikatoren,
- Alters- oder Populationsstruktur, sofern später fachlich vorgesehen.

## Migration

Migration verschiebt Bevölkerung und erzeugt sie nicht.

Erste Zielkorridore:

- normale Nettoveränderung einer Kolonie durch Migration: höchstens **5 % pro realer Woche**,
- außergewöhnliche Krisen- oder Umsiedlungsprogramme dürfen darüber liegen,
- Transport-, Reichweiten- und Aufnahmekapazitäten begrenzen Migration,
- Quellkolonien verlieren dieselbe Population, die Zielkolonien erhalten,
- laufende Migration muss bei Unterbrechung deterministisch behandelt werden.

Migrationsattraktivität soll aus mehreren Faktoren entstehen, nicht nur aus einem globalen Bonus:

- verfügbare Arbeit,
- Versorgung,
- Wohnraum,
- Sicherheit,
- Freiheit oder Politik,
- Nähe und Transportkosten,
- soziale oder kulturelle Bindungen, sofern fachlich vorgesehen.

## Arbeitskräfte

Eine Kolonie besitzt nicht automatisch für jede Aufgabe passende Arbeitskraft.

Zielkorridore:

| Kennzahl | normal | Warnung | kritisch |
|---|---:|---:|---:|
| Beschäftigung passender Erwerbsfähiger | 90–98 % | 80–90 % | unter 80 % |
| freie Arbeitsreserve | 3–10 % | unter 3 % oder über 15 % | über 25 % |
| unbesetzte notwendige Stellen | unter 10 % | 10–20 % | über 20 % |
| Qualifikationslücke in Schlüsselbereich | unter 10 % | 10–25 % | über 25 % |

Vollbeschäftigung von 100 % soll nicht dauerhaft optimal sein, weil Strukturwechsel dann keine Reserve besitzen.

## Priorisierung

Arbeitszuweisung folgt einer stabilen, sichtbaren Priorität. Erste Kategorien:

1. lebenswichtige Versorgung,
2. Sicherheit und Erhaltung,
3. ausdrücklich priorisierte Reichs- oder Kolonieziele,
4. laufende Standardproduktion,
5. Luxus- oder Überschussproduktion.

Der Spieler darf Prioritäten verändern. Automatische Zuweisung muss erklärbar bleiben und darf keine Informationen verwenden, die der Controller nicht besitzt.

## Qualifikation

Qualifikation beeinflusst Produktivität, darf aber nicht jede Umstellung blockieren.

Erste Korridore:

- passende Qualifikation: 100 % Basisproduktivität,
- teilweise passende Qualifikation: etwa 70–95 %,
- unpassende, aber einlernbare Arbeitskraft: etwa 40–70 %,
- nicht zulässige Aufgabe: 0 %, sofern eine harte fachliche Voraussetzung besteht.

Umschulung soll typischerweise mehrere reale Tage bis wenige Wochen dauern, abhängig vom Niveau. Sie bindet Arbeitskraft oder Ausbildungskapazität und konkurriert mit sofortiger Produktion.

## Unterversorgung

Mangelfolgen werden gestuft und zeitverzögert:

### Leichter Mangel

- geringeres Wachstum,
- leichte Produktivitätseinbuße,
- steigende Abwanderungsneigung.

### Schwerer Mangel

- kein oder negatives natürliches Wachstum,
- deutliche Produktivitäts- und Stabilitätsverluste,
- höhere Abwanderung,
- Ausfälle in nicht essentiellen Bereichen.

### Kritischer Mangel

- substantieller Rückgang,
- Notpriorisierung,
- langfristige Schäden oder Ereignisse,
- mögliche Evakuierung oder Zusammenbruch bei anhaltender Dauer.

Ein einzelner kurzer Tick löst keine volle schwere Folge aus. Die Mangellast akkumuliert und erholt sich nach Wiederherstellung schrittweise.

## Koloniegründung

Eine neue Kolonie soll ihre Startbevölkerung bei guter Versorgung und Migration in ungefähr **2 bis 4 realen Wochen** um 50 % steigern können. Diese Rate darf nicht allein aus natürlichem Wachstum entstehen; sie setzt gezielte Migration und Investition voraus.

## Produktivität

Produktivität wird nicht direkt aus Bevölkerungszahl abgeleitet. Sie berücksichtigt:

- Beschäftigungsgrad,
- Qualifikation,
- Versorgung,
- Anlagenzustand,
- Technologie,
- lokale und temporäre Modifikatoren.

Eine Verdopplung der Bevölkerung verdoppelt nur dann Produktion, wenn ausreichend Stellen, Anlagen, Versorgung und Transport vorhanden sind.

## Erholung nach Krise

Nach einer schweren, aber beendeten Versorgungskrise soll eine etablierte Kolonie:

- innerhalb von 1–3 Tagen die essentielle Grundfunktion stabilisieren können,
- innerhalb von 1–2 Wochen den Großteil der Produktivität wiederherstellen können,
- langfristige Bevölkerungs- oder Qualifikationsverluste gegebenenfalls über mehrere Wochen ausgleichen müssen.

## Anti-Exploit-Regeln

- Migration darf nicht durch gleichzeitige Befehle dupliziert werden.
- Wiederholtes Umschalten von Prioritäten darf keine zusätzliche Produktion erzeugen.
- Beschäftigte Arbeitskraft darf nicht parallel in Ausbildung und Produktion voll angerechnet werden.
- Temporäre Entlassung darf Unterhalt oder Bedürfnisse nicht rückwirkend vermeiden.
- Wachstum und Rückgang müssen bei Offline-Nachholung dieselben Ergebnisse liefern.

## Abnahmekriterien

- Bevölkerung bleibt über Migration und Transfers erhalten.
- Gute Versorgung ist erkennbar wertvoll, aber kein einzelner Prozentpunkt entscheidet sofort.
- Arbeitskräfteknappheit, Arbeitslosigkeit und Qualifikationslücken erzeugen unterschiedliche Probleme.
- Kolonien können sich spezialisieren, ohne beliebig Arbeitskraft aus dem Nichts zu erhalten.
- Unterversorgung ist ernst, aber mit Vorwarnung und Erholungspfad verbunden.
- Ein stabiler täglicher Check-in reicht zur Verwaltung normaler Arbeits- und Migrationsänderungen.