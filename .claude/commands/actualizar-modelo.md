---
description: Verifica que Wiki/ refleje los cambios recientes y que el índice esté al día; propone borradores.
---

# Comando: /actualizar-modelo

## Objetivo
Detectar si un cambio reciente (nueva tabla, endpoint, módulo, proceso, etc. — adaptar a tu
dominio) ya quedó reflejado en los documentos de `Wiki/` que describen el modelo del
proyecto, y si falta, señalarlo o redactar un borrador en vez de depender de acordarse solo.

También chequea, como paso aparte, que `Wiki/README.md` no haya quedado desactualizado
respecto a los archivos `.md` que realmente existen en `Wiki/`.

Alcance adicional indicado por el usuario (opcional): $ARGUMENTS

## Flujo de Ejecución

0. **Chequeo del índice de Wiki:**
   - Listar los archivos reales en `Wiki/*.md` y `Wiki/**/*.md` (excluir
     `Cierres_Diarios/` y archivos que empiezan con `_`, que son plantillas).
   - Compararlos contra los links que ya aparecen en `Wiki/README.md`.
   - Señalar cualquier `.md` nuevo que no esté linkeado en ninguna tabla del índice, y
     cualquier link del índice que apunte a un archivo que ya no existe.

1. **Detectar cambios relevantes en el diff** (`git status`/`git diff`) sobre `Output/` y
   `Raw/` — ajustar qué patrones buscar según el dominio real (ej. `CREATE TABLE`, un nuevo
   endpoint, un nuevo componente).

2. **Cruzar cada cambio contra los documentos de modelo** que correspondan en `Wiki/` (ej.
   diccionario de datos, catálogo de objetos, diagrama de relaciones/arquitectura).

3. **Clasificar cada elemento:** 🟢 Sincronizado / 🟡 Parcial / 🔴 Falta.

4. **Para cada 🟡/🔴, redactar un borrador** de la sección faltante, marcando con
   `⚠️ confirmar` cualquier campo que no se pueda inferir solo del cambio y necesite
   confirmación humana.

5. **No escribir los archivos todavía.** Mostrar el resumen clasificado y preguntar si se
   aplican los borradores ahora o se deja constancia para después.

6. **Si se confirma aplicar:** editar los documentos con `Edit` (no reescribir archivos
   enteros) y cerrar con un resumen de qué quedó sincronizado y qué sigue con
   `⚠️ confirmar` pendiente. Esos pendientes van en la sección "Cambios en Wiki/" del PR.
