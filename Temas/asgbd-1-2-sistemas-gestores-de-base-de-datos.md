# **1.2. Sistemas gestores de base de datos**

### **1.2.1. Características de un sistema gestor de bases de datos (SGBD)**

Las características **básicas** de un SGBD son**:**

- **Independencia de datos**: permite separar los datos de las aplicaciones que los usan, permitiendo modificar la estructura de las bases de datos sin afectar las aplicaciones.
- **Control de redundancia de datos**: evita la duplicación innecesaria de datos, mejorando la eficiencia y el uso del espacio.
- **Acceso a múltiples usuarios**: proporciona control de concurrencia para que varios usuarios puedan acceder y modificar datos de manera simultánea sin conflictos.
- **Seguridad de datos**: garantiza la protección de los datos mediante restricciones de acceso basadas en permisos.
- **Control de integridad de datos**: establece restricciones para mantener la validez y consistencia de los datos almacenados en la base.
- **Lenguaje de consulta estandarizado (SQL)**: un SGBD debe soportar el lenguaje de consultas estructuradas (SQL) para la manipulación y gestión de bases de datos.
- **Manejo de transacciones**: proporciona mecanismos para garantizar que las transacciones de base de datos sean completas, correctas y persistentes (ACID: Atomicidad, Consistencia, Aislamiento, Durabilidad).

Las características **avanzadas** de un SGBD son**:**

- **Soporte para datos no relacionales**: capacidad para manejar tipos de datos no estructurados o semi-estructurados, como JSON o XML, además de los datos relacionales.
- **Soporte para bases de datos distribuidas**: permite que los datos estén distribuidos en múltiples servidores o ubicaciones, gestionando la coherencia y el acceso de manera eficiente.
- **Optimización de consultas**: los SGBD avanzados incluyen mecanismos para optimizar el tiempo de respuesta de las consultas a través de la creación de índices, uso de estadísticas y planes de ejecución eficientes.
- **Almacenamiento y procesamiento de datos en memoria**: algunos SGBD pueden manejar los datos en la memoria principal para un acceso más rápido, mejorando el rendimiento.

- **Sistemas de replicación y alta disponibilidad**: los SGBD avanzados permiten replicar bases de datos entre diferentes servidores para mejorar la disponibilidad y la tolerancia a fallos.
- **Soporte para Big Data**: los sistemas modernos soportan grandes volúmenes de datos (Big Data) y trabajan con herramientas y tecnologías como Hadoop o Spark para procesar esos datos a gran escala.
- **Integración con herramientas analíticas**: los SGBD avanzados permiten realizar consultas analíticas avanzadas y análisis en tiempo real, proporcionando herramientas de Business Intelligence (BI).
- **Compatibilidad con transacciones distribuidas**: permite ejecutar y coordinar transacciones a través de múltiples bases de datos o sistemas distribuidos, garantizando la coherencia.

**phpMyAdmin** es una herramienta popular que permite administrar bases de datos MySQL a través de una interfaz gráfica. A continuación, se describen los pasos básicos para crear una base de datos en MySQL utilizando phpMyAdmin:

### 1. **Acceso a phpMyAdmin**

