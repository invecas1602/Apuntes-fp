# Tema 6. Gestión y almacenamiento de información en XML

Los sistemas de almacenamiento de información XML permiten gestionar documentos estructurados de manera eficiente, utilizando diferentes enfoques según las necesidades. Los documentos XML pueden guardarse como archivos en el sistema, lo que resulta sencillo pero poco escalable. Otra opción es almacenarlos en bases de datos relacionales, ya sea como texto en una columna XML o descomponiendo su estructura en tablas. Sin embargo, para documentos más complejos, las bases de datos nativas XML, como BaseX o eXist-db, ofrecen mejores herramientas de consulta mediante XPath y XQuery. También pueden almacenarse en bases de datos NoSQL, convirtiéndolos a formatos como JSON.

Las bases de datos relacionales han integrado compatibilidad con XML, permitiendo almacenar y consultar documentos dentro de su estructura tabular. SQL Server, MySQL y Oracle ofrecen funciones avanzadas para manipular XML con XPath y XQuery. Sin embargo, este método puede ser menos eficiente que el uso de bases nativas.

Para la búsqueda de información en documentos XML, se utilizan lenguajes como XPath y XQuery, que permiten navegar por la jerarquía del documento y extraer datos de manera flexible. Estas herramientas hacen que XML sea una solución versátil para almacenar y consultar información estructurada en múltiples entornos.

### 6.1. Sistemas de almacenamiento de información XML

Los documentos XML se utilizan comúnmente para estructurar y transportar datos, pero su almacenamiento requiere sistemas especializados que garanticen su organización, consulta y manejo eficiente. Los sistemas de **almacenamiento de información XML son herramientas y tecnologías** diseñadas para guardar y gestionar documentos XML de manera óptima.

#### Tipos de sistemas de almacenamiento para XML

#### Almacenamiento como archivo

- **Descripción: los documentos XML se almacenan como archivos** en el sistema de archivos.
- **Ventajas:**
#### – Fácil de implementar y manejar.

  - Ideal para documentos XML pequeños o de uso ocasional.

- **Limitaciones:** – Difícil de escalar con grandes volúmenes de datos.
#### – Consultas complejas requieren procesamiento adicional.

**Ejemplo:**

Un archivo biblioteca.xml almacenado en el sistema de archivos:

<biblioteca> <libro> <titulo>Lenguajes de Marcas</titulo> <autor>Pablo García</autor> </libro> </biblioteca>

#### Almacenamiento en bases de datos relacionales

- **Descripción: las bases de datos relacionales almacenan documen-** tos XML en tablas, ya sea como texto completo o descompuestos en columnas.
- **Métodos comunes:** – **Columna XML: el documento XML se almacena como una ca-** dena de texto. – **Mapeo relacional: los elementos XML se descomponen en ta-** blas y columnas.
- **Ventajas:** – Compatibilidad con bases de datos existentes.
#### – Uso de SQL para consultas.

- **Limitaciones:** – El mapeo relacional puede ser complejo para XML con estructuras anidadas.
#### Ejemplo de almacenamiento en SQL Server:

CREATE TABLE Biblioteca ( ID INT PRIMARY KEY, Datos XML );

INSERT INTO Biblioteca (ID, Datos) VALUES (1, '<libro><titulo>Lenguajes de Marcas</titulo><autor>Pablo García</autor></libro>');

#### Bases de datos nativas XML

- **Descripción: estas bases de datos están diseñadas específicamente** para almacenar y gestionar documentos XML en su formato nativo.
- **Ejemplos:** – **BaseX: base de datos ligera y eficiente para XML.** – **eXist-db: soporta consultas avanzadas con XQuery.** – **MarkLogic: orientada a la gestión de grandes volúmenes de** datos XML.
- **Ventajas:**
#### – Manejo directo del formato XML.

  - Soporte para consultas específicas como XPath y XQuery.

  - Ideal para estructuras XML complejas y jerárquicas.

- **Limitaciones:**
#### – Requiere infraestructura especializada.

  - Menos común que las bases de datos relacionales.

- **Ejemplo en MongoDB:** { "biblioteca": { "libro": { "titulo": "Lenguajes de Marcas", "autor": "Pablo García" } } }
#### Almacenamiento en bases de datos NoSQL

- **Descripción: bases de datos orientadas a documentos, como Mon-** goDB o CouchDB, pueden almacenar XML convirtiéndolo a JSON.
- **Ventajas:**
#### – Escalabilidad y flexibilidad.

