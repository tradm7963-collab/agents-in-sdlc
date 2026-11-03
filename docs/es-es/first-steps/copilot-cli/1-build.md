---
title: "Lección 1 - Crear el cuestionario desde la terminal"
description: "Pide a Copilot CLI todo el Space Quiz en una única solicitud detallada y realiza un ajuste concreto."
authors:
  - jamesmontemagno
lastUpdated: 2026-09-28
---

Pide todo el proyecto en una única solicitud detallada, revisa lo que propone el agente antes de aprobarlo y, después, realiza un cambio pequeño y acotado.

En esta lección:

- crearás un cuestionario sin dependencias en `index.html`.
- abrirás el cuestionario en un explorador desde la sesión.
- realizarás un cambio concreto y lo comprobarás.

## Crea el cuestionario

Envía el siguiente prompt en tu sesión de Copilot CLI:

```plaintext
Crea un cuestionario sobre exploración espacial con 10 preguntas, una barra de progreso, un contador de puntuación y mensajes animados y coloridos (verde para las respuestas correctas y una sacudida roja para las incorrectas). Al final, muestra una pantalla de resultados con una reacción mediante un emoji. Usa un único archivo `index.html`, sin servidor ni dependencias. Debe ser accesible, permitir la navegación con teclado y respetar `prefers-color-scheme`.
```

1. Lee el plan propuesto y aprueba los cambios en los archivos.
2. Abre `index.html` en un explorador y responde a unas cuantas preguntas. Para abrirlo desde la sesión, ejecuta `!open index.html` en macOS, `!start index.html` en Windows o `!xdg-open index.html` en Linux.

## Realiza un cambio pequeño y compruébalo

Pide un ajuste concreto para ver cómo se comporta una solicitud acotada:

```plaintext
The results screen feels flat. Give it a stronger sense of arrival: animate the score counting up and make the emoji reaction larger. Change nothing else.
```

1. Vuelve a cargar la página en el explorador y responde a todas las preguntas hasta el final.
2. Observa que todavía no hay nada en Git, así que no hay ninguna versión con la que comparar las diferencias. Eso cambiará cuando publiques el proyecto.

## Resumen y pasos siguientes

Has creado el cuestionario y lo has perfeccionado con una solicitud acotada. Continúa con la [lección 2: Recoger las instrucciones del proyecto][next-lesson].

[next-lesson]: ../2-project-instructions/
