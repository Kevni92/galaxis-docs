# 0006 – Alpha-Clienttechnologiestack

Status: ersetzt

Datum: 2026-07-22

Ersetzt durch: [0007 – Client-UX, 3D-Raumdarstellung und Lokalisierung](0007-client-ui-rendering-und-lokalisierung.md)

## Historischer Kontext

Diese Entscheidung legte ursprünglich TypeScript, Vue 3, Vite, Vue Router, Pinia, eine zentrale `fetch`-Abstraktion, OpenAPI-Typen, Vitest, Vue Test Utils, Playwright und SVG für die ersten System- und Galaxiekarten fest.

Die grundlegende Vue-/TypeScript-Architektur bleibt erhalten. Die Festlegung auf SVG als primäre Raumdarstellung, der Ausschluss einer 3D-Rendering-Schicht und die fehlende Festlegung für Fenstersystem, Lokalisierung und Begriffskatalog wurden durch Decision 0007 ersetzt.

## Nicht mehr verbindlich

Insbesondere sind folgende frühere Aussagen nicht mehr verbindlich:

- SVG als primäre System- und Galaxiekarte,
- keine 3D-Engine in A0 bis A3,
- eine spätere vollständige visuelle Ersetzung der frühen Raumansichten.

Die aktuelle verbindliche Entscheidung steht vollständig in Decision 0007.
