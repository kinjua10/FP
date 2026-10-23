# Reglas del proyecto (siempre aplican)

> Este archivo lo lee Claude Code automáticamente en cada sesión. Acá va solo lo que aplica
> **siempre**, en todo el repo. Lo que aplica en un contexto puntual va en `.claude/rules/`.
> Reemplazá los ejemplos por las convenciones reales de tu proyecto, pero mantené la
> separación de las tres carpetas: es la base de todo el modelo.

## 1. Enrutamiento de archivos (Raw, Wiki, Output)

1. **Insumos (`Raw/`):**
   - Leer todo el código, capturas o notas que lleguen de afuera desde `Raw/capturas/`,
     `Raw/scripts_originales/` y `Raw/notas_rapidas/`.
   - Considerar estos archivos como fuentes originales que **no deben modificarse,
     renombrarse ni borrarse**. Si hace falta corregir o transformar algo de `Raw/`, el
     resultado va a `Output/`.
   - Ver `Raw/README.md` para convenciones de nombres y tamaño de archivos.

2. **Conocimiento (`Wiki/`):**
   - Empezar siempre por `Wiki/README.md` — es el índice de toda la documentación.
   - Consultar y actualizar ahí las reglas de negocio/dominio, modelos, glosario y
     documentación técnica del proyecto.
   - Si un documento describe modelo/estructura/relaciones y se modifica, revisar si hay
     que sincronizar también otros documentos relacionados (catálogo, diccionario, diagramas).
   - Todo documento nuevo en `Wiki/` se agrega a la tabla que corresponda en
     `Wiki/README.md` en el mismo cambio.

3. **Resultados (`Output/`):**
   - Guardar ahí todo entregable final: scripts optimizados, informes, diagramas.
   - Registrar cada cambio aplicado en `Output/refactoring_log.md` — es la bitácora
     granular de qué se hizo, por qué y qué se descartó.

## 2. Cuándo se actualiza `Wiki/` (quién decide)

Al procesar un insumo de `Raw/` o al generar algo en `Output/`, preguntarse:
**¿esto cambia algo que alguien necesite saber la próxima vez?** (una regla de negocio, una
decisión, una estructura del modelo, un término nuevo, el estado de una iniciativa).

- **Si la respuesta es sí:** proponer el cambio en `Wiki/` dentro del **mismo** PR que el
  resultado en `Output/`, no en uno aparte "para después".
- **Si hay dudas sobre si el insumo es correcto o vigente:** no dar el cambio por hecho.
  Redactarlo marcando con `⚠️ confirmar` lo que no se pueda verificar y dejarlo explícito
  en la descripción del PR.
- **La decisión final es de quien revisa el PR.** El asistente propone; la persona aprueba.
  Por eso la descripción del PR siempre incluye una sección "Cambios en Wiki/" (o "Sin
  cambios en Wiki/" con el motivo).

## 3. Git

- Nunca commitear ni pushear directo a la rama principal (`main`/`master`): siempre rama +
  Pull Request (ver `/ship`).
- Mensajes de commit en formato Conventional Commits (`feat(wiki): ...`, `fix(output): ...`).
- No commitear archivos de más de 10 MB sin confirmación (ver `Raw/README.md`).

## 4. Comandos disponibles

| Comando | Para qué |
| :--- | :--- |
| `/ship` | Rama + commit + PR documentado. |
| `/cierre-diario` | Nota del día en `Wiki/Cierres_Diarios/`. |
| `/actualizar-modelo` | Chequea que `Wiki/` refleje los cambios recientes. |