#### – Compatibilidad con aplicaciones modernas.

- **Limitaciones:** – Requiere conversión de XML a JSON para almacenamiento.

#### Consultas en sistemas de almacenamiento XML

#### Consultas con XPath

- XPath es un lenguaje que permite navegar por la estructura jerárquica de un documento XML.
#### Ejemplo: obtener todos los títulos de un documento XML.

/biblioteca/libro/titulo

#### Consultas con XQuery

- XQuery es un lenguaje más potente que XPath, utilizado para consultas avanzadas.
**Ejemplo:**

for $libro in /biblioteca/libro return $libro/titulo

#### Consultas en bases de datos relacionales

Uso de SQL para extraer datos XML almacenados.

SELECT Datos.value('(/libro/titulo)[1]', 'VARCHAR(- MAX)') FROM Biblioteca

#### Factores a considerar al elegir un sistema de almacenamiento XML

#### Volumen de datos

- Archivos individuales funcionan para volúmenes pequeños.
- Bases de datos nativas o NoSQL son mejores para grandes volúmenes.
#### Frecuencia de consultas

- Consultas frecuentes o complejas requieren bases de datos nativas o relacionales.
#### Estructura del XML

- Documentos muy anidados son más fáciles de manejar en bases de datos nativas.

**Escalabilidad**

- Bases de datos NoSQL o nativas ofrecen mayor escalabilidad que los archivos.
#### Ventajas de los sistemas de almacenamiento XML

- **Flexibilidad: permiten almacenar datos complejos y jerárquicos.**
- **Interoperabilidad: facilitan el intercambio de información entre** diferentes sistemas.
- **Consultas avanzadas: XPath, XQuery y SQL permiten extraer da-** tos de manera eficiente.
- **Compatibilidad con tecnologías modernas: bases de datos NoS-** QL y nativas son ideales para aplicaciones actuales.
#### Ejemplo práctico:

#### Almacenamiento en eXist-db

#### Subir el documento XML:

#### Archivo biblioteca.xml:

<biblioteca> <libro> <titulo>Lenguajes de Marcas</titulo> <autor>Pablo García</autor> </libro> </biblioteca>

#### Consultar con XQuery:

for $libro in /biblioteca/libro return <titulo>{$libro/titulo/text()}</titulo>

Los sistemas de almacenamiento de información XML ofrecen soluciones adaptadas a diferentes necesidades, desde archivos simples hasta bases de datos especializadas. Elegir el sistema adecuado depende del volumen de datos, la complejidad de las consultas y la escalabilidad requerida. Gracias a tecnologías como bases de datos nativas XML y lenguajes de consulta como XPath y XQuery, el manejo de documentos XML es eficiente y versátil en entornos modernos.

### 6.2. BBDD relacionales con XML

Las bases de datos relacionales (BBDD relacionales) son sistemas diseñados para almacenar y gestionar datos estructurados en tablas. Aunque estas bases de datos no están diseñadas específicamente para trabajar con XML, han integrado capacidades para almacenar, consultar y procesar documentos XML, facilitando su uso en entornos que combinan datos relacionales y jerárquicos.

**Métodos para trabajar con XML en bases de datos relacionales**

- **Almacenamiento como texto**: los documentos XML se guardan como cadenas en columnas de tipo TEXT o VARCHAR.
- **Columna de tipo XML**: algunas bases de datos, como SQL Server y DB2, tienen un tipo de dato específico para XML. Esto permite validar y consultar documentos XML directamente.
- **Descomposición de XML**: los datos del XML se descomponen en tablas relacionales, facilitando consultas SQL estándar.

**Ventajas del uso de XML en bases de datos relacionales**

- **Interoperabilidad**: permite almacenar datos jerárquicos junto con datos relacionales en un mismo sistema.
- **Flexibilidad**: soporta documentos XML de tamaños y estructuras variables.
- **Consultas avanzadas**: integración con lenguajes como XPath o XQuery para consultas específicas dentro de XML.
- **Validación**: en algunos sistemas, se pueden validar documentos XML con esquemas como XSD.

**Implementaciones comunes**

#### SQL Server

Tipo de dato XML: SQL Server incluye el tipo de dato XML para almacenar y manipular documentos XML.

#### Ejemplo de creación de tabla:

CREATE TABLE Biblioteca ( ID INT PRIMARY KEY, Documento XML );

#### Inserción de datos XML:

