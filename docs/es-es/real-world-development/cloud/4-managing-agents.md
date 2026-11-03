---
title: "Ejercicio 4 - Supervisión y administración de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has pedido al agente de Copilot en la nube que realice tres tareas distintas para mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente trabaja de forma autónoma y asíncrona, es importante poder supervisar esas tareas.

Hay varias herramientas para administrar las tareas asignadas al agente, como la [página de agentes][agents-page] de GitHub.com. Desde Mission Control puedes ver las tareas de los agentes que tienen solicitudes de cambios (PR) abiertas, consultar las acciones realizadas e incluso guiar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube.
- guiarás una sesión en curso y le pedirás que añada otra funcionalidad.

## Escenario

Después de asignar al agente la tarea de crear un modo de contraste alto, el equipo se dio cuenta de que también sería buen momento para añadir un modo claro. Como ya se estaba trabajando en actualizar el estilo del sitio y añadir una función de alternancia, parecía lógico incluirlo. Guiarás al agente para que añada tanto el modo claro como el de contraste alto.

## Revisa las tareas del agente de Copilot en la nube

Consulta el estado de todas las tareas asignadas al agente de Copilot en la nube.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa las tareas en el panel principal y en el panel izquierdo. Deberías ver las tareas que has asignado a Copilot, entre ellas:
    - actualizar la documentación del código.
    - generar API para modificar juegos.
    - añadir un modo de contraste alto al sitio web.
3. Selecciona una de las tareas en curso y revisa lo que ha hecho Copilot. Por ejemplo:
    - obtener el código del repositorio.
    - preparar el entorno para Copilot.
    - configurar servidores MCP.
    - realizar varios pasos para completar la tarea.

> [!NOTE]
> Los pasos concretos dependerán del estado de la tarea de Copilot y del enfoque que haya seguido.

4. Observa también el panel de solicitudes de cambios, que aparece a la derecha. Desde allí puedes consultar la PR y los archivos modificados.

## Guía al agente en la nube

Ahora que has visto las tareas en curso, pide a Copilot que añada el modo claro mientras implementa el modo de contraste alto.

1. Selecciona la sesión relacionada con el modo de contraste alto. El título exacto dependerá del nombre que haya elegido Copilot y del estado de la tarea.

    ![Sesión de accesibilidad en Mission Control](../../../_images/ex6-accessibility-session.png)

2. Espera unos minutos hasta que el agente termine de configurar el entorno y empiece a trabajar. Lo notarás cuando aparezcan mensajes parecidos a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este mensaje:

    ```plaintext
    Mientras trabajamos en el modo de contraste alto, añadamos también un modo claro. Debe incluir un selector para que las personas puedan elegir el modo de visualización que prefieran.
    ```

    ![Captura de la tarea del agente en la página de agentes, con el cuadro de diálogo para guiar una sesión activa mientras Copilot trabaja resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el mensaje.
5. Observa cómo Copilot lo confirma y lo incorpora al flujo de trabajo.

## Deja que Copilot trabaje

Como antes, Copilot empezará a trabajar en la tarea actualizada. Incorporará la nueva solicitud al terminar el paso en el que estaba trabajando cuando enviaste el mensaje.

El proceso tardará varios minutos. Es un buen momento para hacer una pausa y repasar lo que has aprendido y explorado hasta ahora.

## Resumen y siguientes pasos

En esta lección has explorado la página de agentes de Copilot, que es el centro para supervisar y guiar las tareas del agente de GitHub Copilot en la nube. Puedes realizar un seguimiento de las tareas activas y completadas, revisar el trabajo y redirigir las tareas en curso para cambiar su alcance o añadir indicaciones.

Has explorado estos conceptos:

- has usado Mission Control y la página de agentes para supervisar las tareas del agente en la nube.
- has redirigido una sesión en curso para solicitar otra funcionalidad.

Mientras Copilot termina de trabajar en las funciones de accesibilidad, puedes [iterar sobre las solicitudes de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iteración sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
