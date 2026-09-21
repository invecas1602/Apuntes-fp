# Tema 3. Hojas de estilo

Este capítulo aborda las hojas de estilo (CSS) como una herramienta fundamental en el desarrollo web, que permite definir y controlar la apariencia de los elementos HTML de manera eficiente y separada del contenido. Las hojas de estilo garantizan un diseño uniforme, adaptable y fácil de mantener, mejorando significativamente la experiencia del usuario.

CSS proporciona la capacidad de modificar colores, fuentes, tamaños, márgenes, fondos, bordes y disposición de los elementos, permitiendo la creación de diseños visuales atractivos y dinámicos. Además, facilita la adaptación a distintos dispositivos mediante técnicas como media queries, unidades relativas y el uso de layouts avanzados con Flexbox y Grid.

También se destaca el uso de frameworks como BulmaCSS, que simplifican el diseño mediante clases predefinidas y garantizan un diseño responsive. La aplicación correcta de estas herramientas permite crear sitios web modernos, funcionales y visualmente coherentes, alineados con las demandas actuales del entorno digital.

### 3.1. Qué es una hoja de estilo

Una hoja de estilo es un documento utilizado en el desarrollo web para definir la apariencia y el diseño de los elementos de una página. Se escribe en un lenguaje llamado CSS (Cascading **Style Sheets), que permite controlar cómo se muestran los** elementos HTML en el navegador.

Las hojas de estilo separan el contenido (HTML) de la presentación (CSS), facilitando el diseño, la coherencia visual y el mantenimiento de los sitios web.

#### Función de una hoja de estilo

- **Definir la apariencia de los elementos: permite modificar co-** lores, fuentes, tamaños, márgenes, alineación, bordes, y otros aspectos visuales.
- **Asegurar consistencia: una única hoja de estilo externa puede** aplicarse a varias páginas, garantizando un diseño uniforme.
- **Adaptarse a dispositivos: facilita la creación de diseños responsi-** vos que se ajustan a diferentes tamaños de pantalla (ordenadores, móviles, tablets).

#### Tipos de hojas de estilo

- **CSS en línea (Inline CSS): especifica estilos directamente dentro** de las etiquetas HTML mediante el atributo style. **Ejemplo:** <p style="color: red; font-size: 16px;">Texto con estilo en línea</p>
- **CSS interno (Internal CSS): se escribe dentro de la etiqueta** <style> en la sección <head> del documento HTML. **Ejemplo:** <head> <style> p { color: red; font-size: 16px; } </style> </head>
- **CSS externo (External CSS): se utiliza un archivo .css separado,** vinculado al documento HTML mediante la etiqueta <link>. **Ejemplo:** <head> <link rel="stylesheet" href="estilos.css"> </head>
#### Contenido del archivo estilos.css:

p { color: red; font-size: 16px; }

#### Ventajas de usar hojas de estilo

- **Separación de contenido y diseño: facilita la gestión y edición** de los archivos HTML y CSS.
- **Reutilización del código: una hoja de estilo externa puede apli-** carse a varias páginas web.

- **Mantenimiento eficiente: cambiar un estilo en el archivo CSS** afecta a todas las páginas que lo usan.
- **Diseños responsivos: CSS permite adaptar el diseño a diferentes** dispositivos y resoluciones.
#### Estructura básica de una hoja de estilo

Una hoja de estilo consta de reglas CSS organizadas en bloques de código. Cada regla incluye:

- **Selector: define a qué elementos HTML se aplicará el estilo.**
- **Declaración: especifica las propiedades y valores del estilo.**
**Ejemplo:**

p { color: blue; /* Cambia el color del texto a azul */ font-size: 18px; /* Ajusta el tamaño de la fuente a 18 píxeles */ }

Una hoja de estilo es una herramienta esencial en el diseño web moderno. Gracias a CSS, los desarrolladores pueden controlar y personalizar la apariencia de sus sitios, mejorando la experiencia del usuario y optimizando el proceso de desarrollo.

### 3.2. Sintaxis y estructura básica

