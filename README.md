# Apuntes Física Nuclear y de Partículas
Este repositorio contiene apuntes y material de estudio de elaboración propia para la asignatura Física Nuclear y de Partículas, basados en las clases impartidas durante el Grado en Física en la Universidad de Salamanca. La redacción del texto, la estructura explicativa y la programación de todas las figuras en LaTeX/TikZ han sido realizadas íntegramente por el autor del repositorio. Este material tiene una finalidad puramente educativa y de consulta personal, y no sustituye a los materiales oficiales de la universidad

## Compilación del manuscrito y figuras.
El texto completo se puede encontrar en el siguiente [documento](main.pdf).

### Requisitos
- Una distribución de LaTeX actualizada: [TeX Live](https://tug.org/texlive/) o [MiKTeX](https://miktex.org/).
- **LuaLaTeX**, que es el motor con el que se compila el documento.
- **latexmk** (necesita Perl) y **biber**. Ambos vienen incluidos en TeX Live y MiKTeX.
- Los paquetes principales son `tikz`, `pgfplots`, `babel` (español), `biblatex` y `tcolorbox`. MiKTeX los instala automáticamente la primera vez que se compila.

### Estructura del repositorio
```
├── main.tex                          # Documento principal: preámbulo e \include de cada tema
├── Portada.tex, Resumen.tex
├── Tema 1.tex … Tema 7.tex           # Un archivo por tema
├── Apendice A.tex
└── Imagenes/
    └── Standalone/                   # Una figura por archivo (.tex) y su PDF compilado
        ├── latexmkrc                 # Configuración para compilar las figuras
        ├── B_AnguloSolido.tex
        └── …
```
Cada figura es un documento `standalone` independiente, con su propio preámbulo. El nombre indica el tema y el orden de aparición (`T3_05_…` es la quinta figura del Tema 3; `ApA_…` corresponde al Apéndice A). El documento principal incluye las figuras ya compiladas, con `\includegraphics{Standalone/<nombre>.pdf}`.

### Compilar las figuras
Si modificas alguna figura, o si sus PDF no están en la carpeta, compílalas **antes** que el documento principal:
```bash
cd Imagenes/Standalone
latexmk                                   # compila todas las figuras que hayan cambiado
latexmk B_AnguloSolido.tex    # compila una única figura
```
El `latexmkrc` de la carpeta usa LuaLaTeX, deja cada PDF junto a su `.tex` y guarda los archivos auxiliares en `build/`. También se puede compilar una figura suelta con `lualatex <figura>.tex` desde esa misma carpeta.

### Compilar el documento
Desde la raíz del repositorio:
```bash
latexmk -lualatex main.tex
```
Se genera `main.pdf` en la raíz. Si no tienes `latexmk`, puedes hacerlo a mano:
```bash
lualatex main.tex
biber main
lualatex main.tex
lualatex main.tex
```

### Limpiar archivos auxiliares
```bash
latexmk -c                                # en la raíz
cd Imagenes/Standalone && latexmk -c      # en la carpeta de figuras
```

## Licencia
Este repositorio está licenciado bajo la licencia Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0). Se permite su uso, distribución y adaptación para fines no comerciales, siempre que se cite la autoría y se compartan las adaptaciones bajo la misma licencia.

Puedes consultar el texto completo de la licencia en el archivo [LICENSE](LICENSE).
