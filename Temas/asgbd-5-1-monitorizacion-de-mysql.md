# **5.1. Monitorización de MySQL**

Un aspecto esencial del trabajo del gestor de SGBD es la monitorización del sistema. Para ello contamos herramientas específicas que nos ayudarán a supervisar, de forma constante, ciertos aspectos del SGBD.

Aunque todo SGBD proporciona un conjunto de métricas similares orientadas, tanto al diagnóstico de los problemas de rendimiento de las BD, como a la resolución de problemas en la ejecución de las consultas, cada uno difiere en los detalles de su implementación. MySQL, por ejemplo, proporciona cientos de indicadores estadísticos y de rendimiento, los cuales podremos obtener mediante dos tipos de consulta:

- Consulta de las variables de estado del servidor.
- Consulta de tablas de los esquemas *sys* y *performance\_schema*.

En este capítulo abordaremos las métricas que nos serán de mayor utilidad para obtener una imagen en tiempo real del rendimiento y de la salud general de nuestras bases de datos, así como las sentencias y mecanismos que nos ofrecen acceso a ellas.

### **5.1.1. La sentencia** *SHOW*

Una de las sentencias que nos puede proporcionar más información de utilidad para la monitorización del servidor de BD es *SHOW*. Esta sentencia puede adoptar numerosas fórmulas que proporcionan todo tipo de información acerca de las bases de datos, las tablas que las conforman o sobre el estado del servidor; en particular, *SHOW STATUS* y *SHOW VARIABLES* se cuentan entre las formas de *SHOW* más relevantes.

La sintaxis de *SHOW STATUS* es la siguiente:

SHOW [GLOBAL | SESSION] STATUS [LIKE 'patrón' | WHERE expresión]

Esta sentencia proporciona información acerca del estado del servidor, que se almacenan en variables de estado dentro de tres tablas del esquema de rendimiento (*performance\_schema*): *global\_status*, *session\_status* y *status\_by\_thread*.

Una forma alternativa de acceder a las variables de estado, desde una ventana del Símbolo del sistema, es usar la herramienta *mysqladmin* con la opción *extended-status*:

*SHOW STATUS* admite dos modificadores de ámbito, *GLOBAL*, que muestra todas las variables que representan el estado del servidor o información agregada de todas las conexiones, y *SESSION*, que muestra únicamente los valores de estado relativos a la conexión actual. Si no especificamos el modificador, se aplica *SESSION* por omisión.

Por su parte, la sentencia *SHOW VARIABLES* muestra los valores de las variables de sistema de MySQL. Su sintaxis y opciones de ámbito son idénticas a las de *SHOW STATUS*:

SHOW [GLOBAL | SESSION] VARIABLES [LIKE 'patrón' | WHERE expresión]

La opción *GLOBAL* muestra los valores que se utilizarán para iniciar las variables de sesión para cada nueva conexión al servidor, mientras que *SESSION* (por omisión) presenta los valores efectivos para la conexión actual.

Para obtener los valores de las variables de sistema desde fuera de MySQL, podemos utilizar la herramienta *mysqladmin*, con la opción *variables*, en una ventana de Símbolo del sistema:

> mysqladmin -u *nombre\_de\_usuario* -p variables

### **5.1.2. Elementos monitorizables**

Las variables de estado del sistema son el mecanismo mediante el que MySQL almacena la información estadística del servidor, por lo que, como ya hemos apuntado, será nuestra fuente principal de información a la hora de monitorizar su rendimiento.

### **Rendimiento de las consultas**

En el caso de las consultas, contamos con dos variables de estado que podemos monitorizar para detectar problemas en el volumen de consultas recibidas:

- *Questions*: almacena el número de sentencias ejecutadas.
- *Com\_select*: almacena las sentencias *SELECT*.

Para consultar el valor de ambas, utilizaremos las sentencias siguientes:

SHOW GLOBAL STATUS LIKE "Questions"; SHOW GLOBAL STATUS LIKE "Com\_select"; De la misma forma, podemos también consultar el número de operaciones de inserción (*Com\_insert*), actualización (*Com\_update*) y eliminación (*Com\_delete*), de forma que, sumando los tres valores, podamos obtener el número total de operaciones de escritura en la BD.

Además del número de consultas, nos interesará también cuánto se demora, por término medio, la ejecución de cada una. Para esto contamos, por un lado, con la variable de estado *Slow\_queries*, que almacena el número de consultas que hayan excedido el límite de tiempo estipulado en la variable de sistema *long\_query\_time*:

SHOW GLOBAL STATUS LIKE "Slow\_queries";

Para conocer el valor actual de *long\_query\_time*, ejecutaremos la siguiente sentencia:

