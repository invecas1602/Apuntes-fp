# **5.3. Optimización del servidor**

Gracias a las técnicas de monitorización descritas en este capítulo, así como al análisis de los planes de ejecución, podremos detectar los puntos donde un servidor, o una BD en particular, tienen sus principales **problemas de rendimiento**. En este apartado abordaremos diferentes técnicas para minimizar dichos problemas. En primer lugar, hay que tener presente que la plena optimización de un servidor requiere de un enfoque sistemático en el que se analice el sistema, tanto a nivel de base de datos, como a nivel de hardware.

En general, los cuellos de botella susceptibles de ocasionar un impacto sobre el rendimiento de una BD suelen producirse por una mala configuración u optimización de los dispositivos de almacenamiento, por problemas con la configuración de la memoria, o a causa de un excesivo nivel de fragmentación de las tablas en las bases de datos.

Por otra parte, pueden producirse también problemas de configuración del software que afecten a la estabilidad del servidor, provocando errores en las consultas o incluso la detención total del sistema, lo cual, lógicamente, puede tener un impacto directo y severo sobre el rendimiento y disponibilidad del servidor.

### **5.3.1. Optimización de las bases de datos**

Uno de los principales factores que influyen en el rendimiento de una base de datos es su propio diseño, y en particular, si las tablas están bien construidas, es decir, si constan del número de columnas requerido, y se ha asignado el tipo de datos más adecuado a cada una de ellas. Así, dependiendo del propósito de la BD, puede ser mejor tener pocas tablas con muchas columnas (por ejemplo, si trabajamos con grandes volúmenes de datos), o muchas tablas con pocos campos (por ejemplo, si tenemos que actualizarlas con mucha frecuencia).

Lógicamente, y como ya hemos apuntado, el tipo y número de índices que utilicemos deberá adecuarse a los condicionantes de cada BD para optimizar las búsquedas.

### **Optimizar el motor de almacenamiento**

Sin embargo, uno de los factores que pueden tener un mayor peso el rendimiento de un BD es el motor de almacenamiento utilizado, ya que para ciertas tablas puede resultar más apropiado un motor transaccional, como InnoDB (por defecto en MySQL), o un motor no transaccional como MyISAM. Aunque las características avanzadas de InnoDB hacen que las tablas sobre este motor rindan más, en general, que las tablas MyISAM —por ejemplo, la compresión de los datos está disponible para cualquier tipo de tabla InnoDB, pero únicamente para las de solo lectura con MyISAM—, no siempre es posible trabajar con el motor deseado, especialmente en entornos de producción legados.

![](_page_130_Picture_2.jpeg)

En MySQL, podemos usar el archivo de configuración *my.ini* o *my.cnf* para optimizar el motor InnoDB mediante los siguientes parámetros:

Una de las principales **ventajas de InnoDB**  sobre MyISAM es que dota de transparencia al mecanismo que maneja los accesos compartidos. De esta forma, InnoDB puede trabajar de forma concurrente la mayor parte del tiempo, y, cuando sea necesario, conceder accesos exclusivos para operaciones críticas con un alto nivel de prioridad, y todo ello sin intervención del usuario.

### Para + info

| Tipo de registro        | Información registrada                           |
|-------------------------|--------------------------------------------------|
|                         | Ubicación del archivo ibdata1 , donde se alma   |
| innodb_buffer_pool_size | Tamaño del grupo de búferes que InnoDB           |
| innodb_log_file_size    | Tamaño de los archivos de registro de InnoDB.    |
| innodb_log_buffer_size  | Tamaño del búfer de los archivos de registro. Su |
|                         | fsync() , aunque es posible usar el método       |
|                         | O_DIRECT para realizar las operaciones de E/S    |

![](_page_130_Picture_7.jpeg)

Profundizaremos en el uso de algunos de los parámetros que hemos recogido en la tabla anexa en la sección dedicada a la optimización de la memoria.

**5.3.3.** *Optimización de la memoria*

Visita las páginas

### **5.3.2. Optimización del almacenamiento**

Con respecto al almacenamiento, los principales cuellos de botella suelen encontrarse en el propio hardware, es decir, en los sistemas físicos en donde se registran y desde donde se recuperan los datos.

