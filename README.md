# Plantilla: modelo de trabajo con GitHub + Claude Code + Obsidian

Esta carpeta es el punto de partida para replicar un flujo de trabajo que combina:

- **GitHub** — control de versiones y Pull Requests de todo lo que se produce.
- **Claude Code** — asistente que lee las reglas de `.claude/` y las sigue al generar o
  modificar contenido en este repo.
- **Obsidian** — se abre directamente sobre esta misma carpeta para navegar `Wiki/` como
  una base de conocimiento con links `[[...]]` y backlinks.

No depende de ningún dominio en particular (no es específico de farma, de un stack de datos,
ni de ningún lenguaje): es la estructura de carpetas y las reglas de "qué va dónde" y
"cómo se escribe". Adaptá el contenido de `.claude/rules/` y los comandos a tu propio dominio.

## La idea central: separar insumos, conocimiento y resultados

| Carpeta | Qué va ahí | Regla |
| :--- | :--- | :--- |
| **`Raw/`** | Todo lo que llega de afuera: capturas de pantalla, scripts originales de terceros, notas sueltas, PDFs, exports. | Es **solo lectura** para el asistente: se lee, nunca se modifica ni se sobrescribe directamente. Si hay que corregir algo que está en `Raw/`, el resultado corregido va a `Output/`, no se edita el original. |
| **`Wiki/`** | Documentación viva: reglas de negocio/dominio, modelos, glosario, decisiones, estado de iniciativas en curso, notas de cierre diario. | Se consulta **y** se actualiza constantemente. Es la memoria de largo plazo del proyecto — si algo importante no está en `Wiki/`, para el asistente (y para un compañero nuevo) no existió. |
| **`Output/`** | Todo lo que el asistente genera como entregable: scripts optimizados, informes, diagramas, logs de cambios. | Es el único lugar donde el asistente "escribe resultados finales". Nunca se mezcla con `Raw/`. |

Esta separación es la regla más importante de todo el modelo. Sin ella, un asistente (o una
persona nueva en el equipo) no puede distinguir "esto es un insumo que me pasaron" de "esto
es algo que ya procesamos y es la versión buena".

## Cómo se conecta cada pieza

### 1. GitHub
- Cada tarea termina en una rama (`feat/...`, `fix/...`) y un Pull Request, no en commits
  directos a la rama principal.
- El historial de Pull Requests **es** la bitácora de qué cambió y por qué — por eso el
  mensaje de cada PR describe el motivo, no solo el "qué".
- `Wiki/` y `Output/` se versionan junto con el código: la documentación no vive aparte en un
  wiki externo que se desincroniza.

### 2. Claude Code (`.claude/`)
Carpeta leída automáticamente por Claude Code al abrir el proyecto. Tres piezas:

- **`CLAUDE.md`** — las reglas de enrutamiento de archivos (la tabla de arriba) y cualquier
  convención que aplique siempre, sin excepción, en todo el repo.
- **`rules/*.md`** — reglas que solo aplican en ciertos contextos (ej. "cuando generes SQL",
  "cuando documentes un flujo ETL"). Claude Code carga todos los archivos de esta carpeta;
  para que una regla aplique solo a ciertos archivos se le agrega un encabezado `paths:`
  con los patrones (ver el ejemplo). La primera línea del cuerpo explica en palabras cuándo
  se aplica, para quien la lee.
- **`commands/*.md`** — comandos reusables (`/ship`, `/cierre-diario`, `/actualizar-modelo`)
  que describen un flujo de pasos concretos para una tarea que se repite seguido. El
  encabezado `description:` es lo que se ve en el menú de `/`. Convierten un procedimiento
  que antes había que explicar cada vez en una sola palabra.

#### Quién decide qué entra en `Wiki/`
El asistente **propone** cambios en `Wiki/` dentro del mismo PR que el resultado en
`Output/`, y marca con `⚠️ confirmar` lo que no pudo verificar. **Quien revisa el PR
decide.** Cada PR tiene una sección "Cambios en Wiki/" (ver `/ship`), así esa revisión no
se saltea.

Ver los ejemplos en `rules/00-ejemplo-dominio.md` y `commands/` de esta plantilla — están
pensados para borrarse/reemplazarse por los del dominio real, pero muestran la forma.

### 3. Obsidian
- Se abre esta misma carpeta (la raíz del repo) como *vault* de Obsidian.
- `Wiki/` se navega con links `[[nombre_de_archivo]]` y backlinks — por eso conviene que los
  nombres de archivo sean descriptivos y estables (si lo renombrás, actualizá los links).
- Un archivo índice (`Wiki/README.md`) es el punto de entrada: cualquier documento nuevo se
  agrega a la tabla que corresponda ahí, para que nada quede "huérfano" y sin encontrar.
- Tableros con el plugin Dataview (ya incluido en `.obsidian/`): `Wiki/Tablero_Iniciativas.md`
  lista automáticamente el estado de cada documento de `Wiki/Iniciativas/` a partir de su
  encabezado (ver `_plantilla_iniciativa.md`).
- `.obsidian/` se versiona para compartir plugins, pero `workspace.json` queda fuera vía
  `.gitignore` porque cambia cada vez que alguien abre el vault.

### 4. Archivos pesados y datos sensibles
- Hasta 10 MB se commitea normal; más grande, Git LFS o link externo (detalle en
  `Raw/README.md`).
- Nunca credenciales, `.env` ni datos personales sin anonimizar.

## Qué copiar al nuevo proyecto

1. La estructura de carpetas (`Raw/`, `Wiki/`, `Output/`, `.claude/`, `.obsidian/`) y el
   `.gitignore`.
2. `CLAUDE.md` tal cual (la regla de enrutamiento es independiente del dominio).
3. `Wiki/README.md` como plantilla de índice — vaciar las tablas y dejar las categorías como
   punto de partida.
4. Los comandos de `.claude/commands/` que tengan sentido para el nuevo dominio — reescribir
   el "Flujo de Ejecución" de cada uno con los pasos reales.
5. Reemplazar `rules/00-ejemplo-dominio.md` por las reglas específicas del dominio nuevo
   (ej. estándares de código, reglas de negocio, validaciones obligatorias).

## Qué NO copiar

- Contenido específico de datos/negocio de este proyecto (eso queda en el repo original).
- Memorias de Claude Code (son locales a cada máquina/usuario, no viven en el repo).
