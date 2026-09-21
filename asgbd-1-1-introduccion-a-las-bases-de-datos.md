# **1.1. Introducción a las bases de datos**

Los sistemas informáticos permiten almacenar y procesar la información en la cual se fundamentan aspectos esenciales del mundo que nos rodea. De hecho, hoy en día existen un sinnúmero de actividades basadas en la recopilación y organización, mediante dichos sistemas, de diferentes conjuntos de datos, desde una simple lista de la compra o una agenda de contactos almacenada en un teléfono móvil, hasta el seguimiento de proyectos empresariales, el registro contable de una empresa o la gestión de valores en bolsa, por citar tan solo unos pocos.

Cuando los datos son relativamente escasos, como por ejemplo una relación de códigos postales o un listado de prefijos telefónicos, resulta sencillo disponerlos en forma de lista o de tabla utilizando un procesador de textos o un programa para la confección de hojas de cálculo. Pero a medida que el volumen de información crece, alimentado principalmente por grandes sistemas interconectados en red como internet, resulta cada vez más importante contar con sistemas capaces de organizar los datos de una forma que nos permita comprenderlos mejor y aprovecharnos de todo su potencial.

En los modelos de bases de datos tradicionales, como puede ser el relacional, el conjunto de datos estructurados que contiene la base de datos normalmente se almacena dentro de un único archivo electrónico y utilizando una o varias **tablas**, es decir, estructuras de filas (o **registros**) y de columnas (o **campos**). No obstante, existen otros modelos, como el NoSQL, en el que los datos pueden carecer de estructura fija y estar distribuidos entre múltiples sistemas.

Una **base de datos**, o BD, es una herramienta diseñada para **registrar y organizar datos** de la manera más eficiente posible, ya que no solo facilita la búsqueda de información, sino que mejora su calidad al prevenir, en gran medida, la introducción de datos redundantes e inconsistentes.

### **1.1.1. Objetos de una base de datos**

Los archivos de bases de datos pueden contener diferentes tipos de elementos, denominados **objetos de base de datos**, entre los que se incluye cualquier mecanismo que se utilice para almacenar o manipular los datos. Esto significa que, salvo los datos que contiene cada uno de los registros de una tabla, prácticamente todo dentro de una base de datos es un objeto.

Los objetos de base de datos más utilizados son los siguientes:

- **Tablas**: estructuras lógicas compuestas por filas y columnas en donde se retienen los datos en sí. Las tablas almacenan toda la información persistente de la base de datos, que son los registros, pero también pueden albergar información de forma temporal como resultado de diferentes operaciones, como la selección de un subconjunto determinado de datos.
- **Índices**: se trata de conjuntos de indicadores ordenados mediante los valores de una o varias claves, y que pueden apuntar a los registros de una tabla o a otros objetos almacenados.

En una base de datos relacional de alumnos de una academia, por ejemplo, podríamos tener una tabla para almacenar los datos personales de los alumnos (nombre, dirección, teléfono, correo electrónico, etc.), y una tabla por asignatura para el registro de las calificaciones de cada alumno.

**Nombre Apellido Dirección Teléfono E-mail**

Juan Pérez C/Carpinteros 8 656789089 juan@mail.com

Miguel Ortega Avda. Unamuno, 10 456345687 miguel@mail.com Carlota Sánchez C/Cervantes, 54 624564765 carlota@mail.com

**CAMPOS**

**REGISTROS**

**TABLA DE ALUMNOS**

**1er. Trimestre 2º Trimestre 3er. Trimestre Final**

9 8 7 8 4 10 7 7 9 6 6 7

**CAMPOS**

**REGISTROS**

**TABLA DE CALIFICACIONES**

- • **Restricciones**: mecanismos que permiten aplicar determinadas reglas sobre los datos almacenados, como por ejemplo que un determinado campo no pueda estar vacío o contener un valor duplicado. En general, existen dos tipos de restricciones: las de **tipo 1**, que se incluyen en la propia definición de una columna y que solo afectan al mismo campo al cual definen, y las de **tipo 2**, que se definen tras crear todas las columnas de una tabla y que pueden aplicarse a una o varias de ellas según sea necesario.
- **Disparadores**: se utilizan para definir conjuntos de acciones que ocurrirán cuando se realice una determinada operación sobre una tabla, como por ejemplo la inserción, actualización o eliminación de un registro.
- **Secuencias**: permiten generar valores automáticamente, como por ejemplo los valores de clave única.
- **Vistas**: objetos temporales (es decir, que no necesitan almacenarse de forma permanente) que permiten presentar los datos obtenidos como resultado de una consulta.
- **Cursores**: permiten la selección de un conjunto de registros y procesarlos uno por uno; esto es lo que ocurre cuando una aplicación accede a una base de datos y obtiene varios registros como resultado de una consulta: las filas no se devuelven al mismo tiempo, sino una detrás de otra.
