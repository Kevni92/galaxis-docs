# Diplomatie, Ereignisse und Endgame

Status: Baseline v0.1

Fachliche Grundlage:

- [`docs/09-diplomacy/`](../../docs/09-diplomacy/README.md)
- [`docs/10-events/`](../../docs/10-events/README.md)
- [`docs/11-campaign/`](../../docs/11-campaign/README.md)

## Ziel

Diplomatie soll langfristige Erwartungen und glaubwürdige Verpflichtungen erzeugen. Ereignisse sollen Entscheidungen zuspitzen, nicht den Spieler mit permanenten Pop-ups überlasten. Krisen und Endgame sollen die vorhandenen Systeme bündeln und eine ungefähr zwölfwöchige Kampagne nachvollziehbar abschließen.

## Beziehungen

Beziehungswerte werden aus nachvollziehbaren Ursachen aufgebaut. Ein einzelner kurzfristiger Bonus soll keine langjährige Feindschaft vollständig überschreiben.

Empfohlene Zeitstruktur:

- kurzfristige Eindrücke: mehrere Tage,
- Vertrags- und Vertrauenswirkung: ein bis mehrere Wochen,
- schwere Vertragsbrüche oder Krieg: langfristig bis Kampagnenende relevant,
- langsamer natürlicher Rückgang temporärer Ursachen.

Alle sichtbaren Haltungswerte benötigen eine Ursachenaufschlüsselung.

## Diplomatische Aktionen

Eine Aktion besitzt:

- Voraussetzungen,
- Kosten oder gebundene Kapazität,
- Annahme-, Ablehnungs- und Ablaufzustand,
- gegebenenfalls Abklingzeit,
- sichtbare Folgen,
- Schutz vor Wiederholung und Spam.

Erste Zielwerte:

- normale Anfragefrist: 24–72 reale Stunden,
- erneutes identisches Angebot nach Ablehnung: frühestens nach 2–7 Tagen,
- bedeutende Vertragsverhandlung: mehrere Check-ins statt sofortiger Klickfolge,
- ein Reich soll nicht regelmäßig mehr als 3 gleichzeitige bedeutende Angebote bearbeiten müssen.

## Verträge

Verträge benötigen Mindestlaufzeit, Kündigungsfrist oder Ausstiegskosten.

Erste Korridore:

| Vertragstyp | typische Mindestbindung oder Kündigungsfrist |
|---|---:|
| Handelsabkommen | 3–7 Tage |
| Nichtangriff | 7–14 Tage |
| Forschungskooperation | 7–21 Tage |
| Verteidigungsbündnis | 14–28 Tage oder erhebliche Austrittskosten |

Die Werte werden später je Vertragstyp konkretisiert. Ein Vertrag soll nicht im selben Moment abgeschlossen und folgenlos gebrochen werden können.

## Vertrauen und Vertragsbruch

- Erfüllte langfristige Verpflichtungen bauen Vertrauen langsam auf.
- Ein schwerer Bruch erzeugt unmittelbare und langfristige Kosten.
- Wiederholter Bruch soll kumulativ wirken.
- Vertrauenswerte dürfen nicht durch triviale Kleinstaktionen beliebig hochgefarmt werden.
- AI und Spieler unterliegen denselben sichtbaren Folgen.

## Kriegserklärung und Eskalation

Planbare schwere Eskalation soll im Standardprofil mindestens 24 reale Stunden erkennbar sein, sofern kein offener Krieg besteht.

Ein typischer begrenzter Krieg dauert 5–14 reale Tage. Ein großer Krieg darf 2–4 Wochen dauern, benötigt aber:

- klar erkennbare Kriegsziele,
- Zwischenstände,
- Friedens- oder Rückzugsmöglichkeiten,
- steigende wirtschaftliche Kosten,
- Schutz vor endloser Blockade ohne Entscheidung.

## Kriegsfortschritt

Kriegsfortschritt soll nicht nur vernichtete Flotten zählen. Mögliche Komponenten:

- kontrollierte oder besetzte Zielsysteme,
- erfüllte Kriegsziele,
- militärische Verluste,
- wirtschaftliche Belastung,
- Bündnisbeiträge,
- Dauer und Bereitschaft zum Frieden.

Keine einzelne Komponente soll in allen Kriegstypen allein entscheiden.

## Frieden

Ein Friedensschluss muss im Verhältnis zu Ziel, Fortschritt und tatsächlicher Kontrolle stehen. Ein kleiner Sieg darf nicht regelmäßig das gesamte gegnerische Reich übertragen.

Eroberte Gebiete besitzen Integrations-, Verwaltungs- und Versorgungsbedarf. Friedensbedingungen dürfen keine Güter, Bevölkerung oder Schiffe duplizieren.

## Ereignisdichte

Zielwerte pro Reich:

- bedeutende manuelle Entscheidung: im Median höchstens 1 pro realem Tag,
- kleine informative Ereignisse: gebündelt,
- Routinefolgen: automatisch oder im Rückkehrbericht,
- mehrere zusammenhängende Ereignisse: als Kette mit gemeinsamen Kontext statt unabhängigen Pop-ups.

