# **5.2. Optimización de consultas**

### **5.2.1. Índices**

![](_page_122_Picture_3.jpeg)

Los **índices** son tanto más útiles cuanto más grandes son las tablas indizadas, aunque también elevan los requerimientos de espacio de la base de datos y conllevan un aumento en las operaciones de escritura, lo que puede degradar el rendimiento de las tablas que se actualizan muy a menudo. Por estos motivos, es aconsejable utilizar los índices con criterio basándonos en dos consideraciones fundamentales: el **tipo de datos** que se van a manejar, y la **clase de consultas** que se van a realizar con mayor frecuencia (búsqueda de patrones, de igualdades, de mayor o menor, etc.).

Cada SGBD maneja un conjunto particular de índices, y sus ventajas y desventajas son, en gran medida, propias de cada sistema, por lo que, en esta sección, haremos un repaso de las características genéricas de los tipos de índice más utilizados, aunque con especial énfasis en los que están disponibles en MySQL:

- **B-tree (***Balanced Tree***)**: índice en forma de árbol donde todas las páginas hoja del índice están separadas de la página raíz por el mismo número de nodos o páginas internas. Las páginas hoja son las que se sitúan al final del árbol apuntando a la ubicación física de las filas a las que hacen referencia (los llamados identificadores de tupla, o TID).

En general, los índices B-tree están especialmente indicados en operaciones de búsqueda y cuando se vayan a utilizar con frecuencia operadores del tipo *<*, *<=*, *=*, *>=*, *BETWEEN*, *IN*, *IS NULL* e *IS NOT NULL*.

En MySQL son los índices más comunes, ya que, en la mayor parte de las ocasiones, mejoran las consultas de tipo *SELECT*; por ejemplo:

Los **índices** son esenciales para acelerar las consultas, ya que son el mecanismo que nos permite ordenar los datos de una BD para poder localizar rápidamente valores de columna específicos. De hecho, en una tabla no indizada, es necesario recorrer todos los registros, uno por uno y de manera secuencial, para localizar todas las coincidencias en una búsqueda, mientras que un índice nos proporcionará acceso rápido aleatorio a los datos relevantes.

Es importante remarcar que, si utilizamos comodines, estos deben ir siempre al final de la cadena de búsqueda (por ejemplo, 'Delgado%'):

- **Hash**: en general, este tipo de índice solo puede utilizarse en comparaciones de igualdad, es decir, con los operadores *=* y *<=>*, pero están mejor optimizados para este fin que los de tipo B-tree.

En MySQL, solo el motor de almacenamiento en memoria (*MEMORY*) puede usar índices *hash*.

- **SP-GiST (***Space-Partitioned GiST***)**: específicamente indicados para trabajar con estructuras de datos no equilibradas (es decir, cuando los datos se agrupan por propia naturaleza de manera no uniforme), como los datos de un SIG (sistema de información geográfica), tablas de enrutamiento IP, etc. Soportan el uso de los operadores *<<, >>, ~=, <@, <^, >^,* así como las búsquedas proximales.

En MySQL, reciben en nombre de **índices espaciales**.

- **Índices de prefijo**: en MySQL, se utilizan cuando el espacio en disco escasea y buscamos un índice más ligero que uno del tipo B-tree, ya que se realiza una indización parcial de la columna, lo cual, además de hacer más pequeño el índice, suele acelerar las búsquedas.

- **Índices compuestos, o multicolumna**: en MySQL, este es el nombre que reciben los índices que se emplean cuando se van a realizar búsquedas en dos o más columnas; por ejemplo:

SELECT \* FROM clientes WHERE apellidos = 'Delgado' AND ciudad = 'Madrid';

- **Índices de cobertura**: en MySQL, estos índices abarcan todas las columnas de la tabla, lo que hace innecesario usar la tabla en sí al realizar las consultas. La ventaja de esta aproximación es que reducimos las operaciones de E/S en disco, ya que los índices son más pequeños que las tablas. Las consultas a realizar serían del tipo:

SELECT nombre, apellido, calle, ciudad, cp WHERE apellidos = 'Delgado';

- **Índices agrupados o** *clusterizados*: se trata esencialmente de claves primarias o índices únicos con todas sus columnas definidas como *NOT NULL*, y se utilizan cuando una columna se incrementa automáticamente al añadirse un dato en otra columna. MySQL crea automáticamente un índice agrupado llamado *PRIMARY* —que no es más que tabla almacenada en una estructura de índice B-tree siempre que una columna de la tabla contenga una clave primaria o única. Cualquier otro índice adicional se considerará secundario.

