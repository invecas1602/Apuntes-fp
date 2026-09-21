# **6.4. Técnicas de replicación**

Como sabemos, la replicación, en el contexto de un SGBDD, puede definirse como el proceso de realizar copias de una BD en uno o más nodos del sistema como técnica para reforzar su tolerancia a errores.

Aunque es una práctica común, la replicación de datos tiene ventajas y desventajas que debemos sopesar antes de aplicarla a nuestro sistema. Entre sus ventajas podemos citar las siguientes:

- **Transacciones más simples**: cuando la BD está íntegramente replicada, las consultas pueden realizarse en la copia local, lo que simplifica las consultas. Esto, a su vez, reporta dos grandes beneficios:
  - **Descongestión de la red**: al no tenerse que recabar datos de otros nodos, el tráfico de red se aligera, especialmente en las horas de máxima demanda. En consecuencia, y para equilibrar el uso de la red, la actualización de los datos en los diferentes nodos puede realizarse en horario de baja demanda.
  - **Mejores tiempos de respuesta**: cuando existen réplicas locales de las BD en los nodos, el procesamiento de las consultas resulta más rápido.
- **Fiabilidad del sistema**: el fallo de uno de los nodos no detiene el sistema, ya que las BD están disponibles en los otros nodos.

Por su parte, podemos resumir las desventajas de la replicación de datos en los puntos siguientes:

- **Incremento en los costes**: lógicamente, mantener una copia de las BD en cada nodo exige una mayor inversión en sistemas de almacenamiento, así como en los costes de derivados de dar soporte a la complejidad del sistema, lo que casi siempre implica gastos de personal, comunicaciones, hardware, instalaciones, etc.
- **Inconsistencia en los datos**: el hecho de trabajar con diferentes copias de las BD induce un nivel de inconsistencia en los datos derivado de las actualizaciones que se pueden realizar en los diferentes nodos. Si no se emplean los mecanismos de actualización adecuados (que, por otra parte, requieren de un nivel elevado de coordinación a nivel de aplicación), se incurre en el peligro de que las BD pierdan su consistencia.

Existen diferentes técnicas de replicación, disponibles según el sistema gestor que estemos utilizando, algunas de las cuales son:

- **Replicación de instantáneas**: los datos se distribuyen tal como aparecen en un momento dado en el tiempo, y no se monitorizan

A la hora de distinguir los sistemas que intervienen en un **proceso de replicación**, podemos referirnos al sistema en el que se ubican los datos a replicar —y sobre el cual recaerá la carga principal del proceso—, como el *publicador*, mientras que llamaremos *suscriptores* al resto de los sistemas en los cuales se realiza la copia de los datos replicados.

### Para + info

las actualizaciones entre una imagen y la siguiente. Con esta técnica, se genera una imagen completa de los datos en el momento de realizar la replicación, y a continuación se distribuye a todos los sistemas suscritos.

Las instantáneas se utilizan principalmente al realizar una primera copia completa de los datos, y también se recomienda en algunos casos concretos, como cuando se maneja un volumen muy reducido de datos, cuando los datos apenas registran cambios a lo largo del tiempo, o bien, por el contrario, cuando registran muchos cambios pero de manera muy infrecuente.

Dado que no se realizan copias incrementales, la carga continua sobre el publicador es más reducida que utilizando otras técnicas, si bien los recursos dedicados se incrementarán, en un grado proporcional al volumen de datos replicados, en el momento de generar y distribuir las instantáneas.

- **Replicación de mezcla**: este método suele utilizar una instantánea como punto inicial de las réplicas, y utilizar un mecanismo basado en desencadenadores para ir sincronizando los datos. De esta forma, los suscriptores se van sincronizando periódicamente con el publicador para actualizar las filas que hayan cambiado en cada uno.

Este es el método típico de las arquitecturas cliente-servidor, y, en general, resulta adecuado cuando los suscriptores actualizan sus datos sin conexión de red, o bien cuando cada suscriptor utiliza una partición de datos distinta.

En definitiva, la replicación de mezcla ofrece autonomía a los diferentes sitios, ya que el agente de mezcla —componente encargado combinar los cambios incrementales en las BD— implementa mecanismos que permiten resolver los conflictos que pueden darse cuando se actualizan, de forma simultánea, las mismas filas en distintos nodos. Por este motivo, también resulta una técnica útil para detectar y resolver inconsistencias.

- **Replicación transaccional**: al igual que la replicación de mezcla, se inicia con una instantánea de los datos y objetos de las BD replicadas, y los cambios que se registren en el publicador se entregan, casi en tiempo real, a los suscriptores.

Este tipo de replicación suele realizarse entre servidores, donde interesa que los cambios incrementales se repliquen en cuanto ocurren, o cuando las aplicaciones necesitan acceder a los datos actuales de las filas. También resulta adecuada cuando los datos sufren constantemente un elevado número de actualizaciones.

Hay que tener en cuenta que, en el modelo transaccional estándar, los suscriptores son de solo lectura, ya que la propagación de los cambios es unidireccional (del publicador a los suscriptores), aunque se contemplan dos tipos de publicación que permiten actualizar también los datos en los suscriptores; estos son:

- **Topología punto a punto**: los sitios funcionan, al mismo tiempo, como publicadores y suscriptores, con la limitación de que una misma fila se puede cambiar solo en una ubicación a la vez.
- **Replicación transaccional bidireccional**: similar a la anterior, aunque, en este caso, limitada únicamente a dos servidores.

### **6.4.1. Configuración de la replicación en MySQL**

