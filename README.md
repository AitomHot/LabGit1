# LabGit1
Laboratorio de prácticas de Git


## Slides
Se pueden convertir archivos *.md especialmente formateados para generar documentos utilizando la herramienta ```pandoc``` mediante Docker, de modo que no es necesario instalar nada en local.

Un ejemplo de caso de uos es generar presentaciones pptx.

Para un uso interactivo, es muy conveniente definir este alias

```zsh
alias pandock="docker run --rm -v "$(pwd):/data" -u $(id -u):$(id -g) pandoc/core"
```

Así, podremos ejecutar por ejemplo:

```zsh
pandock slides_aspire.md -o slides_aspire3.pptx
```

### Nota

No es posible utilizar directamente en Macbook la imagen docker ```pandoc/latex``` porque los binarios no son compatibles con linux/arm64/v8. Ver https://hub.docker.com/r/pandoc/latex