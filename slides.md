---
title: Talk Spring DDD
titleTemplate: '%s'
favicon: '/images/spring-logo.svg'
layout: blue
---

# Vom Spaghetti-Code zur Zwiebel: <br> Spring Boot gewürzt mit DDD

---
layout: blue
---

# Wie modelliert man Fachlichkeit im Backend?

Damit die Fachlichkeit besser sichtbar wird, <br> um die Wartbarkeit des Backends zu erhöhen.

---
layout: blue
---

# Agenda

<v-clicks>

1. Problemstellung
2. Fachsprache im Code abbilden
3. Äußere Struktur schaffen
4. Innere Struktur schaffen
5. Kopplung an Technik entfernen
6. Fazit

</v-clicks>

---
layout: blue
---

# Problemstellung

---
layout: image-slide
heading: Problemstellung (Ausgangslage)
subtitle: Backend-Anwendungen werden intern schlecht wartbar
image: /drawio/1-Problemstellung-Ausgangslage.drawio.svg
notes:
  - Fachlichkeit in vielen Service-Klassen verteilt
  - unübersichtlich
  - viele Querverbindungen
  - unklare Zuständigkeiten
  - technisch getriebener Aufbau & Namen
---

---
layout: image-slide
heading: Problemstellung (Ziel)
subtitle: Fachlich gut wartbare/verständliche Backend-Anwendung
image: /drawio/1-Problemstellung-Ziel.drawio.svg
notes:
  - Was? <br> Verständliche Namen, klare Zuständigkeiten und Call-Flow
  - Wie? <br> Fachlichkeit sichtbar machen und Architektur anpassen
  - Ausnahme? <br>  einfach CRUD-App
---