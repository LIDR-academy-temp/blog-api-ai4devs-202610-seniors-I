
# Frontera entre repositorios

## Frase 1. Lo que declaró el agente

Al iniciar Claude Code desde blog-api con blog-ai añadido mediante --add-dir, el agente declaró que se cargaron automáticamente los archivos CLAUDE.md de la carpeta padre y de blog-api, pero no el de blog-ai. Identificó las dos skills de marcadores como disponibles y creó en blog-ai/app/esquemas.py el campo `fragmentos_coincidentes: int`, en español y siguiendo el vocabulario existente del contrato, aunque no había cargado la regla específica de blog-ai.

## Frase 2. Lo que realmente ocurrió

El archivo MARCADORES-blog-api.txt registró la operación Edit sobre `/home/fc/blog/blog-ai/app/esquemas.py`, mientras que MARCADORES-blog-ai.txt no existía. Por tanto, el hook de blog-api sí registró una modificación realizada en el otro repositorio, pero no hubo evidencia de ejecución del hook de blog-ai. La prueba demuestra que disponer de acceso a otro repositorio o de sus skills no garantiza que sus instrucciones y hooks se apliquen automáticamente.