En particular, los dos aspectos principales a tener en cuenta son las **búsquedas en disco**, y la **velocidad de lectura y escritura** de los datos. Estos parámetros van mejorando conforme avanzan las tecnologías de almacenamiento, por lo que, en general, cuando se llega al límite de las características técnicas de los soportes, la opción más aconsejable es reemplazarlos.

No obstante, para mejorar la velocidad de las búsquedas podemos distribuir los datos en diferentes discos, mientras que, para aumentar la velocidad de lectoescritura, podemos leer varios discos en paralelo. Por estos motivos, lo más recomendable es utilizar conjuntos de SSD dispuestos en una matriz de discos denominada RAID.

### **Sistemas RAID**

El tipo de RAID a utilizar dependerá de si prima la tolerancia a fallos o la velocidad, así como del número de discos que formen parte del sistema.

Existen 7 niveles RAID básicos, pero aquí abordaremos únicamente los más utilizados.

Si el factor crítico es la velocidad, una RAID 0 es la más adecuada, ya que su propósito es exclusivamente el de mejorar el rendimiento de las operaciones de lectura y escritura de archivos, almacenando los datos en dos o más discos y usándolos en paralelo.

En una RAID 0, los archivos se reparten en bloques físicos denominados bandas o *strips*, que se distribuyen entre todos los discos de forma rotativa. Los discos no tienen por qué ser del mismo tamaño ni ofrecer la misma tasa de datos, pero el espacio utilizable en cada uno de ellos quedará limitado al espacio ofrecido por el soporte de menor capacidad. En cuanto a la tasa total de datos, será la del disco más lento multiplicada por el número total de discos; en esta configuración, todos los discos funcionan a la tasa de datos más baja, pero esta se suma a una tasa de conjunto. Eso sí, en este nivel no existe redundancia de datos, por lo que, si falla un disco o se eliminan datos por accidente, solo podremos recuperarlos desde una copia de seguridad almacenada fuera de la RAID.

![](_page_132_Picture_0.jpeg)

Por el contrario, una RAID 1 es un sistema de volúmenes reflejados (*mirroring* en inglés). La redundancia de datos es completa, ya que se realiza una copia de cada archivo, de manera que, si cualquiera de los discos fallara, el conjunto pasaría a funcionar en modo reducido, pero no se perderían datos.

Un sistema RAID 1 permite leer en paralelo bandas distintas y usar el disco más rápido para recuperar los datos, lo que aumentará el rendimiento en las operaciones de lectura, pero, en cambio, las operaciones de escritura se realizarán por partida doble y a la velocidad del disco más lento, por lo que no es el sistema adecuado para buscar un aumento en el rendimiento de la BD.

Si disponemos de un número mínimo de 3 discos, y queremos aumentar el rendimiento sin sacrificar la redundancia, podemos usar una RAID 5, que intercala bandas de paridad en cada disco, de forma rotativa, para minimizar el coste de redundancia, ya que no requiere de un disco de paridad dedicado (los discos de paridad se utilizan, en este caso, como mecanismo de corrección de errores).

Aunque podríamos decir que el RAID 5 ofrece los mejor de los dos mundos, es posible anidar dos o más niveles RAID básicos para formar un sistema combinado que amplíe las posibilidades de los niveles básicos. Por ejemplo, una RAID 01 (0+1) está formada por la combinación de una RAID 0 con una RAID 1, es decir, se crea un volumen distribuido entre varios discos, y un espejo de dicho volumen formado por un idéntico número de discos donde se replicará la información de la RAID 0. Otra RAID muy utilizada es la 10 (1+0), en la que partimos de dos matrices de discos en espejo —es decir, dispuestas en una RAID 1—, y se crea con ellas un nuevo volumen distribuido usando RAID 0.

### **Desfragmentación de tablas**

Un problema habitual relacionado con el almacenamiento dedicado al SGBD, es la **fragmentación** de los archivos de datos. Esto sucede cuando las tablas se actualizan con mucha frecuencia, efectuándose constantes operaciones de borrado e inserción de datos, lo cual dejará en la base de datos mucho espacio sin utilizar, y, además, puede afectar también al rendimiento del sistema.

En una **RAID 5** podemos aprovisionar un disco de reserva (spare en inglés) para poder reemplazar rápidamente cualquiera de los discos de la matriz en caso de fallo. Si el disco está conectado y listo para su uso, se lo denomina *hot spare* y si está en reposo, recibe el nombre de *standby spare*. Este tipo de RAID se denomina 5E.

