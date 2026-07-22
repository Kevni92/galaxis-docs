# Wirtschaft und Versorgung

Status: Baseline v0.1

Fachliche Grundlage: [`docs/06-economy/`](../../docs/06-economy/README.md)

## Ziel

Die Wirtschaft soll verständliche Engpässe, echte Opportunitätskosten und mehrere tragfähige Spezialisierungen erzeugen. Güter müssen standortgebunden bleiben; Produktion, Lagerung, Transport, Reservierung, Handel und Verbrauch dürfen keine Bestände duplizieren.

## Erste Güterstruktur

Für den MVP wird eine überschaubare Kette mit vier Rollen empfohlen:

1. **Grundgüter** – Ernährung, Energie oder vergleichbare essentielle Versorgung,
2. **Rohstoffe** – natürlich gewonnene Eingaben,
3. **Industriegüter** – Bau, Instandhaltung und Standardschiffe,
4. **Hochwertige oder strategische Güter** – fortgeschrittene Technologie, Spezialschiffe, Großprojekte.

Der endgültige Güterkatalog wird in einem eigenen B1-Issue festgelegt. Jede zusätzliche Güterart benötigt eine eigenständige Entscheidung oder einen Engpass, der nicht bereits durch ein anderes Gut abgebildet wird.

## Produktionsketten

Eine Standardkette soll im MVP typischerweise 1 bis 3 Umwandlungsschritte besitzen. Längere Ketten sind nur für strategische Endprodukte sinnvoll.

Ziel:

- Grundversorgung lokal oder regional robust möglich,
- spezialisierte hochwertige Produktion stärker auf Transport und Handel angewiesen,
- kein Gut benötigt standardmäßig mehr als drei seltene Vorprodukte,
- jede Produktionsstufe besitzt sichtbare Eingaben, Ausgaben, Kapazität und Auslastung.

## Startwirtschaft

Das Startreich soll:

- mindestens 7 Versorgungstage essentielle Reserve besitzen,
- seine aktuelle Grundversorgung ohne sofortigen Neubau decken,
- eine kleine Sicherheitsreserve an Baumaterial besitzen,
- nicht gleichzeitig erste Kolonie, maximale Forschung und maximale Flottenrüstung voll finanzieren können,
- innerhalb des ersten Tages mindestens zwei sinnvolle Investitionsoptionen besitzen.

Die Startwirtschaft darf kein verstecktes Defizit enthalten, das ohne Vorwissen innerhalb weniger Stunden zum Kollaps führt.

## Überschuss und Reserve

Ein gesundes Reich hält:

- essentielle Güter: 7 bis 14 Tage,
- häufige Bau- und Instandhaltungsgüter: 3 bis 10 Tage des normalen Verbrauchs,
- strategische Güter: abhängig von Projektplanung, typischerweise 1 bis 3 größere Vorhaben,
- frei disponierbaren Haushaltsüberschuss: 10 bis 25 %.

Sehr große Reserven verursachen mindestens Opportunitätskosten durch Lagerkapazität, gebundenes Kapital oder Verfall, sofern fachlich vorgesehen.

## Lager

Lagerkapazität soll:

- frühe kurzfristige Schwankungen abfangen,
- Spezialisierung und Transportplanung ermöglichen,
- nicht unbegrenzt und kostenlos skalieren,
- Überproduktion sichtbar machen.

Dauerhaft verworfene Produktion über 25 % gilt als Warnsignal. Automatische Produktionsdrosselung oder alternative Verwendung soll möglich sein, statt Ressourcen stillschweigend zu vernichten.

## Reservierung

Befehle reservieren benötigte Ressourcen atomar. Dabei gilt:

- reservierte und freie Bestände sind getrennt,
- idempotente Wiederholung reserviert nicht erneut,
- Abbruch folgt dokumentierten Rückerstattungsregeln,
- Verlust oder Blockade einer Quelle verändert nicht rückwirkend bereits angenommene Reservierungen,
- Teilzahlungen benötigen explizite Fachregel.

## Preise und Bewertung

Für interne AI-, Prognose- und Vergleichszwecke erhält jedes Gut einen Baselinewert. Dieser ist keine zwingende globale Marktpreisgarantie.

Empfohlen:

```text
Referenzwert = gewichtete Summe direkter Inputs
             + Arbeits- und Kapitalkosten
             + Transportreferenz
             + Knappheits- oder Strategiefaktor
```

Preise dürfen auf lokale Knappheit reagieren, benötigen aber:

