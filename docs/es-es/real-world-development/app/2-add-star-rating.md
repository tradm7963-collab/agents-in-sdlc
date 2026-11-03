---
title: "Lección 2 - Añade valoraciones con estrellas: una mejora rápida"
description: "Inicia tu primera sesión de agente en la aplicación GitHub Copilot, haz un pequeño cambio en las tarjetas de juegos y fusiónalo en tu primera solicitud de cambios."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Ya has recorrido el espacio de trabajo y usado un chat rápido. Ahora iniciarás una **sesión de agente** y harás tu primer cambio en el proyecto. Será pequeño: los datos de los juegos ya incluyen una valoración con estrellas, pero las tarjetas de la página principal no la muestran. Pedirás al agente que la añada, revisarás el cambio y lo fusionarás en tu primera solicitud de cambios.

En esta lección:

- iniciarás una sesión de agente y aprenderás cómo se estructura.
- pedirás al agente que realice un cambio pequeño y acotado en el proyecto.
- revisarás el cambio en la vista de diferencias del espacio de trabajo.
- ejecutarás la aplicación en local para comprobar el cambio en el navegador.
- abrirás y fusionarás tu primera solicitud de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración con estrellas, que ya aparece en la página de detalles. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, el editor y la descripción. Como ejercicio inicial, pedirás al agente que muestre en cada tarjeta la valoración existente: es un cambio pequeño y autónomo, ideal para tu primera sesión.

## Anatomía de una sesión

Una **sesión** es una conversación con un agente que se ejecuta en su propio espacio de trabajo aislado. Cada sesión tiene un **árbol de trabajo de Git y una rama dedicados**, lo que permite ejecutar varias sesiones a la vez —una para añadir una función y otra para corregir un error, por ejemplo— sin que sus cambios entren en conflicto. Las sesiones aparecen en la barra lateral, agrupadas por repositorio. Selecciona una para cambiar a ella.

En una sesión verás tres elementos: la **conversación** con el agente, la **actividad de las herramientas** mientras explora y edita archivos, y la lista de **archivos modificados** con sus diferencias.

## Inicia una sesión y solicita el cambio

Inicia una sesión nueva para explorar el proyecto y empezar a implementar la funcionalidad. Durante la [configuración de la aplicación][prior-lesson], añadiste el proyecto desde su repositorio de GitHub. Ahora crearás una sesión para ese repositorio y solicitarás el cambio.

1. Vuelve a la aplicación GitHub Copilot o ábrela.
2. Selecciona **+** en la parte superior de la barra lateral para iniciar una sesión.
3. Selecciona `tailspin-toys` como repositorio.
4. Elige un **new working tree** y el modo **Interactive** debajo del cuadro de mensaje. Envía este mensaje:

    ```plaintext
    Muestra `starRating` sobre 5 en las tarjetas de juegos de la página de lista. Si la valoración es `null`, muestra «No rating yet». Mantén el diseño actual de las tarjetas, añade pruebas y ejecuta las comprobaciones pertinentes.
    ```

5. Pulsa <kbd>Enter</kbd> para enviar el mensaje a Copilot.

La aplicación Copilot empieza por crear un árbol de trabajo nuevo, una copia aislada del proyecto. Después, explora el proyecto, localiza los archivos que debe actualizar para añadir la función y crea el código necesario. ¡Ya has añadido una función con la aplicación Copilot!

## Revisa las diferencias

Todos los cambios generados por IA deben revisarse antes de fusionarlos, aunque sean pequeños. Examina los cambios desde la aplicación Copilot.

1. En la esquina superior derecha de la aplicación, selecciona **Toggle review panel**. En el panel que se abre, selecciona **Changes** para ver los archivos modificados y sus diferencias.

    ![Barra de herramientas superior de la aplicación GitHub Copilot con una flecha que señala el botón Toggle review panel, a la derecha de Create PR](../../../_images/app-2-review-panel.png)

2. Deberías ver código nuevo en `GameCard.astro`, el archivo principal que se usa para mostrar los detalles de los juegos. Debería ser parecido al siguiente: un bloque pequeño que muestra la valoración cuando existe y, si `starRating` es `null`, muestra «No rating yet».

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot, como todas las herramientas de IA generativa, es probabilístico, no determinista; por eso, el código concreto puede variar. Sin embargo, debería ser relativamente parecido.

## Comprueba los cambios

Revisa los resultados de las comprobaciones automatizadas del agente antes de abrir el navegador. Confirma que las pruebas cubren tanto un valor numérico de `starRating` como la alternativa para `null`. Un requisito previo ausente o una comprobación omitida no cuentan como superados; revisa cualquier solicitud de instalación antes de aprobarla.

No basta con leer el código y dar por hecho que funciona. Pide a Copilot que abra el sitio web para examinar la interfaz de usuario (UI) actualizada. Para ello, pídele que inicie el sitio y lo abra en un canvas del navegador.

> [!TIP]
> Un canvas es un widget interactivo disponible dentro de la aplicación Copilot. Más adelante explorarás canvases personalizados e incluso crearás uno, pero por ahora usarás el canvas de navegador integrado.

1. Envía este mensaje para pedir a Copilot que inicie la aplicación y abra la página en el canvas del navegador:

    ```plaintext
    Inicia la aplicación y ábrela en el canvas del navegador.
    ```

2. En unos instantes, la aplicación se iniciará y se abrirá una ventana del navegador dentro de la aplicación Copilot.
3. Confirma que las tarjetas de juegos con valoración muestran el valor sobre cinco.
4. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión y cierre el canvas del navegador:

    ```plaintext
    Detén el servidor de desarrollo y cierra el canvas del navegador.
    ```

## Abre y fusiona tu primera solicitud de cambios

¡Ya has creado la función! Ahora crearás una solicitud de cambios (PR) para incorporarla al código existente.

1. Selecciona **Create PR** en la esquina superior derecha.
2. Si se te solicita, selecciona **Sign in with your browser** y sigue las instrucciones para autenticarte.
3. Si Copilot indica que la política del repositorio requiere una incidencia relacionada antes de crear la PR, confirma que debe seguir ese proceso.
4. Copilot empezará a crear la PR.
5. Selecciona la burbuja **PR** justo encima del chat para abrir la solicitud en el panel de revisión. Revísala allí según sea necesario.
6. Cuando esté lista, selecciona **Ready to merge**.
7. En el cuadro de diálogo, selecciona **Merge pull request** para fusionarla.

## Resumen y siguientes pasos

¡Enhorabuena! Has publicado tu primer cambio con la aplicación GitHub Copilot. En concreto:

- has iniciado una sesión de agente y aprendido cómo se estructuran las sesiones.
- has pedido al agente que haga un cambio pequeño y acotado en las tarjetas de juegos.
- has revisado el cambio en la vista de diferencias del espacio de trabajo.
- has ejecutado la aplicación en local para comprobar la valoración con estrellas en el navegador.
- has abierto la PR 1, revisado sus comprobaciones y autorizado explícitamente la fusión.

A continuación, [partirás de la incidencia de filtrado y usarás los modos Plan y Autopilot][next-lesson] para crear una función más amplia.

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Administrar incidencias y solicitudes de cambios con la aplicación GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instala-y-configura-la-aplicacion-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
