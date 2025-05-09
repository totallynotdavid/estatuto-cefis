# Estatuto del CEFIS [![Open in Overleaf][#overleaf-badge]][#github-repo-zip]

[#overleaf-badge]: https://tinyurl.com/overleaf-badge
[#github-repo-zip]: https://www.overleaf.com/docs?snip_uri=https://github.com/totallynotdavid/estatuto-cefis/archive/refs/heads/master.zip

Este repositorio contiene el código fuente de la propuesta elaborada por el Comité Estatutario para el Estatuto oficial del Centro de Estudiantes de Física (CEFIS) de la Universidad Nacional Mayor de San Marcos. Este documento, de ser aprobado, será la referencia normativa para la organización estudiantil en nuestra Escuela.

## Contexto

En febrero/marzo de 2024, tras la renuncia en bloque de la Junta Directiva del CEFIS, la aprobación del Estatuto quedó en suspenso. Mediante Asamblea General, se estableció un Comité Estatutario encargado de elaborar una propuesta que fuera aprobada por la comunidad estudiantil de la E.P. de Física de manera gradual, título por título, para evitar problemas similares.

El Comité Estatutario estuvo inicialmente conformado por:

- David Duran (Consejo de Facultad)
- Michael Valenzuela (Estudiante de la Base 22)
- José Quispe (Delegatura de la Base 22)
- Aldo Arroyo (Estudiante de la Base 20)
- Walter Orellana (Estudiante de la Base 21)
- Sergio Cordero (Estudiante de la Base 19 y exsecretario de la Junta Directiva del CEFIS)

Las reuniones del Comité se realizaron de forma virtual y fueron documentadas mediante grabaciones. Para la elaboración del documento se consideraron estatutos de otras facultades y centros de estudiantes. El objetivo fue crear un marco normativo claro que orientara a las futuras Juntas Directivas, proporcionándoles simultáneamente la flexibilidad necesaria para actuar con eficacia ante situaciones extraordinarias.

## Estructura del proyecto

El proyecto está diseñado para ser modular:

- El contenido principal está en `main.tex`.
- El estilo y los comandos específicos para el estatuto están en `estatuto.sty`.
- Las definiciones del glosario y abreviaciones están en `glosario.tex`.

## Cómo colaborar

### Opción recomendada: Overleaf

La forma más sencilla de colaborar es utilizando Overleaf, una plataforma online que no requiere instalación: [![Open in Overleaf][#overleaf-badge]][#github-repo-zip]

### Configuración local

Si prefieres trabajar localmente, necesitarás una distribución de LaTeX (como TeX Live o MiKTeX), un editor de texto (Visual Studio Code con extensión LaTeX Workshop, TeXstudio o TeXmaker) y Git para control de versiones.

Para clonar el repositorio:

```bash
git clone https://github.com/totallynotdavid/estatuto-cefis
cd estatuto-cefis
```

Instala las dependencias necesarias. En sistemas Debian/Ubuntu, puedes usar:

```bash
tlmgr update --self --all
```

Para instalar paquetes adicionales, puedes usar el gestor de paquetes de tu distribución LaTeX. Por ejemplo, en TeX Live:

```bash
tlmgr install babel babel-spanish lm geometry setspace microtype lastpage hyperref refcount cleveref enumitem fancyhdr xcolor tocloft l3kernel l3packages glossaries glossaries-extra latexmk
```

La forma más sencilla de compilar el documento es usando `latexmk`:

```bash
latexmk -pdf main.tex
```

`latexmk` se encargará de ejecutar automáticamente `pdflatex` y `makeglossaries` varias veces para asegurarse de que todas las referencias y glosarios estén actualizados.

Para eliminar los archivos generados durante la compilación, usa `latexmk -c` para limpieza básica o `latexmk -C` para limpieza completa (archivos auxiliar del glosario puede que no se eliminen).

Si prefieres hacerlo manualmente, tendrías que ejecutar:

```bash
pdflatex main.tex % Genera archivos auxiliares, te dará errores de referencias
makeglossaries main % Procesa el glosario
pdflatex main.tex % Incorpora el glosario y actualiza algunas referencias
pdflatex main.tex % Termina de actualizar referencias y el índice
```

`latexmk` automatiza todo este proceso. Si quieres entender qué hace `latexmk`, puedes añadir la opción `-verbose`:
```bash
latexmk -pdf -verbose main.tex
```

## Modificando el documento

La mayoría de las modificaciones de contenido se harán en `main.tex`. Al inicio encontrarás los metadatos:

```latex
\newcommand{\DocNom}{ESTATUTO DEL\\CENTRO DE ESTUDIANTES DE FÍSICA}
\newcommand{\DocCorto}{Estatuto del CEFIS} % Usado en el encabezado
\newcommand{\DocFecha}{\today}
\newcommand{\DocAutor}{Comité Estatutario de la Escuela Profesional de Física}
\newcommand{\DocUniversidad}{Universidad Nacional Mayor de San Marcos}
```

El estatuto utiliza comandos específicos para su estructura jerárquica. Para títulos (el nivel más alto):

```latex
\Titulo{Nombre del título}
```

Para capítulos dentro de un título:

```latex
\Capitulo{Nombre del capítulo}
```

Para artículos (que se numeran automáticamente):

```latex
\Articulo[etiqueta-opcional]{Encabezado del artículo}
```

La "etiqueta-opcional" se usa para referenciar artículos o incisos desde otra parte del documento.

Dentro de un artículo, puedes tener listas numeradas (ítems, sub-ítems, sub-sub-ítems). Usa el entorno `artitems` y los comandos `\artitem`, `\subartitem`, `\subsubartitem`. Aquí un ejemplo:

```latex
\begin{artitems} % Inicia una lista de primer nivel (1., 2., ...)
    \artitem[etiqueta-opcional]{Ítem de primer nivel}
    \begin{enumerate} % Inicia una lista de segundo nivel (a., b., ...)
        \subartitem{Ítem de segundo nivel}
        \begin{enumerate} % Inicia una lista de tercer nivel ( (i)., (ii)., ...)
            \subsubartitem{Ítem de tercer nivel}
        \end{enumerate}
    \end{enumerate}
\end{artitems}
```

## Referencias a artículos o íncisos

Primero debes etiquetarlos (como se mostró más arriba) y luego puedes referenciarlos en el texto. Por convención, usamos el prefijo `art:` para artículos o `item:` para ítems.

Para referenciar un Artículo (e.g., "Art. 5"): Usa `\aref{etiqueta-del-articulo}`. Por ejemplo:

```latex	
conforme al \aref{art:principios-cefis}
```

resultará en "conforme al Art. 5" si "principios-cefis" es la etiqueta del artículo 5.

Para referenciar ítems o cualquier otra cosa etiquetada de forma más genérica (e.g., "ítem 5.2.a"): Usa `\cref{etiqueta-del-item}` o `\Cref{etiqueta-del-item}` (con mayúscula inicial). Por ejemplo:

```latex
... de conformidad con el \cref{item:fines-obj-cefis:desarrollo-academico}
```

resultará en "...de conformidad con el ítem 6.2" si "fines-obj-cefis:desarrollo-academico" es la etiqueta del ítem 6.2.

El prefijo `art:` en `\label{art:nombre}` es una convención. Lo importante es que la etiqueta sea única.

## Glosario y abreviaciones

Las definiciones se encuentran en `glosario.tex`. Para abreviaciones:

```latex
\newacronym{cefis}{CEFIS}{Centro de Estudiantes de Física}
```

Para términos del glosario:

```latex
\newglossaryentry{estatuto}{name={estatuto}, description={...}}
```

Para usar estos términos en el texto, puedes emplear `\gls{cefis}` (primera vez aparecerá completo, luego solo la abreviatura), `\Gls{cefis}` (con inicial mayúscula), `\glspl{cefis}` o `\Glspl{cefis}` (formas plurales).

## Aspectos técnicos

El archivo `estatuto.sty` define la apariencia y estructura del documento. Carga los paquetes LaTeX necesarios, define comandos personalizados y configura contadores para numeración automática. Modificarlo requiere un conocimiento más avanzado de LaTeX.

La siguiente lista no es exhaustiva, pero incluye los paquetes más importantes:

- `babel`: Soporte para múltiples idiomas.
- `geometry`: Control de los márgenes y dimensiones de la página.
- `hyperref`: Creación de enlaces internos (ToC, referencias) y externos en el PDF.
- `fancyhdr`: Personalización de encabezados y pies de página.
- `enumitem`: Personalización avanzada de listas (usado para los ítems de artículos).
- `cleveref`: Referencias cruzadas "inteligentes" (`\cref`).
- `tocloft`: Personalización de la Tabla de Contenidos.
- `xparse`: Facilita la creación de comandos complejos con argumentos opcionales.
- `glossaries-extra`: Manejo de glosarios y abreviaciones.

... y otros para cosas como tipografía, espaciado, etc.

Si encuentras problemas durante la compilación, estos pueden deberse a referencias que muestran "??", en cuyo caso debes compilar varias veces (probablemente estés usando pdflatex); glosarios que no aparecen, lo que requiere verificar que se ejecute `makeglossaries`; o paquetes faltantes, que debes instalar con el gestor de tu distribución LaTeX.

## Contribuciones

Si quieres contribuir al proyecto, te recomendamos:

1. Crear un fork del repositorio (para colaboradores externos)
2. Trabajar en una rama separada: `git checkout -b feature/nueva-funcionalidad`
3. Realizar cambios y verificar la compilación
4. Crea un PR (pull request) explicando tus modificaciones

Si tienes acceso directo al repositorio, considera trabajar en ramas separadas para cambios significativos y comunicar tus cambios al resto del equipo.

## Licencia

Este documento es propiedad del Centro de Estudiantes de Física (CEFIS) de la Universidad Nacional Mayor de San Marcos. Todos los derechos reservados. Para consultas sobre uso o distribución, contacta al CEFIS.
