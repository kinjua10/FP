# Tablero de iniciativas

> Requiere el plugin **Dataview** en Obsidian (ya viene en `.obsidian/`). Lee el encabezado
> de cada archivo en `Wiki/Iniciativas/` (ver `_plantilla_iniciativa.md`). En GitHub se ve
> el código de la consulta, no la tabla: es normal.

## En curso y bloqueadas

```dataview
TABLE estado, responsable, actualizado
FROM "Wiki/Iniciativas"
WHERE tipo = "iniciativa" AND (estado = "en-curso" OR estado = "bloqueada")
  AND !startswith(file.name, "_")
SORT actualizado ASC
```

## Propuestas

```dataview
TABLE responsable, inicio
FROM "Wiki/Iniciativas"
WHERE tipo = "iniciativa" AND estado = "propuesta" AND !startswith(file.name, "_")
SORT inicio DESC
```

## Terminadas

```dataview
TABLE responsable, actualizado AS "cerrada"
FROM "Wiki/Iniciativas"
WHERE tipo = "iniciativa" AND estado = "terminada" AND !startswith(file.name, "_")
SORT actualizado DESC
```

## Últimos cierres diarios

```dataview
LIST
FROM "Wiki/Cierres_Diarios"
WHERE !startswith(file.name, "_")
SORT file.name DESC
LIMIT 7
```
