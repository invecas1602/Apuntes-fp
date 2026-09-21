# Tema 1. Qué son los lenguajes de marcas

Los lenguajes de marcas son herramientas fundamentales en el mundo de la informática, utilizadas para estructurar, describir y organizar datos. Estos lenguajes han demostrado ser versátiles y esenciales en múltiples contextos desde su uso en el diseño web hasta la integración de sistemas complejos. Este capítulo explora los conceptos básicos y las principales características de los lenguajes de marcas, centrándose en el estándar **XML (eXtensible Markup Language) como ejemplo destacado.**

### 1.1. Conceptos generales

Un lenguaje de marcas es un sistema de codificación que utiliza etiquetas ("marcas") para identificar elementos dentro de un documento. Estas etiquetas no son visibles en el resultado final (por ejemplo, en una página web o un documento generado) pero determinan cómo debe interpretarse o presentarse el contenido.

Además, permiten estructurar, definir y presentar información de forma organizada. Se utilizan ampliamente en la creación de documentos digitales, sistemas de intercambio de datos y diseño web, destacando por su versatilidad y facilidad de uso.

Por ejemplo, en HTML (HyperText Markup Language), una etiqueta como <h1> indica un título principal dentro de una página web.

#### Características principales

- **Estructura jerárquica**: los lenguajes de marcas suelen organizar la información en una estructura jerárquica basada en árboles, lo que facilita la representación de datos complejos.
- **Legibilidad**: aunque están destinados principalmente a las máquinas, los lenguajes de marcas son legibles para los humanos, lo que facilita su creación y depuración.
- **Independencia del formato**: los lenguajes de marcas separan el contenido de su presentación, permitiendo que un mismo documento pueda ser visualizado en distintos dispositivos o formatos.
- **Extensibilidad**: algunos lenguajes de marcas, como XML, permiten crear nuevas etiquetas adaptadas a las necesidades específicas de los usuarios o aplicaciones.

#### Tipos de lenguajes de marcas

Los lenguajes de marcas pueden clasificarse según su propósito principal:

- **Lenguajes de descripción de documentos**: diseñados para estructurar y presentar documentos, como HTML y LaTeX.
- **Lenguajes de intercambio de datos**: se utilizan para transferir datos entre sistemas de manera estructurada, como XML y JSON (aunque este último no usa etiquetas).
- **Lenguajes de presentación**: orientados a la definición del estilo y la apariencia de los datos, como CSS.
- **Lenguajes especializados**: diseñados para aplicaciones específicas, como MathML, para expresiones matemáticas o SVG o para gráficos vectoriales.
#### Aplicaciones comunes

- **Diseño web**: lenguajes como HTML y CSS son la base de las páginas web modernas.
- **Intercambio de datos**: XML es ampliamente usado en la comunicación entre aplicaciones.
- **Documentación científica**: laTeX facilita la creación de documentos técnicos de alta calidad.
- **Almacenamiento de datos**: archivos XML o JSON son comunes en configuraciones y bases de datos.
**Beneficios**

- **Estandarización**: promueven la interoperabilidad al seguir estándares definidos por organismos como el W3C.
- **Portabilidad**: los documentos marcados pueden interpretarse en diferentes plataformas y sistemas.
- **Escalabilidad**: permiten manejar desde documentos simples hasta sistemas complejos con millones de registros.
Los lenguajes de marcas son una pieza fundamental en la gestión de la información digital. Su flexibilidad, legibilidad y capacidad para adaptarse a diversas aplicaciones los convierten en herramientas esenciales para desarrolladores y profesionales en el área de la tecnología.

### 1.2. Clasificación

Los lenguajes de marcas pueden clasificarse en función de su propósito y uso. A continuación, se presentan las principales categorías:

#### Lenguajes de marcas para estructuración de datos

Estos lenguajes se utilizan para organizar y estructurar información de forma jerárquica, facilitando su almacenamiento, intercambio y procesado.

