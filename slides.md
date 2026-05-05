---
title: Talk Spring DDD
titleTemplate: '%s'
favicon: 'images/spring-logo.svg'
layout: blue
addons:
  - fancy-arrow
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

<ol class="agenda-list">
  <li style="animation-delay: 2s">Problemstellung</li>
  <li style="animation-delay: 6s">Fachsprache im Code abbilden</li>
  <li style="animation-delay: 10s">Äußere Struktur schaffen</li>
  <li style="animation-delay: 14s">Innere Struktur schaffen</li>
  <li style="animation-delay: 18s">Kopplung an Technik entfernen</li>
  <li style="animation-delay: 22s">Fazit</li>
</ol>

---
layout: blue
---

# Problemstellung

---
layout: image-slide
heading: Problemstellung (Ausgangslage)
subtitle: Backend-Anwendungen werden __intern schlecht wartbar|2000__
image: /drawio/1-Problemstellung-Ausgangslage.drawio.svg
notes:
  - Fachlichkeit in vielen Service-Klassen verteilt
  - unübersichtlich
  - viele Querverbindungen
  - unklare Zuständigkeiten
  - technisch getriebener Aufbau & Namen
---

<template #overlay>
  <FancyArrow
    from="[data-id=subtitle]@right"
    to="[data-id=notes-box]@top-left"
    color="orange"
    width="3"
    duration="2000"
    delay="4000"
  />
</template>

---
layout: image-slide
heading: Problemstellung (Ziel)
subtitle: Fachlich gut __wartbare/verständliche|2000__ Backend-Anwendung
image: /drawio/1-Problemstellung-Ziel.drawio.svg
notes:
  - __Was?|2000__ <br> Verständliche Namen, klare Zuständigkeiten und Call-Flow
  - __Wie?|2000__ <br> Fachlichkeit sichtbar machen und Architektur anpassen
  - ((Ausnahme?|4000)) <br>  einfach CRUD-App
---

---
layout: blue
---

# Fachsprache im Code abbilden

---
layout: image-slide
heading: Fachsprache im Code abbilden
subtitle: Namensgebung gemäß Fachexperten
image: /drawio/2-Fachsprache-im-Code-abbilden.drawio.svg
notes:
  - Mit Fachexperten __reden|2000__ (+ Glossar)
  - Nomen und Verben fachlich (+ deutsch), z.B. Buch ausleihen, statt update Book
  - kein mentales Mapping mehr, Missverständnisse reduzieren
  - 'DDD: "Ubiquitous Language"'
---

---
layout: blue
---

# Äußere Struktur schaffen

---
layout: image-slide
heading: Äußere Struktur schaffen
subtitle: Fachliche Module schneiden
image: /drawio/3-Aeussere-Struktur-Fachliche-Module.drawio.svg
notes:
  - Gibt es fachliche Grenzen (__Bounded Contexts|2000__)?
  - Eigene top-level Packages, z.B. „Bestellung" oder „Lieferung"
  - Spring __Modulith|4000__ prüft Grenzen
  - Microservices?
  - 'DDD: "Strategisches Design"'
---

---
layout: blue
---

# Innere Struktur schaffen

---
layout: image-slide
heading: Innere Struktur schaffen
subtitle: "Vorarbeit: Refactoring von bestehenden Service-Klassen"
image: /drawio/4-Innere-Struktur-Refactoring.drawio.svg
notes:
  - Vor dem Umbau erst einmal aufräumen & vereinfachen
  - Klassen mit ähnlichen fachlichen Aufgaben zusammen ziehen
  - Klassen, die nur weiterleiten, entfernen
---

---
layout: image-slide
heading: Innere Struktur schaffen
subtitle: Logik aus Service-Klassen herausziehen
image: /drawio/4-Innere-Struktur-Logik-herausziehen.drawio.svg
notes:
  - __Orchestrierung|2000__ in Use Cases verschieben
  - __Validierungsregeln|4000__ in Entities verschieben
  - übrig bleiben kleine Domain-Services
  - "Vorteil: klare Zuständigkeiten, nachvollziehbarer Call-Flow"
---

---
layout: image-slide
heading: Innere Struktur schaffen
subtitle: Domain modellieren
image: /drawio/4-Innere-Struktur-Domain-modellieren.drawio.svg
notes:
  - "bereits da: Logik in Entity und fachliche Namen für Methoden (keine Setter)"
  - Einführung von __Value Objects|2000__ , z.B. „Geld" oder „EmailAdresse"
  - Aggregates schneiden
  - 'DDD: "Taktisches Design"'
---

