# **6.1. Bases de datos distribuidas**

Las **bases de datos distribuidas** son un conjunto de bases de datos que están distribuidas físicamente en varios servidores o ubicaciones diferentes, pero que están conectadas a través de una red. En este tipo de sistemas, los datos no se almacenan en un único servidor centralizado, sino que se distribuyen entre varios nodos (computadoras o servidores) que colaboran entre sí para realizar operaciones de almacenamiento y procesamiento de datos.

El objetivo principal de las bases de datos distribuidas es proporcionar acceso rápido a los datos, mejorar la disponibilidad y ofrecer tolerancia a fallos, al tiempo que permiten a los usuarios trabajar con los datos de manera uniforme, como si estuvieran en un solo lugar.

### **Funcionalidades y usos de las bases de datos distribuidas**

Las bases de datos distribuidas ofrecen diversas funcionalidades y se utilizan en una amplia gama de aplicaciones que requieren escalabilidad, disponibilidad y rendimiento eficiente en entornos distribuidos. Algunas de las funcionalidades clave incluyen:

- **Distribución de datos**: los datos se dividen y distribuyen en varios servidores o nodos. Esto mejora la escalabilidad, ya que permite a los sistemas manejar grandes volúmenes de datos al añadir más servidores.
- **Replicación de datos**: los datos se copian y mantienen en múltiples ubicaciones, lo que mejora la disponibilidad y garantiza que los datos no se pierdan en caso de fallo de algún servidor. También facilita la recuperación ante desastres.
- **Tolerancia a fallos**: si uno de los servidores en la red falla, los demás nodos pueden seguir proporcionando acceso a los datos, garantizando la continuidad del servicio.
- **Transacciones distribuidas**: las bases de datos distribuidas permiten realizar transacciones que abarcan varios nodos, asegurando que todas las operaciones se completen correctamente o se reviertan si ocurre un fallo (principios ACID).
- **Escalabilidad horizontal**: permiten aumentar la capacidad de procesamiento y almacenamiento añadiendo más servidores o nodos al sistema, en lugar de mejorar las capacidades de un solo servidor (escalabilidad vertical).

### **Usos de las bases de datos distribuidas**

- **Empresas globales**: utilizan bases de datos distribuidas para mantener sus datos cerca de los usuarios, ofreciendo tiempos de respuesta más rápidos y facilitando el acceso a los datos desde múltiples ubicaciones geográficas.
- **Aplicaciones de alta disponibilidad**: sistemas críticos como los de bancos, telecomunicaciones y comercio electrónico dependen de bases de datos distribuidas para garantizar un tiempo de actividad constante.
- **Big Data y análisis**: las bases de datos distribuidas se usan para almacenar y procesar grandes volúmenes de datos, aprovechando la capacidad de procesamiento distribuido.
- **Internet de las cosas (IoT)**: en el IoT, los dispositivos conectados generan grandes cantidades de datos que deben almacenarse y procesarse de manera eficiente. Las bases de datos distribuidas permiten manejar estos datos en tiempo real.

### **Tipos de bases de datos distribuidas y sus pros y contras**

Existen varios tipos de bases de datos distribuidas, cada una con características, ventajas y desventajas. A continuación, se describen cinco tipos de bases de datos distribuidas:

### **Bases de datos relacionales distribuidas**

Estas bases de datos distribuidas siguen el modelo de base de datos relacional, donde los datos se organizan en tablas relacionadas entre sí. El motor de base de datos se distribuye entre varios nodos.

Por ejemplo: MySQL Cluster, PostgreSQL con sharding.

Los pros son:

- Mantenimiento de las propiedades ACID, que garantiza la consistencia en las transacciones.
- Amplia compatibilidad con herramientas de análisis y consulta, ya que utiliza SQL.
- Soporte para replicación y distribución de datos en nodos. Y los contras son:
- Escalabilidad limitada comparada con bases de datos no relacionales distribuidas.
- Las consultas distribuidas pueden ser más lentas, ya que involucran múltiples nodos.

### **Bases de datos NoSQL distribuidas**

Estas bases de datos distribuidas se utilizan principalmente para datos no estructurados o semiestructurados. No utilizan el modelo de base de datos relacional y son altamente escalables.

Por ejemplo: Cassandra, MongoDB (en clústeres).

Los pros son:

- Escalabilidad horizontal extremadamente eficiente.
- Ideal para grandes volúmenes de datos no estructurados y distribuidos geográficamente.
- Gran rendimiento en operaciones de lectura y escritura a gran escala.

Los contras son:

- Menos estrictas con las propiedades ACID, lo que puede comprometer la consistencia de los datos.
- Falta de compatibilidad con SQL, lo que dificulta su adopción en entornos tradicionales.

### **Bases de datos distribuidas orientadas a grafos**

Las bases de datos de grafos distribuidas son ideales para gestionar datos interrelacionados, como redes sociales, sistemas de recomendación o análisis de relaciones.

Por ejemplo: Neo4j (clustered), Amazon Neptune.

Los pros son:

- Excelente rendimiento para consultas que implican múltiples relaciones o conexiones entre datos.
- Ideal para analizar grandes redes interrelacionadas y datos jerárquicos.

Los contras son:

- Escalabilidad limitada en comparación con otras bases de datos NoSQL.
- Puede ser más compleja de implementar y mantener.

### **Bases de datos distribuidas en tiempo real**

Estas bases de datos están diseñadas para procesar grandes cantidades de datos en tiempo real. Se utilizan en sistemas de análisis en tiempo real, como en la detección de fraudes o aplicaciones de transmisión en vivo.

Por ejemplo: Apache Kafka, Redis Cluster.

Los pros son:

- Soportan una alta velocidad de entrada y salida de datos, ideal para el análisis en tiempo real.
- Baja latencia, lo que permite resultados casi instantáneos.

Los contras son:

- A menudo no son adecuadas para almacenamiento a largo plazo o análisis profundos de datos históricos.
- Menos robustas en cuanto a garantizar las propiedades ACID.

### **Bases de datos distribuidas en la nube**

Este tipo de bases de datos se ejecutan en plataformas en la nube y están diseñadas para aprovechar los recursos elásticos y escalables de la infraestructura en la nube.

Por ejemplo: Google Cloud Spanner, Amazon Aurora.

Los pros son:

- Escalabilidad infinita gracias a la infraestructura en la nube.
- Alta disponibilidad y tolerancia a fallos mediante la replicación en múltiples zonas geográficas.

Los contras son:

- Dependencia del proveedor de la nube, lo que puede limitar la flexibilidad.
- Costos elevados a largo plazo si no se optimiza adecuadamente el uso de recursos.

Las bases de datos distribuidas ofrecen soluciones para manejar grandes volúmenes de datos, mejorar la disponibilidad y tolerancia a fallos, y proporcionar escalabilidad horizontal. Sin embargo, la elección del tipo de base de datos distribuida depende de las necesidades específicas del sistema, como el tipo de datos, la necesidad de procesamiento en tiempo real, la tolerancia a fallos y los requerimientos de escalabilidad. Al gestionar bases de datos distribuidas, es importante considerar las compensaciones entre consistencia, disponibilidad y partición en la red (modelo CAP), según los requerimientos del proyecto.