**Ejemplos:**

- **XML (eXtensible Markup Language)**: permite estructurar información de manera flexible y extensible. Se utiliza en documentos, configuraciones y bases de datos.
- **JSON (JavaScript Object Notation)**: aunque técnicamente no es un lenguaje de marcas, se usa ampliamente como alternativa ligera a XML para estructurar datos.
#### Lenguajes de marcas para el diseño web

Se emplean para definir la estructura, presentación y funcionalidad de las páginas web.

**Ejemplos:**

- **HTML (HyperText Markup Language)**: define la estructura de las páginas web mediante etiquetas que representan encabezados, párrafos, enlaces, imágenes, etc.
- **CSS (Cascading Style Sheets)**: no es un lenguaje de marcas puro, pero complementa a HTML definiendo estilos y presentación visual.
#### Lenguajes de marcas especializados

Diseñados para necesidades específicas en sectores concretos.

**Ejemplos:**

- **SVG (Scalable Vector Graphics)**: se emplea para la descripción de gráficos vectoriales en 2D.
- **MathML (Mathematical Markup Language)**: acostumbra a usarse para representar expresiones matemáticas en páginas web y documentos.
- **RSS (Really Simple Syndication)**: usado para sindicación de contenido, como noticias y blogs.

#### Lenguajes de marcas basados en estándares específicos

Estos lenguajes suelen estar diseñados con la finalidad de cumplir con ciertos estándares y facilitar la interoperabilidad entre sistemas.

**Ejemplos:**

- **XHTML (eXtensible HyperText Markup Language)**: combina HTML y XML para garantizar documentos más estrictos y compatibles.
- **SOAP (Simple Object Access Protocol)**: utilizado en servicios web para el intercambio de información entre aplicaciones.
#### Lenguajes de marcas propios o personalizados

Permiten crear lenguajes adaptados a las necesidades de una organización o aplicación. Estos lenguajes personalizados generalmente están basados en XML.

**Ejemplo:**

- Un lenguaje de marcas diseñado para el sector educativo, como
#### SCORM (Sharable Content Object Reference Model), que se usa

en plataformas de e-learning.

En la siguiente tabla se encuentra un resumen de los lenguajes de marcas siguiendo esta clasificación.

|Tipo|Ejemplos|Uso principal|
|---|---|---|
|Estructuración de datos.|XML, JSON.|Organización e intercambio de datos.|
|Diseño web.|HTML, CSS.|Creación y diseño de páginas web.|
|Especializados.|SVG, MathML, MusicXML, RSS.|Aplicaciones específicas.|
|Basados en estándares.|XHTML, SOAP.|Interoperabilidad y compatibilidad.|
|Personalizados.|SCORM, lenguajes empresariales.|Soluciones específicas por sectores.|

### 1.3. Herramientas de edición

La creación y manipulación de documentos en lenguajes de marcas requiere herramientas adecuadas que faciliten el trabajo de edición. Estas herramientas varían en funcionalidad, desde editores básicos hasta entornos integrados de desarrollo (IDE). A continuación, se presenta una clasificación de las principales herramientas disponibles.

#### Editores de texto simples

Son programas básicos que permiten escribir código de lenguajes de marcas sin funciones avanzadas. Son ideales para aprender y comprender las estructuras básicas de los lenguajes.

**Ejemplos:**

- **Bloc de notas (Windows)**: se trata de una opción básica y accesible para empezar.
- **Nano o Vim (Linux)**: editores en consola, ligeros y eficientes para usuarios avanzados.
#### Editores de texto enriquecidos

Estos editores ofrecen funcionalidades avanzadas como resaltado de sintaxis, autocompletado y validación básica.

**Ejemplos:**

- **Notepad++**: ligero y compatible con múltiples lenguajes.
- **Sublime Text**: editor personalizable con soporte para plugins.
- **Visual Studio Code (VS Code)**: amplio soporte para lenguajes de marcas, con plugins específicos para XML, HTML y otros.
#### Entornos integrados de desarrollo (IDE)

