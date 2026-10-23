---
paths:
  - "Output/sql_optimizado/**"
  - "Raw/scripts_originales/**"
---

# Ejemplo de regla de dominio (borrar/reemplazar)

**Se aplica cuando:** se genera o revisa código en `Output/sql_optimizado/` o se analiza un
script de `Raw/scripts_originales/`. *(Reemplazá esto por el disparador real.)*

## Cómo carga Claude Code este archivo

- Claude Code lee automáticamente todos los `.md` de `.claude/rules/`.
- Un archivo **sin** el bloque `paths:` de arriba se carga siempre, igual que `CLAUDE.md`.
- Un archivo **con** `paths:` se carga solo cuando el asistente trabaja con archivos que
  coinciden con esos patrones. Así una regla de SQL no ocupa contexto mientras se edita
  `Wiki/`.
- La línea "Se aplica cuando" no controla la carga: está para que una persona entienda
  rápido para qué sirve la regla. Mantené las dos cosas coherentes.

## Qué poner en una regla real

- Estándares de código obligatorios (encabezados, manejo de errores, convenciones de
  nombres).
- Reglas de negocio o de cumplimiento normativo específicas del dominio.
- Checklist de validación antes de considerar algo terminado.

### Ejemplo concreto (reemplazar)

```sql
-- Todo script en Output/sql_optimizado/ empieza con este encabezado:
-- Autor:        <nombre>
-- Fecha:        AAAA-MM-DD
-- Origen:       Raw/scripts_originales/<archivo_original>.sql
-- Motivo:       <qué se optimizó y por qué>
-- Ver también:  Output/refactoring_log.md#AAAA-MM-DD
```

- [ ] El script original en `Raw/` quedó intacto.
- [ ] Hay una entrada nueva en `Output/refactoring_log.md`.
- [ ] Si cambió una tabla o relación, se actualizó el documento de modelo en `Wiki/`.

## Cómo escribir una regla nueva

1. **Un archivo por tema** (no todo junto en uno solo), con prefijo numérico para ordenarlos
   (`10-sql.md`, `20-documentacion.md`).
2. **`paths:` lo más acotado posible.** Si la regla aplica siempre, va en `CLAUDE.md`, no acá.
3. **Primera línea del cuerpo: cuándo se aplica.** Si no es obvio para quien lee el archivo
   por primera vez, tampoco lo es para el asistente.
4. **Ejemplos concretos** (bloques de código, nombres reales de archivos/tablas) antes que
   descripciones abstractas.