CSS (Cascading Style Sheets) utiliza una sintaxis sencilla para definir los estilos de los elementos HTML. Comprender su estructura básica es esencial para aplicar y personalizar diseños en sitios web.

#### Estructura de una regla CSS

Una regla CSS consta de las siguientes partes:

selector { propiedad: valor; }

**Componentes**

- **Selector: indica a qué elementos HTML se aplicará el estilo.**
- **Propiedad: define qué aspecto del elemento se modificará (color,** tamaño, margen, etc.).
- **Valor: especifica el detalle que se aplicará a la propiedad.**
- **Llaves ({}): encierra las declaraciones de estilo.**
- **Punto y coma (;): separa múltiples declaraciones dentro de un** mismo bloque.
#### Ejemplo básico:

p { color: blue; /* Cambia el color del texto a azul */ font-size: 16px; /* Ajusta el tamaño de la fuente */ text-align: center; /* Centra el texto */ }

Donde:

- El selector es p (aplica a todos los párrafos <p>).
- Las propiedades son color, font-size y text-align.
- Los valores son blue, 16px y center.

#### Tipos de selectores

#### Selectores básicos

- **Elemento: aplica estilos a todas las etiquetas de ese tipo.** h1 { color: red; }
- **Clase (.clase): aplica estilos a los elementos con una clase específica.** .destacado { font-weight: bold; }
- **ID (#id): aplica estilos a un elemento único identificado por un ID.** #principal { background-color: lightgray; }
#### Selectores avanzados

- **Grupo de selectores: aplica el mismo estilo a varios elementos.** h1, h2, h3 { color: green; }
- **Selectores descendientes: aplica estilos a los elementos dentro** de un contenedor. div p { color: purple; }
- **Selectores de atributos: aplica estilos a elementos con un atribu-** to específico. input[type="text"] { border: 1px solid black; }

- **Selectores pseudoclase: aplica estilos basados en un estado o** condición. a:hover { text-decoration: underline; }
- **Selectores pseudoelemento: aplica estilos a una parte específica** de un elemento. p::first-line { font-weight: bold; }
#### Declaraciones múltiples

Un bloque CSS puede contener varias declaraciones de propiedad y valor, separadas por punto y coma.

**Ejemplo:**

div { margin: 20px; padding: 10px; border: 2px solid black; }

#### Comentarios en CSS

Los comentarios se utilizan para describir el código y mejorar su legibilidad. No afectan la ejecución del estilo.

#### Sintaxis de comentario

/* Este es un comentario */

**Ejemplo:**

/* Cambia el color del texto a azul */ p { color: blue; }

#### Importancia de la cascada y especificidad

**Cascada**

- Si dos reglas se aplican al mismo elemento, la más específica tendrá prioridad.
- Si ambas tienen la misma especificidad, se aplica la última en el orden del archivo CSS.
**Especificidad**

- Determina qué regla tiene prioridad basándose en el tipo de selector.
- Orden de prioridad: ID > Clase > Elemento.
#### Ejemplo de conflicto:

p { color: red; }

#principal { color: blue; }

Si el párrafo tiene el ID principal, el color será azul.

La sintaxis y estructura de CSS es sencilla pero poderosa. Con una comprensión básica de selectores, propiedades y valores, es posible controlar la apariencia de un sitio web de manera eficiente y profesional.

### 3.3. Propiedades CSS básicas

Las propiedades CSS básicas son los atributos que permiten definir y personalizar la apariencia de los elementos HTML. Estas propiedades se organizan en categorías según su funcionalidad, como el estilo del texto, el fondo, el tamaño o la disposición de los elementos.

#### Propiedades de texto

Estas propiedades permiten estilizar y formatear el contenido textual.

#### Color del texto

color: red; /* Cambia el color del texto */

#### Tamaño de la fuente

font-size: 16px; /* Tamaño de la fuente en píxeles */

#### Tipo de fuente

font-family: Arial, sans-serif; /* Fuente principal y alternativa */

#### Estilo de fuente

font-style: italic; /* Texto en cursiva */

#### Grosor de la fuente

font-weight: bold; /* Texto en negrita */

#### Alineación del texto

text-align: center; /* Centra el texto */

#### Decoración del texto

text-decoration: underline; /* Subraya el texto */

#### Transformación del texto

text-transform: uppercase; /* Convierte el texto a mayúsculas */

#### Espaciado entre letras y líneas

letter-spacing: 2px; /* Espaciado entre letras */ line-height: 1.5; /* Altura de línea */

#### Propiedades de fondo

Controlan el color, la imagen y otros aspectos visuales del fondo.

#### Color de fondo

background-color: lightblue; /* Fondo azul claro */

#### Imagen de fondo

background-image: url("imagen.jpg"); /* Aplica una imagen como fondo */

#### Posición del fondo

background-position: center; /* Centra la imagen de fondo */

#### Tamaño del fondo

background-size: cover; /* Escala la imagen para cubrir todo el fondo */

#### Repetición del fondo

background-repeat: no-repeat; /* Evita que la imagen de fondo se repita */

#### Propiedades de borde

Definen los bordes de los elementos.

#### Estilo del borde

border-style: solid; /* Borde sólido */

#### Ancho del borde

border-width: 2px; /* Grosor del borde */

#### Color del borde

border-color: black; /* Color del borde */

#### Borde resumido

border: 2px solid black; /* Ancho, estilo y color del borde */

#### Esquinas redondeadas

border-radius: 10px; /* Bordes redondeados */

#### Propiedades de espacio

Controlan el espacio dentro y fuera de los elementos.

#### Margen (espacio exterior)

margin: 20px; /* Espacio fuera del elemento */

#### Relleno (espacio interior)

padding: 10px; /* Espacio dentro del elemento */

#### Margen y relleno individual

margin-top: 10px; /* Margen superior */ padding-left: 5px; /* Relleno izquierdo */

#### Propiedades de visualización

Controlan cómo se muestran los elementos en la página.

#### Tipo de visualización

display: block; /* El elemento se comporta como un bloque */ display: inline; /* El elemento se comporta como en línea */

**Visibilidad**

visibility: hidden; /* Oculta el elemento pero mantiene su espacio */

**Desbordamiento**

overflow: scroll; /* Muestra barras de desplazamiento si el contenido desborda */

#### Propiedades de tamaño

Definen el ancho y alto de los elementos.

#### Ancho y alto

width: 300px; /* Ancho del elemento */ height: 150px; /* Alto del elemento */

#### Ancho y alto máximo/mínimo

max-width: 500px; /* Ancho máximo permitido */ min-height: 100px; /* Altura mínima permitida */

#### Propiedades adicionales

**Sombra**

box-shadow: 5px 5px 10px gray; /* Sombra alrededor del elemento */

**Opacidad**

opacity: 0.8; /* Hace el elemento ligeramente transparente */

#### Ejemplo práctico de propiedades CSS básicas:

body { background-color: #f0f0f0; /* Fondo gris claro */ font-family: Arial, sans-serif; /* Fuente principal */ color: #333; /* Texto gris oscuro */ margin: 0; /* Sin margen exterior */ padding: 0; /* Sin relleno interior */ }

h1 { text-align: center; color: #007bff; /* Azul */ font-size: 2em; }

p { line-height: 1.5; margin: 20px; text-indent: 20px; /* Sangría en el inicio del párrafo */ }

Estas propiedades básicas de CSS son esenciales para personalizar el diseño de un sitio web y garantizar una presentación profesional y atractiva.

### 3.4. Diseño responsive

#### Propiedades adicionales

**Sombra** **¿Qué es el diseño responsive?**

box-shadow: 5px 5px 10px gray; /* Sombra alrededor del elemento */

**Opacidad**

opacity: 0.8; /* Hace el elemento ligeramente transparente */

#### Ejemplo práctico de propiedades CSS básicas:

body { background-color: #f0f0f0; /* Fondo gris claro */ font-family: Arial, sans-serif; /* Fuente principal */ color: #333; /* Texto gris oscuro */ margin: 0; /* Sin margen exterior */ padding: 0; /* Sin relleno interior */ }

h1 { text-align: center; color: #007bff; /* Azul */ font-size: 2em; }

p { line-height: 1.5; margin: 20px; text-indent: 20px; /* Sangría en el inicio del párrafo */ }

Estas propiedades básicas de CSS son esenciales para personalizar el diseño de un sitio web y garantizar una presentación profesional y atractiva.

El diseño responsive es un enfoque en el desarrollo web que busca garantizar que los sitios web se adapten correctamente a diferentes tamaños de pantalla y dispositivos, como teléfonos móviles, tablets, ordenadores portátiles y monitores de escritorio. Su objetivo principal es mejorar la experiencia del usuario independientemente del dispositivo utilizado.

El diseño responsive utiliza técnicas y herramientas como media queries, **unidades relativas, y layouts flexibles para que el contenido de una** página se ajuste dinámicamente a diferentes resoluciones de pantalla.

#### Características clave del diseño responsive

- **Adaptabilidad: el contenido y los elementos visuales se ajustan** automáticamente al tamaño del dispositivo.
- **Un diseño único: se evita crear versiones separadas para disposi-** tivos móviles y escritorio, simplificando el mantenimiento.
- **Optimización para dispositivos móviles: el diseño se enfoca en** pantallas más pequeñas primero (Mobile First) y luego escala a dispositivos más grandes.
#### Herramientas y técnicas del diseño responsive

#### Media queries

Las media queries son una característica de CSS que permite aplicar estilos dependiendo de las características del dispositivo, como el ancho de pantalla, la orientación o la resolución.

#### Ejemplo básico:

/* Estilo por defecto (escritorio) */ body { font-size: 16px; }

/* Estilo para dispositivos con un ancho máximo de 768px (tablets y móviles) */ @media (max-width: 768px) { body { font-size: 14px; } }

/* Estilo para dispositivos con un ancho máximo de 480px (móviles) */ @media (max-width: 480px) { body { font-size: 12px; } }

#### Unidades relativas

El uso de unidades relativas permite que los tamaños de los elementos se ajusten proporcionalmente.

- **Unidades relativas comunes:** – **em: relativo al tamaño de la fuente del elemento padre.** – **rem: relativo al tamaño de la fuente raíz (html).** – **%: relativo al tamaño del contenedor padre.** – **vh y vw: relativo al 1% del ancho o altura de la ventana gráfica.** **Ejemplo:** body { font-size: 1rem; /* Relativo al tamaño de la fuente base */ } div { width: 50%; /* Ocupa el 50% del ancho del contenedor padre */ height: 50vh; /* Ocupa el 50% de la altura de la ventana gráfica */ }

#### Layouts flexibles (Flexbox y Grid)

- **Flexbox: sistema de diseño unidimensional que distribuye ele-** mentos de manera flexible. **Ejemplo:** .container { display: flex; flex-wrap: wrap; /* Permite que los elementos se ajusten en varias líneas */ justify-content: center; /* Centra los elementos horizontalmente */ gap: 10px; /* Espacio entre elementos */ }
- **Grid: sistema de diseño bidimensional que organiza elementos en** filas y columnas. **Ejemplo:** .container { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* Ajusta el número de columnas automáticamente */ gap: 15px; /* Espacio entre columnas y filas */ }
#### Imágenes y multimedia responsivos

- **Imágenes fluidas:** img { max-width: 100%; /* Ajusta el ancho al contenedor */ height: auto; /* Mantiene la proporción */ }
- **Videos responsivos: se utilizan contenedores con proporción fija.** .video-container { position: relative; padding-top: 56.25%; /* Relación 16:9 */ height: 0; } .video-container iframe { position: absolute;

top: 0; left: 0; width: 100%; height: 100%; }

#### Enfoque "Mobile First"

El diseño Mobile First comienza con la creación de estilos optimizados para dispositivos móviles y luego se amplía para pantallas más grandes. Esto asegura que la experiencia en móviles, donde se origina la mayoría del tráfico web, sea prioritaria.

#### Ejemplo de Mobile First:

/* Estilo por defecto (para móviles) */ body { font-size: 14px; }

/* Estilos para tablets y escritorio */ @media (min-width: 768px) { body { font-size: 16px; } }

@media (min-width: 1200px) { body { font-size: 18px; } }

#### Frameworks para diseño responsive

Los frameworks CSS incluyen componentes y clases predefinidas que facilitan la creación de diseños responsivos.

**Ejemplos:**

- **Bootstrap: sistema de rejillas y utilidades para diseño móvil y** responsive.
- **Bulma CSS: framework que destaca por su sencillez.**
- **Tailwind CSS: framework de utilidades altamente personalizable.**
- **Foundation: herramienta avanzada para diseño adaptativo.**

#### Ventajas del diseño responsive

- **Mejor experiencia del usuario: contenido accesible y legible en** cualquier dispositivo.
- **Optimización para SEO: google favorece los sitios responsivos en** los resultados de búsqueda.
- **Mantenimiento más fácil: un único diseño se adapta a múltiples** dispositivos, reduciendo el tiempo de desarrollo.
El diseño responsive es una práctica esencial en el desarrollo web moderno. Permite que los sitios se adapten automáticamente a diferentes dispositivos, mejorando la experiencia del usuario y maximizando el alcance del contenido. Con herramientas como media queries, unidades relativas y frameworks, los desarrolladores pueden crear sitios web visualmente atractivos y funcionales en cualquier entorno.

### 3.5. Layouts avanzados en CSS

Los layouts avanzados en CSS permiten organizar y distribuir el contenido de una página de manera flexible y eficiente. Estas técnicas, como **Flexbox y CSS Grid, son fundamentales para crear diseños modernos,** adaptables y responsivos.

#### Sistema Flexbox

Flexbox (Flexible Box) es un sistema unidimensional que organiza elementos en filas o columnas, ofreciendo un control preciso sobre la alineación, distribución y orden de los elementos.

#### Características principales

- Trabaja en un eje principal (horizontal o vertical) y un eje secundario (perpendicular al principal).
- Permite centrar y distribuir elementos de manera sencilla.
- Soporta elementos dinámicos y adaptables.

#### Propiedades principales de Flexbox

- **Contenedor flex:** .contenedor { display: flex; /* Activa Flexbox en el contenedor */ flex-direction: row; /* Dirección de los elementos: fila (por defecto) */ justify-content: space-between; /* Espaciado entre elementos */ align-items: center; /* Alineación vertical en el eje cruzado */ }
- **Elementos flexibles:** .elemento { flex-grow: 1; /* Hace que los elementos crezcan para llenar el espacio disponible */ flex-shrink: 0; /* Impide que los elementos se reduzcan */ flex-basis: 200px; /* Tamaño inicial del elemento */ }
- **Ejemplo práctico de Flexbox:** .contenedor { display: flex; flex-direction: row; justify-content: center; align-items: center; gap: 10px; /* Espaciado entre elementos */ } .elemento { background-color: lightblue; padding: 20px; border: 1px solid #000; } <div class="contenedor"> <div class="elemento">Elemento 1</div> <div class="elemento">Elemento 2</div> <div class="elemento">Elemento 3</div> </div>

#### Sistema CSS Grid

CSS Grid es un sistema de diseño bidimensional que permite organizar elementos en filas y columnas. Es ideal para diseños complejos que requieren una estructura clara y precisa.

#### Características principales

- Define áreas específicas para cada elemento.
- Soporta alineación avanzada tanto horizontal como verticalmente.
- Compatible con layouts adaptables y responsivos.
#### Propiedades principales de CSS Grid

- **Contenedor Grid:** .contenedor { display: grid; /* Activa Grid en el contenedor */ grid-template-columns: repeat(3, 1fr); /* Tres columnas de igual ancho */ grid-template-rows: auto 200px; /* Dos filas: la primera automática y la segunda fija */ gap: 10px; /* Espaciado entre filas y columnas */ }
- **Elementos de la Grid:** .elemento { grid-column: 2 / span 2; /* Ocupa desde la segunda columna y abarca dos columnas */ grid-row: 1 / 2; /* Ocupa la primera fila */ }
- **Ejemplo práctico de Grid:** .contenedor { display: grid; grid-template-columns: repeat(3, 1fr); /* Tres columnas iguales */ gap: 10px; background-color: #f0f0f0; padding: 10px; } .elemento { background-color: lightcoral; padding: 20px; text-align: center;

}

<div class="contenedor"> <div class="elemento">1</div> <div class="elemento">2</div> <div class="elemento">3</div> <div class="elemento">4</div> <div class="elemento">5</div> <div class="elemento">6</div> </div>

#### Sistema de rejillas híbrido (Grid + Flexbox)

Ambos sistemas pueden combinarse para lograr layouts más avanzados. Por ejemplo, usar CSS Grid para la estructura principal y Flexbox para la distribución interna de los elementos.

#### Ejemplo híbrido:

.contenedor { display: grid; grid-template-columns: 1fr 2fr; gap: 20px; }

.flex { display: flex; justify-content: space-between; align-items: center; background-color: lightgreen; padding: 10px; }

<div class="contenedor"> <div class="flex"> <div>Elemento A</div> <div>Elemento B</div> </div> <div class="flex"> <div>Elemento C</div> <div>Elemento D</div> </div> </div>

#### Diseño responsive con layouts avanzados

Combinar media queries con Flexbox o Grid permite crear diseños adaptables a diferentes resoluciones de pantalla.

#### Ejemplo de Grid responsive:

.contenedor { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* Ajusta las columnas automáticamente */ gap: 15px; }

#### Ventajas de los layouts avanzados

- **Flexibilidad: permiten diseños adaptativos y escalables.**
- **Organización: mejoran la estructura y la disposición del contenido.**
- **Control preciso: facilitan el control de alineación, espacio y tama-** ño de los elementos. **Conclusión** Los layouts avanzados en CSS, como Flexbox y Grid, son herramientas poderosas para crear diseños modernos y responsivos. Su dominio permite a los desarrolladores estructurar el contenido de manera eficiente y optimizar la experiencia del usuario en cualquier dispositivo.

### 3.6. Tipografía en CSS

La tipografía en CSS se refiere al conjunto de propiedades que permiten controlar el estilo, tamaño, alineación y otras características del texto en una página web. La elección y personalización de la tipografía son fundamentales para mejorar la legibilidad, accesibilidad y la estética de un sitio web.

#### Propiedades principales de tipografía

#### Propiedad font-family

Define la fuente utilizada para el texto. Se pueden especificar varias fuentes como alternativas en caso de que alguna no esté disponible.

**Ejemplo:**

p { font-family: Arial, Helvetica, sans-serif; }

- **Arial: fuente principal.**
- **Helvetica: fuente alternativa.**
- **sans-serif: categoría genérica para fuentes sin remates.**
#### Propiedad font-size

Controla el tamaño de la fuente.

#### Unidades comunes:

- **Pixeles (px): tamaño absoluto.**
- **Ems (em) y rems (rem): tamaño relativo al elemento padre (em)** o raíz (rem).
- **Porcentajes (%): relativo al tamaño del texto del elemento padre.**
**Ejemplo:**

h1 { font-size: 2em; /* Dos veces el tamaño base */ }

#### Propiedad font-weight

Controla el grosor del texto.

#### Valores comunes:

- **normal: grosor estándar.**
- **bold: texto en negrita.**
- **100, 200, ..., 900: grosor numérico (100 más delgado, 900 más** grueso).
**Ejemplo:**

p { font-weight: bold; }

#### Propiedad font-style

Define si el texto estará en estilo normal, cursiva o inclinada.

**Ejemplo:**

blockquote { font-style: italic; }

#### Propiedad line-height

Controla el espacio vertical entre líneas de texto. Es importante para mejorar la legibilidad.

**Ejemplo:**

p { line-height: 1.5; /* 1.5 veces la altura del texto */ }

#### Propiedad letter-spacing

Ajusta el espacio entre caracteres.

**Ejemplo:**

h1 { letter-spacing: 2px; }

#### Propiedad text-align

Controla la alineación horizontal del texto.

#### Valores comunes:

- left: alineado a la izquierda.
- right: alineado a la derecha.
- center: centrado.
- justify: justificado.
**Ejemplo:**

p { text-align: justify; }

#### Propiedad text-transform

Cambia la capitalización del texto.

**Ejemplo:**

h2 { text-transform: uppercase; /* Todo en mayúsculas */ }

#### Propiedad text-decoration

Define decoraciones como subrayados, tachados o eliminaciones.

**Ejemplo:**

a { text-decoration: none; /* Sin subrayado */ }

#### Uso de fuentes personalizadas

#### Fuentes de sistema

Son fuentes preinstaladas en los dispositivos (Arial, Times New Roman, etc.).

#### Fuentes web con Google Fonts

Google Fonts permite incluir fuentes personalizadas en un sitio web.

**Ejemplo:**

Añadir el enlace en el <head> del HTML:

<link href="[https://fonts.googleapis.com/css2?fami-](https://fonts.googleapis.com/css2?fami-) ly=Roboto:wght@400;700&display=swap" rel="stylesheet">

#### Usar la fuente en CSS:

body { font-family: 'Roboto', sans-serif; }

#### Fuentes con @font-face

Permite incluir fuentes personalizadas directamente en el CSS.

**Ejemplo:**

@font-face { font-family: 'MiFuentePersonalizada'; src: url('mifuente.woff2') format('woff2'), url('mifuente.woff') format('woff'); }

h1 { font-family: 'MiFuentePersonalizada', sans-serif; }

#### Buenas prácticas en tipografía

- **Legibilidad: usa tamaños y colores que permitan una lectura** cómoda.
- **Consistencia: limita la cantidad de fuentes utilizadas (2 o 3 como** máximo).
- **Contraste: asegúrate de que el color del texto contraste adecua-** damente con el fondo.
- **Responsive: adapta los tamaños de las fuentes utilizando unida-** des relativas (em, rem, %).
- **Accesibilidad: usa la propiedad line-height y asegúrate de que los** textos sean comprensibles.

#### Ejemplo práctico de tipografía en CSS

body { font-family: 'Roboto', Arial, sans-serif; font-size: 16px; line-height: 1.6; color: #333; background-color: #f9f9f9; margin: 0; padding: 20px; }

h1 { font-size: 2.5rem; font-weight: 700; text-align: center; margin-bottom: 20px; }

p { font-size: 1rem; letter-spacing: 0.5px; text-align: justify; }

a { color: #007bff; text-decoration: none; }

a:hover { text-decoration: underline; }

La tipografía en CSS es crucial para crear una experiencia de usuario atractiva y funcional. Con las propiedades adecuadas, los desarrolladores pueden diseñar páginas web que sean visualmente coherentes, legibles y accesibles para todos los usuarios.

### 3.7. BulmaCss-Un framework para CSS

#### BulmaCSS es un framework CSS moderno basado en un sistema de clases, diseñado para facilitar la creación de interfaces de usuario atractivas y responsivas. Es completamente modular y no requiere el uso de JavaScript, centrándose únicamente en la presentación visual.

#### Características principales de BulmaCSS

- **Ligero y modular: solo se incluyen las funcionalidades necesa-** rias, permitiendo personalizar los estilos.
- **Sistema de diseño responsive: utiliza un sistema de columnas ba-** sado en flexbox, lo que facilita la creación de layouts adaptativos.
- **Basado en clases: todas las funcionalidades se implementan a** través de clases predefinidas, simplificando la escritura de código.
- **Sin dependencias: no requiere JavaScript ni otros frameworks ex-** ternos para funcionar.
- **Estética moderna: viene con estilos atractivos y listos para usar,** ideales para proyectos rápidos.
#### Instalación de BulmaCSS

#### Usando CDN

Es la forma más rápida de incluir Bulma en tu proyecto.

**Ejemplo:**

<link rel="stylesheet" href="[https://cdn.jsdelivr](https://cdn.jsdelivr). net/npm/bulma@0.9.4/css/bulma.min.css">

#### Instalación con npm

Para proyectos más complejos, puedes instalar Bulma usando npm.

**Comando:**

npm install bulma

Luego, incluye Bulma en tu archivo principal CSS o SCSS:

@import 'bulma';

#### Componentes principales de BulmaCSS

Bulma ofrece una amplia gama de clases y componentes predefinidos que facilitan el desarrollo.

#### Sistema de columnas

Permite dividir el contenido en columnas responsivas.

**Ejemplo:**

<div class="columns"> <div class="column">Columna 1</div> <div class="column">Columna 2</div> <div class="column">Columna 3</div> </div>

**Botones**

Clases para botones con diferentes estilos.

**Ejemplo:**

<button class="button is-primary">Botón Primario</button> <button class="button is-link">Botón Secundario</button>

**Navbar**

Sistema predefinido para barras de navegación.

**Ejemplo:**

<nav class="navbar"> <div class="navbar-brand"> <a class="navbar-item" href="#">Logo</a> </div> <div class="navbar-menu"> <div class="navbar-start"> <a class="navbar-item" href="#">Inicio</a> <a class="navbar-item" href="#">Acerca</a> </div> </div> </nav>

**Formularios**

Estilos para campos de entrada, botones y formularios.

**Ejemplo:**

<div class="field"> <label class="label">Nombre</label> <div class="control"> <input class="input" type="text" placeholder="Introduce tu nombre"> </div> </div> <button class="button is-success">Enviar</button>

**Tarjetas**

Para mostrar contenido destacado en un formato atractivo.

**Ejemplo:**

<div class="card"> <div class="card-content"> <p class="title">Título de la tarjeta</p> <p class="subtitle">Subtítulo</p> </div> </div>

#### Sistema de colores en Bulma

Bulma incluye una amplia paleta de colores para personalizar elementos.

**Ejemplo:**

<p class="has-text-primary">Texto en color primario</ p> <p class="has-background-warning">Fondo de advertencia</p>

#### Sistema responsive en Bulma

Bulma utiliza breakpoints predefinidos para crear diseños responsivos. Puedes aplicar clases basadas en el tamaño de la pantalla.

**Breakpoints:**

- **Mobile: menos de 768px.**
- **Tablet: entre 768px y 1023px.**
- **Desktop: más de 1024px.**
**Ejemplo:**

<div class="columns"> <div class="column is-half-desktop is-full-mobile">Columna responsiva</div> </div>

#### Ventajas de BulmaCSS

- **Facilidad de uso: las clases predefinidas permiten desarrollar rá-** pidamente sin necesidad de escribir CSS personalizado.
- **Completamente responsive: incluye soporte para adaptarse au-** tomáticamente a cualquier dispositivo.
- **Estilos modernos: el diseño visual de Bulma es atractivo y ade-** cuado para proyectos actuales.
- **Comunidad activa: cuenta con documentación extensa y soporte** de la comunidad.
#### Desventajas de BulmaCSS

- **Dependencia de clases: todo el diseño depende del uso correc-** to de las clases, lo que puede limitar la flexibilidad en proyectos complejos.
- **Sobrecarga de estilos: en proyectos pequeños, puede incluir más** estilos de los necesarios.
#### Ejemplo práctico de una página con Bulma:

<!DOCTYPE html> <html lang="es"> <head> <meta charset="UTF-8"> <meta name="viewport" content="width=device-width, initial-scale=1.0"> <link rel="stylesheet" href="[https://cdn.jsdeli-](https://cdn.jsdeli-) vr.net/npm/bulma@0.9.4/css/bulma.min.css"> <title>Página con Bulma</title> </head> <body> <section class="hero is-primary"> <div class="hero-body"> <p class="title">Bienvenido a Bulma</p> <p class="subtitle">Framework CSS moderno y flexible</p> </div> </section>

<div class="container"> <div class="columns"> <div class="column is-half"> <h2 class="title is-4">Sección 1</h2> <p>Contenido de la primera columna.</ p> </div> <div class="column is-half"> <h2 class="title is-4">Sección 2</h2> <p>Contenido de la segunda columna.</ p> </div> </div>

<button class="button is-primary">Botón Primario</button> <button class="button is-danger">Botón Peligro</button> </div> </body> </html>

BulmaCSS es un framework poderoso y fácil de usar para crear interfaces modernas y responsivas sin necesidad de escribir CSS desde cero. Es una excelente opción para proyectos que requieren rapidez y diseños visualmente atractivos.