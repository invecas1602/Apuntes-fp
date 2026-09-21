# **6.6. Balanceo de carga**

La replicación no es solo una técnica para reforzar la redundancia y la tolerancia a errores de un SGBDD; también es una herramienta de utilidad para los equilibradores o "balanceadores" de carga.

En el balanceo de carga con replicación, los clientes realizan sus peticiones al balanceador, que efectúa las escrituras sobre el servidor configurado como maestro, y las lecturas sobre los distintos servidores esclavos. De esta forma se reparte la carga del sistema entre todos los servidores del sistema.

![](_page_157_Diagram_4.jpeg)

*Uso de la replicación como técnica de balanceo de carga en un SGBDD.*

En este apartado haremos un repaso de los conceptos generales relacionados con el balanceo de carga, utilizando como referencia el producto de MySQL para la gestión de bases de datos de alta disponibilidad, MySQL Cluster. Como su propio nombre indica, este software está diseñado para configurar varios servidores de MySQL, nodos de datos y servidores de administración, en una disposición perfectamente coordinada que recibe el nombre de clúster.

Es importante no confundir el concepto de *anfitrión* o *host* con el de *nodo*. En un clúster, cada computadora puede ejecutar uno o más procesos, y son estos procesos los que constituyen los diferentes nodos del clúster: servidores de base de datos, nodos de datos, servidores de coordinación y otros programas especializados en el acceso a la información.

### Atención

Una ventaja de los clústeres es que sus requerimientos técnicos suelen ser relativamente modestos, gracias a la naturaleza distribuida de los procesos que se realizan en él. En el caso de MySQL Cluster, dado que su motor de almacenamiento trabaja en la memoria, el único requerimiento crítico es contar con una buena cantidad de RAM. Además, lógicamente deberemos proveer a los nodos encargados del almacenamiento físico de los datos con dispositivos de almacenamiento de capacidad suficiente y, cuanto más rápidos, mejor. Por lo demás, no suele ser necesario realizar ninguna configuración especial en el sistema operativo subyacente, salvo los habituales para cualquier otro tipo de SGBD.

![](_page_158_Picture_2.jpeg)

En cuanto a las características de red, normalmente se ofrece soporte para la pila TCP/IP y cualquier topología de red estándar. La velocidad de comunicación mínima recomendada entre los anfitriones es de 100 Mbps y, por motivos de seguridad y eficiencia, se recomienda configurar una subred para uso exclusivo del clúster. En un clúster MySQL, por ejemplo, las comunicaciones entre los nodos no están cifradas ni protegidas en forma alguna, por lo que es necesario colocar el clúster tras un muy estricto cortafuegos.

El motor NDB de MySQL Cluster replica automáticamente los datos del clúster de forma síncrona dentro del propio clúster, y de forma asíncrona, usando el procedimiento estándar de replicación de MYSQL, entre diferentes clústeres NDB.

### **6.6.1. Configuración básica de un clúster NDB**

Típicamente, la configuración mínima de un clúster (como, por ejemplo, la de un clúster NDB) está compuesta por tres nodos, cada uno de un tipo distinto:

- **Nodo de administración**: se encarga de administrar el resto de los nodos del clúster, y sus funciones abarcan desde la configuración y replicación de los datos, hasta la configuración, inicio, detención y coordinación general de los nodos. Por este motivo, es necesario iniciar este nodo antes que los demás.

La instrucción para iniciar un nodo de administración en un clúster NDB es *ndb\_mgmd*.

- **Nodo de datos**: es el nodo encargado de almacenar los datos. Su número debe coincidir con el número de fragmentos o particiones de la BD, multiplicado por el número de réplicas de dichos fragmentos. Por ejemplo, si existen dos particiones y tres réplicas, será necesario disponer de un total de seis nodos de datos.

MySQL Cluster utiliza un motor de almacenamiento, en memoria y "clusterizado", llamado NBDCLUSTER, conocido también como NDB (*Network Database*).