Ein Ereignis darf ohne Entscheidung auskommen, wenn keine echte Alternative besteht.

## Entscheidungsfristen

| Bedeutung | typische Frist |
|---|---:|
| informativ oder reine Bestätigung | keine manuelle Frist nötig |
| normale bedeutende Wahl | 24–48 reale Stunden |
| langfristige diplomatische oder Krisenwahl | 48–96 reale Stunden |
| operative Wahl im bereits offenen Konflikt | kann kürzer sein, benötigt aber vorher bekannte Regeln oder Standardentscheidung |

Jede befristete Entscheidung besitzt eine sichtbare Standardoption. Abwesenheit darf nicht zur zufälligen oder geheimen Auswahl führen.

## Anomalien

Eine Anomalie soll typischerweise:

- durch Erkundung entdeckt werden,
- mindestens eine Investitions- oder Risikoentscheidung besitzen,
- nicht immer sofort den vollen Wert preisgeben,
- in 1–3 klaren Untersuchungsschritten lösbar sein,
- einen für die Kampagnenphase angemessenen Ertrag oder Einfluss besitzen.

Seltene hohe Belohnungen benötigen entsprechend seltene Chance, Risiko oder Opportunitätskosten. Ein früher Zufallsfund darf die Kampagne nicht regelmäßig allein entscheiden.

## Regionale Krisen

Regionale Krisen werden typischerweise ab Woche 4–6 relevant und betreffen mehrere Systeme oder Reiche.

Eine Krise besitzt:

- Vorzeichen oder Warnphase,
- Ausbruch,
- eine oder mehrere Eskalationsstufen,
- Gegenmaßnahmen,
- Erfolg, Teilerfolg und Scheitern,
- langfristige Folgen.

Eine Phase dauert typischerweise 2–7 reale Tage.

## Galaktische Krisen

Galaktische Endgame-Krisen beginnen typischerweise Woche 8–10. Sie sollen:

- vorhandene Wirtschaft, Forschung, Flotten und Diplomatie gleichzeitig relevant machen,
- mehrere sinnvolle Rollen für verschiedene Reichstypen bieten,
- Fortschritt und Eskalation sichtbar darstellen,
- weder allein durch eine einzelne Flotte noch nur durch einen Ressourcenwert gelöst werden,
- den Kampagnenabschluss vorbereiten, ohne frühere Entscheidungen bedeutungslos zu machen.

## Siegespfade

Mindestens mehrere der folgenden Richtungen sollen realistisch möglich sein:

- politischer oder diplomatischer Einfluss,
- wirtschaftliche Leistungs- oder Versorgungsdominanz,
- technologische Leistung,
- militärische Zielerfüllung,
- Krisenbewältigung,
- mehrdimensionale Kampagnenwertung.

Ein Reich soll normalerweise nicht alle Pfade gleichzeitig maximieren können.

## Siegankündigung

Ein endgültiger Sieg soll typischerweise 48–96 reale Stunden vorher als ernsthafte Möglichkeit sichtbar sein. Andere Reiche benötigen sinnvolle Gegenmaßnahmen, sofern die Kampagne nicht bereits eindeutig entschieden ist.

Überraschende formale Abschlüsse ohne ausreichende Vorwarnung sollen unter 5 % der neutralen Endgame-Läufe liegen.

## Niederlage und Erholung

- Einzelne verlorene Flotte oder Kolonie ist keine automatische formale Niederlage.
- Ein Reich mit verbleibender Handlungsfähigkeit erhält Wiederaufbau- oder Diplomatieoptionen.
- Formale Niederlage setzt dauerhaften Verlust eigenständiger Handlungsfähigkeit oder eine ausdrückliche Bedingung voraus.
- Übernahme eines AI-Reiches oder Beobachtermodus darf keine Informationen übertragen, die das neue Reich nicht besitzt.

## Anti-Exploit-Regeln

- kein Vertrauensfarming durch wiederholte kostenlose Kleinstaktionen,
- kein Vertragswechsel zur rückwirkenden Kostenvermeidung,
- keine doppelte Belohnung derselben Krise oder Anomalie,
- keine Ereignisentscheidung nach Ablauf durch wiederholte Requests,
- keine Nutzung des Online-Status für Kriegsziele oder AI-Auswahl,
- keine Punkteerzeugung durch gegenseitig abgesprochene triviale Kriege,
- keine Endlosschleife aus Krise, Belohnung und erneutem identischem Trigger.

## Abnahmekriterien

- Verträge besitzen glaubwürdige Bindung und Folgen.
- Diplomatische Aktionen überlasten den täglichen Check-in nicht.
- begrenzte Kriege liegen im Dauerziel und besitzen sinnvolle Friedensausgänge.
- Ereignisdichte bleibt kontrollierbar und Entscheidungen haben echte Alternativen.
- Krisen durchlaufen sichtbare Phasen und bieten mehreren Strategien Rollen.
- mehrere Siegesrichtungen erreichen realistische Chancen.
- Sieg und Niederlage besitzen ausreichende Vorwarnung und passen zum asynchronen Modell.