---
layout: image-slide
heading: Innere Struktur schaffen
subtitle: Domain-driven REST-API
image: /drawio/4-Innere-Struktur-Action-API.drawio.svg
notes:
  - Trigger der Use Cases über Action-Endpunkte
  - __Verben|2000__  nutzen statt 100%-RESTful z.B. /publish
  - Fachlichkeit statt CRUD
  - Prozesse statt Resourcen/Daten
  - Commands in CQRS
---

---
layout: image-slide
heading: Innere Struktur schaffen
subtitle: Zwischenziel erreicht
image: /drawio/4-Innere-Struktur-Zwischenziel.drawio.svg
notes:
  - Code ist übersichtlicher und fachlich orientiert
  - Bis hier genügt es in vielen Projekten
  - "aber: Kopplung an Infrastruktur noch vorhanden (ist das schlimm?)"
---

---
layout: blue
---

# Kopplung an Technik entfernen

---
layout: image-slide
heading: Kopplung an Technik entfernen
subtitle: Welche Verbindungen zur Technik gibt es?
image: /drawio/5-Kopplung-an-Technik-entfernen-Verbindungen.drawio.svg
notes:
  - Eingehende Aufrufe sind unproblematisch (API zu Business)
  - Ausgehende Aufrufe erzeugen Kopplung an Technik (Business zu Persistenz bzw Service-Client)
  - "Lösung: Abhängigkeiten umdrehen (__DIP|2000__)"
---

---
layout: image-slide
heading: Kopplung an Technik entfernen
subtitle: API-Client auftrennen
image: /drawio/5-Kopplung-an-Technik-entfernen-API-Client.drawio.svg
notes:
  - Der fachliche Kern sollte nicht direkt von Infrastruktur abhängen
  - Entkopplung der API-Clients über Interfaces (Ports)
  - Implementierung (Adapters) kann sich beliebig ändern
  - Hexagonale Architektur
---

---
layout: image-slide
heading: Kopplung an Technik entfernen
subtitle: Persistenz auftrennen
image: /drawio/5-Kopplung-an-Technik-entfernen-Persistenz.drawio.svg
notes:
  - Die Entities hängen noch von der Infrastruktur ab (zb JPA)
  - Entities & Repositories auftrennen
  - Mapping notwendig!
  - Code wird __aufgebläht|2000__ (Dopplungen)
---

---
layout: image-slide
heading: Kopplung an Technik entfernen
subtitle: "Konsequenz: Projektstruktur ändern"
image: /drawio/5-Kopplung-an-Technik-entfernen-Onion.drawio.svg
notes:
  - Packages umbenennen, Klassen verschieben
  - Ringe statt Schichten
  - es ergibt sich ein Onion/Clean-Aufbau samt Hexagonaler Architektur
---

---
layout: blue
---

# Fazit

---
layout: image-slide
heading: Fazit
subtitle: Evolution des Backend-Services
image: /drawio/6-Fazit-Spaghetti-zu-Onion.drawio.svg
notes:
  - kein Big-Bang notwendig
  - Fachlichkeit in Code sichtbar gemacht
  - Architektur leicht angepasst
  - "Vorteil: besser wartbar für Entwickler, langfristig stabil"
---

---
layout: image-slide
heading: Fazit
subtitle: "Beispiel: DDD + Java/Spring-Boot"
image: /drawio/6-Fazit-Beispiel-Robin.drawio.svg
notes:
  - "siehe auch weitere Beispiele (mit Onion-Struktur) hier:"
  - "https://github.com/maciejwalkowiak/implementing-ddd-with-spring-talk"
  - "https://github.com/mattiacirioloWS/spring-io-conf-25"
---

---
layout: image-slide
heading: Fazit
subtitle: Layered Arc vs Onion/Hex-Arc
image: /drawio/6-Fazit-Layer-vs-Onion.drawio.svg
notes:
  - Kein großer Unterschied, Abhängigkeit wird lediglich gedreht über Interface
  - Konzept bzw Ordner-Namen zweitrangig, Fokus auf äußere fachliche Module
  - "Oliver Drotbohm: https://youtu.be/U6QLMCQKGtU?t=877"
---

---
layout: image-slide
heading: Fazit
subtitle: "Empfehlung: __einfach starten|2000__"
image: /drawio/6-Fazit-Empfehlung-Robin.drawio.svg
notes:
  - Module einführen
  - Layer beibehalten
  - Use Cases herausziehen
  - Kopplung an Spring Boot ist in Ordnung, Entity nicht auftrennen, aber mit Logik
  - Fachliche Namen für Klassen und Methoden
---

<template #overlay>
  <FancyArrow
    from="[data-id=subtitle]@right"
    to="[data-id=notes-box]@top-left"
    color="orange"
    width="3"
    duration="2000"
    delay="4000"
  />
</template>

---
layout: blue
---

# Ende