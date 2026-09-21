# **1.4. Tipos de SGBD**

Para clasificar los tipos de SGBD disponibles en el mercado podemos utilizar diferentes criterios, algunos de ellos verdaderamente amplios. Es el caso de la clasificación por número de usuarios —donde podemos dividirlos entre **monousuario** y **multiusuario**—, por su ámbito de aplicación —de **propósito general** o de **propósito específico**—, o según el número de sitios que abarcan —**centralizados** o **distribuidos**.

Otra clasificación posible se basa en el número de capas que presenta el SGBD. Un SGBD de una sola capa, o **monocapa**, está diseñado para instalarse en los ordenadores de los usuarios domésticos o de pequeños negocios, y normalmente se accede a ellos desde la máquina en la que están instalados (aunque es posible compartir los archivos de base de datos como recursos en red). Un ejemplo de este tipo de sistema es LibreOffice Base.

Cuando no accedemos a la BD desde la máquina en la que está alojada, sino que el SGBD reside en un servidor y el acceso a él se produce a través de una capa de presentación ejecutada en una máquina cliente, estamos ante una arquitectura de **dos capas**.

Finalmente, hablamos de arquitectura de **tres capas** cuando los clientes no realizan ninguna llamada al servidor de base de datos, sino que existe un servidor de aplicaciones interpuesto que realiza la intermediación con el SGBD, y donde se desarrolla la lógica funcional o lógica de negocio del sistema —es decir, las reglas que se deben cumplir antes de realizar una solicitud o devolver una respuesta. En esta arquitectura, los clientes actúan, pues, como meras interfaces de formularios.

No obstante, la clasificación más habitual se basa en el modelo lógico utilizado, siendo los SGBD **relacionales** y **no relacionales** los más utilizados hoy en día. De entre los dos, los relacionales son, con diferencia, los SGBD más implementados —gracias en parte a la rigidez de sus esquemas, que simplifica su gestión, y a la accesibilidad que proporciona el lenguaje SQL—, pero otros modelos pueden resultar más adecuados en determinados escenarios. Son los siguientes:

- **Relacionales**: sistema donde los datos se organizan en tablas bidimensionales (es decir, compuestas de filas y columnas), y cada una de estas tablas tiene definido un campo clave que identifica, de forma unívoca, cada uno de los registros. Podemos encontrar SGBD relacionales para todo tipo de plataformas, desde PC de escritorio (Microsoft Access), como en estaciones de trabajo y en servidores de cualquier envergadura (Oracle Database, Microsoft SQL Server, MySQL, etc.).

En las arquitecturas de dos y tres capas se requiere del uso de unos componentes de software llamados *conectores*. Entre los más utilizados se cuentan los que siguen las normas ODBC y JDBC. El estándar ODBC (*Open Database Connectivity*) provee de una biblioteca que permite a los clientes realizar consultas al servidor y obtener los resultados. Por su parte, la norma JDBC es una interfaz de programación específica para Java, que permite al software programado con este lenguaje acceder a las BD compatibles.

Para + info

- **Orientados a objetos**: en estos sistemas, los datos se tratan como objetos utilizando conceptos de la programación orientada a objetos como el encapsulamiento (una técnica para proteger los datos y ocultar la información innecesaria entre diferentes entidades), el polimorfismo (que nos permite procesar datos de forma distinta según sea su tipo) y la herencia (un mecanismo gracias al cual un objeto puede adquirir propiedades de otro), aunque también se aplican técnicas relacionales en aspectos como las transacciones o el control de la concurrencia. Un ejemplo de este tipo de SGBD es Object DB.
- **Jerárquicos**: sistemas en los que los datos se organizan en forma de árbol invertido en relaciones de uno a muchos (1:N). El árbol se desarrolla a partir de un nodo raíz y se ramifica en diversos nodos hijo. Este tipo de SGBD se utiliza principalmente en grandes servidores de empresa y computadoras centrales en sectores como la banca, los mercados verticales, la industria manufacturera o en el ámbito gubernamental. Un ejemplo es el IMS de IBM.
- **De red**: sistemas de naturaleza jerárquica en los que los datos se organizan a partir de relaciones de uno a uno (1:1) o de muchos a muchos (N:N); en otras palabras, es la generalización del modelo jerárquico. Esto permite la existencia de varios nodos padre para cada nodo hijo.
- **NoSQL**: sistemas de tipo no relacional (es decir, que no se basan en el modelo tabla/clave tradicional, en el que existe un esquema definido y permanente), que están optimizados según el tipo de datos que manejen (sus esquemas están implícitos en los datos, lo cual significa que pueden ir cambiando dentro de la misma BD). Existen cuatro tipos de SGBD NoSQL:
  - **De documentos**: pueden almacenar diferentes tipos de documentos, típicamente con estructura JSON, XML o BSON, a los cuales se asocia una clave específica. Los datos pueden recuperarse mediante dicha clave, pero, al tratarse de un sistema semiestructurado, también es posible indizar los documentos para obtener datos sin conocerla. Dos ejemplos populares de este tipo de SGBD son MongoDB y Apache CouchDB.
  - **De valores clave**: los registros almacenados pueden ser cualquier tipo de objeto binario (un texto, una imagen, un vídeo, etc.), y a estos se asocia una clave única, como en el caso anterior. Esto proporciona a la BD una gran flexibilidad y velocidad de lectura y escritura. Ejemplos de SGBD para el almacenamiento de valores clave son Redis, Apache Cassandra, el Cloud Bigtable de Google y Amazon DynamoDB.

