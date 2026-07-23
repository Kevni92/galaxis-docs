# Komponenten, Lokalisierung und Begriffskatalog

Status: Freigegeben

## Zweck

Dieses Dokument definiert den gemeinsamen Komponentenbestand, die Datenlayouts, Zustände, Sprachdateien und rekursiven Begriffserklärungen. Einzelne Fachbereiche dürfen Inhalte ergänzen, aber keine eigenen parallelen UI-Grundsysteme einführen.

## Komponentenprinzip

Jede wiederkehrende Interaktion wird als zentrale Komponente mit dokumentierten Varianten umgesetzt. Eine Komponente besitzt:

- eindeutigen Zweck,
- zulässige Varianten,
- Eingaben und Ausgaben,
- sichtbare Zustände,
- Fokus- und Tastaturverhalten,
- Lokalisierungsanforderungen,
- Barrierefreiheitsregeln,
- Beispiele für richtige und falsche Verwendung.

## Buttons

Verbindliche Buttonarten:

- `PrimaryButton`: wichtigste bestätigende Aktion eines Dialogs,
- `SecondaryButton`: gleichwertige Alternative mit geringerer Gewichtung,
- `TertiaryButton`: schwache oder ergänzende Aktion,
- `DangerButton`: irreversible oder deutlich schädliche Aktion,
- `IconButton`: kompakte Werkzeugaktion mit zugänglichem Namen,
- `SplitButton`: Hauptaktion mit eng verwandten Alternativen,
- `ToggleButton`: sichtbarer umschaltbarer Zustand,
- `CommandButton`: löst einen serverautoritativen Spielbefehl aus.

Jede Variante unterstützt mindestens:

```text
default
hover
focus
pressed
loading
disabled
disabled-with-reason
```

Ein deaktivierter `CommandButton` zeigt den bekannten Grund über Tooltip, Hilfetext oder Validierungsbereich. Der Client darf eine Aktion nicht allein deshalb aktivieren, weil ihre Schaltfläche sichtbar ist.

## Tabellen und Datenlayouts

### PropertyGrid

Für kompakte Label-Wert-Daten. Label links, Wert rechts. Einheiten, Unsicherheit und Datenstand werden sichtbar angegeben.

### DataTable

Für sortierbare Sammlungen gleichartiger Entitäten. Sortierung, Auswahl, Pagination und Tastaturnavigation sind einheitlich.

### ComparisonTable

Für die Gegenüberstellung weniger Alternativen. Unterschiede werden hervorgehoben, ohne nur Farbe zu verwenden.

### LedgerTable

Für Einnahmen, Ausgaben, Reservierungen, Salden und Zeitreihen mit klarer Summenzeile.

### QueueTable

Für laufende Befehle, Bau-, Forschungs- und Flottenwarteschlangen. Zeigt Reihenfolge, Status, Ziel, Start, Abschluss und Blockierungsgrund.

### TimelineTable

Für Rückkehrberichte, Ereignisse, Kämpfe und vergangene Ergebnisse.

### TreeTable

Für hierarchische Inhalte wie Technologieabhängigkeiten oder Objektstrukturen, wenn eine reine Liste die Beziehung nicht ausdrückt.

### OutlinerList

Für stark verdichtete, gruppierte Objektübersichten. Sie zeigt nur handlungsrelevante Statusinformationen und verweist auf Details.

## Weitere zentrale Komponenten

- Fenster und Dialog,
- Tabs,
- Abschnitt und Abschnittsüberschrift,
- Ressourcenwert,
- Statusbadge,
- Fortschrittsanzeige,
- Warnung und Ursache,
- Tooltip,
- Concept-Popover,
- Kontextmenü,
- Formularfelder,
- leere Zustände,
- Ladezustände,
- Fehler- und Konfliktzustände,
- Toast oder nicht blockierende Rückmeldung,
- Bestätigungsdialog,
- Shortcut-Hinweis.

## Datenzustände

Komponenten unterscheiden mindestens:

- bekannter Nullwert,
- unbekannter Wert,
- nicht anwendbar,
- noch nicht geladen,
- veraltet,
- geschätzt,
- serverseitig blockiert,
- fehlende Berechtigung,
- technischer Fehler.

`0`, `—`, `unbekannt` und `nicht verfügbar` sind keine austauschbaren Darstellungen.

## Sprachdateien

Alle sichtbaren Texte verwenden stabile Lokalisierungsschlüssel. Empfohlene Struktur:

```text
localization/
├── de/
│   ├── ui.yml
│   ├── commands.yml
│   ├── resources.yml
│   ├── errors.yml
│   └── concepts.yml
└── en/
    ├── ui.yml
    ├── commands.yml
    ├── resources.yml
    ├── errors.yml
    └── concepts.yml
```

