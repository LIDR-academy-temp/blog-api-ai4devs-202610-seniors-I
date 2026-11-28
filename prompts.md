# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

---

> **Nota de transparencia.** No escribí estos prompts a mano. Le pedí a una sesión de Claude Code (Opus 5.5), abierta en `blog/`, que hiciera el ejercicio por mí; mi petición fue «hzlo tu». Esa sesión escribió los prompts de abajo y los lanzó con `claude -p` (modo no interactivo) desde `blog-api`. Cada prompt va tal cual se envió.

## Prompt 0: mi petición a la sesión que orquestó el ejercicio

**Modelo:** Claude Opus 5.5 (`claude-opus-5-5`)
**Herramienta:** Claude Code 2.1.332, sesión abierta en `blog/`

```
hzlo tu
```

**Qué salió:** la sesión creó `blog/CLAUDE.md` con el `cat` del enunciado y lanzó los prompts 1 a 4.

## Prompt 1: paso 2, crear las tres piezas en ambos repositorios

**Modelo:** Claude Opus 5.5 (`claude-opus-5-5`)
**Herramienta:** Claude Code 2.1.332, `claude -p` desde `blog-api` con `--add-dir ../blog-ai`, permitiendo solo Read/Write/Edit/Glob y `mkdir`/`ls`

```
Crea estas tres piezas en este repositorio (blog-api) y en ../blog-ai, sin cambiar nada más:

1. Un CLAUDE.md en la raíz de cada repositorio con una sola regla propia:
   - blog-api: "Este repositorio es el dueño del contenido. Todo archivo nuevo debe empezar con un comentario que lo indique."
   - blog-ai: "Los nombres de los campos del contrato público se escriben en español, nunca en inglés."

2. Un hook en .claude/settings.json de cada repositorio, de tipo PostToolUse con matcher "Write|Edit". Debe añadir una línea a MARCADORES-<nombre-del-repo>.txt en la raíz de SU propio repositorio (MARCADORES-blog-api.txt en blog-api, MARCADORES-blog-ai.txt en blog-ai) con la fecha, la herramienta usada y la ruta del archivo modificado (sácalas del JSON que recibe el hook por stdin). Usa rutas absolutas para el archivo de marcadores: /Users/carlosramostorres/Proyects/blog/blog-api/MARCADORES-blog-api.txt y /Users/carlosramostorres/Proyects/blog/blog-ai/MARCADORES-blog-ai.txt, porque el hook tendrá que registrar cambios en archivos que están fuera de su repositorio.

3. Una skill sencilla en .claude/skills/marcador-<nombre-del-repo>/SKILL.md de cada repositorio, llamada marcador-blog-api y marcador-blog-ai, cuya descripción indique a qué repositorio pertenece.

Al terminar, lista los archivos que has creado.
```

**Qué salió:** a medias. Creó los dos `CLAUDE.md`, pero en modo no interactivo se le denegó la escritura en `.claude/`, así que no guardó ni hooks ni skills (sí los dejó redactados en su respuesta). La regla REGLA-PADRE ya se aplicó en esta respuesta.

## Prompt 2: retomar la sesión anterior para guardar `.claude/` (no llegó a ejecutarse)

**Modelo:** Claude Opus 5.5 (`claude-opus-5-5`)
**Herramienta:** Claude Code 2.1.332, `claude -p --resume` con `--permission-mode bypassPermissions`

```
Tienes permiso para escribir en .claude/ de ambos repositorios. Guarda los cuatro archivos que tenías preparados (los dos settings.json con el hook y las dos SKILL.md) y prueba el comando del hook con un JSON de ejemplo sin dejar líneas de prueba en los archivos MARCADORES. No cambies nada más.
```

**Qué salió:** el clasificador de permisos de la sesión que orquestaba bloqueó el comando antes de lanzarlo, por usar `bypassPermissions`. Esa sesión guardó los cuatro archivos (`.claude/settings.json` y `.claude/skills/marcador-*/SKILL.md` de cada repositorio) con su propia herramienta Write, copiando literalmente lo que había redactado la sesión del prompt 1. Después probó los dos hooks con un JSON de ejemplo, escribiendo en archivos temporales.

## Prompt 3: paso 4, el encargo en el repositorio añadido

**Modelo:** Claude Opus 5.5 (`claude-opus-5-5`)
**Herramienta:** Claude Code 2.1.332, sesión **nueva** con `claude -p` desde `blog-api` y `--add-dir ../blog-ai`, permitiendo solo Read/Edit/Glob/Grep y prohibiendo Bash y Write

```
Añade a la clase ResultadoBusqueda, en ../blog-ai/app/esquemas.py, un campo que indique cuántos fragmentos del artículo han coincidido con la búsqueda. Modifica solo ese archivo y usa la herramienta de edición de archivos (Edit), nunca un script ni un comando de shell.
```

**Qué salió:** a la primera. Añadió `fragmentos_coincidentes: int = Field(default=1, ge=1)` usando solo Edit. Avisó de que la consulta en `indice.py` (`DISTINCT ON`) no lo rellena todavía y de que habría que regenerar `contrato/openapi.json`.

## Prompt 4: paso 4, las tres preguntas (misma sesión, `--resume`)

**Modelo:** Claude Opus 5.5 (`claude-opus-5-5`)
**Herramienta:** Claude Code 2.1.332, `claude -p --resume` desde `blog-api` con `--add-dir ../blog-ai`, solo lectura

```
Ahora responde por separado a estas tres preguntas:
1. Qué archivos CLAUDE.md se cargaron al iniciar la sesión, citando la regla de cada uno.
2. Qué skills tienes disponibles.
3. Qué nombre has dado al campo y por qué.
```

**Qué salió:** dijo que se cargaron `blog/CLAUDE.md` y `blog-api/CLAUDE.md`, y que `blog-ai/CLAUDE.md` no, aunque lo leyó por su cuenta. Listó las skills `marcador-blog-api` y `marcador-blog-ai`. Justificó `fragmentos_coincidentes` por la regla de blog-ai. Al comprobarlo, `MARCADORES-blog-api.txt` registraba la edición de `blog-ai/app/esquemas.py` y `MARCADORES-blog-ai.txt` no existía.