INSERT INTO Biblioteca (ID, Documento) VALUES (1, '<libro><titulo>Lenguajes de Marcas</titulo><autor>Pablo García</autor></libro>');

#### Consulta de datos XML:

SELECT Documento.value('(/libro/titulo)[1]', 'VAR- CHAR(MAX)') AS Titulo FROM Biblioteca WHERE ID = 1;

**MySQL**

En MySQL, los documentos XML suelen almacenarse como cadenas en columnas de tipo TEXT o LONGTEXT.

#### Ejemplo de creación de tabla:

CREATE TABLE Biblioteca ( ID INT PRIMARY KEY, Documento LONGTEXT );

#### Consulta de datos XML con XPath: desde la versión 5.1, MySQL permite realizar consultas XPath usando la función ExtractValue.

**Ejemplo:**

SELECT ExtractValue(Documento, '/libro/titulo') AS Titulo FROM Biblioteca WHERE ID = 1;

**Oracle**

Oracle incluye un tipo de dato XMLTYPE, que permite almacenar y consultar XML directamente.

#### Ejemplo de creación de tabla:

CREATE TABLE Biblioteca ( ID NUMBER PRIMARY KEY, Documento XMLTYPE );

#### Consulta con XPath:

SELECT EXTRACT(Documento, '/libro/titulo/text()') AS Titulo FROM Biblioteca WHERE ID = 1;

#### Consultas avanzadas con XML

#### Uso de XPath

Navega por la estructura del XML para extraer elementos específicos.

#### Ejemplo: obtener el título de un libro.

/libro/titulo

#### Uso de XQuery

Permite realizar transformaciones y consultas más complejas.

**Ejemplo:**

for $libro in /biblioteca/libro return $libro/titulo

#### Consultas mixtas con SQL y XML

#### Ejemplo en SQL Server:

SELECT Documento.query('/libro') FROM Biblioteca WHERE ID = 1;

#### Limitaciones del uso de XML en BBDD relacionales

- **Sobrecarga de almacenamiento: los documentos XML grandes** pueden ocupar mucho espacio en la base de datos.
- **Consultas complejas: las consultas a documentos XML dentro de** una base relacional pueden ser más lentas que las consultas a datos tabulares.
- **Compatibilidad: no todas las bases de datos relacionales tienen** soporte avanzado para XML.
#### Ejemplo práctico

#### Crear y consultar documentos XML en SQL Server:

#### Crear tabla con columna XML:

CREATE TABLE Biblioteca ( ID INT PRIMARY KEY, Documento XML );

#### Insertar un documento XML:

INSERT INTO Biblioteca (ID, Documento) VALUES (1, '<libro><titulo>Lenguajes de Marcas</titulo><autor>Pablo García</autor></libro>');

#### Consultar un valor específico del XML:

SELECT Documento.value('(/libro/titulo)[1]', 'VAR- CHAR(MAX)') AS Titulo FROM Biblioteca WHERE ID = 1;

#### Extraer todo el documento XML:

SELECT Documento.query('/libro') FROM Biblioteca;

**Conclusión**

El uso de XML en bases de datos relacionales combina lo mejor de ambos mundos: la organización tabular de las bases de datos y la flexibilidad jerárquica de XML. Aunque no siempre es la solución más eficiente, esta integración es valiosa para aplicaciones que requieren trabajar con ambos tipos de datos. Herramientas como SQL Server, MySQL y Oracle proporcionan un soporte robusto para manejar documentos XML dentro del ecosistema relacional.

### 6.3. Búsqueda de Información en Documentos XML

La búsqueda de información en documentos XML se realiza utilizando lenguajes y técnicas diseñados para navegar, extraer y manipular los datos almacenados en su estructura jerárquica. Entre los métodos más comunes están XPath, XQuery y las consultas específicas en bases de datos que soportan XML.

#### Métodos principales para buscar información en XML

#### XPath (XML Path Language)

#### XPath es un lenguaje de consulta que permite navegar por la estructura

jerárquica de un documento XML para localizar elementos, atributos o valores específicos.

- **Características principales:**
#### – Selección precisa de nodos.

#### – Navegación a través de jerarquías.

  - Soporte para expresiones lógicas y filtros.

- **Ejemplo básico: dado el siguiente XML:** <biblioteca> <libro> <titulo>Lenguajes de Marcas</titulo> <autor>Pablo García</autor> </libro> <libro> <titulo>Diseño Web</titulo> <autor>Laura Sánchez</autor> </libro> </biblioteca>

#### – Seleccionar todos los títulos:

