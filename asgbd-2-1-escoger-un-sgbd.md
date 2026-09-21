# **2.1. Escoger un SGBD**

A la hora de escoger en SGBD, existen una serie de consideraciones fundamentales que se deben tomar en cuenta:

- Nivel de **integración** con los sistemas actuales.
- Coste y complejidad de una **migración de datos**, en caso de ser necesaria.
- **Necesidades inherentes** del proyecto: tipo de datos, volumen de información, número de conexiones concurrentes, rendimiento esperado, etc.
- Características de **seguridad**.
- Características de **disponibilidad** y **escalabilidad**.
- Disponibilidad de **API** para la integración con software cliente o aplicaciones web.
- **Documentación** existente y **nivel de soporte**, tanto del desarrollador como de la comunidad.

En esta obra nos vamos a centrar en los SGBD relacionales, por ser los más extendidos en el ámbito empresarial, y en particular en aquellos que se basan en el lenguaje SQL, que es, con diferencia, el lenguaje de base de datos predominante en este ámbito. Precisamente por este motivo, la oferta de SGBD basados en SQL es muy amplia, por lo que debemos tener muy claras sus principales características antes de decantarnos por una opción en particular.

Según la empresa de estudios estadísticos Statista, el SGBD relacional más utilizado, a enero de 2022, era Oracle Database, seguido de MySQL, Microsoft SQL Server y, a mucha distancia, PostgreSQL. A continuación, repasaremos las principales características de estas plataformas, centrándonos especialmente en MySQL, ya que va ser el SGBD en el que vamos a basar la parte práctica de este libro.

![](_page_28_Picture_6.jpeg)

### Para + info

*Ranking* mundial de los sistemas de gestión de bases de datos relacionales, a enero de 2022, según la web de Statista.