Otro tipos de índice no disponibles en MySQL son:

- **BRIN (***Block Range Index***)**: se puede emplear en columnas con un orden lineal, como por ejemplo los campos de fecha y hora en una tabla de ventas, y está especialmente indicado para el uso en tablas masivas al ser más fácil de mantener y ocupar mucho menos espacio que un índice B-tree. Esto es así porque, en este caso, el índice solo almacena en cada página los valores mínimo y máximo de la columna indizada.
- **GIN (***Generalized Inverted Index***)**: se usa para indizar tipos de datos de valor múltiple, como matrices (*array*), JSON (*jsonb*), rangos (*range*), etc., ya que no indiza el valor completo de la columna sino elementos individuales, lo cual lo hace también apropiado para la búsqueda de textos.
- **GiST (***Generalized Search Tree***)**: índice en forma de árbol equilibrado (similar a un B-tree) que resulta útil en columnas con valores de tipo geométrico bidimensionales, así como para trabajar con búsquedas proximales (o de *nearest-neighbour*), con datos dinámicos y en la búsqueda de textos.

A la hora de optar por uno u otro tipo de índice, los principales factores a considerar son el tipo de motor de almacenamiento que estamos utilizando, los tipos de datos que manejamos, qué columnas necesitamos indizar, cuál es el tamaño de la tabla y cuál es la finalidad del índice.

En MySQL, podemos crear un índice B-tree utilizando la sentencia *CREATE INDEX*:

CREATE INDEX nombre\_del\_índice ON nombre\_de\_tabla (lista\_de\_columnas)

Por ejemplo, para crear un índice compuesto, podríamos usar una sentencia del tipo siguiente:

CREATE INDEX nombre\_apellidos ON clientes (nombre, apellidos);

Para conocer los índices de una tabla, se utiliza la sentencia *SHOW INDEXES*:

SHOW INDEXES FROM clientes;

Y para eliminar un índice, DROP INDEX:

### **5.2.2. Planes de ejecución**

![](_page_125_Picture_2.jpeg)

De esta forma, cuando existen varias posibilidades a la hora de ejecutar una sentencia, para decidir la mejor estrategia el planificador debe estimar el *coste de ejecución* que tendrá cada una antes de que se pueda devolver la primera fila, y el coste final tras haber devuelto todas las filas como resultado de la sentencia.

Para obtener un plan de ejecución se utiliza la instrucción *EXPLAIN* seguida de la sentencia a evaluar, como por ejemplo el listado de personas que se apellidan *Delgado* en la tabla *clientes*:

EXPLAIN SELECT \* FROM clientes WHERE apellidos='Delgado';

*EXPLAIN* funciona exclusivamente con sentencias *SELECT, INSERT, UP-DATE, REPLACE* y *DELETE*. El planificador nos proporciona una tabla con información acerca de cómo se ejecuta la sentencia *SELECT* especificada. Las columnas de dicha tabla son las siguientes:

Llamamos **plan de ejecución** a la lista de instrucciones que el SGBD necesita ejecutar, una tras otra, para llevar a cabo una consulta. Se elabora con base a diferentes estrategias de ejecución: método de acceso a las tablas (escaneo secuencial, de índice, etc.), el uso de las cláusulas de agrupación o el de los algoritmos de combinación (*JOIN*), entre otras.

| Tipo de registro | Información registrada                                   |
|------------------|----------------------------------------------------------|
| id               | Identificador de SELECT.                                 |
| select_type      | Tipo de SELECT.                                          |
| table            | Nombre de la tabla de la fila de salida.                 |
| partitions       | Particiones coincidentes.                                |
| type             | Tipo de unión.                                           |
| possible_keys    | Posibles índices a elegir.                               |
| key              | Índice escogido.                                         |
| key_len          | Longitud de la clave escogida.                           |
| ref              | Columnas comparadas con el índice.                       |
| rows             | Estimación de las filas que se examinarán.               |
| filtered         | Porcentaje de filas filtradas por condición de la tabla. |
| Extra            | Información adicional.                                   |

![](_page_126_Picture_11.jpeg)

Cuando no tenemos índices, las columnas *possible\_keys* y *key* aparecen con valor nulo (*NULL*), y el número de filas examinadas (*rows*) se corresponderá, directamente, con el número total de filas de la tabla. Sin embargo, si creamos un índice en la columna apellidos y repetimos la consulta, veremos que solo se han tenido que recorrer las filas cuyo valor de columna coincide con la cadena buscada.

