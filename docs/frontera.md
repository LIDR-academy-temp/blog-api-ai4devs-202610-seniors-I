<!-- Archivo de blog-api: este repositorio es el dueño del contenido. -->
# Frontera: lo que dijo el agente y lo que registraron los marcadores

1. El agente dijo que solo cargó los `CLAUDE.md` de `blog/` y de `blog-api`, tenía las skills `marcador-blog-api` y `marcador-blog-ai`, y llamó al campo `fragmentos_coincidentes` porque leyó por su cuenta la regla de `blog-ai`, que no se cargó al iniciar.

2. Solo `MARCADORES-blog-api.txt` registró la edición de `blog-ai/app/esquemas.py`, y `MARCADORES-blog-ai.txt` ni siquiera existe: los guardarraíles se cargan desde la carpeta donde arranca el agente, y `--add-dir` no activa los del otro repo.