Son herramientas completas que combinan edición, depuración y validación, orientadas a proyectos más complejos.

**Ejemplos:**

- **Eclipse**: cuenta con plugins para trabajar con XML, HTML y lenguajes relacionados.
- **IntelliJ IDEA**: muy utilizado para desarrollo web y proyectos que incluyen lenguajes de marcas como parte de sistemas más amplios.

- **NetBeans**: compatible con XML y HTML, ideal para desarrolladores Java que trabajan con lenguajes de marcas.
#### Herramientas específicas para lenguajes de marcas

Estas herramientas se diseñan exclusivamente para trabajar con documentos de un lenguaje de marcas concreto, ofreciendo características como validación y transformación.

**Ejemplos:**

- **Oxygen XML Editor**: completo y profesional, con soporte para XML, XSLT, XQuery y otros estándares.
- **XMLSpy**: orientado a la edición avanzada de XML, con herramientas de validación y diseño de esquemas.
- **Dreamweaver**: ideal para diseño web con soporte integrado para HTML, CSS y JavaScript.
#### Herramientas en línea

Estas herramientas consisten en soluciones basadas en la web que no requieren instalación. Son útiles para ediciones rápidas y validaciones.

**Ejemplos:**

- **CodePen**: perfecto para trabajar con HTML, CSS y JavaScript de forma colaborativa.
- **XML Validator**: útil para validar rápidamente la estructura de documentos XML.
- **JSFiddle**: similar a CodePen, con soporte para HTML y lenguajes relacionados.
#### Complementos de navegadores

Algunos navegadores y herramientas asociadas permiten editar y validar lenguajes de marcas directamente.

**Ejemplos:**

- **DevTools (Chrome, Firefox, Edge)**: herramientas integradas para inspeccionar y modificar HTML y CSS en tiempo real.
- **Firebug (obsoleto, pero precursor de DevTools)**: ayudaba a depurar HTML y CSS.
Tabla resumen con el tipo de tarea y la herramienta recomendada:

Tipo de tarea Herramienta recomendada

Edición básica Bloc de notas, Notepad++

Edición avanzada VS Code, Sublime Text

Proyectos complejos Eclipse, IntelliJ IDEA, NetBeans

Validación y transformación XML Oxygen XML Editor, XMLSpy

Diseño web Dreamweaver, CodePan

El uso de una herramienta u otra dependerá del nivel de complejidad del proyecto y de las necesidades específicas del usuario. Sin embargo, dominar al menos una herramienta básica y una avanzada es fundamental para trabajar con lenguajes de marcas de manera eficiente.

#### Complementos de navegadores

Algunos navegadores y herramientas asociadas permiten editar y validar lenguajes de marcas directamente.

**Ejemplos:**

- **DevTools (Chrome, Firefox, Edge)**: herramientas integradas para inspeccionar y modificar HTML y CSS en tiempo real.
- **Firebug (obsoleto, pero precursor de DevTools)**: ayudaba a depurar HTML y CSS.
Tabla resumen con el tipo de tarea y la herramienta recomendada:

#### Tipo de tarea Herramienta recomendada

|Edición básica|Bloc de notas, Notepad++|
|---|---|
|Edición avanzada|VS Code, Sublime Text|
|Proyectos complejos|Eclipse, IntelliJ IDEA, NetBeans|
|Validación y transformación XML|Oxygen XML Editor, XMLSpy|
|Diseño web|Dreamweaver, CodePan|

El uso de una herramienta u otra dependerá del nivel de complejidad del proyecto y de las necesidades específicas del usuario. Sin embargo, dominar al menos una herramienta básica y una avanzada es fundamental para trabajar con lenguajes de marcas de manera eficiente.

### 1.4. XML: estructura, sintaxis y etiquetas