*EXPLAIN* nos indica qué índices ha evaluado antes de decidirse por uno de ellos. Esta decisión se toma teniendo en cuenta el número de índices presente y la construcción de cada uno. Vamos a verlo con un ejemplo:

![](_page_126_Picture_3.jpeg)

En primer lugar, creamos dos índices, uno sobre la columna apellidos, y otro multicolumna incluyendo nombre y apellidos:

CREATE INDEX apellidos ON clientes (apellidos);

CREATE INDEX nombre\_apellidos ON clientes (apellidos,nombre);

Si ejecutamos una consulta sobre la columna *apellidos*, el planificador optará por el índice más ligero, del de apellidos, ya que el nombre no figura como cadena de búsqueda. Sin embargo, ante esta otra búsqueda, se utilizará el índice *nombre\_apellidos*:

EXPLAIN SELECT \* FROM clientes WHERE nombre='Jorge' and apellidos='Delgado';

Es importante remarcar que, a la hora de crear índices multicolumna, el orden de las columnas especificadas importa, teniendo prioridad siempre la primera de ellas. Así, si realizamos una búsqueda sobre la columna *nombre*, no se utilizará el índice *nombre\_apellidos*, pese a haberse incluido esta columna en su definición.

De hecho, la ordenación de los campos a indizar debe obedecer a la frecuencia con la que estos aparecerán en las cláusulas *WHERE* que utilizaremos con mayor asiduidad, ya que los primeros campos tienen preferencia sobre los últimos. Por norma general, el planificador usará preferentemente el índice multicampo cuando el primero de los campos especificados en su creación aparezca en la cláusula *WHERE*.

En cuanto a los costes de ejecución, podemos obtenerlos utilizando la sentencia *EXPLAIN ANALYZE*. Tomemos, por ejemplo, el análisis de una consulta realizada sobre nuestra base de datos *filmoteca*.

![](_page_127_Picture_2.jpeg)

### La consulta es la siguiente:

1 SELECT título, director, género 2 FROM películas INNER JOIN géneros 3 ON películas.idGénero = géneros.idGénero 4 AND año LIKE '2022' 5 GROUP BY director, título;

### Y el resultado:

+--------------+------------------+---------+ | título | director | género | +--------------+------------------+---------+ | Bullet Train | David Leitch | Acción | | The Whale | Darren Aronofsky | Drama | +--------------+------------------+---------+

Ahora, utilicemos *EXPLAIN ANALYZE* para analizar el plan de ejecución:

1 EXPLAIN ANALYZE 2 SELECT título, director, género 3 FROM películas INNER JOIN géneros 4 ON películas.idGénero = géneros.idGénero 5 AND año LIKE '2022' 6 GROUP BY director, título;

### Obtenemos la siguiente información:

-> Table scan on <temporary> (cost=4.01..4.01 rows=1) (actual time=0.072..0.072 rows=2 loops=1) -> Temporary table with deduplication (cost=1.50..1.50 rows=1) (actual time=0.071..0.071 rows=2 loops=1) -> Nested loop inner join (cost=1.40 rows=1) (actual time==0.044..0.053 rows=2 loops=1) -> Filter: ((`películas`.`año` like '2022') and (`películas`.`idGénero` is not null)) (cost=1.05 rows=1) (actual time=0.033..0.040 rows=2 rows=1 loops=1) -> Table scan on películas (cost=1.05 rows=8) (actual time=0.027..0.032 rows=8 loops=1) -> Single-row index lookup on géneros using PRIMARY (idGénero=`películas`.`idGénero`) (cost=0.35 rows=1) (actual time=0.006..0.006 rows=1 loops=2)

Como podemos comprobar, en la salida de *EXPLAIN ANALYZE* se detallan, entre otros aspectos:

- El coste de cada operación (*cost*).
- El número de filas examinadas en cada caso (*rows*).
- El tiempo medio (en milisegundos) invertido en localizar la primera fila (primer valor de *actual time*).
- El tiempo medio (en milisegundos) invertido en localizar todas las filas (segundo valor de *actual time*).

Si únicamente nos interesan los valores de coste y número de filas, podemos utilizar *EXPLAIN FORMAT=TREE en lugar de EXPLAIN ANALYZE.*

![](_page_128_Picture_4.jpeg)

### Para + info

Para calcular sus costes de ejecución, los SGBD emplean unidades arbitrarias basadas en fórmulas que toman en cuenta el número bloques y de registros de una tabla, además de ciertos parámetros de rendimiento, como podrían ser el coste de recuperación por página, el coste de CPU por tupla y el coste de CPU por filtro.
