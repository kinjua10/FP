---
description: Crea rama, commit y Pull Request documentado con los cambios actuales.
---

# Comando: /ship

## Objetivo
Publicar los cambios probados en GitHub abriendo una rama y un Pull Request documentado.

Contexto adicional del usuario (opcional): $ARGUMENTS

## Chequeos previos (si alguno falla, frenar y avisar)
1. **Rama actual:** si es `main`/`master`, crear la rama nueva antes de commitear. Nunca
   pushear directo a la rama principal.
2. **`Raw/` intacto:** revisar `git status` / `git diff --stat`. Si aparece algún archivo
   de `Raw/` *modificado o borrado* (no agregado), frenar: los originales no se tocan.
3. **Archivos pesados:** si algún archivo nuevo pesa más de 10 MB, listarlo y preguntar si
   va con Git LFS, se excluye o se sube igual.
4. **Wiki/ e índice:** si hay `.md` nuevos en `Wiki/`, verificar que estén linkeados en
   `Wiki/README.md`. Si no, ofrecer agregarlos antes de seguir.
5. **Nada sensible:** no incluir `.env`, credenciales ni exports con datos personales.

## Flujo
1. Crear una rama semántica (ej. `feat/nombre-corto`, `fix/nombre-corto`, `docs/nombre-corto`).
2. Commit en formato Conventional Commits (ej. `feat(wiki): agrega glosario de X`).
3. **Mostrar el resumen (rama, archivos, mensaje de commit, borrador del PR) y pedir
   confirmación** antes de pushear.
4. Subir la rama al remoto.
5. Abrir el Pull Request (CLI `gh` o el servidor MCP de GitHub que corresponda) con esta
   descripción:

   ```markdown
   ## Qué cambia
   <resumen en 2-4 bullets>

   ## Por qué
   <motivo; no solo el "qué">

   ## Cambios en Wiki/
   <documentos actualizados, o "Sin cambios en Wiki/ porque ...">
   <listar cualquier "⚠️ confirmar" pendiente para quien revisa>

   ## Bitácora
   <entrada relevante de Output/refactoring_log.md, si existe>
   ```
6. Devolver el link del PR.
