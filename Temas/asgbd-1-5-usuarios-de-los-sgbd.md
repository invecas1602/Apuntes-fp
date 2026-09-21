# **1.5. Usuarios de los SGBD**

Cuando hablamos de un usuario, normalmente nos referimos a las personas que utilizan una determinada solución informática, ya sea un programa, una aplicación web o una base de datos, sin tener necesariamente que conocer su funcionamiento interno. De hecho, los usuarios finales suelen ser personas sin una formación técnica específica, que acceden a las funciones del sistema mediante una interfaz de usuario relativamente sencilla.

Sin embargo, en lo relativo a los SGBD podemos distinguir tres tipos de usuario más:

- **Administradores**: se encargan de la instalación, configuración y mantenimiento del SGBD, lo que implica acceso a los recursos de hardware y software sobre los que se despliega la solución. Estos usuarios gestionan directamente los archivos en donde residen los datos de la BD, así como su seguridad, disponibilidad y rendimiento, por lo que deben tener un conocimiento profundo tanto del SGBD como de la plataforma tecnológica en la que este se sustenta.
- **Diseñadores**: aunque a veces el administrador y el diseñador de una BD son la misma persona, la figura del diseñador posee entidad propia, ya que tiene como función específica la de realizar el diseño lógico de la BD. Esto implica un conocimiento exhaustivo y detallado de todos los datos que se deberán incluir (procedencia, tipo, condiciones y restricciones, relaciones, etc.), así como de las reglas que será necesario aplicar en cada uno de los escenarios de uso posibles.
- **Programadores**: muchas veces resulta necesario programar aplicaciones que faciliten a los usuarios finales el acceso a los datos de la BD, o que, simplemente, obtengan de ella la información necesaria para realizar sus funciones. Para ello es posible utilizar un conjunto de métodos comunes, o bien API propietarias, compatibles con uno o varios lenguajes de programación.

![](_page_23_Picture_5.jpeg)

Una **API** (*Application Programming Interface*, es decir, interfaz de programación de aplicaciones) es un conjunto de definiciones y protocolos que permiten la comunicación entre dos entidades de software distintas, de forma que una pueda acceder a las funciones de la otra. Dicha comunicación se desarrolla mediante peticiones y respuestas, un proceso en el que el componente o aplicación que realiza las solicitudes se denomina *cliente*, y el que las atiende y envía la respuesta recibe el nombre de *servidor*.

### **1.6. El lenguaje estructurado de consulta (SQL)**

El SQL es la herramienta más utilizada para la gestión de bases de datos relacionales, y, a pesar de contar con interfaces gráficas, es el método con el que los administradores, diseñadores y programadores suelen desempeñar la mayor parte de las tareas relativas al SGBD, ya que, por lo general, es la forma más directa y flexible de interactuar con la BD. De hecho, los entornos gráficos para la gestión de BD no hacen más que ejecutar, internamente, instrucciones en SQL.

![](_page_24_Picture_3.jpeg)

**SQL** son las siglas de *Structured Query Language* (en español, lenguaje estructurado de consulta) y su función principal es la de extraer y organizar la información contenida en una BD estructurada.

De esta forma, no solo facilita la creación, modificación y eliminación de las tablas, sino la manipulación de los registros, la realización de consultas o el control del acceso a los datos, entre otras funciones.

### **Sintaxis**

La sintaxis del SQL incluye los siguientes elementos fundamentales:

- **Cláusulas**: instrucciones individuales que conforman las sentencias y las consultas.
- **Expresiones**: pueden ser literales (por ejemplo, el valor de una columna) o no (una operación matemática).
- **Predicados**: especifican condiciones o valores booleanos (verdadero/falso) que se emplean para limitar el alcance de las consultas y las sentencias.
- **Consultas**: se utilizan para recuperar el contenido de la base de datos con base en un criterio determinado (por ejemplo, todos los países que empiecen por la letra a).
- **Sentencias**: cadenas de cláusulas, expresiones y predicados que permiten definir los datos y objetos que pueblan la BD, controlar las sesiones y conexiones, realizar diagnósticos, etc.

### **Operadores**

Como los lenguajes de programación al uso, el SQL contempla un conjunto de **operadores** de comparación y lógicos que permiten la evaluación de condiciones, como por ejemplo igual (=), mayor que (>), menor que (>), diferente a (<>), es nulo (*is null*), es cierto (*is true*), es falso (*is false*), etc.

### **Tipos de datos**

Para cada columna de una tabla SQL debe declararse el tipo o tipos de datos que puede contener. Entre ellos se incluyen las cadenas de caracteres; los valores binarios, booleanos y numéricos; y valores de tiempo.

### **Identificadores**

Los nombres de las tablas, columnas y objetos de una base de datos SQL se denominan identificadores, y normalmente no pueden coincidir con una palabra reservada (como una cláusula), a no ser que estén delimitados (entrecomillados).

### **Constantes y variables**

La variables locales se utilizan para almacenar datos durante la ejecución de procesos por lotes. Pueden variar de un proceso al siguiente y expiran cuando finaliza la ejecución del lote.

El contenido de la variable puede proceder de la propia BD como resultado de una consulta, o ser un valor arbitrario (por ejemplo, un texto para imprimir en pantalla). Una constante es, al igual que una variable, un contenedor para un valor, con la diferencia de que en el caso de la constante el valor permanece inalterado durante la ejecución del programa.

![](_page_25_Picture_10.jpeg)

### Para + info

En este enlace encontrarás la traducción al castellano del manual de referencia de MySQL.

[bit.ly/3WmXBRy](http://bit.ly/3WmXBRy)

![](_page_25_Picture_14.jpeg)

![](_page_27_Picture_0.jpeg)