- **De columnas anchas**: los datos se almacenan en tablas cuyas columnas pueden ir cambiando de nombre y formato de una fila a otra. Además, contienen columnas anchas donde se agrupan los datos relacionados, lo cual permite recuperarlos mediante una sola operación.
- **De grafos**: utilizan estructuras de datos no lineales (los grafos) compuestas por nodos (llamados vértices) unidos por uno o varios enlaces (las aristas o arcos), que pueden ser unidireccionales (dirigidos) o sin una dirección concreta (no dirigidos). En este caso, los datos son los nodos, y las relaciones, las aristas. Un ejemplo de este tipo de SGBD es Neo4j.

![](_page_21_Diagram_4.jpeg)

*A la izquierda, una BD organizada según el modelo jerárquico, y a la derecha, una organizada según el modelo de red.*

#### Para + info

Puedes obtener más información acerca de algunos de los SGBD NoSQL más importantes en los siguientes enlaces:

**1** bit.ly/3DsB25j

Cloud Bigtable

**2** go.aws/3gZotXf

Amazon DynamoDB

**3** bit.ly/3DqmDGu

Azure Cosmos DB

**4** bit.ly/3DsB25j

Apache Cassandra

**5** bit.ly/3zrv1ob

MongoDB

**6** bit.ly/3UbzW4s

Apache CouchDB

**7** ravendb.net

**8** redis.io

**9** neo4j.com

Los SGBD NoSQL (cuyo significado puede ser tanto *no SQL*, como *no solo SQL*) están especialmente indicados para grandes bases de datos en permanente crecimiento, como las que manejan empresas de Internet de la envergadura de Google o Facebook, ya que son muy escalables (pueden crecer fácilmente), extremadamente rápidos y, al ser de naturaleza distribuida, proporcionan una muy alta disponibilidad de los datos.

### Para + info

### **1.4.1. SGBD comerciales y libres**

A la hora de decidirse por un SGBD, las empresas y desarrolladores deben tener en cuenta tanto el contexto tecnológico donde se va a implantar la solución, como las necesidades propias del proyecto que se va a abordar. De esta forma, en un ecosistema basado exclusivamente en productos de Microsoft, tiene sentido optar por productos que se integren sin problemas, como Microsoft SQL Server, con las ventajas inherentes, en cuanto a soporte, de un producto comercial, mientras que, en plataformas heterogéneas, vale la pena considerar la implantación de un SGBD de código abierto.

Por suerte, existen excelentes alternativas de software gratuito que podemos usar para implementar diferentes modelos de base de datos. Si bien algunos de estos SGBD nacieron (y persisten) como plataformas comerciales, en la actualidad también cuentan con versiones gratuitas, como es el caso de Microsoft SQL Server Express y de MySQL Community Edition. Si bien estos SGBD no son de código abierto, sí proporcionan la posibilidad de obtener versiones muy completas y funcionales de sus alternativas de pago.

![](_page_22_Picture_4.jpeg)

En el ámbito del software libre, contamos también con excelentes alternativas, como PostgreSQL, MariaDB, MongoDB, CouchDB o Redis, entre otras. En algunos casos, estos SGBD ofrecen servicios de cuota en la nube o contratos de soporte, lo que abarata los costes de implementación y mitiga la necesidad de contar con personal altamente especializado.

De hecho, los servicios de bases de datos en la nube, como pueden ser Cloud Bigtable de Google, DynamoDB de Amazon, o Azure SQL Database y Azure Cosmos DB de Microsoft, empiezan a ganar popularidad gracias a sus excelentes prestaciones en lo relativo a escalabilidad y disponibilidad. Además, en muchas ocasiones cuentan también con mecanismos que facilitan la integración de las BD con aplicaciones programadas en diferentes lenguajes.