[bit.ly/3U1IwDe](https://bit.ly/3U1IwDe)

![](_page_28_Picture_10.jpeg)

### **2.1.1. Oracle Database**

![](_page_29_Picture_2.jpeg)

Oracle Database es un sistema de gestión de bases de datos **multimodelo** —contempla los modelos objeto-relacional, JSON y de grafos— desarrollado por Oracle Corporation, cuyos principales argumentos de venta son su **seguridad**: en materia de cifrado, gestión de claves, controles de acceso, etc.; su **flexibilidad**: la posibilidad de implementarlo en un centro de datos propio o en la nube; y la **convergencia**: emplea una sola BD para todos los tipos de datos.

De esta forma, Oracle ofrece un catálogo de productos diferenciados, diseñados y optimizados específicamente para cada escenario de uso.

**Oracle Database 19c y 21c** son la últimas versiones del producto que nació, en 1979, como el primer SGBD basado en SQL disponible en el mercado. La versión 19c es la que cuenta con soporte a largo plazo, mientras que la 21c es la que incorpora las últimas mejoras y nuevas funciones del producto, aunque a costa de un nivel de estabilidad menor.

Así, en la última versión se han incluido, entre otras, un conjunto de mejoras de múltiples modelos, cargas de trabajo y multicliente, como la compatibilidad con JSON binario para escaneos 10 veces más rápidos y AutoML, que ofrecen a los usuarios no expertos acceso a características de aprendizaje automático en la base de datos. Algunas de las principales características tecnológicas que Oracle desarrolla para su plataforma, y que contribuyen a diferenciarla de sus competidores, son:

- Tecnologías avanzadas de **analítica y almacenamiento de datos** local o en la nube.
- Capacidades de **alta disponibilidad** que permiten el escalado y la consolidación eficiente de las BD.
- Posibilidad de **usar Python, R, SQL**, entre otras herramientas, para integrar las funciones de aprendizaje automático en aplicaciones de bases de datos.

### **2.1.2. Microsoft SQL Server**

![](_page_30_Picture_2.jpeg)

SQL Server 2019 es la última versión de este SGBD desarrollado por Microsoft. Utiliza el dialecto **T-SQL**, y su motor de base de datos ocupa los primeros puestos en los índices TPC-E (*On-Line Transaction Processing Benchmark*) y TCP-H (*Decision Support Benchmark*). Esto hace que sea apto para utilizarse en una amplia **variedad de entornos** y en aplicaciones que exigen un **alto rendimiento**.

En su versión más reciente, Microsoft SQL Server incorpora tecnologías punteras, como los llamados *Big Data Clusters* para potenciar Kubernetes como plataforma de despliegue, o el sistema de archivos distribuido Apache Hadoop (HDFS), y ofrece soporte para su integración con múltiples lenguajes de programación, como Java, C/C++, Scala, Node.js, C#/ VB.NET, Python, Ruby, .NET Core o, incluso, lenguajes no soportados de forma expresa.

Como Oracle Database, SQL Server ofrece también funciones para el aprendizaje automático con R, Python, Java y .NET. Además, tomando como referencia la base de datos de vulnerabilidades del NIST (*National Institute of Standards and Technology*), este SGBD se presenta, en los últimos años, como el **más seguro**, soportando características como el cifrado de datos transparente, seguridad a nivel de fila, enmascaramiento dinámico de datos y Always Encripted, una tecnología diseñada para proteger datos sensibles.

### **2.1.3. PostgreSQL <sup>y</sup> otros SGBD**

**PostgreSQL** es un SGBD objeto-relacional de código abierto en desarrollo desde 1995. Se trata de un sistema de alta concurrencia —permite que los procesos escriban en una tabla sin bloquear el acceso a ella—, con soporte para una amplia variedad de tipos de datos (aunque los usuarios pueden crear sus propios tipos indizables), para transacciones distribuidas, y para el uso de diversos lenguajes de programación (C, C++, Java, etc.), incluyendo un lenguaje propio llamado PL/PgSQL.Además de ser el segundo SGBD de código abierto más utilizado a nivel mundial (solo por detrás de MySQL), su licencia permite su utilización con fines comerciales, como es el caso de EDB Postgres o de CYBERTEC PostgreSQL.

### Para + info

Web del Transaction Processing Performance Council (TPC):

![](_page_30_Picture_5.jpeg)

t[pc.org](https://www.tpc.org)

![](_page_30_Picture_8.jpeg)

#### **Kubernetes** es

una tecnología de virtualización de código abierto basada en contenedores —programas ejecutables que combinan su código fuente con las bibliotecas y dependencias de un sistema operativo—, que automatizan el despliegue, administración y escalado de aplicaciones.

### Para + info

Otro SGBD de código abierto muy extendido es **MariaDB**. Desarrollada inicialmente por los responsables originales de MySQL (de hecho, utiliza el programa cliente de línea de instrucciones *mysql*), es el SGBD incluido por defecto en la mayor parte de distribuciones del sistema operativo Linux, y su desarrollo tiene como foco la estabilidad, el rendimiento y la compatibilidad con otras plataformas, como Oracle.

Finalmente, entre los SGBD empresariales más populares está **IBM Db2**. De hecho, IBM engloba bajo este nombre toda una familia de productos para la gestión de datos, la mayor parte de ellos disponibles en la plataforma IBM Cloud Pak for Data, bien como complemento, bien como servicio de orígenes de datos, de modo que prácticamente todos los datos están disponibles en los entornos híbridos o multinube que se utilizan, por ejemplo, en aplicaciones de inteligencia artificial y aprendizaje automático.

Al igual que Oracle Database, Db2 es una propuesta multimodelo, lo que evita la necesidad de replicar o migrar los datos. Por ejemplo, IBM Db2 Big SQL es un motor SQL sobre Hadoop híbrido que proporciona procesamiento en paralelo masivo y consulta de datos avanzada. Este producto ofrece una única conexión de base de datos o consulta para fuentes dispares, como Hadoop HDFS y WebHDFS, así como bases de datos NoSQL y almacenes de objetos, entre otras características avanzadas.

### **2.1.4. MySQL**

![](_page_31_Picture_5.jpeg)

**MySQL** es un SGBD relacional desarrollado por Oracle Corporation que se distribuye bajo dos tipos de licencia, GPL (licencia pública general) y licencia comercial. La edición *Community* es la versión gratuita, mientras que existen diversas versiones *Enterprise* comerciales que incluyen soporte técnico por parte de Oracle y diversas herramientas administrativas.

Este SGBD se utiliza principalmente en **aplicaciones web** y, de hecho, forma parte de la denominada **pila LAMP** (o **WAMP**), que proporciona el conjunto de tecnologías que se utilizan a la hora de configurar un servidor web: el sistema operativo (Linux o Windows), el software servidor web (Apache), el SGBD (MySQL o MariaDB) y el lenguaje de programación (PHP).

Además del soporte para PHP, existen API de acceso a las BD de MySQL mediante una amplia variedad de lenguajes, que incluyen C, C++, C#, Pascal, Java (con un controlador JDBC nativo), Perl, Python y Ruby, entre otros. Además, gracias a MyODBC —la interfaz ODBC de MySQL—, cualquier lenguaje con soporte ODBC será capaz de conectarse con MySQL.

Como interfaz de usuario, normalmente se utiliza *mysql* como cliente de línea de instrucciones, MySQL Workbench como entorno gráfico integrado y phpMyAdmin como interfaz web, aunque existen muchas otras interfaces y aplicaciones que permiten interactuar con este SGBD.

Si bien MySQL ofrece las funciones estándar de un SGBD actual, posee ciertas características únicas, como la posibilidad de escoger un motor de almacenamiento distinto para cada tabla (entre las múltiples alternativas tenemos motores nativos, como MyISAM, InnoDB, MySQL Cluster y Archive, o desarrollados por terceros, como IBM DB2, solidDB, memcache y httpd, entre otros muchos), y la posibilidad de agrupar transacciones desde varias conexiones para aumentar el rendimiento de la BD.

Ponte a prueba

**¿Qué SGBD bajo licencia GPL goza de un mayor nivel de implementación en todo el mundo?**

- a) Oracle Database.
- b) PostgreSQL.
- c) MariaDB.
- d) MySQL.
- e) Ninguno de los anteriores.
