# Besitz und Kontrolle von Sternensystemen

Status: Freigegeben

## Zweck

Dieses Dokument trennt territorialen Anspruch, souveränen Besitz, militärische Kontrolle und Besetzung. Diplomatische Anerkennung, Krieg und Friedensschlüsse werden in D7 konkretisiert.

## Grundsatz

Ein System besitzt keinen pauschalen Eigentumswert:

- Mehrere Reiche können Ansprüche besitzen.
- Souveräner Besitz gehört höchstens einem Reich.
- Militärische Kontrolle kann vom Besitzer abweichen.
- Mehrere Reiche können militärisch präsent sein.
- Ein System kann umstritten sein, ohne den Besitzer zu wechseln.

## Anspruch

Ein Anspruch ist eine territoriale Forderung. Er gewährt weder Besitz noch automatisch Bau-, Nutzungs- oder Bewegungsrechte. Quelle, Beginn, Status und gegebenenfalls Ablauf werden gespeichert. Entstehung und diplomatische Wirkung folgen in D7.

## Souveräner Besitz

Souveräner Besitz ist die dauerhafte territoriale Zuordnung zu einem Reich. Er kann durch anerkannte Kolonisierung, Außenposten, Vertrag, Frieden oder Ereignis entstehen. Eine Flotte allein reicht nicht aus.

## Militärische Kontrolle und Besetzung

Militärische Kontrolle beschreibt die aktuelle Beherrschung strategischer Punkte. Sie ist vorübergehend und überträgt nicht automatisch Kolonien, Bevölkerung oder Anlagen.

Besetzung liegt vor, wenn ein fremdes Reich ein souverän besessenes System militärisch kontrolliert. Der ursprüngliche Besitzer bleibt bestehen, bis eine anerkannte Regel den dauerhaften Übergang bewirkt.

## Umstrittener Zustand

`Umstritten` ist ein abgeleiteter Zustand bei konkurrierenden Ansprüchen, militärischen Kräften, Krieg, Besetzung oder widersprüchlichen Verträgen. Die zugrunde liegenden Zustände bleiben erhalten.

## Territoriale Grundlage

Souveräner Besitz benötigt eine fachlich definierte Grundlage wie Kolonie oder anerkannten Außenposten. Flotten und temporäre Missionen sind keine Grundlage. Der Verlust der letzten Grundlage löst eine dokumentierte Neubewertung aus, keinen stillen Besitzverlust.

## Besitz- und Kontrollwechsel

Ein Besitzwechsel ist autoritativ und protokolliert. Er enthält System, alten und neuen Besitzer, Grund, Wirksamkeitszeitpunkt sowie Behandlung von Kolonien, Anlagen, Ansprüchen und Zugangsrechten.

Militärische Kontrolle kann häufiger wechseln und zeitweise uneindeutig sein. Grundlage sind autoritativ ausgewertete militärische Zustände.

## Grenzen

Sichtbare Grenzen werden aus souverän besessenen, dem betrachtenden Reich bekannten Systemen abgeleitet. Sie sind keine eigene Wahrheitsquelle. Besetzte und umstrittene Systeme sowie Ansprüche werden getrennt dargestellt.

## Rechte

Jede spätere Aktion muss ausdrücklich angeben, ob sie Anspruch, Besitz, militärische Kontrolle, Besetzung oder ein Zugangsrecht benötigt. Eine allgemeine Abfrage `gehört Reich` ist unzureichend.

## Wissen und Offline-Fortschritt

Besitzinformationen können öffentlich sein; militärische Kontrolle kann aktuelle Sensorik erfordern. Veraltete Angaben werden markiert. Relevante Besitz- und Kontrollwechsel erscheinen im Rückkehrbericht. Irreversible Verluste benötigen angemessene Reaktionsfenster.

## Anforderungen an Client und Server

Der Client stellt Anspruch, Besitz, Besetzung, Kontrolle und umstrittenen Zustand unterscheidbar dar. Der Server speichert die Zustände getrennt, erlaubt höchstens einen souveränen Besitzer, unterstützt mehrere Ansprüche und Präsenzen und prüft Aktionen gegen den korrekten Zustand.

## Offene Folgefragen

1. Welche Objekte bilden eine territoriale Grundlage?
2. Wie entstehen und verfallen Ansprüche?
3. Wie wird militärische Kontrolle konkret bestimmt?
4. Welche Folgen besitzt Besetzung für Kolonien und Wirtschaft?
5. Welche Besitzinformationen sind öffentlich?

## Akzeptanzkriterien

- Anspruch, Besitz, Kontrolle und Besetzung sind getrennt.
- Flottenanwesenheit erzeugt keinen dauerhaften Besitz.
- Besetzung überträgt nicht automatisch Souveränität.
- Grenzen sind abgeleitet.
- Mehrere Ansprüche und umstrittene Zustände sind abbildbar.

## Verwandte Dokumente

- [Galaxiestruktur und Generierung](galaxiestruktur-und-generierung.md)
- [Erkundung und Informationsstände](erkundung-und-informationsstaende.md)
- [Bewegung und Verbindungen](bewegung-und-verbindungen.md)
- [Reiche – Übersicht](../03-empires/README.md)
- [Diplomatie – Übersicht](../09-diplomacy/README.md)
