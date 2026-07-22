# Idee: Lokales LLM als strategischer AI-Controller

Status: Unverbindliche Idee

> Dieses Dokument gehört nicht zur fachlichen Dokumentation und hat keinen Einfluss auf das Spiel. Es beschreibt ausschließlich eine mögliche spätere technische und spielerische Richtung.

## Kurzbeschreibung

Ein lokal betriebenes Large Language Model könnte ein AI-gesteuertes Reich auf strategischer Ebene unterstützen. Der Galaxis-Server würde das Modell über eine lokale REST-Schnittstelle ansprechen, beispielsweise über Ollama oder `llama-server`.

Das LLM würde keine Spielzustände direkt verändern. Es dürfte ausschließlich strukturierte Ziele oder erlaubte Befehle vorschlagen. Der Server bliebe für Spielregeln, Validierung, Simulation, Zeit, Zufall und Persistenz vollständig autoritativ.

## Mögliche Architektur

```text
Galaxis-Server
├── Simulation und Spielregeln
├── EmpireController
│   ├── PlayerEmpireController
│   └── AiEmpireController
│       ├── RuleBasedController
│       └── LlmStrategicPlanner
├── CommandQueue
└── REST-Client zum lokalen LLM-Dienst
```

Ein abstrakter Anbieter könnte verschiedene lokale oder spätere entfernte Modelle kapseln:

```text
LlmProvider
├── OllamaProvider
├── LlamaCppProvider
├── RemoteProvider
└── MockProvider
```

## Aufgabenteilung

### LLM: strategische Ebene

Mögliche Aufgaben:

- langfristige Reichsziele priorisieren,
- diplomatische Haltung bestimmen,
- auf Krisen und bedeutende Ereignisse reagieren,
- Forschungs- oder Wirtschaftsschwerpunkte empfehlen,
- Kolonien strategisch spezialisieren,
- Persönlichkeit und Rollenspiel eines Reiches prägen.

### Klassische AI: operative Ebene

Mögliche Aufgaben:

- konkrete Gebäude auswählen,
- Flotten und Ziele zuordnen,
- Ressourcenengpässe ausgleichen,
- Bau- und Forschungswarteschlangen verwalten,
- gültige Routen und Aktionen bestimmen.

### Deterministische Systeme: taktische Ebene

Dazu gehören insbesondere:

- Kampfberechnung,
- Pfadfindung,
- Ressourcenberechnung,
- Befehlsvalidierung,
- Zustandsübergänge.

## Möglicher Entscheidungsablauf

1. Der Server erzeugt eine kompakte Beobachtung aus Sicht des AI-Reiches.
2. Fog of War und verborgene Informationen werden bereits vor dem LLM-Aufruf berücksichtigt.
3. Das LLM erhält nur zulässige Aktionstypen und ein festes Antwortschema.
4. Das LLM liefert Ziele, Prioritäten und vorgeschlagene Befehle als strukturiertes JSON.
5. Der Server validiert jeden Vorschlag wie einen Spielerbefehl.
6. Nur gültige Befehle gelangen in die normale `CommandQueue`.
7. Bei Fehlern übernimmt eine regelbasierte Fallback-AI.

Beispiel einer möglichen LLM-Antwort:

```json
{
  "goals": [
    {
      "goal": "secure_eastern_border",
      "priority": 90,
      "duration_days": 7
    }
  ],
  "commands": [
    {
      "action": "reinforce_border",
      "target": "eastern_sector",
      "priority": 90
    }
  ]
}
```

## Sicherheits- und Konsistenzgrenzen

Das LLM dürfte nicht:

- direkt auf Datenbank oder Spielzustand schreiben,
- eigene Ressourcen, Einheiten oder Ergebnisse erzeugen,
- unbekannte Informationen erhalten,
- Spielregeln überschreiben,
- nicht freigegebene Befehlstypen erfinden,
- für den Fortgang der Simulation zwingend erforderlich sein.

Das Spiel müsste auch ohne erreichbares LLM vollständig funktionieren.

## Mögliche Auslöser

Ein LLM-Aufruf wäre nicht bei jedem Tick sinnvoll. Denkbare Auslöser wären:

- ein strategisches Zeitintervall,
- Erstkontakt,
- Kriegserklärung oder Friedensangebot,
- Verlust eines wichtigen Systems,
- schwerer Ressourcenengpass,
- neue Kolonie,
- bedeutendes politisches Ereignis,
- Abschluss eines bisherigen Plans.

## Lokaler Singleplayer

Im lokalen Singleplayer könnte der Server einen Dienst auf demselben Rechner ansprechen:

```text
Galaxis-Server → localhost → Ollama oder llama-server
```

Der Client sollte das Modell nicht direkt ansprechen. Alle AI-Entscheidungen müssten über den Server laufen.

## Späterer Multiplayer

In einem Multiplayer-Szenario müsste die AI serverseitig oder über einen kontrollierten zentralen AI-Dienst laufen. Ein Modell auf dem Rechner eines Spielers wäre nicht vertrauenswürdig.

Bei Übernahme eines AI-Reiches durch einen Spieler könnten bestehende Ziele und laufende Befehle erhalten bleiben. Der zuständige `EmpireController` würde von AI auf Spieler wechseln.

## Mögliche Teststrategie

Normale PR-Tests würden kein echtes LLM starten. Stattdessen könnte ein `MockLlmProvider` feste Antworten liefern, darunter:

- gültige Pläne,
- ungültiges JSON,
- unerlaubte Befehle,
- Timeouts,
- widersprüchliche Aktionen.

Damit könnten Zustandszusammenfassung, Schema, Validierung, Fog of War und Fallback deterministisch getestet werden.

Tests mit einem echten lokalen Modell wären höchstens für manuelle Versuche oder Nachtläufe geeignet.

## Chancen

- individuellere und glaubwürdigere Reichspersönlichkeiten,
- flexiblere diplomatische Reaktionen,
- nachvollziehbare strategische Ziele,
- bessere Wiederverwendbarkeit derselben AI-Schnittstelle für verschiedene Modelle.

## Risiken

- schwankende Qualität und Reproduzierbarkeit,
- zusätzliche Hardwareanforderungen,
- hohe Antwortzeiten bei vielen Reichen,
- ungültige oder unlogische Vorschläge,
- größerer Entwicklungs- und Testaufwand,
- mögliche Abhängigkeit von konkreten Modellfähigkeiten.

## Offene Fragen

- Soll das LLM nur optional oder als ausdrücklich aktivierbarer Spielmodus angeboten werden?
- Welche Modelle und Hardwareklassen wären realistisch?
- Wie kompakt muss der übergebene Reichszustand sein?
- Wie häufig darf ein Reich planen?
- Wie werden Persönlichkeit und strategisches Gedächtnis gespeichert?
- Welche Entscheidungen dürfen ausschließlich klassische Algorithmen treffen?
- Wie wird die Qualität eines strategischen Plans objektiv bewertet?