El XML (eXtensible Markup Language) es un lenguaje de marcas que permite definir y estructurar datos de forma sencilla y legible tanto para humanos como para máquinas. Se utiliza ampliamente en aplicaciones web, bases de datos y sistemas de intercambio de información.

A continuación, se explican los conceptos básicos relacionados con su estructura, sintaxis y etiquetas.

#### Estructura de un documento XML

Este tipo de documento consta de varias partes principales que forman su estructura:

1. **Declaración XML (opcional, pero recomendada):** – Es la primera línea del documento y especifica la versión de XML y la codificación utilizada. **Ejemplo:** <?xml version="1.0" encoding="UTF-8"?>
2. **Elemento raíz:** – Es el contenedor principal de todos los elementos del documento. Solo puede haber un único elemento raíz. **Ejemplo:** <libro> <!-- Otros elementos --> </libro>
3. **Elementos secundarios:** – Representan las partes internas del documento y están anidados dentro del elemento raíz.

**Ejemplo:**

<libro> <titulo>Lenguaje de Marcas</titulo> <autor>Profesor Informática</autor> <editorial>Educación Digital</editorial> </libro>

4. **Atributos:** – Proporcionan información adicional sobre un elemento en forma de pares nombre="valor". **Ejemplo:** <libro categoria="educativo"> <titulo>Lenguaje de Marcas</titulo> </libro>
#### Sintaxis de XML

Para que un documento XML sea válido y esté bien formado, debe cumplir con una serie de reglas sintácticas:

1. **Cierre de etiquetas obligatorio:** – Cada etiqueta de apertura debe tener su correspondiente etiqueta de cierre. Correcto: <titulo>Lenguaje de Marcas</titulo> Incorrecto: <titulo>Lenguaje de Marcas
2. **Sensibilidad a mayúsculas y minúsculas:** – Las etiquetas son sensibles a las diferencias entre mayúsculas y minúsculas. Correcto: <Titulo>Texto</Titulo> Incorrecto: <titulo>Texto</Titulo>

3. **Anidación correcta:** – Las etiquetas deben estar correctamente anidadas. Correcto: <libro> <titulo>Lenguaje de Marcas</titulo> </libro> Incorrecto: <libro> <titulo>Lenguaje de Marcas</libro></titulo>
4. **Uso de atributos entre comillas:** – Los valores de los atributos deben estar entre comillas dobles o simples. Correcto: <libro categoria="educativo"></libro> Incorrecto: <libro categoria=educativo></libro>
5. **Declaración del carácter raíz único:** – Un documento XML debe tener un único elemento raíz que contenga todos los demás elementos.
#### Etiquetas en XML

Las etiquetas son el núcleo de XML y se utilizan para identificar y organizar los datos.

1. **Etiquetas de apertura y cierre:** – Una etiqueta de apertura (<etiqueta>) se combina con una etiqueta de cierre (</etiqueta>). **Ejemplo:** <nombre>Juan</nombre>

2. **Etiquetas autocerradas:** – Se usan para elementos que no contienen datos o hijos. **Ejemplo:** <imagen src="foto.jpg" />
3. **Nombres de etiquetas:** – Deben comenzar con una letra o un guión bajo (_). – No pueden contener espacios, empezar con números o incluir caracteres especiales. Correcto: <libro></libro> Incorrecto: <123libro></123libro>
#### Ejemplo de documento XML completo:

<?xml version="1.0" encoding="UTF-8"?> <biblioteca> <libro categoria="educativo"> <titulo>Lenguaje de Marcas</titulo> <autor>Profesor Informática</autor> <editorial>Educación Digital</editorial> <publicacion año="2024" /> </libro> <libro categoria="novela"> <titulo>La Odisea</titulo> <autor>Homero</autor> <editorial>Clásicos Griegos</editorial> <publicacion año="800 AC" /> </libro> </biblioteca>

