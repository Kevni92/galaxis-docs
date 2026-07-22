# S04 – Begrenzter Krieg und Wiederaufbau

Szenario-ID: `BAL-S04-KRIEG-v1.0`

Status: Baseline

## Zweck

Prüfen, ob ein begrenzter Krieg strategische Kosten, erkennbare Kriegsziele, plausible Kampfverluste und einen Wiederaufbaupfad erzeugt, ohne durch einen einzelnen knappen Kampf regelmäßig die gesamte Kampagne zu entscheiden.

## Ausgangslage

- zwei annähernd gleich starke Reiche,
- jeweils vier bis sechs Kolonien,
- eine umstrittene Grenzregion,
- je eine Hauptflotte und ein kleiner Unterstützungsverband,
- mehrere Rückzugs- und Versorgungsrouten,
- essentielle Reserven für 7–12 Tage,
- Friedenshaushalt vor Eskalation stabil,
- keine galaktische Krise,
- ein klar definiertes begrenztes Kriegsziel.

## Varianten

- Kräfteverhältnis 1,0 : 1,
- Kräfteverhältnis 1,25 : 1,
- Kräfteverhältnis 1,5 : 1,
- Kräfteverhältnis 2,0 : 1,
- passender Gegenentwurf gegen stärkeren Verband,
- unterbrochene Versorgung einer Seite,
- früher geordneter Rückzug,
- zu spät angeordneter Rückzug.

## Laufzeit

- Kampfvergleich: bis Abschluss des Gefechts,
- Kriegsverlauf: 21 reale Tage im Standardprofil,
- Wiederaufbau: weitere 14 reale Tage.

## Sollmetriken Kampf

| Kennzahl | Ziel |
|---|---:|
| Siegquote bei 1,0 : 1 | 40–60 % je Seite |
| Siegquote stärkere Seite bei 1,25 : 1 | 60–75 % |
| Siegquote stärkere Seite bei 1,5 : 1 | 70–85 % |
| Siegquote stärkere Seite bei 2,0 : 1 | über 85 % |
| Gewinnerverlust bei knappem Kampf | häufig 5–20 % |
| Verliererverlust mit Rückzug | häufig 20–50 % |
| Vollvernichtung bei annähernd gleicher Stärke | unter 10 % |

## Sollmetriken Krieg

| Kennzahl | Ziel |
|---|---:|
| Dauer begrenzter Krieg | 5–14 reale Tage |
| Kriegsanteil laufender Reichsleistung | 25–45 % bei größerer Anstrengung |
| Zeit bis Grundfunktion nach Kriegsende | 1–3 Tage |
| Zeit bis Großteil wirtschaftlicher Leistung wiederhergestellt | 1–2 Wochen |
| vollständige formale Niederlage nach einer knappen Schlacht | selten |
| Friedensschluss ohne Bezug zum Kriegsziel | 0 % |

## Zu prüfende Entscheidungen

- Angriff oder Abschreckung,
- Hauptflotte konzentrieren oder Routen schützen,
- Rückzugsschwelle,
- Reparatur oder Neubau,
- Kriegsziel weiterverfolgen oder Frieden suchen,
- zivile Investition kürzen oder Reserven verbrauchen,
- Verbündete oder Handelspartner einbeziehen.

## Invarianten

- Kampf ist mit Seed reproduzierbar,
- Flotten und Schiffe existieren nicht gleichzeitig in mehreren Verbänden,
- Schäden, Reparatur und Bergung erhalten Bestände,
- Kriegsergebnisse übertragen nur erlaubte Werte,
- Online-Status beeinflusst keine Kampfentscheidung,
- AI und Spieler verwenden dieselben Befehle und Kampfregeln,
- Offline-Verarbeitung entspricht regulärer Verarbeitung.

## Warnsignale

- erste Schlacht entscheidet fast immer den ganzen Krieg,
- Sieg ist wirtschaftlich billiger als Friedensbetrieb,
- Rückzug ist entweder bedeutungslos oder risikolos,
- Reparatur ist immer schlechter oder immer besser als Neubau,
- Versorgung besitzt keinen Einfluss auf tiefe Operationen,
- Eroberung liefert sofort vollen Produktionswert,
- unterlegene Seite besitzt keinen realistischen Friedens- oder Wiederaufbaupfad.

## Erfolgsdefinition

Das Szenario besteht, wenn Kräfteverhältnisse zuverlässig wirken, Gegenrollen und Logistik relevant bleiben, begrenzte Kriege im Zielkorridor enden und eine knappe Niederlage schmerzhaft, aber nicht regelmäßig kampagnenbeendend ist.