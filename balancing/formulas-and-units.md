# Formeln, Einheiten und Rundung

Status: Baseline v0.1

## Zweck

Dieses Dokument definiert gemeinsame mathematische Regeln, damit verschiedene Fachsysteme dieselben Einheiten, Modifikatorreihenfolgen und Rundungsprinzipien verwenden. Konkrete Fachformeln dürfen ergänzt werden, müssen aber diese Invarianten einhalten.

## Autoritative Zahlendarstellung

Die serverautoritative Simulation verwendet keine binären Fließkommazahlen für spielstandsrelevante Berechnungen.

Empfohlene interne Darstellung:

- Mengen: ganzzahlige **Mikroeinheiten** oder eine fachlich festgelegte kleinste Einheit,
- Prozentsätze: **Basispunkte**, wobei `10_000 bp = 100 %`,
- Zeit: ganzzahlige Kampagnenzeit in Sekunden oder einer kleineren festgelegten Takteinheit,
- Geld oder abstrakte Haushaltswerte: kleinste ganzzahlige Währungseinheit,
- Wahrscheinlichkeiten: ganzzahliger Bereich, beispielsweise `0..1_000_000`.

Die konkrete technische Darstellung wird im Server festgelegt, muss aber deterministisch, überlaufsicher und migrationsfähig sein.

## Einheitenpflicht

Jeder numerische Parameter besitzt:

- eine eindeutige Kennung,
- eine Einheit,
- einen Standardwert,
- einen erlaubten Wertebereich,
- eine Balancingversion,
- eine fachliche Quelle,
- eine Beschreibung, wann er ausgewertet wird.

Ein Wert ohne Einheit oder Auswertungszeitpunkt gilt als unvollständig.

## Modifikatorarten

Modifikatoren werden in klar getrennten Gruppen ausgewertet:

1. **Basiswert**
2. **additive absolute Änderungen**
3. **additive prozentuale Änderungen derselben Gruppe**
4. **multiplikative Faktoren unterschiedlicher Ursachen**
5. **fachliche Mindest- und Höchstgrenzen**
6. **Rundung auf autoritative Einheit**

Allgemeine Form:

```text
Zwischenwert = Basiswert + Summe(absolute Änderungen)
Prozentwert  = Zwischenwert × (10_000 + Summe(additive Basispunkte)) / 10_000
Ergebnis     = Prozentwert × Produkt(multiplikative Faktoren)
Ergebnis     = clamp(Ergebnis, Minimum, Maximum)
Ergebnis     = autoritativ runden
```

Prozentwerte dürfen nicht unkontrolliert mehrfach in derselben Gruppe multipliziert werden, nur weil sie aus verschiedenen Datenquellen stammen. Jede Formel dokumentiert ausdrücklich, welche Faktoren additiv und welche multiplikativ sind.

## Produktionsformel

Erste gemeinsame Struktur:

```text
Effektive Produktion =
    Basisleistung
  × Beschäftigungsfaktor
  × Versorgungsfaktor
  × Anlagenzustand
  × Technologieeffekt
  × lokaler Modifikator
  × temporärer Modifikator
```

Alle Faktoren verwenden einen dokumentierten Wertebereich. Für normale Zustände sollen Faktoren typischerweise zwischen `0` und `2,0` liegen. Werte oberhalb davon benötigen eine ausdrückliche Begründung und einen Test gegen exponentielle Skalierung.

## Beschäftigungsfaktor

```text
Beschäftigungsfaktor =
  min(zugewiesene passende Arbeitskraft / benötigte Arbeitskraft, 1,0)
  × Qualifikationsfaktor
```

Überbesetzung erhöht nicht automatisch die Produktion. Eine Fachregel kann begrenzte Reservebesetzung erlauben, muss aber abnehmenden Grenznutzen definieren.

## Versorgungsfaktor

Der Versorgungsfaktor wird nicht nur aus dem aktuellen Tick bestimmt, sondern kann eine geglättete oder kumulierte Mangellast verwenden:

```text
Mangellast_neu =
  Mangellast_alt × Erholungsfaktor
  + max(0, Sollbedarf - gedeckter Bedarf)

Versorgungsfaktor = Funktion(Mangellast, aktueller Deckungsgrad)
```

Dadurch erzeugt ein einzelner kurzer Mangel keine sofortige volle Langzeitstrafe, anhaltender Mangel bleibt aber wirksam.

## Bevölkerungsänderung

```text
Bevölkerung_neu = Bevölkerung_alt
  + Geburten
  - Todesfälle
  + Zuwanderung
  - Abwanderung
  + Ereignisänderungen
```

Jede Teilgröße wird getrennt berechnet und protokollierbar gehalten. Migration ist keine natürliche Wachstumsrate und darf nicht doppelt gezählt werden.

Empfohlene Rate:

```text
Natürliche Änderung = Bevölkerung × Rate_pro_Zeiteinheit × Zeitintervall
```

Nicht ganzzahlige Reste werden je Populationseinheit fortgeschrieben, statt pro Tick verworfen zu werden.

## Forschungsfortschritt