El XML es una herramienta poderosa y flexible empleada habitualmente para estructurar información. Su sintaxis sencilla y sus reglas claras permiten que este lenguaje sea ampliamente utilizado en múltiples aplicaciones, desde configuraciones de software hasta intercambios de datos entre sistemas. Dominar su estructura, sintaxis y etiquetas es el primer paso para trabajar eficazmente con este lenguaje.

### 1.5. Elaboración de documentos XML bien formados

Un documento XML bien formado es aquel que cumple con todas las reglas sintácticas del lenguaje XML, asegurando que pueda ser procesado correctamente por cualquier parser XML.

A continuación, se presentan las claves para crear documentos XML bien formados.

#### Pasos para elaborar un documento XML bien formado

1. **Planificar la estructura del documento:**
#### – Identificar el elemento raíz.

  - Definir los elementos secundarios y sus relaciones jerárquicas.

  - Decidir qué datos irán como atributos y cuáles como contenido.

2. **Escribir la declaración XML:** – Definir la versión de XML y la codificación que se usará: <?xml version="1.0" encoding="UTF-8"?>
3. **Crear el elemento raíz:** – El elemento raíz debe englobar todos los demás elementos. **Ejemplo:** <biblioteca> <!-- Contenido aquí --> </biblioteca>
4. **Añadir elementos y atributos:** – Utilizar etiquetas para cada elemento y atributos para datos complementarios. **Ejemplo:** <libro categoria="educativo"> <titulo>Lenguaje de Marcas</titulo> <autor>Tever</autor> </libro>

5. **Validar la sintaxis:** – Asegurarse de que no hay errores en la anidación de etiquetas, cierre de elementos o uso de atributos.
#### Ejemplo de documento XML bien formado:

<?xml version="1.0" encoding="UTF-8"?> <biblioteca> <libro categoria="educativo"> <titulo>Lenguaje de Marcas</titulo> <autor>Tever</autor> <editorial>Educación Digital</editorial> <publicacion año="2024" /> </libro> <libro categoria="ficción"> <titulo>La Odisea</titulo> <autor>Homero</autor> <editorial>Clásicos Griegos</editorial> <publicacion año="800 AC" /> </libro> </biblioteca>

#### Validación de un documento XML

Aunque un documento bien formado cumple con las reglas sintácticas, puede resultar útil validarlo para garantizar que sigue un esquema específico o DTD (Document Type Definition). Herramientas como Oxygen XML Editor o validadores en línea pueden facilitar este proceso.

Un documento bien formado es el punto de partida para utilizar XML de manera eficiente, asegurando que sea interoperable y compatible con diferentes aplicaciones y sistemas.

### 1.6. El espacio de nombres en XML

El espacio de nombres en XML (o XML Namespace) es una característica que permite evitar conflictos entre nombres de elementos y atributos en un documento XML cuando se combinan vocabularios de diferentes fuentes. Esto se logra utilizando identificadores únicos, generalmente en forma de URIs (Uniform Resource Identifiers).

**¿Por qué es necesario el espacio de nombres en XML?**

Cuando un documento XML utiliza múltiples vocabularios (por ejemplo, elementos de diferentes estándares o sistemas), puede haber conflictos si dos elementos o atributos tienen el mismo nombre, pero significados distintos. El espacio de nombres ayuda a diferenciar estos elementos y evita ambigüedades.

**Declaración del espacio de nombres**

Un espacio de nombres se declara utilizando el atributo `xmlns` (abreviatura de XML Namespace) en un elemento. Se puede aplicar a:

1. Un elemento y sus descendientes.
2. Atributos específicos mediante un prefijo.

#### Tipos de declaraciones de espacios de nombres

#### Espacio de nombres predeterminado

Se declara sin un prefijo y se aplica a todos los elementos del nivel en el que se define y sus descendientes.

**Ejemplo:**