En MySQL, las replicaciones se realizan de forma asíncrona o semi-síncrona, unidireccional, y normalmente entre un **servidor maestro** (el publicador) y uno o varios **servidores esclavos** (los suscriptores). Es el servidor maestro el que mantiene los registros binarios de actualizaciones, que utilizará cuando un servidor esclavo de conecte a él con el fin de poner al corriente sus datos.

No obstante, en MySQL existe también la posibilidad de operar en modo **maestro dual** (no existen servidores esclavos, únicamente dos maestros sincronizados con una BD compartida), o utilizando un diseño de **replicación en cadena**, que se produce cuando la información replicada en un esclavo se replica, a su vez, en otro esclavo conectado al primero. Mediante esta técnica es posible crear un anillo de replicación donde todos los servidores conectados actúan como esclavos del anterior y maestros del siguiente dentro del anillo.

Para configurar la replicación en MySQL, es necesario contar, en el servidor maestro, con el privilegio *SUPER*, mientras que, para conectarse al maestro, los servidores esclavos deben utilizar una cuenta (idealmente, dedicada solo a este cometido) con el privilegio *REPLICATION SLAVE*. Además, para utilizar las instrucciones *LOAD TABLE FROM MASTER* y *LOAD DATA FROM MASTER* desde un servidor esclavo, la cuenta deberá contar también con los privilegios globales *SUPER* y *RELOAD*, y con el privilegio *SELECT* para todas las tablas que se deseen cargar.

### Atención

![](_page_152_Picture_1.jpeg)

Supongamos que, dentro de nuestro dominio *ilerna.com*, queremos inicializar un nuevo servidor esclavo.

En primer lugar, detenemos el servidor maestro y abrimos su archivo de configuración (*my.ini* o *my.cnf*). En él deberemos incluir el nombre base de los archivos de registro binario, si no estuviera ya presente (por ejemplo, *SERVIDOR01-bin*), junto con otras dos opciones que sirven para asegurar una mayor consistencia en las transacciones InnoDB:

[mysqld] Log-bin=SERVIDOR01-bin innodb\_flush\_log\_at\_trx\_commit=1 sync\_binlog=1

Por defecto, el identificador de servidor es 1, pero podemos cambiarlo, en el archivo de configuración, con la opción *server-id*, o bien de forma dinámica con la siguiente instrucción:

SET GLOBAL server\_id = 10;

En el servidor esclavo, editaremos también el archivo de configuración, asegurándonos de que posee un identificador de servidor distinto al del servidor maestro:

[mysqld] server-id=2

A continuación, reiniciamos los servidores, y crearemos, en el servidor maestro, una cuenta para replicación con la que poder conectar desde cualquier máquina de nuestro dominio, asignándole los privilegios que necesitemos (en nuestro caso, el de esclavo de replicación):

CREATE USER 'repl'@'%.ilerna.com' IDENTIFIED BY 'contraseña';

GRANT REPLICATION SLAVE ON \*.\* TO 'repl'@'%.ilerna.com';

El siguiente paso consiste en la realización del volcado binario de las tablas del servidor maestro, bloqueando las sentencias de escritura. Iniciamos una nueva sesión de *mysql* en el servidor maestro, y ejecutamos lo siguiente:

FLUSH TABLES WITH READ LOCK;

En una sesión distinta, determinamos el nombre (*File*) y posición (*Position*) del archivo generado:

Ahora ya estamos listos para configurar la comunicación de la réplica con la fuente; en nuestro ejemplo, podríamos hacerlo mediante la siguiente sentencia:

1 CHANGE REPLICATION SOURCE TO 2 SOURCE\_HOST='Servidor01.ilerna.com', 3 SOURCE\_USER='repl', 4 SOURCE\_PASSWORD='*contraseña*', 5 SOURCE\_LOG\_FILE='SERVIDOR01-bin.000001', 6 SOURCE\_LOG\_POS=157;

Finalmente, iniciamos el proceso de replicación:

START REPLICA;

Y para detener la replicación, utilizaremos la siguiente instrucción:

STOP REPLICA;

Si deseamos conocer el estado de la replicación, podemos utilizar las siguientes instrucciones para conocer el estado del servidor maestro y del servidor esclavo, respectivamente:

SHOW MASTER STATUS\G SHOW REPLICA STATUS\G

La información del esclavo incluye los posibles errores que se hayan podido producir durante la replicación. Por ejemplo, si no se ha podido conectar con el maestro, lo veremos reflejado en los campos *Last\_IO\_Errno* y *Last\_IO\_Error*; o bien, si queremos saber si los hilos de E/S y SQL están funcionando, deberemos revisar los campos *Slave\_IO\_Running* y *Slave\_SQL\_Running*.

Además, acerca de los esclavos, podemos conocer su identificador de servidor, nombre de anfitrión, puerto, maestro al que están suscritos y UUID, mediante la siguiente sentencia:

SHOW REPLICAS;

Si estamos configurando una **nueva combinación de fuente y réplica**, una vez realizado el volcado podemos salir de la sesión para eliminar el bloqueo de lectura.

Por el contrario, si necesitáramos sincronizar datos con el esclavo antes de proceder a una nueva réplica, debemos dejar el bloqueo activo hasta haber completado la operación.

![](_page_154_Picture_4.jpeg)

### Atención

### Para + info

En el apartado 13.4.2.3 del manual en línea de MySQL se detallan las opciones de la sentencia *CHANGE REPLICATION SOURCE TO*.

[bit.ly/3X3zRSr](http://bit.ly/3X3zRSr)

![](_page_154_Picture_8.jpeg)

### Atención

![](_page_155_Picture_0.jpeg)