```text
Fortschritt_neu = Fortschritt_alt
  + Forschungsleistung
  × Bereichseignung
  × Versorgungs- und Stabilitätsfaktor
  × Zeitintervall
```

Technologiekosten werden in derselben Forschungsfortschrittseinheit angegeben. Ein Wechsel der Technologie darf Fortschritt nur nach einer ausdrücklich dokumentierten Fachregel reduzieren.

## Reisezeit

Erste Struktur für eine Route:

```text
Reisezeit = Summe je Kante(
  Basisdistanz / effektive Geschwindigkeit
  × Kantenmodifikator
  × Logistikmodifikator
) + feste Übergangszeiten
```

Die Route wird bei Befehlsannahme gegen den autoritativen Wissens- und Weltzustand validiert. Spätere Veränderungen können Verzögerung, Umleitung oder Abbruch auslösen, dürfen aber nicht rückwirkend eine bereits vergangene Reisezeit umschreiben.

## Haushaltsbilanz

```text
Periodensaldo =
  regelmäßige Einnahmen
  + einmalige Einnahmen
  - laufender Unterhalt
  - reservierte Ausgaben
  - einmalige Ausgaben
```

Reservierte Mittel bleiben vom frei verfügbaren Bestand getrennt. Ein idempotent wiederholter Befehl darf weder erneut reservieren noch erneut abbuchen.

## Kampfschaden

Eine erste abstrahierte Struktur:

```text
Rohschaden = Waffenleistung × Zielwirksamkeit × Kampfsituation
Abgefangener Schaden = Funktion(Schilde, Panzerung, Abwehr, Sättigung)
Strukturschaden = max(0, Rohschaden - abgefangener Schaden)
```

Zufall darf Ergebnisse variieren, aber nicht die Bedeutung der Ausgangslage verdecken. Zufallsstreuung erhält einen begrenzten Korridor und einen autoritativen Seed. Ein deutlich stärkerer Verband muss über viele Läufe zuverlässig häufiger gewinnen.

## Abnehmender Grenznutzen

Stapelbare Boni sollen bei Bedarf eine Sättigungsfunktion verwenden, beispielsweise:

```text
Effektiver Bonus = MaxBonus × Rohbonus / (Rohbonus + Sättigung)
```

So kann Spezialisierung lohnend bleiben, ohne unbegrenzt exponentiell zu skalieren. Jede Verwendung nennt `MaxBonus` und `Sättigung`.

## Mindest- und Höchstgrenzen

Grenzen müssen fachlich begründet sein. Eine harte Grenze ist geeignet, wenn:

- ein Zustand außerhalb des Bereichs keinen Sinn ergibt,
- technische Stabilität geschützt werden muss,
- eine bekannte Exploit-Kombination verhindert wird.

Eine weiche Grenze mit abnehmendem Nutzen ist geeigneter, wenn Spezialisierung weiterhin möglich bleiben soll.

## Rundung

### Anzeige

Der Client darf Werte für die Darstellung runden, muss bei entscheidungsrelevanten Prognosen die Genauigkeit und mögliche Abweichung kenntlich machen.

### Autoritative Berechnung

- Zwischenwerte bleiben in hoher ganzzahliger Genauigkeit erhalten.
- Rundung erfolgt möglichst erst am Ende einer fachlichen Transaktion.
- Wiederholte kleine Raten führen Restwerte fort.
- Negative und positive Werte verwenden dieselbe symmetrische Rundungsregel.
- Verteilungen konservierter Mengen verwenden die Methode der größten Reste oder eine gleichwertige deterministische Verteilung.
- Gleichstände werden durch stabile IDs oder eine autoritative Reihenfolge gebrochen.

## Erhaltungssätze

Für physische oder anderweitig konservierte Größen gilt:

```text
Bestand vorher + erzeugt - verbraucht - zerstört = Bestand nachher
```

Transport, Reservierung, Handel oder Eigentumswechsel dürfen den Gesamtbestand nicht verändern. Jede Abweichung muss als ausdrücklich protokollierte Erzeugung, Vernichtung oder Korrektur erklärbar sein.

## Zeitintegration

Offline-Nachholung und reguläre Verarbeitung müssen fachlich gleichwertige Ergebnisse liefern. Eine Optimierung mit größeren Zeitschritten ist nur zulässig, wenn:

- dieselben Zustandsgrenzen in derselben Reihenfolge erkannt werden,
- keine Ressourcen durch Aggregation verloren gehen,
- Zufallsereignisse reproduzierbar bleiben,
- Ergebnis und Änderungsprotokoll dem regulären Lauf entsprechen.

## Formeltests

Jede produktive Formel benötigt mindestens:

- Neutralfall,
- Minimum und Maximum,
- Null- und Leermengenfall,
- Grenzwert direkt unter und über einer Schwelle,
- sehr großes, aber erlaubtes Eingangsszenario,
- deterministische Wiederholung,
- Erhaltungstest, sofern eine konservierte Größe betroffen ist,
- Vergleich zwischen regulärer und aggregierter Zeitverarbeitung.