### Para + info

Podemos identificar fácilmente una base de datos fragmentada con una sentencia como la siguiente (suponiendo que el nombre de la base de datos a analizar sea *empresa*):

1 USE empresa; 2 SELECT table\_name AS tabla, 3 ROUND(data\_length/1024/1024) AS tamaño\_datos\_mb, 4 ROUND(data\_free/1024/1024) AS espacio\_libre\_mb 5 FROM information\_schema.tables 6 WHERE ROUND(data\_free/1024/1024) > 500 7 ORDER BY espacio\_libre\_mb;

El resultado podría ser similar al siguiente:

+----------+-----------------+------------------+ | tabla | tamaño\_datos\_mb | espacio\_libre\_mb | +----------+-----------------+------------------+ | clientes | 8654 | 4668 | +----------+-----------------+------------------+

Lo que hace la sentencia es listar las tablas con más de 500 MB de espacio sin utilizar (podemos cambiar este umbral editando la línea 5), y el resultado nos muestra que la tabla clientes tiene un tamaño de unos 8,5 GB, que incluye un espacio sin usar de en torno a 4,5 GB. Esto indica un muy alto nivel de fragmentación, que podemos reducir utilizando la sentencia *OPTIMIZE TABLE*:

OPTIMIZE TABLE clientes;

En MySQL, podemos optimizar tablas InnoDB, MyISAM y de tipo ARCHI-VE. Esto hará también que las páginas índice se reordenen, y actualizará la información estadística.

Otro método para desfragmentar tablas es mediante el uso de la instrucción *mysqlcheck*:

> mysqlcheck -o empresa clientes -u root -p*contraseña*

Con esta instrucción, podemos optimizar todas las tablas de una base de datos, o todas las bases de datos del SGBD:

> mysqlcheck -o empresa -u root -p*contraseña*

Tras la optimización de las tablas, y si ejecutamos de nuevo la consulta de utilización de espacio anteriormente descrita, deberemos observar una reducción drástica del espacio que estas ocupan. De la misma forma, el valor de la columna *espacio\_libre\_mb* tendrá que ser 0 en todos los casos, ya que no debería existir espacio alguno sin utilizar en las tablas optimizadas:

+----------+-----------------+------------------+

| tabla | tamaño\_datos\_mb | espacio\_libre\_mb |

+----------+-----------------+------------------+

| clientes | 3134 | 0 |

+----------+-----------------+------------------+

![](_page_134_Picture_2.jpeg)

### **5.3.3. Optimización de la memoria**

Según el motor de almacenamiento utilizado, existen también diferencias en el modo en que la memoria se emplea para almacenar los datos más utilizados de forma temporal. En general, los tamaños de caché deben estar suficientemente dimensionados como para dar cabida a estos datos, pero sin llegar a sobrecargar la memoria física, lo cual implicaría el uso del archivo de paginación del sistema operativo, degradando el rendimiento de la BD.

El tamaño de la caché del procesador también es importante, ya que, si este resulta insuficiente para dar cabida a todos los datos que deber procesar, se producirá un cuello de botella en el ancho de banda de la memoria.

Existen numerosos factores a considerar cuando se trata de optimizar la memoria, pero, en general, los procesos relacionados con un SGBD dedicado nunca deberían ocupar más del 90% de la memoria total del sistema.

En la versión de MySQL para Linux, podemos ver la memoria virtual que está utilizando el proceso *mysqld* en cada momento ejecutando la instrucción *ps aux | grep mysqld*, mientras que, bajo Windows, deberemos recurrir al Administrador de tareas y buscar el proceso *mysqld.exe.*

El parámetro que se utiliza para asignar el tamaño de la memoria virtual es, en las BD que utilizan el motor InnoDB de MySQL, *innodb\_buffer\_ pool\_size*, y su valor normalmente debe situarse entre el 50% y el 75% de la memoria física del sistema. En MyISAM, el parámetro equivalente sería *key\_buffer\_size*, y habría que asignarle entorno a un 40% de la memoria del sistema.

Si optimizamos tablas InnoDB, recibiremos un mensaje indicando que no se soporta la optimización, y que se efectuará una operación de recreación y análisis en su lugar (*Table does not support optimize, doing recreate + analyze instead*). Esto es debido a que, en lugar de desfragmentar directamente los archivos de la BD, como sucede con tablas MyISAM, en las tablas InnoDB el sistema efectúa una operación de tipo *ALTER TABLE* para reclamar el espacio sin utilizar. No obstante, el resultado final será el mismo, y, si la optimización ha tenido éxito, deberemos ver el mensaje de confirmación *status*: *OK.*

