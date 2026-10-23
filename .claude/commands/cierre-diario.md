---
description: Escribe la nota de cierre del día en Wiki/Cierres_Diarios/ (qué se hizo, qué queda).
---

# Comando: /cierre-diario

## Objetivo
Dejar una nota corta en `Wiki/Cierres_Diarios/AAAA-MM-DD.md` con qué se hizo hoy y qué queda
pendiente, para que la próxima sesión (propia o de otra persona) pueda retomar sin tener que
reconstruir el contexto desde cero.

Notas adicionales del usuario (opcional): $ARGUMENTS

## Flujo
1. Revisar `git log --since=midnight`, `git diff` y la conversación para listar qué se tocó.
2. Copiar la estructura de `Wiki/Cierres_Diarios/_plantilla.md` y completar en
   `Wiki/Cierres_Diarios/AAAA-MM-DD.md` (fecha de hoy):
   - Qué se hizo (3-6 bullets, con links `[[...]]` a los archivos tocados).
   - Qué quedó pendiente o bloqueado, y por qué.
   - Decisiones tomadas que no sean obvias leyendo solo el código.
   - Por dónde arrancar mañana.
3. Si ya existe la nota del día, agregar al final en vez de sobrescribir.
4. Si alguna decisión debería vivir en un documento permanente de `Wiki/` (no solo en el
   cierre), señalarlo y ofrecer actualizarlo.