/biblioteca/libro/titulo

**Resultado:**

<titulo>Lenguajes de Marcas</titulo> <titulo>Diseño Web</titulo>

  - **Obtener el autor del segundo libro:**

/biblioteca/libro[2]/autor

**Resultado:**

<autor>Laura Sánchez</autor>

  - **Seleccionar libros cuyo título contenga "Diseño":**

/biblioteca/libro[contains(titulo, 'Diseño')]

#### XQuery (XML Query Language)

#### XQuery es un lenguaje más avanzado que permite realizar búsquedas

y transformaciones en documentos XML. Extiende las capacidades de XPath, permitiendo manipular datos y generar nuevos documentos XML.

- **Ejemplo básico de XQuery:**
#### Documento XML:

<biblioteca> <libro> <titulo>Lenguajes de Marcas</titulo> <autor>Pablo García</autor> </libro> <libro> <titulo>Diseño Web</titulo> <autor>Laura Sánchez</autor> </libro> </biblioteca>

  - **XQuery para obtener los títulos de todos los libros:**

for $libro in /biblioteca/libro return $libro/titulo

**Resultado:**

<titulo>Lenguajes de Marcas</titulo> <titulo>Diseño Web</titulo>

#### – Crear una lista de autores:

<autores> { for $autor in /biblioteca/libro/autor return <autor>{$autor/text()}</autor> } </autores>

**Resultado:**

<autores> <autor>Pablo García</autor> <autor>Laura Sánchez</autor> </autores>

#### Consultas en bases de datos XML

- **SQL Server:**
#### Consulta de un nodo específico:

SELECT Documento.value('(/biblioteca/libro/titulo) [1]', 'VARCHAR(MAX)') AS Titulo FROM Biblioteca WHERE ID = 1;

- **MySQL:**
#### Uso de ExtractValue para extraer datos:

SELECT ExtractValue(Documento, '/biblioteca/libro/ titulo') AS Titulo FROM Biblioteca;

- **Oracle:**
#### Consulta con EXTRACT:

SELECT EXTRACT(Documento, '/biblioteca/libro/titulo/ text()') AS Titulo FROM Biblioteca;

#### Ejemplo práctico de búsqueda

**XML:**

<biblioteca> <libro> <titulo>Lenguajes de Marcas</titulo> <autor>Pablo García</autor> <año>2025</año> </libro> <libro> <titulo>Diseño Web</titulo> <autor>Laura Sánchez</autor> <año>2023</año> </libro> </biblioteca>

#### Consultas XPath:

Obtener todos los libros publicados después de 2024:

/biblioteca/libro[año > 2024]

Obtener el título y autor de todos los libros:

/biblioteca/libro/(titulo|autor)

#### Herramientas para búsqueda en XML

- **Editores y validadores XML:** – Oxygen XML Editor – XMLSpy
- **Herramientas en línea:** – FreeFormatter XML Tools
- **Lenguajes de programación:** – **Python: Librerías como xml.etree.ElementTree, lxml** – **JavaScript: DOMParser, XPathEvaluator** – **Java: JAXP, DOM**

#### Ventajas de las búsquedas en XML

- **Precisión: XPath y XQuery permiten localizar elementos específicos** dentro de documentos complejos.
- **Flexibilidad: se pueden aplicar filtros avanzados y transformaciones** en los datos.
- **Compatibilidad: la mayoría de bases de datos relacionales y** herramientas modernas soportan búsquedas en XML.
La búsqueda de información en documentos XML es una tarea fundamental para extraer datos relevantes y utilizarlos en diferentes contextos. Herramientas como XPath y XQuery, junto con lenguajes de programación y bases de datos, permiten consultas eficientes y transformaciones avanzadas, haciendo de XML una tecnología versátil en la gestión de datos jerárquicos.

#### Ventajas de las búsquedas en XML

- **Precisión: XPath y XQuery permiten localizar elementos específicos** dentro de documentos complejos.
- **Flexibilidad: se pueden aplicar filtros avanzados y transformaciones** en los datos.
- **Compatibilidad: la mayoría de bases de datos relacionales y** herramientas modernas soportan búsquedas en XML.
La búsqueda de información en documentos XML es una tarea fundamental para extraer datos relevantes y utilizarlos en diferentes contextos. Herramientas como XPath y XQuery, junto con lenguajes de programación y bases de datos, permiten consultas eficientes y transformaciones avanzadas, haciendo de XML una tecnología versátil en la gestión de datos jerárquicos.