- begrenzte Änderungsrate,
- Mindestliquidität oder Fallback,
- Schutz vor Selbsthandel und Kreisgeschäften,
- getrennte Behandlung von tatsächlichem Preis und analytischem Referenzwert.

## Versorgung

Essentielle Deckungsgrade:

| Deckung | Zustand | erste Wirkung |
|---:|---|---|
| 95–100 % | vollständig | keine Mangelstrafe |
| 80–95 % | leicht | kleine Effizienz- und Wachstumsverluste |
| 50–80 % | schwer | deutliche Priorisierung, Stabilitäts- und Produktivitätsverlust |
| unter 50 % | kritisch | Notbetrieb, Rückgang, mögliche langfristige Schäden |

Die Wirkung berücksichtigt Dauer und kumulierte Mangellast.

## Transport

Transport besitzt:

- Route,
- Kapazität,
- Laufzeit,
- Kosten,
- Priorität,
- Quelle und Ziel,
- Status und Unterbrechungsregeln.

Erste Auslastungsziele:

- normaler stabiler Betrieb: 60 bis 85 % Auslastung,
- über 90 %: Engpasswarnung,
- dauerhaft 100 %: Ausbau, Priorisierung oder alternative Route notwendig.

Eine reine Kapazitätserhöhung soll nicht automatisch wirtschaftlich sein; Infrastruktur besitzt Bau- und Unterhaltskosten.

## Handel

Handel soll:

- Spezialisierung ermöglichen,
- Risiken durch Abhängigkeit erzeugen,
- nicht automatisch besser als Eigenproduktion sein,
- Vertrags-, Transport- und Ausfallrisiko besitzen.

Ein Handelsvertrag benötigt nachvollziehbare Mengen, Preis- oder Tauschregel, Laufzeit, Transportverantwortung und Unterbrechungsfolgen.

## Haushalt

Erste Zielanteile eines stabilen Reiches:

| Bereich | typischer Anteil laufender Mittel |
|---|---:|
| Grundversorgung und Infrastruktur | 25–45 % |
| Verwaltung und Erhaltung | 10–20 % |
| Forschung | 10–25 % |
| Friedensmilitär | 10–25 % |
| frei für Expansion, Reserve oder Projekte | 10–25 % |

Die Bereiche dürfen sich überschneiden, wenn das Fachmodell keine einheitliche Währung nutzt. Entscheidend ist die erkennbare Opportunitätskostenwirkung.

## Defizite

Defizite verlaufen gestuft:

1. frei verfügbare Reserve sinkt,
2. geplante nicht essentielle Vorhaben werden verzögert,
3. Unterhalt oder Versorgung wird priorisiert,
4. Effizienz und Stabilität sinken,
5. bei anhaltendem Defizit werden Anlagen, Flotten oder Leistungen reduziert.

Ein kurzer Defizittag darf nicht sofort Anlagen zerstören. Ein strukturelles Defizit darf aber nicht folgenlos durch unbegrenzte Schulden überdeckt werden.

## Krieg und Wirtschaft

- Beute und Eroberung dürfen Kriegskosten teilweise ausgleichen, aber einen typischen Krieg nicht risikolos selbst finanzieren.
- Besetzte oder beschädigte Produktionsorte liefern nicht sofort vollen Wert.
- Flottenunterhalt und Ersatz verdrängen zivile Investition.
- Blockaden wirken über Transport und Versorgung, nicht über willkürliche globale Abzüge.
- Nach Kriegsende benötigt die Wirtschaft einen realistischen Wiederaufbaupfad.

## Anti-Exploit-Regeln

- keine Ressourcenerzeugung durch Handel mit sich selbst,
- keine doppelte Nutzung reservierter Bestände,
- keine negative Kostenkombination,
- keine unendliche profitable Produktionsschleife,
- keine Rundungsgewinne durch Aufteilen in viele Kleinsttransaktionen,
- keine rückwirkende Vermeidung von Unterhalt durch kurzfristiges Umschalten,
- keine Informationslecks durch Markt- oder Transportdaten.

## Abnahmekriterien

- Startwirtschaft bleibt ohne versteckten Kollaps spielbar.
- Expansion, Forschung, Reserve und Militär konkurrieren sichtbar.
- Essentielle Versorgung ist robust, aber nicht bedeutungslos.
- Spezialisierung und Handel bieten Nutzen mit Abhängigkeit.
- Lagerung und Transport erzeugen planbare Engpässe statt permanente Mikroklicks.
- Defizite besitzen Vorwarnung, Stufen und Erholungspfad.
- Alle Erhaltungssätze bestehen in normaler und Offline-Verarbeitung.