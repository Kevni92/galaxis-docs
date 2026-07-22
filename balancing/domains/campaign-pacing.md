# Kampagne und Pacing

Status: Baseline v0.1

Fachliche Grundlage:

- [`docs/01-gameplay/`](../../docs/01-gameplay/README.md)
- [`docs/11-campaign/`](../../docs/11-campaign/README.md)
- [Decision 0001](../../decisions/0001-asynchrones-kampagnen-und-controller-grundmodell.md)

## Ziel

Die Kampagne soll in ungefähr zwölf realen Wochen einen klaren Bogen von Aufbruch bis Abschluss erreichen. Ein täglicher Check-in muss genügen; intensiveres Spielen darf Analyse- und Planungsvorteile, aber keinen proportionalen Produktionsvorteil erzeugen.

## Standardprofil

Die exakte Umrechnung realer Zeit in Kampagnenzeit wird im Server-Datenkatalog festgelegt. Die erste Kalibrierung soll folgende Wirkung erreichen:

- kurze Vorgänge: Stunden bis höchstens ein Tag,
- mittlere Vorhaben: mehrere Tage,
- richtungsprägende Vorhaben: ungefähr eine Woche oder länger,
- keine wichtige frühe Spielphase besteht hauptsächlich aus untätigem Warten.

## Entscheidungstakt

| Kategorie | Zielhäufigkeit |
|---|---:|
| kritische manuelle Entscheidung | selten; nicht planmäßig täglich |
| bedeutende strategische Entscheidung | 1–5 pro Tag über alle Systeme |
| Ereignisentscheidung | im Median höchstens 1 pro Tag |
| Routineentscheidung | automatisiert, gebündelt oder als Priorität |
| langfristige Richtungsentscheidung | mehrmals pro Woche |

## Bau- und Vorhabenkorridore

| Vorhaben | Frühes Spiel | Mittleres Spiel | Spätes Spiel |
|---|---:|---:|---:|
| kleiner Ausbau | 8–24 h | 12–36 h | 12–48 h |
| bedeutendes Gebäude oder Upgrade | 1–3 Tage | 2–5 Tage | 3–7 Tage |
| Koloniegründung bis funktionsfähig | 4–8 Tage ab Auftrag | 3–7 Tage | 3–7 Tage |
| großer Flotten- oder Infrastrukturblock | 3–7 Tage | 5–10 Tage | 7–14 Tage |
| richtungsprägendes Reichsvorhaben | 5–10 Tage | 7–14 Tage | 7–21 Tage |

Parallelität, Spezialisierung und vorbereitete Ressourcen können tatsächliche Dauer verändern. Die Korridore beschreiben den wahrgenommenen Abschluss, nicht zwingend einen einzelnen Timer.

## Rückkehr und Offline-Fortschritt

Ein Rückkehrbericht soll bei normalem täglichem Check-in typischerweise enthalten:

- 0 bis 3 wichtige abgeschlossene Vorgänge,
- 0 bis 2 neue dringliche Probleme,
- gebündelte Routineergebnisse,
- aktualisierte Prognosen für laufende Ziele.

Nach 72 Stunden Abwesenheit darf der Bericht umfangreicher sein, muss aber priorisiert bleiben. Mehr als zehn gleichrangige manuelle Entscheidungen gelten als Überlastungssignal.

## Reaktionsfenster

| Situation | Mindestziel im Standardprofil |
|---|---:|
| planbare schwere diplomatische Eskalation | 24 reale Stunden |
| bedeutende Ereigniswahl | 24–48 reale Stunden |
| Endgame-Siegankündigung | mehrere Check-ins; Ziel 48–96 Stunden |
| normale Produktionsstörung | mindestens ein Check-in bis schwerer Folge |
| bereits offener Krieg | kürzere operative Veränderungen zulässig, aber keine Online-Status-Ausnutzung |

## Fortschrittskontrolle

Wöchentlich zu messende Kennzahlen:

- Kolonien und erschlossene Systeme,
- Produktions- und Versorgungsleistung,
- Technologieabschlüsse,
- Flottenwert und Unterhaltsquote,
- Zahl wichtiger Beziehungen und Konflikte,
- Fortschritt auf Siegespfaden,
- manuelle Entscheidungen und Zeitdruck.

## Anti-Snowballing

Wachstum darf Vorteile erzeugen, benötigt aber steigende Anforderungen:

- Verwaltung und Logistik skalieren mit Ausdehnung,
- zusätzliche Kolonien benötigen Versorgung und Arbeitskräfte,
- große Flotten verursachen laufenden Unterhalt,
- technologische Spezialisierung hat Opportunitätskosten,
- diplomatische Dominanz erzeugt Gegenreaktionen,
- Eroberung liefert nicht sofort den vollen wirtschaftlichen Wert.

Anti-Snowballing soll keine künstliche Bestrafung des Führenden sein. Es soll aus nachvollziehbaren Kosten von Größe, Entfernung, Integration und Bedrohungswahrnehmung entstehen.

## Aufholmechanismen

Zulässige erste Instrumente:

- Technologietransfer und bekannte Forschungserleichterung,
- günstigere Nutzung bereits erschlossener Infrastruktur,
- Bündnisse und gemeinsame Verteidigung,
- höhere Flexibilität kleiner konsolidierter Reiche,
- diplomatische Reaktion auf dominante Reiche,
- Wiederaufbau statt sofortiger formaler Niederlage.

Aufholmechanismen dürfen keinen absichtlichen Rückstand zur optimalen Strategie machen.

## Abnahmekriterien

- Median der Kampagnenabschlüsse liegt im Zielbereich.
- Frühe, mittlere und späte Phase sind anhand Entscheidungen unterscheidbar.
- Ein täglicher Check-in bleibt praktisch ausreichend.
- Keine Phase besitzt regelmäßig mehrere Tage ohne sinnvolle Entscheidung oder Rückmeldung.
- Kein einzelner früher Vorteil entscheidet in neutralen Szenarien regelmäßig die gesamte Kampagne.
- Gelegenheitsspieler bleiben handlungsfähig, Intensivspieler behalten zusätzliche Analysetiefe.