- Abre phpMyAdmin en tu navegador web (normalmente está disponible a través de http://localhost/phpmyadmin si estás trabajando en un servidor local).
- Inicia sesión con tus credenciales (usuario y contraseña de MySQL).

### 2. **Crear una nueva base de datos**

- Una vez que hayas iniciado sesión, selecciona la opción *Base de datos* en la parte superior.
- En la sección *Crear base de datos*, ingresa el nombre de la base de datos que deseas crear. Por ejemplo, puedes nombrarla mi\_base\_datos.
- Selecciona el **conjunto de caracteres (collation)** que prefieras. Generalmente, utf8\_general\_ci es una buena opción para evitar problemas de codificación. –Haz clic en el botón *Crear*.

### 3. **Crear tablas en la base de datos**

- Una vez creada la base de datos, serás redirigido automáticamente a la página donde puedes crear tablas.
- Ingresa el nombre de la tabla, por ejemplo, usuarios, y especifica el número de columnas que tendrá la tabla. –Haz clic en *Continuar*.

### 4. **Definir estructura de la tabla**

- Especifica el nombre de cada columna, el tipo de datos (como INT, VARCHAR, TEXT, DATE, etc.), el tamaño y cualquier atributo adicional.
- Establece la columna clave primaria (Primary Key) marcando la opción *A\_I* (Auto Increment) para un campo de tipo INT, que podría ser el id de la tabla.
- Una vez que hayas ingresado todos los campos y configuraciones, haz clic en *Guardar*.

### 5. **Insertar datos**

- –Haz clic en la tabla que acabas de crear (por ejemplo, usuarios), y selecciona la pestaña *Insertar*.
- Ingresa los datos para las columnas correspondientes y haz clic en *Continuar* para guardar los registros.

### 6. **Ejecutar consultas SQL**

- También puedes realizar consultas SQL directamente desde la pestaña *SQL*.

Por ejemplo, puedes insertar datos utilizando una consulta SQL como:

INSERT INTO usuarios (nombre, correo) VALUES ('Juan', 'juan@example.com');

### 7. **Gestionar la base de datos**

- Puedes realizar varias acciones, como modificar tablas, crear índices, exportar bases de datos, importar archivos .sql, y mucho más a través de las herramientas integradas en phpMyAdmin.

Una de las características avanzadas que podemos aplicar en MySQL a través de phpMyAdmin es la **optimización de consultas mediante la creación de índices**. Esto mejora significativamente el rendimiento de las consultas SQL, ya que los índices permiten que el SGBD acceda a los datos de manera más eficiente.

Por otra parte, los **índices** permiten al sistema gestor de bases de datos (SGBD) localizar rápidamente los registros en una tabla sin necesidad de revisar todas las filas. Los índices son útiles para columnas que se utilizan frecuentemente en las condiciones WHERE, JOIN, GROUP BY o ORDER BY de las consultas SQL.

### 1. **Seleccionar la tabla**

- Una vez dentro de phpMyAdmin, selecciona la base de datos en la que deseas trabajar.
- En la lista de tablas, haz clic en la tabla donde deseas crear el índice.

### 2. **Ir a la estructura de la tabla**

–Después de seleccionar la tabla, dirígete a la pestaña *Estructura*.

### 3. **Añadir un índice**

- En la parte inferior de la página de estructura, verás una sección llamada *Índices*. –Haz clic en el enlace *Añadir índice*.

### 4. **Seleccionar las columnas para el índice**

- Se abrirá un cuadro de diálogo donde podrás seleccionar una o más columnas sobre las que deseas crear el índice.
- Si estás indexando una columna que contiene valores únicos (como el número de identificación de un usuario o una dirección de correo electrónico), puedes seleccionar la opción *único* para garantizar que no haya valores duplicados.
- Especifica el tipo de índice que deseas crear:
  - **INDEX**: índice estándar para mejorar la búsqueda.
  - **UNIQUE**: garantiza que todos los valores del índice sean únicos.
  - **FULLTEXT**: se usa para búsquedas avanzadas de texto (solo para columnas de tipo texto).
  - **PRIMARY**: define una clave primaria (si aún no existe).

### 5. **Guardar el índice**

- Una vez que hayas seleccionado las columnas y el tipo de índice, haz clic en *Guardar*.
- phpMyAdmin creará el índice y lo mostrará en la sección de índices de la tabla.

Vamos a verlo con un ejemplo: supongamos que tienes una tabla llamada clientes y deseas crear un índice sobre la columna apellido, ya que con frecuencia realizas búsquedas o consultas filtradas por este campo.

- 1. Ve a la base de datos que contiene la tabla clientes.
- 2. Selecciona la tabla clientes y ve a la pestaña *Estructura*.
- 3. Haz clic en *Añadir índice*.

- 4. Selecciona la columna apellido en el cuadro de diálogo.
- 5. Elige el tipo de índice (en este caso, un **INDEX** normal).
- 6. Haz clic en *Guardar*.

Ahora, las consultas que utilicen la columna apellido en una cláusula WHERE o ORDER BY serán más rápidas porque MySQL utilizará el índice creado para buscar los registros más eficientemente.

### **Consultas optimizadas**

Después de crear el índice, si ejecutas una consulta como la siguiente, la búsqueda será mucho más rápida:

sql

Copiar código

SELECT \* FROM clientes WHERE apellido = 'García';

El índice que creaste acelerará esta consulta, ya que MySQL utilizará el índice para buscar directamente los registros en lugar de revisar toda la tabla.

Las ventajas del uso de índices son:

- **Mejora de la velocidad de búsqueda**: las consultas que buscan valores en las columnas indexadas se ejecutan mucho más rápido.
- **Mejora en las consultas de clasificación**: las columnas utilizadas en cláusulas ORDER BY también se benefician de la presencia de un índice.

Sin embargo, **los índices también tienen algunas desventajas**. Por ejemplo, ocupan espacio adicional en disco y pueden ralentizar las operaciones de inserción o actualización de datos, ya que MySQL necesita actualizar los índices cada vez que se modifican los datos.

### **1.2.2. Funciones de un SGBD**

![](_page_14_Picture_2.jpeg)

Los **sistemas gestores de bases de datos**, o SGBD, son las aplicaciones que nos permiten crear, gestionar y acceder a la información almacenada en las BD. Para insertar, modificar u obtener datos de una BD se emplea un mecanismo denominado consulta, que es una solicitud realizada al SGBD utilizando un lenguaje determinado. Uno de los lenguajes de consulta más populares es el SQL, aunque existen muchos otros.

En concreto, las principales funciones que desempeña un SGBD son las siguientes:

- Permite separar los datos almacenados del programa que los gestiona y proporciona a los datos **independencia física y lógica**.
- Permite a sus usuarios realizar de forma eficiente las cuatro operaciones fundamentales sobre la BD, **creación o inserción**, **modificación**, **eliminación y consulta**, tanto a nivel estructural como de los datos en sí.
- Permite el **acceso seguro** a los datos y a las funciones propias del SGBD.
- Permite el **uso concurrente**, es decir, por parte de múltiples usuarios al mismo tiempo, de la BD.
- Almacena en un catálogo, también llamado **diccionario de datos**, el esquema de la BD, en el cual se describen, entre otras cosas, las características de los datos (nombre, tipo, tamaño…), las restricciones a aplicar, las relaciones que se dan entre ellos, los usuarios a los que se permite el acceso e información estadística sobre el uso de la BD.
- Proporciona mecanismos para **manejar y mostrar los datos** de la BD de múltiples formas, con un alto nivel de complejidad y mediante un sencillo lenguaje de consultas.
- Minimiza los datos redundantes o inconsistentes mediante la aplicación de **condiciones y reglas**.
- Protege la **disponibilidad e integridad** de los datos mediante **copias de seguridad**.

- Proporciona las características de integración necesarias para que los usuarios puedan acceder a la BD a través de **aplicaciones cliente**.
- Proporciona una **interfaz de administración** y un conjunto de **herramientas de software** que facilitan la gestión eficiente de todas las funciones anteriormente descritas, además de la **monitorización y la optimización** del propio SGBD.

### **1.2.3. Arquitectura de un SGBD**

La separación entre los datos almacenados en la BD y el SGBD que nos permite manejarlos se basa en la existencia de una determinada **arquitectura**, entendiendo como tal un esquema organizativo y funcional basado en diferentes capas o **niveles de abstracción**, cada cual con sus características específicas.

Si bien existen diferentes criterios a la hora de diseñar la arquitectura de un sistema informático, lo más habitual es que las capas inferiores sean las más próximas al hardware físico y las superiores las más cercanas al software de aplicación y las interfaces de usuario. Este es también el enfoque de la arquitectura propuesta conjuntamente, en 1975, por el instituto ANSI (American National Strandard Institute) y el comité SPARC (Standards Planning and Requirements Committee).

De esta forma, la llamada arquitectura ANSI/SPARC para sistemas de bases de datos, propone un esquema de tres niveles o capas de abstracción.

### **La arquitectura ANSI/SPARC**

El nivel inferior de la arquitectura ANSI/SPARC, denominado **nivel interno**, es el que concierne al **almacenamiento físico** de los datos, es decir, a la forma en que la información se conserva, dentro de archivos informáticos, utilizando distintos dispositivos y sistemas de almacenamiento. Algunos de entre los más utilizados por los SGBD son:

- **NAS (***Network-Attached Storage***)**: equipo de red configurado para actuar exclusivamente como servidor de archivos para un grupo heterogéneo de clientes. Por lo general, está permanentemente activo para garantizar la disponibilidad de los archivos, y puede contener uno o más dispositivos de almacenamiento, a menudo dispuestos en RAID (*Redundant Array of Independent Disks*). Esta es una técnica que permite combinar varias unidades físicas en una o más unidades lógicas, lo cual puede proporcionar, dependiendo del número de

dispositivos combinados y del tipo de RAID seleccionado, una mayor velocidad de acceso a los datos, uno o varios niveles de redundancia, o ambas características al mismo tiempo.

- **SAN (***Storage Area Network***)**: sistema de almacenamiento en red basado en bloques en lugar de en archivos. Ello implica que, mientras que un NAS aparece como un servidor de archivos en red (es decir, con un sistema de archivos ya definido), el almacenamiento en un SAN se gestiona desde el propio equipo cliente, en el cual se pueden montar y formatear los volúmenes SAN como si fueran locales.

El nivel intermedio es el **nivel conceptual**, y en él se describe puramente la **organización lógica** de los datos, es decir, la estructura y los objetos de la BD (atributos, restricciones, relaciones, usuarios, etc.), sin tener en cuenta la naturaleza o disposición de los mecanismos físicos de almacenamiento. En las bases de datos relacionales, un instrumento fundamental para ello es el esquema de base de datos, cuyo proceso de diseño recibe el nombre de *modelado de datos*.

Finalmente, en el nivel superior, o **nivel externo**, se describen esencialmente las **vistas de los datos**, es decir, la parte de los datos almacenados en la BD que interesa a cada usuario. Por este motivo, si bien únicamente pueden existir un nivel interno y uno conceptual, en la arquitectura ANSI/SPARC pueden existir varios niveles externos.

Estos tres niveles de abstracción pueden relacionarse, a su vez, con los tipos de usuario que acostumbran a interactuar con cada uno de ellos: los **administradores del sistema** trabajan a nivel físico; los **administradores de bases de datos**, a nivel lógico; y los **usuarios finales**, a nivel externo. De ello se infiere que los niveles interno y conceptual se ubican, habitualmente, en un servidor de bases de datos, y los niveles externos, en equipos cliente remotos.

![](_page_16_Picture_6.jpeg)

### Para + info

La **arquitectura de tres niveles** resulta muy útil para dotar a los datos de una BD de independencia lógica y física. La independencia física permite actuar sobre el aspecto físico de las bases de datos (reorganizando o reubicando los archivos, por ejemplo) sin tener que modificar los esquemas superiores. Por su parte, la independencia lógica permite alterar la estructura y contenidos de la BD sin que ello tenga efecto sobre los niveles interno o externos.

![](_page_17_Picture_1.jpeg)

Es importante tener en cuenta que un esquema de base de datos únicamente define las características de sus tablas y cómo estas se relacionan entre ellas o con otros modelos de datos, y que, por tanto, no contiene los datos en sí.

Un ejemplo claro son los documentos esquema XML, en los que, utilizando el lenguaje **XML Schema**, se declara un espacio de nombres —un contenedor abstracto de identificadores únicos— en el contexto del cual se definen los elementos que contiene el **documento XML** donde se hallan los datos:

En el ejemplo anterior, el esquema comienza indicando la versión del lenguaje XML que se utilizará, y la codificación de caracteres del documento. En la línea 2 es donde se declara el espacio de nombres, y, a continuación, se declaran un elemento raíz llamado *Procesador* (línea 3), y un atributo numérico (de tipo *double*) denominado *Velocidad* (línea 9). Observamos también que el elemento raíz posee dos elementos anidados de tipo cadena (*string*), *Marca* (línea 6) y *Modelo* (línea 7).

 <?xml version="1.0" encoding="UTF-8"?> <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"> <xsd:element name="Procesador"> <xsd:complexType> <xsd:sequence> <xsd:element name="Marca" type="xsd:string"/> <xsd:element name="Modelo" type="xsd:string"/> </xsd:sequence> <xsd:attribute name="Velocidad" type="xsd:double"/> </xsd:complexType> </xsd:element> </xsd:schema>

> Las líneas en los listados de código de esta obra se han numerado para facilitar la identificación de las líneas largas y de los elementos o fragmentos de código que los constituyen. A no ser que se indique expresamente lo contrario, dicha numeración no forma parte del código en sí.

### Atención
