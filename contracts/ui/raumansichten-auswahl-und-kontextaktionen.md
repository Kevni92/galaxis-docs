# Raumansichten, Auswahl und Kontextaktionen

Status: Freigegeben

## Zweck

Dieser Vertrag definiert, welche Informationen und Interaktionen ein Client für Sternensystem- und Galaxieansicht bereitstellen muss. Er legt keine konkrete Renderingbibliothek fest.

## Raumobjekt

Ein für den aktuellen Reichskontext sichtbares Raumobjekt benötigt mindestens:

```json
{
  "id": "obj_...",
  "objectType": "planet",
  "knowledgeLevel": "explored",
  "displayNameKey": "object.earth.name",
  "systemId": "sys_...",
  "localPosition": {
    "x": 120.5,
    "y": -44.0
  },
  "renderKind": "terrestrial_planet",
  "links": {
    "self": "/api/v1/...",
    "details": "/api/v1/..."
  }
}
```

`localPosition` ist fachlich relevant. `renderKind` wählt ausschließlich eine Darstellungsfamilie und erzeugt keine Regel. Zusätzliche visuelle Parameter dürfen übertragen werden, wenn sie keine geheimen Eigenschaften ableiten lassen.

Ein Objekt ohne freigegebene Existenz wird nicht als Platzhalter übertragen.

## Visuelle Transformation

Der Client darf aus `localPosition` eine dreidimensionale Transformation erzeugen:

```text
sceneX = project(localPosition.x)
sceneY = visualHeight(object)
sceneZ = project(localPosition.y)
```

`sceneY`, Skalierung, Rotation und Animation sind nicht fachlich. Sie dürfen nicht in Befehlsdaten zurückgesendet oder zur Validierung verwendet werden.

## Auswahlzustand

Auswahl ist zunächst lokaler Clientzustand:

```json
{
  "view": "system",
  "selectedObjectIds": ["flt_9"],
  "primaryObjectId": "flt_9"
}
```

Auswahl darf keine Ressource verändern. Szene, Outliner und geöffnetes Detailfenster verwenden denselben Auswahlzustand.

## Primäraktion

Für ein sichtbares Objekt bedeutet die Primäraktion:

- Objekt auswählen,
- Objekt in Szene und Outliner fokussieren,
- bei Himmelskörpern oder verwaltbaren Objekten das modale Detailfenster öffnen oder aktualisieren.

Das Fenster verwendet die Detailressource des Objekts. Fehlende Berechtigung oder veraltetes Wissen wird als definierter Zustand angezeigt.

## Sekundäraktion auf freiem Raum

Bei ausgewählter bewegungsfähiger Flotte bildet ein Sekundärklick auf die Systemebene einen Zielvorschlag:

```json
{
  "selection": {
    "fleetIds": ["flt_9"]
  },
  "target": {
    "type": "local_position",
    "systemId": "sys_1",
    "x": 160.0,
    "y": -12.5
  }
}
```

Der Client kann den Vorschlag an eine Kontextaktions- oder Befehlsvorschau senden. Die Flotte bewegt sich erst nach Annahme eines fachlichen Befehls.

## Sekundäraktion auf Objekt

Für Auswahl und Zielobjekt fragt der Client verfügbare Kontextaktionen ab oder verwendet eine gleichwertige bereits gelieferte serverautoritative Repräsentation.

Beispielanfrage:

```json
{
  "selection": {
    "fleetIds": ["flt_9"]
  },
  "target": {
    "type": "object",
    "objectId": "pln_3"
  },
  "expectedStateVersion": 1842
}
```

Beispielantwort:

```json
{
  "stateVersion": 1842,
  "actions": [
    {
      "actionId": "fleet.move_to_object",
      "labelKey": "fleet.action.move_to_object",
      "enabled": true,
      "commandType": "fleet.move.local",
      "preview": {
        "duration": 240
      }
    },
    {
      "actionId": "fleet.colonize",
      "labelKey": "fleet.action.colonize",
      "enabled": false,
      "disabledReason": "COLONY_CAPABILITY_REQUIRED",
      "commandType": "fleet.colonize"
    }
  ]
}
```

