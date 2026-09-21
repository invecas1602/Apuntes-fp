# **6.3. Arquitecturas de SGBDD**

Dependiendo de cómo estén estructurados y organizados los programas que conforman el sistema, podemos distinguir entre diferentes modelos de arquitectura de SGBDD.

Estos pueden describir también los diferentes niveles o capas de abstracción del sistema, las funciones de sus distintos componentes de software que en él participan, y la relaciones que se establecen entre todos ellos, así como la manera en que se relaciona el conjunto con otros sistemas externos.

En lo relativo a los SGBDD, las arquitecturas dependen directamente del nivel de homogeneidad o heterogeneidad presente entre los diferentes SGBD que los conforman, del grado de autonomía de cada uno de ellos, y de la distribución física de los datos. Tomando en cuenta estos parámetros, las arquitecturas más habituales serían las siguientes:

- **Cliente-servidor**: se trata de una arquitectura en dos niveles, típica de los sistemas homogéneos, en la que las funciones se reparten entre dos tipos de máquina, los servidores y los clientes:
  - **Servidores**: se ocupan de procesar los datos, de gestionar las consultas, y de organizar y optimizar las transacciones.
  - **Clientes**: albergan la interfaz de usuario, y se ocupan de gestionar y de controlar la consistencia de sus transacciones.

![](_page_144_Diagram_6.jpeg)

- **Colaborativa o de igual a igual**: cada sistema actúa, al tiempo, como cliente y servidor, compartiendo sus recursos y coordinando sus actividades con el resto de los pares. Este modelo requiere de la existencia de ciertos esquemas, habitualmente distribuidos en cuatro capas:
  - **Externo**: representa la vista de usuario de los datos.
  - **Conceptual global**: representa la distribución lógica global de los datos.
  - **Conceptual local**: representa la organización lógica de los datos en cada sistema.
  - **Interno local**: representa la organización física de los datos en cada sistema.

- **Multibase de datos**: sistema integrado de base de datos, típico de los SGBDD heterogéneos, formado por múltiples sistemas autónomos. Esta arquitectura, normalmente, contempla seis niveles de esquema: –**Vistas de multibase de datos**: representa las múltiples vistas de usuario que comprenden subconjuntos de la base de datos distribuida integrada.
  - **Conceptual de multibase de datos**: representa la lógica de la base de datos integrada, compuesta por todas las definiciones de estructuras lógicas globales de la multibase de datos distribuida.
  - **Interno de multibase de datos**: representa el reparto local de los datos entre las diferentes ubicaciones que conforman la multibase de datos distribuida.

![](_page_145_Diagram_2.jpeg)

*Diagrama de la arquitectura SGBDD colaborativa o entre iguales.*

- –**Vista local**: vistas de usuario de los datos locales en cada sistema.
- **Conceptual local**: organización lógica local de los datos en cada sistema.
- **Interno local**: ubicación física de los datos dentro de cada sistema local.

En lo que concierne específicamente a la distribución de los datos, existen cinco alternativas generales para el diseño de las tablas que forman parte de la BDD:

- **Replicadas**: todos los sistemas que forman parte del SGBDD almacenan una copia íntegra de todas las bases de datos, por lo que el acceso a las tablas es mucho más rápido, ya que no se realizan conexiones a otros sistemas para ejecutar las consultas de los usuarios. Esto implica unos costes de almacenamiento y de procesamiento durante las operaciones de actualización muy superiores que en otros diseños, por lo que se recomienda especialmente cuando se trabajan con BD que se actualicen raramente y sujetas a un alto volumen de consultas.
- **Parcialmente replicadas**: se copian las tablas, o ciertas partes de ellas, en diferentes sistemas en función del volumen de consultas que registren en ellos. De esta forma, los datos más solicitados estarán replicados y, por tanto, disponibles de forma inmediata, en aquellos servidores en donde se reciban más solicitudes de acceso, lo que optimiza las necesidades de almacenamiento y el coste de actualización de las BD.
- **Fragmentadas**: las tablas se dividen en dos o más fragmentos, también llamados particiones, que se almacenan en ubicaciones distintas. De esta forma, se aumenta el grado de paralelismo del sistema y, por lo tanto, evitamos la posibilidad de perder toda una BD a causa del fallo de un solo servidor. En este modelo no existe redundancia en los datos, ya que solo existe una copia de cada partición.

![](_page_146_Diagram_2.jpeg)

*Diagrama de la arquitectura de tipo multibase de datos distribuida.*

- **De distribución mixta**: en este diseño se combinan fragmentación y replicación parcial, de forma que los fragmentos de las tablas se copian en distintos servidores en función del volumen de peticiones de acceso a los datos contenidos en ellos.
- **No replicadas ni fragmentadas**: las tablas se reparten en diferentes sitios, de forma que estén lo más cercanas posibles a la ubicación que aglutine el mayor volumen de peticiones de acceso a ellas, pero ninguna de ellas se fragmenta o se replica. Es un diseño adecuado para ahorra en costes de comunicación y cuando no se accede de forma frecuente a datos procedentes de diferentes servidores.

### **Las reglas de Date**

Como resumen de todo lo expuesto hasta ahora, y a modo de referencia o guía para el diseño e implementación de un SGBDD, podemos utilizar las llamadas *12 reglas de Date*, establecidas por investigador y analista especializado en teoría de bases de datos Christopher J. Date (Watford, Inglaterra, 1941), que vemos resumidas en la siguiente tabla:
