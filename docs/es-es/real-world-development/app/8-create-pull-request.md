---
title: "Lección 8 - Crea y fusiona la PR de la funcionalidad"
description: "Revisa en conjunto el filtrado, las instrucciones, la actualización de la habilidad, el perfil de QA y las pruebas; después, crea una PR y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación del filtrado, las actualizaciones de instrucciones y de la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Es hora de revisarlos juntos y abrir una solicitud de cambios. Ya fusionaste personalmente la PR de valoración con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo habitual sería dividir la función, las actualizaciones de instrucciones, la actualización de la habilidad y el agente de QA en varias PR. Para simplificar el taller, has mantenido todo el flujo de trabajo de filtrado y calidad en una sola sesión y rama, y lo incluirás en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- inspeccionarás la PR completa de la función y las pruebas de validación.
- autorizarás Agent Merge solo después de la revisión y confirmarás que la PR se ha fusionado.

## Escenario

Durante el flujo de trabajo de filtrado, has usado Copilot para planificar, implementar y validar una función. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR y mantener bajo el control del desarrollador la autorización para fusionarla.

## Introducción a Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de cambios en la aplicación GitHub Copilot. Al activarlo, la sesión de la aplicación lee la solicitud y resuelve los bloqueos: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y vuelve a aplicar los cambios sobre la rama base cuando es necesario. La fusiona en cuanto GitHub lo permite. Se ejecuta en segundo plano, sigue funcionando tras reiniciar la aplicación y se desactiva cuando se fusiona la solicitud.

Hasta ahora has seleccionado **Merge pull request** tú mismo. Agent Merge puede encargarse de esa responsabilidad, pero sigue necesitando tu autorización explícita para editar código y fusionar. Revisa las acciones permitidas y el trabajo antes de conceder permiso para fusionar.

## Usa Agent Merge para gestionar la PR

Ya has creado y revisado todo el código. Ahora permite que Agent Merge gestione el proceso de la PR.

1. Usa el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El botón cambiará a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Elegir la opción del menú desplegable no lo inicia por sí solo.

Se iniciará el proceso de Agent Merge. El agente:

- creará la solicitud de cambios con un título y una descripción.
- si has iniciado la sesión desde una incidencia, la mencionará en el cuerpo de la descripción.
- volverá a aplicar los cambios sobre la rama de destino o resolverá posibles conflictos de fusión.
- supervisará el proceso de CI para confirmar que se superen todas las comprobaciones.
- supervisará la PR para detectar comentarios de otros desarrolladores o de la revisión de código de Copilot, y hará cambios para resolverlos.
- podrá fusionar automáticamente la PR cuando todo termine correctamente.

Deja que Agent Merge también fusione la PR cuando se superen todas las comprobaciones.

5. Revisa la diferencia de la PR y las pruebas de validación antes de conceder permiso para fusionarla.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que **Merge pull request** está marcado.
8. Pide explícitamente al agente que fusione la PR:

    ```plaintext
    Fusiona la PR cuando se hayan superado todas las comprobaciones y aprobaciones obligatorias. No omitas las protecciones del repositorio.
    ```

9. Supervisa el progreso y resuelve cualquier bloqueo que se indique. Antes de continuar, confirma que el estado de la PR es **Merged**. Tener habilitado el permiso de fusión o un agente en ejecución no confirma que la PR se haya fusionado.

> [!IMPORTANT]
> Agent Merge no omite las protecciones del repositorio ni los permisos que falten. Resuelve esos bloqueos antes de continuar.

## Resumen y siguientes pasos

Has automatizado varias partes del proceso de desarrollo: la generación del código, las pruebas y la validación, y ahora el proceso de la solicitud de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- has inspeccionado la PR completa de la función y las pruebas de validación.
- has autorizado Agent Merge después de la revisión y confirmado que la PR se ha fusionado.

A continuación, [usarás un canvas existente y crearás otro para clasificar tareas][next-lesson], y explorarás una forma más completa de inspeccionar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Administrar incidencias y solicitudes de cambios con la aplicación GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