Eine deaktivierte Aktion darf angezeigt werden, wenn ihr Grund dem Reich bekannt ist. Unbekannte geheime Voraussetzungen dürfen nicht durch einen zu genauen Fehlergrund geleakt werden.

## Kontextaktionszustände

Eine Aktion enthält mindestens:

- stabile `actionId`,
- Lokalisierungsschlüssel,
- aktiviert oder deaktiviert,
- sicheren Grund bei Deaktivierung,
- resultierenden Befehlstyp,
- bekannte Kosten, Dauer und Risiken,
- Bestätigungsanforderung,
- aktuelle `stateVersion`.

Die Liste ist eine Momentaufnahme. Vor Befehlsannahme validiert der Server erneut.

## Lokaler Bewegungsbefehl

Ein bestätigter lokaler Bewegungsbefehl adressiert eine Position oder einen fachlich definierten Objektanker:

```json
{
  "type": "fleet.move.local",
  "payload": {
    "fleetId": "flt_9",
    "systemId": "sys_1",
    "target": {
      "type": "position",
      "x": 160.0,
      "y": -12.5
    }
  }
}
```

oder:

```json
{
  "type": "fleet.move.local",
  "payload": {
    "fleetId": "flt_9",
    "systemId": "sys_1",
    "target": {
      "type": "object_anchor",
      "objectId": "pln_3",
      "anchor": "orbit"
    }
  }
}
```

Der Server bestimmt die verbindliche Route, Startzeit, Dauer und Zielposition.

## Galaxieaktion

Ein Sekundärklick auf ein bekanntes System kann Kontextaktionen für eine ausgewählte Flotte liefern. Ein interstellarer Bewegungsbefehl adressiert das Zielsystem und optional eine bekannte Route. Der Server wählt oder validiert ausschließlich bekannte und nutzbare Verbindungen.

## Detailfenster

Ein Objekt-Deep-Link muss mindestens folgende Zustände wiederherstellen können:

- Kampagne,
- Raumansicht `system` oder `galaxy`,
- fokussiertes System,
- ausgewähltes Objekt,
- geöffnetes Detailfenster,
- aktiver Tab.

Das Detailfenster ist eine Clientdarstellung von Ressourcen und Befehlen. Es ist keine eigene fachliche Entität.

## Tastaturäquivalenz

- Objektliste und Szene verwenden dieselben Objekt-IDs.
- `Enter` auf einem Objekt entspricht der Primäraktion.
- Kontexttaste oder `Shift+F10` entspricht der Sekundäraktion auf dem Objekt.
- Eine alternative Zielauswahl muss lokale Bewegungsziele ohne präzisen Zeiger ermöglichen.
- Fokus und Auswahl dürfen nicht allein durch Hover entstehen.

## Fehler- und Konfliktfälle

Mindestens zu unterscheiden sind:

- Auswahlobjekt nicht mehr sichtbar,
- Ziel nicht bekannt,
- Zielposition außerhalb des Systems,
- Flotte nicht mehr steuerbar,
- Aktion seit Vorschau ungültig,
- `stateVersion` überholt,
- Route nicht verfügbar,
- unzureichende Fähigkeit oder Versorgung,
- fehlende Berechtigung,
- Ressource aus Wissensschutz nicht auffindbar.

Ein Konflikt führt zu sicherem Reload und einer verständlichen Erklärung. Der Client setzt die Flotte nicht optimistisch an die Zielposition.

## Akzeptanzkriterien

- Fachliche XY-Position und visuelle 3D-Transformation sind getrennt.
- Primärauswahl öffnet Himmelskörperdetails modal.
- Sekundäraktionen können freie Positionen und Objekte adressieren.
- Kontextaktionen sind serverautoritativ und werden vor Ausführung erneut validiert.
- Maus und Tastatur verwenden dieselben IDs und Befehle.
- Unbekannte Objekte, Aktionen und Voraussetzungen werden nicht geleakt.