SHOW VARIABLES LIKE 'long\_query\_time';

Por defecto, este valor es de 10 segundos, pero podemos ajustarlo (por ejemplo, a 7 segundos) con la siguiente orden:

SET GLOBAL long\_query\_time = 7;

Por otro lado, podemos ejecutar consultas sobre la tabla *events\_ statements\_summary\_by\_digest* del esquema de rendimiento (*performance\_schema*), donde, entre otros datos, se almacena toda la información referente a las veces que se ejecutan las sentencias y los diferentes tiempos de ejecución (en picosegundos). Para obtener un resumen del tiempo de ejecución medio para cada base de datos (trasladado a milisegundos), podemos utilizar una sentencia como la siguiente:

1 SELECT schema\_name AS esquema 2 , SUM(count\_star) cantidad 3 , ROUND((SUM(sum\_timer\_wait)/SUM(count\_star)) 4 / 1000000000) AS media\_ms 5 FROM performance\_schema.events\_statements\_summary\_by\_digest 6 WHERE schema\_name IS NOT NULL 7 GROUP BY schema\_name;

El resultado podría ser similar al siguiente:

+---------+----------+----------+ | esquema | cantidad | media\_ms | +---------+----------+----------+ | empresa | 10458 | 38 | +---------+----------+----------+ Esta tabla almacena también el número de sentencias que han generado error por cada esquema, por lo que podemos consultar este dato mediante una sentencia como la que sigue:

1 SELECT schema\_name AS esquema 2 , SUM(sum\_errors) núm\_errores 3 FROM performance\_schema.events\_statements\_summary\_by\_digest 4 WHERE schema\_name IS NOT NULL 5 GROUP BY schema\_name;

No obstante, si queremos obtener una relación más detallada, podemos realizar una consulta sobre la tabla *statements\_with\_errors\_or\_warnings* del esquema *sys*:

SELECT \* FROM sys.statements\_with\_errors\_or\_warnings;

O bien, para obtener una relación de las consultas más lentas, recurrir a la tabla *statements\_with\_runtimes\_in\_95th\_percentile* en ese mismo esquema:

SELECT \* FROM sys.statements\_with\_runtimes\_in\_95th\_percentile;

![](_page_119_Picture_7.jpeg)

#### Para + info

En el repositorio del proyecto *MySQL sys schema* encontraremos toda la información acerca de los objetos contenidos en este esquema:

![](_page_119_Picture_10.jpeg)

[bit.ly/3hfn3J1](http://bit.ly/3hfn3J1)

### **Conexiones**

Las siguientes variables de estado almacenan información de gran valor de cara a diagnosticar problemas con las conexiones:

- *Threads\_connected*: conexiones abiertas.
- *Threads\_running*: conexiones actualmente en ejecución.
- *Aborted\_connects*: intentos fallidos de conexión.
- *Connection\_errors\_internal*: conexiones rechazadas a causa de un error en el servidor.

- • *Connection\_errors\_max\_connections*: conexiones rechazadas debido al límite establecido en la variable de sistema *max\_connections*.

Como en el caso de las variables referentes a las consultas, podemos obtener esta información mediante *SHOW STATUS*; por ejemplo:

SHOW GLOBAL STATUS LIKE "Aborted\_connects";

![](_page_120_Picture_4.jpeg)

### Para + info

En la sección 5.1.10 del manual en línea de MySQL encontraremos el listado y descripción de todas las variables de estado del servidor:

[bit.ly/3VPgrQB](http://bit.ly/3VPgrQB)

![](_page_120_Picture_8.jpeg)

### **5.1.3. Informes de rendimiento**

MySQL Workbench proporciona un cuadro de control que podemos usar para monitorizar el estado general del servidor, y que encontraremos en el apartado *Dashboard* de la sección *Performance*, en la barra lateral izquierda.

El panel se divide en tres secciones:

- **Estado de la red (***Network Status***)**: en esta columna de estado de red veremos gráficas que nos muestran, en tiempo real, el tráfico de red entrante y saliente, además del número total de conexiones.
- **Estado de MySQL (***MySQL Status***)**: en la columna central se nos muestra el porcentaje de eficiencia de la caché de tablas abiertas, una gráfica de las sentencias SQL ejecutadas, e información acerca de cuántas operaciones de selección y acceso a las bases de datos se están realizando, así como el total agregado desde el inicio del servidor.
- **Estado de InnoDB (***InnoDB Status***)**: en esta última columna se presentan los datos más relevantes acerca de la actividad de disco generada por el motor de la base de datos, así como sobre el uso del conjunto de búferes que se utilizan para optimizar las operaciones del servidor.

![](_page_120_Picture_14.jpeg)
