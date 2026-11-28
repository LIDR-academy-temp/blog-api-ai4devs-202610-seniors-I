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

## Prompt 1

**Modelo:** Opus 4.8
**Herramienta:** Claude Code

```
Estamos preparando el ejercicio del Módulo 7 de AI4DEVS.

Sin modificar ningún archivo, confirma desde qué directorio estás trabajando, resume brevemente la función de este repositorio e identifica si existen:

1. Un archivo CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas del agente.
3. Skills propias del proyecto.

No crees archivos, no implementes cambios ni inicies todavía la práctica.
```

## Prompt 2

**Modelo:** Opus 4.8
**Herramienta:** Claude Code

```
Estamos preparando el ejercicio del Módulo 7 de AI4DEVS.

Sin modificar ningún archivo, confirma el directorio de trabajo y la rama actual. Identifica si este repositorio contiene:

1. Un archivo CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas del agente.
3. Skills propias del proyecto.

Distingue las instrucciones y herramientas globales de las que pertenecen a este repositorio.

No crees archivos ni implementes cambios. Responde brevemente.
```

## Prompt 3

**Modelo:** Opus 4.8
**Herramienta:** Claude Code

```
Prepara prompts.md para el ejercicio del Módulo 7.

Sustituye el ejemplo de la plantilla y registra literalmente los dos prompts de exploración que utilicé antes de comenzar la práctica, con modelo y herramienta.

Prompt 1:
Estamos preparando el ejercicio del Módulo 7 de AI4DEVS.

Sin modificar ningún archivo, confirma desde qué directorio estás trabajando, resume brevemente la función de este repositorio e identifica si existen:

1. Un archivo CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas del agente.
3. Skills propias del proyecto.

No crees archivos, no implementes cambios ni inicies todavía la práctica.

Prompt 2:
Estamos preparando el ejercicio del Módulo 7 de AI4DEVS.

Sin modificar ningún archivo, confirma el directorio de trabajo y la rama actual. Identifica si este repositorio contiene:

1. Un archivo CLAUDE.md o AGENTS.md.
2. Hooks o comprobaciones automáticas del agente.
3. Skills propias del proyecto.

Distingue las instrucciones y herramientas globales de las que pertenecen a este repositorio.

No crees archivos ni implementes cambios. Responde brevemente.

Registra también este prompt de preparación como Prompt 3, conservando su texto literal desde la conversación si está disponible. Si no lo está, indícalo y no lo reconstruyas.

No modifiques archivos distintos de prompts.md. No hagas commit ni inicies la práctica todavía.
```

## Prompt 4

**Modelo:** Opus 4.8
**Herramienta:** Claude Code

```
Estamos realizando el ejercicio Blog Polirepo del Módulo 7 de AI4DEVS.

Trabaja sobre blog-api y ../blog-ai. Prepara estas tres piezas en cada repositorio:

1. CLAUDE.md en la raíz, con una sola regla propia:
- blog-api: este repositorio es dueño del contenido y todo archivo nuevo debe comenzar con un comentario que lo indique.
- blog-ai: los nombres de los campos del contrato público deben escribirse en español, nunca en inglés.

2. Un hook PostToolUse para las herramientas Write y Edit. Cada hook debe añadir una línea al archivo MARCADORES-blog-api.txt o MARCADORES-blog-ai.txt, respectivamente, en la raíz de su propio repositorio, indicando fecha, herramienta y ruta absoluta del archivo modificado. Debe poder registrar rutas de archivos fuera de su repositorio. Configura los hooks como propios de cada proyecto.

3. Una skill llamada marcador-blog-api y otra marcador-blog-ai, respectivamente, con una descripción que identifique su repositorio.

No modifiques funcionalidades, contratos ni otros archivos ajenos al ejercicio. Antes de terminar, identifica qué archivos creaste y qué configuraciones necesitan reiniciar Claude Code para activarse.

Registra este prompt literalmente como el siguiente en blog-api/prompts.md, con el modelo y herramienta actuales. No hagas commit ni abras PR.
```


## Prompt 5

**Modelo:** Opus 4.8
**Herramienta:** Claude Code

```text
Estamos en la prueba del Módulo 7 de AI4DEVS.

Modifica únicamente el archivo ../blog-ai/app/esquemas.py.

Añade a la clase ResultadoBusqueda un campo que indique cuántos fragmentos del artículo coincidieron con la búsqueda.

Utiliza exclusivamente la herramienta Edit para modificarlo. No uses Bash, Python ni scripts para editar archivos.

No modifiques ningún otro archivo.

Al terminar, responde por separado:

1. ¿Qué archivos CLAUDE.md se cargaron al iniciar esta sesión? Cita las reglas que recibiste y distingue lo cargado automáticamente de lo que hayas leído después.
2. ¿Qué skills tienes disponibles? Distingue las propias de cada repositorio de las globales.
3. ¿Qué nombre le diste al campo y por qué?

No corrijas otros problemas ni hagas commit.
```

**Qué salió:** Claude añadió `fragmentos_coincidentes: int` mediante Edit. Declaró haber cargado la regla padre y la de blog-api, pero no la de blog-ai. El hook de blog-api registró la modificación del archivo de blog-ai; no se encontró un archivo de marcadores de blog-ai.
