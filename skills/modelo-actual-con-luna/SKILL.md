---
name: modelo-actual-con-luna
description: Reducir el consumo del modelo principal durante desarrollo de software reservándolo para programar y revisar, y delegando lectura, exploración, comandos, pruebas y documentación a GPT-6 Luna con razonamiento máximo. Usar cuando se solicite este reparto de trabajo o ahorrar uso del modelo principal mediante subagentes.
---

# Modelo actual con Luna

## Objetivo

Ahorrar tanto uso del modelo principal como sea posible sin comprometer la corrección y calidad del trabajo. Reservar el modelo seleccionado por el usuario para programar, decidir la arquitectura, resolver problemas y revisar e integrar cambios. Encargar a el modelo de la familia luna mas nuevo en este caso GPT-6 Luna con razonamiento máximo la recopilación de información y las tareas operativas: leer y explorar archivos, buscar referencias, inspeccionar logs, ejecutar comandos y pruebas, usar Playwright y preparar documentación.

Luna debe entregar evidencia resumida y accionable para que el principal pueda decidir y escribir código sin cargar archivos completos ni repetir la exploración. El ahorro buscado es principalmente el uso del modelo principal; no prometer menos tokens totales ni ahorro facturado garantizado. Mantener Luna en `max` por elección expresa del usuario.

## Preferencia de modelos

- Realizar programación, decisiones de arquitectura, revisión e integración final en el agente principal, conservando el modelo y razonamiento seleccionados por el usuario. GPT-6.1 Sol en Light es un ejemplo, no un modelo obligatorio. No cambiar la configuración del modelo principal.
- Para subagentes de lectura, exploración, comandos, pruebas, Playwright y documentación, usar explícitamente `model: "gpt-6-luna"` y `reasoning_effort: "max"`. No sustituir `max` por otro esfuerzo ni heredar el modelo del principal.
- La invocación de esta skill autoriza delegación de esas tareas auxiliares dentro del alcance del encargo. Una instrucción posterior del usuario prevalece sobre esta preferencia.

## Coordinación

### Verificar modelo y esfuerzo efectivos

Al crear un subagente, enviar explícitamente `model: "gpt-6-luna"` y `reasoning_effort: "max"` en los parámetros de la herramienta, no únicamente en el mensaje. No asumir que el selector visual, la preferencia de la skill o la confirmación del propio agente demuestran la configuración efectiva.

Antes de asignar trabajo sustancial, iniciar el agente con una instrucción breve de esperar la tarea y comprobar la configuración efectiva mediante los metadatos de ejecución disponibles. Leer sólo modelo y esfuerzo; no volcar conversaciones ni datos privados. Si existen registros locales de Codex, contrastar `turn_context.model`, `turn_context.effort` y `collaboration_mode.settings.reasoning_effort` del agente correspondiente. Una etiqueta del selector que contradiga los metadatos debe reportarse como discrepancia, sin atribuirle una causa no comprobada.

Si la ejecución indica un esfuerzo distinto de `max`, detener ese agente y recrearlo una sola vez con los parámetros explícitos. Si persiste o no es posible verificarlo, informar la limitación antes de delegar trabajo sustancial; no presentar `max` como confirmado. No modificar registros de sesión ni configuración global para aparentar el esfuerzo solicitado. Reutilizar únicamente agentes cuya configuración coincida con esta preferencia.

Asignar tareas concretas con contexto suficiente: objetivo, archivos relevantes, criterios de aceptación, comandos de prueba y resultado esperado. Evitar copiar toda la conversación si un resumen basta.

Delegar la exploración y ejecución operativa que el encargo requiera a agentes Luna, reutilizando agentes con contexto relevante en lugar de crear uno por archivo o comando. Paralelizar tareas independientes cuando produzcan resultados útiles. Asignar archivos distintos a cada agente que escriba y evitar duplicar su trabajo en el principal.

El principal puede leer fragmentos necesarios para editar o revisar con precisión, ejecutar la edición y resolver directamente un bloqueo inmediato cuando delegarlo sólo añada espera o trabajo duplicado. Esta excepción no debe convertirse en una segunda exploración completa. Respetar los requisitos de coordinación de la herramienta de subagentes disponible.

Solicitar a Luna informes breves con rutas y líneas relevantes, hechos comprobados, resultados de comandos, fallos y preguntas pendientes. Evitar volcados de logs, archivos enteros o la conversación completa; ampliar el contexto únicamente cuando un hallazgo lo requiera. Los comandos deben mantenerse dentro de la autorización del encargo.

Los agentes de pruebas pueden escribir pruebas y ejecutar verificaciones apropiadas; deben informar comandos, resultados, fallos y limitaciones. Los agentes de documentación deben basarse en el código y comportamiento comprobados, indicando lo no verificado. Los cambios al código del producto y la resolución de fallos corresponden al agente principal.

Revisar las contribuciones antes de integrarlas. No declarar una prueba aprobada si no se ejecutó. Cerrar los subagentes cuando terminen y reportar los resultados importantes al usuario.

## Disponibilidad y consumo

Comprobar que la herramienta de subagentes admite el modelo y esfuerzo solicitados. Si no están disponibles, comunicar la limitación sin cambiar silenciosamente de modelo ni lanzar procesos CLI como sustitución automática. Continuar el trabajo independiente en el agente principal.

Esta skill configura la preferencia de delegación; no modifica el selector de modelos ni garantiza una reducción del total de tokens o del uso facturado. Evitar reintentos repetidos y delegaciones redundantes.
