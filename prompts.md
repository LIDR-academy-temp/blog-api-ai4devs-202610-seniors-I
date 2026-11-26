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

Borra el ejemplo de abajo cuando escribas el primero.

---

## Prompt 1

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea en los repositorios blog-api y blog-ai un CLAUDE.md en la raíz con una sola
regla propia del repositorio, sin cambiar nada más.
blog-api: es el respositorio dueño del contenido y todo archivo nuevo debe empezar
con un comentario que lo indique.
blog-ai: los nombres de los campos del contrato público deben escribirse en
español, nunca en inglés.
```

**Qué salió:** Funcionó a la primera y creó los dos CLAUDE.md con una sola línea. Además aplicó la regla padre que vive en la raíz dónde se encuentran clonados los tres repositorios.


## Prompt 2

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Crea un hook que se ejecute al escribir o editar un archivo mediante PostToolUse
para las herramientas Write y Edit. Tiene que añadir una línea
MARCADORES-<nombre-del-repo>.txt en la raíz de su propio repositorio, con la
fecha, la herramienta utilizada y la ruta del archivo modificado. Utiliza rutas
absoluta, ya que el hook tendrá que registrar cambios en archivos situados fuera
de este repositorio.
```

**Qué salió:** Ha creado a la primera el hook `.claude/hooks/marcadores.sh` y `.claude/settings.json`, y lo ha ejecutado para probar que funciona correctamente tanto en `blog-api` como en `blog-ai`. No ha tocado nada de `blog-ai`.


## Prompt 3

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
Finalmente crea una skill llamada marcador-<nombre-del-repo> cuya descripción
indique a qué repositorio pertenece.
```

**Qué salió:** Ha creado una skill en ambos proyectos que lee y resume los marcadores que el hook PostToolUse escribe.


## Prompt 4

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
En el archivo `../blog-ai/app/esquemas.py`, añade a la clase `ResultadoBusqueda`
un campo que indique cuántos fragmentos del artículo han coincidido con la
búsqueda. Modifica únicamente este archivo y utiliza la herramienta de edición de
archivos, no utilices un script.
```

**Qué salió:** Ha modificado el archivo y además ha generado un marcador que indica que se ha editado el archivo `esquemas.py`.


## Prompt 5

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
¿Qué archivos CLAUDE.md se cargaron al inicio de la sesión? Cita la regla de cada uno
```

**Qué salió:** Se cargaron los archivos de `blog/claude.md` y de `blog/blog-api/claude.md`, y me ha citado la regla padre de cada uno. No se ha cargado en ningún momento `blog/blog-ai/claude.md`.


## Prompt 6

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
¿Qué skills tienes disponibles?
```

**Qué salió:** Tiene las skills de `marcador-blog-api` y `marcador-blog-ai` aunque no haya cargado el CLAUDE.md del proyecto de AI. Además, tiene disponibles un listado de skills que son comunes a todos los proyectos (code-review, simplify, security-review...).


## Prompt 7

**Modelo:** Opus 5.5
**Herramienta:** Claude Code

```
¿Qué nombre le has dado al campo y porqué?
```

**Qué salió:** 

```
Lo llamé fragmentos_coincidentes, por estas razones:

- Sigue las convenciones del archivo. Los campos de esquemas.py van en español, sin
  tildes y en snake_case: fragmentos_indexados, posts_indexados, motivos_omision.
  Además, ya se usa fragmentos para hablar de un número de fragmentos:
  RespuestaIndexar.fragmentos y RespuestaSalud.fragmentos_indexados. El nombre nuevo
  sigue ese patrón.
- Sale de tu propia descripción. Pediste un campo que indique cuántos fragmentos
  «han coincidido» con la búsqueda, y el adjetivo es «coincidentes».
- No se confunde con fragmento. ResultadoBusqueda ya tiene fragmento, que es el
  texto del mejor fragmento. Con un nombre como fragmentos a secas, alguien podría
  pensar que es una lista de textos y no un número.

Una alternativa más explícita sería num_fragmentos_coincidentes. La descarté porque
ningún campo del contrato usa el prefijo num_: indexados y omitidos también son
números y no lo llevan.

Como es parte del contrato que consume blog-api, cambiarle el nombre ahora sale
barato, porque aún nadie lo usa. Más adelante sería romper el contrato. Si prefieres
otro nombre, mejor cambiarlo ya.

REGLA-PADRE aplicada: gobierno desde fuera de todos los repositorios.
```