Este motor es el que se encarga de almacenar las tablas y los datos en los nodos de datos, de manera que sean directamente accesibles desde el resto de los servidores MySQL del clúster.

### Para + info

En consecuencia, usando un solo nodo no contaremos con la posibilidad de realizar réplicas, por lo que se recomienda configurar un mínimo de dos nodos de datos. Normalmente, es el propio motor de almacenamiento el que particiona los datos de forma automática, aunque es posible configurar algunos aspectos de su funcionamiento.

En un clúster NDB, podemos iniciar un nodo de datos de un solo hilo con la instrucción *ndbd*, o de varios hilos con *ndbmtd*.

- **Nodo SQL**: es el nodo encargado de acceder a los datos. Al igual que sucede con los nodos de datos, se recomienda contar con varios nodos SQL (así como utilizar más de un nodo de administración), a fin de dotar al sistema de un nivel adecuado de redundancia y escalabilidad. En el caso de un clúster NDB, se trata de una versión especial de *mysqld* (y, por lo tanto, no compatible con un servidor MySQL estándar), basada en una API especializada en el acceso a datos clusterizados.

Al igual que sucede con la edición estándar de MySQL, la configuración de los nodos se realiza estableciendo el valor de un conjunto de opciones, parámetros y variables de estado y de sistema.

La configuración global de un clúster NDB —que define los anfitriones y los nodos del clúster— se realiza dentro de la sección específica del archivo de configuración del administrador, denominado *config.ini*. Además, cada nodo del clúster cuenta con su propio archivo de configuración *my.ini* o *my.cnf*.

![](_page_159_Picture_7.jpeg)

Supongamos que queremos configurar un clúster con un nodo administrador, un servidor MySQL y dos nodos de datos con dos réplicas por nodo. En este caso, el archivo *config.ini* podría quedar como sigue:

[ndb\_mgmd] Hostname= admin.ilerna.com DataDir= c:/adm-cluster/data

[ndbd default] NoOfReplicas= 2 DataDir= c:/adm-cluster/data

[ndbd] HostName= ndbd1.ilerna.com [ndbd] HostName= ndbd2.ilerna.com

[mysqld] HostName= mysql.ilerna.com

En el apartado *[ndb\_mgmd]* incluiremos la definición de los nodos de administración, en sendos apartados *[ndbd]* los de los nodos de datos, y en *[mysqld]*, las definiciones de los nodos SQL.

Es necesario incluir una sección distinta por cada nodo, excepto para las opciones por defecto de todos los nodos de un mismo tipo, lo cual se logra añadiendo la palabra default al nombre de la sección; en este ejemplo, hemos incluido una sección *[ndbd]* por cada nodo de datos, más una sección *[ndbd default]* con las opciones por defecto para todos los nodos de este tipo. Como se puede observar, las secciones de configuración por defecto deben situarse antes de las definiciones individuales de cada nodo.

En cuanto a las configuraciones locales de cada nodo, será necesario incluir ciertos parámetros en el archivo *my.ini* o *my.cnf*, o, en su lugar, especificarlos como opciones de instrucción en el Símbolo del sistema.

En nuestro ejemplo, y para el nodo SQL, necesitamos incluir, en su archivo de configuración local, la opción que activa el motor NDB, y también proporcionar la cadena de conexión con el nodo de administración:

[mysqld] ndbcluster ndb-connectstring=admin.ilerna.com

En los nodos de datos, simplemente incluiremos en sus archivos de configuración la cadena de conexión al administrador, de la siguiente manera:

[mysql\_cluster] ndb-connectstring=admin.ilerna.com

En todos los casos, el puerto de comunicaciones por omisión es el 1186.

### **6.7. Optimización de consultas sobre BDD**

