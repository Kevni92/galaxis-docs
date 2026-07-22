# S01 – Startreich und erster Check-in

Szenario-ID: `BAL-S01-STARTREICH-v1.0`

Status: Baseline

## Zweck

Prüfen, ob ein neues Reich ohne Vorwissen stabil startet, mehrere sinnvolle erste Entscheidungen besitzt und innerhalb des täglichen Check-in-Rhythmus sichtbaren Fortschritt erzeugt.

## Ausgangslage

- ein menschlich oder durch ein neutrales AI-Profil kontrolliertes Reich,
- ein kontrolliertes Heimatsystem,
- eine etablierte Heimatkolonie,
- drei direkt verbundene unbekannte oder teilweise bekannte Nachbarsysteme,
- ausreichende Grundproduktion für laufende Versorgung,
- mindestens sieben Versorgungstage essentielle Reserve,
- keine aktiven Verträge, Kriege oder Krisen,
- eine verfügbare Einführungstechnologie,
- begrenzte Bau-, Forschungs- und Flottenkapazität,
- kein bereits gebautes Kolonieschiff.

## Strategieprofile

- ausgewogen,
- schnelle Expansion,
- frühe Forschung,
- frühe Flottenabsicherung,
- keine neuen Befehle nach dem Start.

## Laufzeit

- Schnelllauf: 72 reale Stunden im Standardprofil,
- vollständiger Lauf: 14 reale Tage im Standardprofil.

## Erwartete Entscheidungen

Innerhalb der ersten Sitzung müssen mindestens zwei, besser drei plausible Richtungen erkennbar sein:

- Erkundung und Vorbereitung einer Kolonie,
- Kernraumausbau und Versorgungssicherheit,
- Forschung,
- Flotten- oder Sensorabsicherung.

Keine Richtung darf ohne relevante Opportunitätskosten gleichzeitig mit allen anderen maximal verfolgt werden.

## Sollmetriken

| Kennzahl | Ziel |
|---|---:|
| erste relevante Erkundungsrückmeldung | 4–12 h |
| erster Ausbau abgeschlossen | 8–24 h |
| erste Technologie | Tag 2–4 |
| erste Kolonie beauftragt, Expansionsprofil | Tag 3–6 |
| wirtschaftlicher Kollaps bis Tag 7 | unter 5 % der neutralen Seeds |
| essentielle Reserve an Tag 3 | mindestens 3 Tage bei ausgewogenem Profil |
| bedeutende manuelle Entscheidungen | 1–5 pro Tag |
| vollständige Handlungsunfähigkeit ohne neue Befehle nach 72 h | unter 5 % |

## Invarianten

- keine negativen Bestände,
- keine doppelte Reservierung,
- unbekannte Systemdaten bleiben verborgen,
- Offline- und reguläre Verarbeitung liefern denselben Endzustand,
- Spieler- und AI-Controller verwenden dieselben Befehle,
- ein idempotent wiederholter Startbefehl erzeugt keine zweite Wirkung.

## Warnsignale

- nur eine offensichtlich sinnvolle erste Aktion,
- unmittelbares Defizit ohne sichtbare Ursache,
- mehrere Stunden oder Tage ohne Rückmeldung,
- Koloniegründung innerhalb des ersten Tages ohne Spezialisierung oder Risiko,
- notwendige wiederholte Mikrobefehle,
- Flottenbau, Forschung und Kolonie gleichzeitig ohne Engpass.

## Erfolgsdefinition

Das Szenario besteht, wenn der Start stabil, verständlich und entscheidungsreich ist, alle Invarianten halten und mindestens drei Strategieprofile unterschiedliche, aber grundsätzlich tragfähige Verläufe erzeugen.