Komponenten enthalten keine fest eingebauten sichtbaren Sätze. Technische Test-IDs, maschinenlesbare Fehlercodes und stabile Action-IDs sind keine sichtbaren Texte.

## Kontextwerte

Ein lokalisierter Text erhält ausschließlich explizit benannte und typisierte Werte:

```yaml
colony:
  reserves:
    stable: "Die Vorräte reichen noch {days, duration}."
    critical: "[warning]Die Vorräte reichen nur noch {days, duration}.[/warning]"
```

Der Aufrufer stellt beispielsweise bereit:

```json
{
  "days": 34
}
```

Sprachdateien dürfen nicht auf beliebige Objektpfade oder den vollständigen Clientzustand zugreifen.

## Formatierer

Mindestens folgende zentral registrierte Formatierer sind vorgesehen:

```text
{value, number}
{value, signedNumber}
{value, percent}
{value, currency}
{value, duration}
{value, campaignDate}
{value, resource}
{value, distance}
```

Pluralformen und grammatische Auswahl werden über eine dokumentierte Message-Format-Syntax unterstützt.

## Sichere Formatierungsgrammatik

Sprachdateien dürfen eine kleine Whitelist verwenden:

```text
[b]fett[/b]
[i]kursiv[/i]
[positive]+25[/positive]
[negative]-12[/negative]
[warning]Versorgung kritisch[/warning]
[concept:population]Bevölkerung[/concept]
[icon:food]
[kbd:open_research]
```

Die Tags werden in sichere Komponenten übersetzt. Beliebiges HTML, JavaScript, CSS oder dynamische Imports sind verboten.

## Begriffskatalog

Spielbegriffe besitzen stabile IDs und strukturierte Einträge:

```yaml
concepts:
  population:
    title: "Bevölkerung"
    short: "Die auf einer Kolonie lebende Gesamtbevölkerung."
    description: >
      Bevölkerung besteht aus aggregierten Bevölkerungsgruppen und
      beeinflusst Arbeit, Versorgung und Wachstum.
    category: "population"
    related:
      - population_group
      - workforce
      - colony
    sources:
      - "docs/05-population/bevoelkerung-und-arbeit.md"
```

Der Begriffskatalog ergänzt das fachliche Glossar, ersetzt aber nicht die ausführlichen Fachdokumente.

## Concept-Popover

Ein markierter Begriff ist per Hover und Tastaturfokus erklärbar.

- Hover oder Fokus zeigt Titel und Kurzdefinition.
- Klick oder Aktivierung fixiert das Popover.
- Verknüpfte Begriffe innerhalb der Erklärung sind erneut aktivierbar.
- Rekursive Navigation ersetzt den Inhalt im selben Popover und führt einen Breadcrumb beziehungsweise Verlauf.
- Zurücknavigation ist möglich.
- `F1` oder eine sichtbare Aktion öffnet den vollständigen Katalogeintrag in einem Standardfenster.
- Es werden keine unkontrollierten Kaskaden verschachtelter Popups erzeugt.

## Lokalisierung von Serverdaten

Der Server überträgt stabile Codes, IDs und numerische Werte. Der Client lokalisiert beispielsweise:

- Befehlstypen,
- Statuscodes,
- Fehlergründe,
- Ressourcentypen,
- Wissensstufen,
- Kontextaktionen.

Der Server darf zusätzlich einen sicheren menschenlesbaren Fallback liefern. Dieser ersetzt nicht den stabilen maschinenlesbaren Code.

## Testanforderungen

- Jeder sichtbare Schlüssel muss in der Basissprache vorhanden sein.
- Ungenutzte oder fehlende Schlüssel werden automatisiert gemeldet.
- Kontextparameter werden gegen eine definierte Signatur geprüft.
- Unzulässige Markup-Tags werden abgelehnt.
- Tabellen, Dialoge und Tabs werden mit langen Übersetzungen getestet.
- Zahlen, Datum und Pluralformen werden mindestens für Deutsch und Englisch geprüft.
- Concept-Popovers werden auf Fokus, Rekursion, Zurücknavigation und Zyklen getestet.
- Komponenten-Snapshots dürfen keine fachlichen Serverregeln duplizieren.

## Akzeptanzkriterien

- Wiederkehrende UI-Fälle verwenden einen dokumentierten gemeinsamen Komponententyp.
- Label-Wert-Daten folgen einem einheitlichen Property-Grid.
- Jeder Buttontyp besitzt definierte Zustände und einen eindeutigen Zweck.
- Keine sichtbaren Texte sind ohne begründete Ausnahme in Fachkomponenten festgeschrieben.
- Sprachdateien unterstützen sichere Formatierung und typisierte Kontextwerte.
- Fachbegriffe sind per Maus und Tastatur erklärbar.
- Rekursive Begriffsnavigation erzeugt keine unendliche Popup-Kaskade.