<libro xmlns="[http://www.ejemplo.com/libros"](http://www.ejemplo.com/libros")> <titulo>Lenguaje de Marcas</titulo> <autor>Profesor de Informática</autor> </libro>

#### Espacio de nombres con prefijo

Se declara con un prefijo que se asocia al URI del espacio de nombres, permitiendo su uso explícito en los elementos.

**Ejemplo:**

<biblioteca xmlns:lib="[http://www.ejemplo.com/li-](http://www.ejemplo.com/li-) bros"> <lib:libro> <lib:titulo>Lenguaje de Marcas</lib:titulo> </lib:libro> </biblioteca>

#### Uso de espacios de nombres en atributos

Los espacios de nombres no se aplican automáticamente a los atributos, excepto cuando se utilizan prefijos explícitos.

Correcto:

<lib:libro xmlns:lib="[http://www.ejemplo.com/libros"](http://www.ejemplo.com/libros")> <lib:titulo>Lenguaje de Marcas</lib:titulo> <lib:autor categoria="educativo">Tever</lib:autor> </lib:libro>

Incorrecto:

<lib:libro xmlns:lib="[http://www.ejemplo.com/libros"](http://www.ejemplo.com/libros")> <lib:titulo>Lenguaje de Marcas</lib:titulo> <!-- Sin prefijo, no está en el espacio de nombres --> <autor categoria="educativo">Profesor Informática</autor> </lib:libro>

#### Resolución de conflictos

El uso de prefijos permite combinar elementos de diferentes vocabularios sin conflictos.

#### Ejemplo con dos espacios de nombres:

<documento xmlns:lib="[http://www.ejemplo.com/libros"](http://www.ejemplo.com/libros") xmlns:rev="[http://www.ejemplo.com/revistas"](http://www.ejemplo.com/revistas")> <lib:libro> <lib:titulo>Lenguaje de Marcas</lib:titulo> <lib:autor>Tever</lib:autor> </lib:libro> <rev:revista> <rev:titulo>Programación Moderna</rev:titulo> <rev:editor>Revistas Digitales</rev:editor> </rev:revista> </documento>

#### Espacios de nombres y XML Schema

Cuando se valida un documento XML con un esquema (XML Schema), los espacios de nombres son esenciales para garantizar que los elementos se interpreten correctamente.

Ejemplo de esquema con espacio de nombres:

<xs:schema xmlns:xs="[http://www.w3.org/2001/XMLSche-](http://www.w3.org/2001/XMLSche-) ma" targetNamespace="[http://www.ejemplo.com/](http://www.ejemplo.com/) libros" xmlns="[http://www.ejemplo.com/libros"](http://www.ejemplo.com/libros") elementFormDefault="qualified">

<xs:element name="libro"> <xs:complexType> <xs:sequence> <xs:element name="titulo" type="xs:string"/> <xs:element name="autor" type="xs:string"/> </xs:sequence> </xs:complexType> </xs:element> </xs:schema>

#### Ventajas del uso de espacios de nombres

- **Evita conflictos:** – Permite que múltiples vocabularios coexistan en un solo documento XML.
- **Claridad semántica:** – Cada elemento o atributo está claramente identificado y asociado a un vocabulario específico.
- **Compatibilidad con estándares:** – Facilita la interoperabilidad entre sistemas y aplicaciones.
#### Errores comunes al usar espacios de nombres

- **No declarar el espacio de nombres:** – Resultado: el documento puede no ser válido.
- **Usar prefijos no declarados:** – Resultado: el parser XML no reconocerá los elementos o atributos.
- **Declaraciones mal ubicadas:** – Los espacios de nombres deben declararse en el elemento correcto para aplicarse adecuadamente.
Los espacios de nombres en XML son esenciales para trabajar con documentos complejos que combinan diferentes vocabularios. Su correcta implementación asegura que los datos sean interpretados sin ambigüedades y facilita su uso en sistemas distribuidos y aplicaciones interoperables.