Como ya vimos en el apartado dedicado a la optimización de consultas, el SGBD comprueba la validez y crea una representación interna de cada consulta, que podemos definir como un gráfico o árbol de consulta. A continuación, el planificador evalúa las posibles estrategias de ejecución, y selecciona la que considera más apropiada.

En los sistemas de bases de datos distribuidas, la optimización de consultas es un mecanismo más crucial, si cabe, que en un SGBD independiente, pero también es más complejo, debido esencialmente a la presencia de particiones de datos distribuidas en varios nodos y a las limitaciones que, posiblemente, puedan imponer la velocidad de las comunicaciones y las diferentes capacidades de proceso de los nodos locales.

![](_page_161_Picture_4.jpeg)

*En MySQL Workbench podemos obtener una representación gráfica del plan de ejecución de las consultas.*

De esta forma, en un SGBDD, los posibles árboles de consulta y, por tanto, las posibles estrategias de ejecución, se multiplican, y pueden demorar en exceso el mismo proceso de evaluación. No olvidemos que, en este escenario, el tiempo total de ejecución de una consulta es la suma del tiempo que se tarda en comunicar con las BD, el tiempo de ejecución de cada consulta local, el requerido para recuperar los datos de diferentes sitios, y, finalmente, el tiempo que se tarda en entregar el resultado a la aplicación que los hubiera solicitado.

Por estos motivos, a menudo se opta, en los SGBDD, no por el mejor plan de ejecución, sino por uno lo suficientemente bueno, que se deriva de un proceso de optimización a dos niveles: global y local.

Para ello se realiza un proceso de asignación en el que las consultas globales se dividen entre los diferentes sitios donde residen localmente los datos. A grandes rasgos, el proceso sería el siguiente:

- 1. El sitio responsable de la consulta utiliza el diccionario de datos global y reconstruye una vista global de los fragmentos a consultar y de su ubicación.
- 2. El planificador global lanza consultas locales en todos los sitios que almacenan los fragmentos, o bien, si los datos están replicados, en el sitio que presente una menor carga y una mayor velocidad de comunicación.
- 3. El planificador global crea un plan de ejecución distribuido, cuyo principal objetivo es el de evitar, en lo posible, las transferencias de datos entre diferentes sitios. Este plan contempla la ubicación de los fragmentos, el orden en el que se ejecutará cada paso de la consulta y las operaciones relacionadas con los resultados intermedios.
- 4. Los planificadores locales optimizan las consultas locales, que se consolidan mediante una operación de unión de tipo *UNION*, si se trata de fragmentos horizontales, o de tipo *JOIN* si estos fueran verticales.

Se pueden utilizar diversas técnicas para mejorar el rendimiento del SGBDD en la ejecución de las consultas. Una de ellas es optimizar el uso de los recursos del sistema según criterios como el coste de las comunicaciones o la capacidad de proceso de los sitios involucrados. Para ello podemos utilizar, básicamente, tres enfoques:

- **Envío de los datos**: los fragmentos de datos se envían al cliente desde el que se realiza la consulta, y donde se ejecutará la operación. Este enfoque suele utilizarse cuando los operandos se ubican en sitios distintos, o cuando el coste de las comunicaciones es bajo y la capacidad de proceso del sitio cliente es mayor que la de los sitios locales donde residen los datos.

![](_page_162_Diagram_5.jpeg)

- **Envío de la operación**: las operaciones se ejecutan en los sitios donde residen los datos, y el resultado se transfiere al sitio cliente. Esta suele ser la mejor estrategia cuando los operandos están disponibles en un mismo sitio.

![](_page_163_Picture_2.jpeg)

![](_page_163_Diagram_5.jpeg)

*Optimización de recursos mediante el envío de la operación.*

- **Envío híbrido**: en este caso, los fragmentos de datos se envían a los equipos con mayor capacidad de proceso, los cuales ejecutan la operación y envían el resultado al cliente.

![](_page_163_Diagram_10.jpeg)

*Optimización de recursos mediante el envío híbrido de datos y operación.*
