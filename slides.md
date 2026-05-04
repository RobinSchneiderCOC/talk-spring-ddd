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
layout: white
---

<ImageSlide>
  <template #title>
    <h2 class="text-2xl font-bold leading-none">Problemstellung (Ausgangslage)</h2>
    <p class="text-base !mt-0 opacity-60">Backend-Anwendungen werden intern schlecht wartbar</p>
  </template>
  <template #image>
    <img src="/drawio/1-Problemstellung-Ausgangslage.drawio.svg" class="w-[80%] h-[80%] object-contain object-left dark:invert" />
  </template>
  <template #content>
    <ul class="list-disc list-inside flex flex-col gap-2">
      <li>Fachlichkeit in vielen Service-Klassen verteilt</li>
      <li>unübersichtlich</li>
      <li>viele Querverbindungen</li>
      <li>unklare Zuständigkeiten</li>
      <li>technisch getriebener Aufbau &amp; Namen</li>
    </ul>
  </template>
</ImageSlide>

---
layout: white
---

<ImageSlide>
  <template #title>
    <h2 class="text-2xl font-bold leading-none">Problemstellung (Ziel)</h2>
    <p class="text-base !mt-0 opacity-60">Fachlich gut wartbare/verständliche Backend-Anwendung</p>
  </template>
  <template #image>
    <img src="/drawio/1-Problemstellung-Ziel.drawio.svg" class="w-[80%] h-[80%] object-contain object-left dark:invert" />
  </template>
  <template #content>
    <ul class="list-disc list-inside flex flex-col gap-2">
      <li>Was? <br> Verständliche Namen, klare Zuständigkeiten und Call-Flow</li>
      <li>Wie? <br> Fachlichkeit sichtbar machen und Architektur anpassen</li>
      <li>Ausnahme: einfach CRUD-App</li>
    </ul>
  </template>
</ImageSlide>