### Para + info

Para ver el valor actual de este parámetro (en GB), utilizaremos la sentencia siguiente:

### SELECT @@innodb\_buffer\_pool\_size/1024/1024/1024;

Por otra parte, hay que tener en cuenta que el tamaño óptimo de los archivos de registro de InnoDB, que se utilizan para recuperar el servidor en caso de fallo, y que se establecen mediante el parámetro *innodb\_log\_file\_size*, debe estar en consonancia con el tamaño asignado al grupo de búferes, y se recomienda que se sitúe entorno al 25% de dicho tamaño.

Además, es necesario prever el uso de memoria para funciones como el manejo de las conexiones y otros búferes globales, como el búfer de registro o las cachés de tablas, y también para el esquema de rendimiento, en caso de tenerlo activado. Esta cantidad de memoria, que puede situarse fácilmente entre 500 y 1.500 MB, no se incluye en el tamaño del grupo de búferes, y por lo tanto debe deducirse de dicha cifra.

Por último, debemos considerar el número de instancias del grupo de búferes. Estas instancias son subdivisiones del búfer que mejoran la concurrencia de las operaciones de lectura y escritura de las páginas en caché, y su cantidad se define mediante el parámetro *innodb-buffer-pool-instances*.

Por defecto, el número de instancias es 8, excepto si el tamaño del grupo de búferes es inferior a 1 GB, en cuyo caso será de 1. No obstante, y dado que no se recomienda tener instancias de grupo de búferes con menos de 1 GB de memoria, una buena práctica para determinar el número óptimo de instancias es dividir por 1,5 el tamaño del grupo de búferes, de forma que, a cada instancia, correspondan 1,5 GB de memoria.

Para ver el número actual de instancias, podemos usar la siguiente sentencia:

SELECT @@innodb\_buffer\_pool\_instances;

De esta forma, en un servidor con 16 GB de memoria dedicado en exclusiva a MySQL, una configuración estándar de InnoDB, en el archivo de configuración *my.ini* o *my.cnf*, podría ser la siguiente:

[mysqld] innodb\_buffer\_pool\_size = 12G innodb\_log\_file\_size = 3G innodb-buffer-pool-instances = 8 La opción *innodb\_buffer\_pool\_size* puede definirse también de forma dinámica (en bytes) utilizando *SET*:

SET GLOBAL innodb\_buffer\_pool\_size = 3221225471;

El número debe ser múltiplo del número de instancias (*innodb-buffer-pool-instances*) multiplicado por el tamaño de *innodb\_buffer\_pool\_chunk\_size*, que define el tamaño de los fragmentos de memoria en que se subdivide cada instancia — por defecto, 134217728 bytes (128 MB). Por lo tanto, en el ejemplo anterior, y suponiendo que tengamos dos instancias, basta con dividir 3221225472 entre 2, y el resultado entre 134217728, para conocer el número total de *chunks* por instancia (en este caso, 12).

### **5.3.4. Depuración de errores**

Con el fin de localizar problemas si el servidor no se inicia o falla con frecuencia, es posible utilizar una versión compilada con soporte para depuración de errores de *mysqld* para crear un archivo de trazas. En Windows, este programa está incluido en algunas instalaciones de MySQL, se denomina *mysql-debug.exe*, y podemos iniciarlo con la siguiente instrucción:

> mysqld-debug --debug --standalone

Una vez iniciado el servidor en modo depuración (opción --*debug*), y no como servicio de Windows (opción --*standalone*), podemos utilizar *mysql.exe* para reproducir el error, cuya huella quedará registrada en el archivo de trazas. El formato de dicho archivo obedece al paquete DBUG, con el que se compila el servidor de MySQL.

Ponte a prueba

**Qué tipo de RAID es el que permite reflejar los volúmenes para obtener una redundacia completa de los datos?**

- a) RAID 0
- b) RAID 5
- c) RAID 1
- d) RAID 7

![](_page_137_Picture_0.jpeg)

![](_page_137_Picture_2.jpeg)

**SISTEMAS GESTORES DE BASES DE DATOS DISTRIBUIDAS Y REPLICADAS**
