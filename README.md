# Modelo actual con Luna

Skill para Codex que reserva el modelo principal para decisiones de arquitectura, programación y revisión final, y delega exploración, comandos, pruebas y documentación a GPT-6 Luna con razonamiento `max`.

La estrategia busca reducir el uso del modelo principal sin perder la revisión e integración centralizadas. El ahorro depende de la tarea y de las herramientas disponibles; no garantiza menos tokens totales ni menor facturación.

## Requisitos

- Codex con soporte para skills y subagentes.
- La herramienta de subagentes debe aceptar explícitamente `gpt-6-luna` y `reasoning_effort: max`.
- Si el modelo o el esfuerzo no se pueden verificar, la skill indica comunicar esa limitación en vez de afirmar que se usó `max`.

## Instalar

Clona este repositorio y copia la carpeta de la skill a tu directorio de skills de usuario:

```bash
git clone https://github.com/julioarias0264-hub/modelo-actual-con-luna.git
mkdir -p ~/.codex/skills
cp -R modelo-actual-con-luna/skills/modelo-actual-con-luna ~/.codex/skills/
```

Después, inicia una conversación nueva en Codex para que descubra la skill. Para actualizarla, vuelve a copiar la carpeta desde el repositorio.

Consulta la [guía oficial para crear skills](https://developers.openai.com/codex/skills) para conocer el formato y las opciones actuales.

## Contenido

- `skills/modelo-actual-con-luna/SKILL.md`: instrucciones completas de la skill.

## Licencia

Este repositorio todavía no incluye una licencia. Añadir un archivo `LICENSE` permitirá especificar claramente cómo otras personas pueden reutilizar y distribuir el contenido.
