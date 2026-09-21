# **3.2. Consultas y vistas**

Los SGBD proporcionan una serie de sentencias para permitir a los usuarios debidamente autorizados la obtención y modificación de la información que almacenan. Gracias a estas instrucciones, podemos obtener una relación de las bases de datos, tablas, columnas de tabla y procesos existentes en dentro de una instancia de MySQL, así como acceso a los registros almacenados dentro de cada una de sus BD.

### **Introducción a las consultas**

Las consultas son el mecanismo que se utiliza para ver y modificar la información almacenada en las bases de datos que alberga cada instancia del SGBD. Sin entrar en el detalle de la sintaxis básica y opciones de cada una, las consultas más comunes son las que nos permiten realizar las siguientes operaciones:

- Crear una base de datos:

CREATE DATABASE filmoteca;

- Utilizar una base de datos:

USE filmoteca;

- Crear una tabla:

1 CREATE TABLE actores

2 (id INT AUTO\_INCREMENT PRIMARY KEY,

3 nombre VARCHAR(30) NOT NULL, 4 apellido VARCHAR(50) NOT NULL, 5 nacionalidad VARCHAR(50) NOT NULL

6 );

- Añadir, modificar y eliminar columnas de una tabla:

ALTER TABLE actores ADD fecha\_nacimiento DATE NOT NULL;

- Insertar registros en una tabla:

1 INSERT INTO 2 actores(nombre,apellido,nacionalidad,fecha\_nacimiento) 3 VALUES 4 ('Alison','Larter','Estados Unidos','1976-02-28');

- Mostrar los datos de las filas de una o más tablas:

SELECT \* FROM actores;

- Actualizar los registros de una tabla:

UPDATE actores SET nombre='Ali' WHERE id=1;

- Eliminar registros individuales de una tabla:

DELETE FROM actores WHERE apellido='Larter';

- Eliminar todos los registros de una tabla:

TRUNCATE TABLE actores;

- Eliminar una base de datos, tabla o vista:

DROP TABLE actores;

### **Sentencias SHOW**

Aunque es posible obtener la lista de bases de datos mediante sentencias *SELECT* (por ejemplo, usando *SELECT schema\_name FROM information\_schema.schemata* obtendríamos una relación de todas las BD almacenadas en el *INFORMATION\_SCHEMA*), resulta más cómodo hacerlo mediante la sentencia *SHOW DATABASES*.

De igual forma, podemos obtener una relación de tablas y columnas de tabla utilizando las sentencias *SHOW TABLES* y *SHOW COLUMNS*; por ejemplo:

USE filmoteca;

SHOW TABLES;

SHOW COLUMNS FROM filmoteca.actores;

Por último, podemos obtener la lista de procesos en ejecución usando la sentencia *SHOW PROCESSLIST.*

### **3.2.1. Gestión de vistas**

![](_page_74_Picture_2.jpeg)

Las características particulares de las vistas les confieren tres ventajas fundamentales sobre las consultas: según la complejidad de la consulta, pueden suponer un importante ahorro de tiempo; evitan los errores derivados de teclear o confeccionar una consulta de forma incorrecta; y hacen posible que determinados usuarios consulten datos a los que, de otra forma, no tendrían acceso, al carecer de los permisos necesarios para manipular directamente las tablas.

Vamos a estudiar la creación y uso básico de las vistas a través de un ejemplo práctico.

En primer lugar, y utilizando las consultas que hemos repasado al principio de esta sección, crearemos la base de datos *filmoteca* y dos tablas, *géneros* y *películas*:

|    | 1 CREATE DATABASE filmoteca; 2 USE filmoteca; 3 CREATE TABLE géneros |
|----|----------------------------------------------------------------------|
| 4  | (idGénero INT AUTO_INCREMENT PRIMARY KEY,                            |
| 5  | género VARCHAR(50) NOT NULL                                          |
| 6  | ); 7 CREATE TABLE películas                                          |
| 8  | (idPelícula INT AUTO_INCREMENT PRIMARY KEY,                          |
| 9  | título VARCHAR(100) NOT NULL,                                        |
| 10 | año INT NOT NULL,                                                    |
| 11 | país VARCHAR(50) NOT NULL,                                           |
| 12 | director VARCHAR(100) NOT NULL,                                      |
| 13 | idGénero INT,                                                        |
| 14 | CONSTRAINT cfGéneros                                                 |
| 15 | FOREIGN KEY (idGénero)                                               |
| 16 | REFERENCES géneros(idGénero)                                         |
| 17 | );                                                                   |

La columna *idGénero* es la clave foránea de la tabla películas y hace referencia a la columna *idGénero* de la tabla *géneros*. Esto limita la información que podemos almacenar en esta columna a los registros

Conceptualmente, las **vistas** no son más que consultas almacenadas en el catálogo de la BD, que se pueden reutilizar y sobre las que, en tanto que objetos de la base de datos, podemos asignar privilegios a los usuarios del SGBD.

de la tabla referenciada o padre, logrando así conservar la integridad referencial de la BD. En otras palabras, únicamente podremos introducir el género de las películas usando alguno de los identificativos previamente almacenados en la tabla géneros.

A continuación, introduciremos algunos registros en ambas tablas:

 1 INSERT INTO géneros(género) 2 VALUES 3 ('Acción'), 4 ('Bélica'), 5 ('Comedia'), 6 ('Drama'), 7 ('Histórica'), 8 ('Terror'); 9 INSERT INTO películas(título,año,país,director,idGénero) 10 VALUES 11 ('Vértigo (De entre los muertos)','1958', 12 'Estados Unidos','Alfred Hitchcock','7'), 13 ('Bullet Train','2022','Estados Unidos', 14 'David Leitch','1'), 15 ('Un pez llamado Wanda','1988','Reino Unido', 16 'Charles Crichton','3'), 17 ('Lawrence de Arabia','1962','Reino Unido', 18 'David Lean','5'), 19 ('Horizonte Final','1997','Reino Unido', 20 'Paul W.S. Anderson','6');

Para comprobar que ambas tablas están correctamente vinculadas, utilizamos la siguiente sentencia:

1 SELECT título,director,año,país,género 2 FROM películas 3 JOIN géneros USING (idGénero);

El resultado deber ser el siguiente:

| título               | director                                | año   país                     | género    |
|----------------------|-----------------------------------------|--------------------------------|-----------|
| Bullet Train         | David Leitch                            | 2022   Estados Unidos   Acción |           |
| Un pez llamado Wanda | Charles Crichton   1988   Reino Unido   |                                | Comedia   |
| Lawrence de Arabia   | David Lean                              | 1962   Reino Unido             | Histórica |
| Horizonte Final      | Paul W.S. Anderson   1997   Reino Unido |                                | Terror    |

Para almacenar esta consulta como vista, utilizaremos la sentencia *CREATE VIEW*:

1 CREATE VIEW filmoteca.pelis AS 2 SELECT título,director,año,país,género 3 FROM películas 4 JOIN géneros USING (idGénero);

Con ello hemos creado una vista, denominada *pelis*, que contiene el resultado de la consulta anterior. Para ver todos sus registros, solo tenemos que utilizar la sentencia siguiente:

SELECT \* FROM pelis;

Las vistas no son objetos estáticos, sino que reflejan los cambios que se hubieran producido en las tablas referenciadas en la consulta que se lleva a cabo. Para someterlo a prueba, añadamos un nuevo registro a la tabla películas:

1 INSERT INTO películas(título,año,país,director,idGénero) 2 VALUES 3 ('Salvar al soldado Ryan','1998', 4 'Estados Unidos','Steven Spielberg','2');

Al ejecutar *SELECT \* FROM pelis*, el nuevo registro aparece, efectivamente, en la parrilla resultante.

Para cambiar la definición de la vista, utilizamos la sentencia *ALTER VIEW*, cuya sintaxis es similar a *CREATE VIEW*. Por ejemplo, para eliminar la columna país de la vista *pelis*, usaríamos la sentencia siguiente:

1 ALTER VIEW filmoteca.pelis AS 2 SELECT título,director,año,género 3 FROM películas 4 JOIN géneros USING (idGénero);

Finalmente, para eliminar una vista, utilizaremos la sentencia *DROP VIEW*:

DROP VIEW filmoteca.pelis;

### **Sinónimos de tabla y vista**

Algunos SGBD, como Oracle Database, permiten crear sinónimos de tabla para poder referirnos a estos objetos de una forma distinta o abreviada, utilizando la siguiente sentencia:

CREATE SYNONYM films FOR filmoteca.películas;

Por desgracia, MySQL no soporta esta función de forma nativa. Sin embargo, las vistas pueden, en muchos casos, asumir el papel de sinónimos para las tablas; así sucede en nuestro ejemplo, donde la sentencia *SELECT título,director FROM películas* tiene el mismo efecto que *SELECT título,director FROM pelis*.

Es posible, incluso, crear una nueva vista a partir de una vista previa, con lo cual obtenemos, a efectos prácticos, un sinónimo; por ejemplo:

CREATE VIEW filmoteca.films AS SELECT \* FROM pelis;

Tras ejecutar la sentencia anterior, obtendremos el mismo resultado ejecutando *SELECT \* FROM films* y *SELECT \* FROM pelis*.

### **3.2.2. Operaciones DML sobre vistas**

En MySQL, las vistas que conservan una relación de uno a uno entre sus filas y las de la tabla subyacente, son, por lo general, actualizables. Esto significa que será posible utilizar sentencias de manipulación de datos como *INSERT*, *UPDATE* o *DELETE* sobre una de estas vistas, con la finalidad de actualizar la tabla base de la cual deriva.

![](_page_77_Picture_10.jpeg)

No obstante, existen una serie de condiciones que permiten o impiden realizar operaciones de tipo DML sobre las vistas. Específicamente, una vista no es actualizable en MySQL si su definición contiene cualquiera de los siguientes elementos: funciones agregadas o de ventana (como *SUM()*, *COUNT()*, etc.), *DISTINCT*, *GROUP BY*, *HAVING*, *UNION*, algunos tipos de *JOIN*, una subconsulta dependiente, una referencia a una vista no actualizable en la cláusula *FROM*, o una subconsulta en la cláusula *WHERE* que haga referencia a una tabla en la cláusula *FROM*.

En algunas ocasiones, se permite el uso de operaciones de actualización y eliminación, pero no de inserción. Es el caso de las subconsultas no dependientes, o de referencias múltiples a cualquiera de las columnas de la tabla base. Dado que MySQL marca las vistas actualizables en el momento de su creación, es posible consultar esta propiedad en

Para que una vista actualizable sea insertable, las columnas de la vista deben satisfacer los siguientes requisitos: no puede haber nombres de columna duplicados, la vista debe incluir todas las columnas de la tabla base que no tengan definido un valor por defecto, y dichas columnas deben ser referencias simples, no expresiones.

### Para + info

la columna *IS\_UPDATABLE* de la tabla *INFORMATION\_SCHEMA.VIEWS*; en el ejemplo de la sección anterior, para comprobar si la vista pelis es actualizable, usaríamos las siguientes sentencias:

1 USE information\_schema; 2 SELECT TABLE\_NAME,IS\_UPDATABLE FROM views 3 WHERE TABLE\_NAME='pelis';

![](_page_78_Picture_4.jpeg)

Retomando el ejemplo de la sección anterior, supongamos que nos hemos equivocado al introducir el año en la segunda fila de la tabla películas, y queremos corregirlo a través de la vista pelis. Podemos hacerlo con la siguiente sentencia:

1 UPDATE pelis 2 SET año='2022' 3 WHERE título='Bullet Train';

Sin embargo, no es posible eliminar esta fila usando una sentencia como *DELETE FROM pelis WHERE título='Bullet Train'*, al tratarse de una vista de tipo *JOIN*. Tampoco resultará posible insertar una nueva fila a través de esta vista, ya que la columna *idGénero* no se incluyó en la consulta *SELECT* en el momento de crear la vista, y dicha columna no tiene un valor asignado por defecto en la tabla base *películas*.

No obstante, nada nos impide insertar nuevos valores en la tabla géneros:

INSERT INTO pelis(género) VALUES ('Aventuras'),('Musical');

La siguiente sentencia crea una nueva vista (*films*) que sí será actualizable utilizando *INSERT* y *DELETE*:

1 CREATE VIEW filmoteca.films AS 2 SELECT título,año,país,director,idGénero 3 FROM películas;

Ahora probemos a insertar dos filas en esta misma vista:

1 INSERT INTO films(título,año,país,director,idGénero) 2 VALUES 3 ('El fantasma del Paraíso','1974','Estados Unidos','Brian De Palma','9'), 4 ('Título de prueba','2000','País','Director','1';

Finalmente, procedamos a eliminar el último registro introducido:

DELETE FROM films WHERE título='Título de prueba';

De esta forma, hemos podido comprobar cómo las vistas son actualizables dependiendo de la selección definida en el momento de crearlas, así como del tipo de actualización que vayamos a realizar sobre ellas.

### **3.3. Protección de datos y confidencialidad**

### **3.3.1. Monitorización de usuarios**

Una parte importante del trabajo de un administrador de SGBD consiste en monitorizar las actividades de realizan los usuarios, especialmente en lo que concierne a los procesos de autenticación, ya que esto permite la detección temprana de cualquier tipo de comportamiento irregular que pudiera apuntar a la existencia de una brecha de seguridad.

Para realizar una auditoría de procesos, existen numerosas herramientas de terceros, como Nagios, Monyog o Cacti, pero en MySQL podemos obtener una foto fija de todos los procesos en ejecución mediante la tabla *PROCESSLIST del INFORMATION\_SCHEMA*:

SELECT \* FROM information\_schema.PROCESSLIST;

Utilizando esta sentencia, podemos obtener el listado de los procesos en ejecución de un determinado usuario, y almacenarlo en un archivo de texto para su análisis posterior.

Supongamos que queremos monitorizar la actividad del usuario *leonardo*, y almacenarla en un archivo de texto separado por comas para poder procesarlo en cualquier software compatible con archivos CSV. La consulta quedaría como sigue:

1 SELECT 'ID', 'USER', 'HOST', 'DB', 'COMMAND', 'TIME', 'STATE', 'INFO' 2 UNION ALL 3 SELECT ID, USER, HOST, DB, COMMAND, TIME, STATE, INFO 4 FROM information\_schema.PROCESSLIST 5 WHERE USER='leonardo' 6 INTO OUTFILE 'C:/audit/audit\_proc.txt' 7 FIELDS TERMINATED BY ',' 8 ENCLOSED BY '"' 9 LINES TERMINATED BY '\n';

Es posible que el servidor esté funcionando con la opción *--secure-file-priv*, por lo que no pueda ejecutar la consulta. En este caso, debemos dirigir la salida del archivo de texto al directorio configurado para la salida de información (que podemos averiguar con la sentencia *SELECT @@GLOBAL.secure\_file\_priv*, y que, por defecto, es *C:\ProgramData\MySQL\MySQL Server 8.0\ Uploads\)*, modificando la opción *INTO OUTFILE* en consecuencia:

Para realizar una auditoría de inicios de sesión, la única opción disponible en la edición Community de MySQL es el registro general de consultas, mientras que la edición Enterprise dispone del complemento *audit\_log* que permite registrar únicamente los inicios de sesión.

![](_page_80_Picture_2.jpeg)

Para comprobar la configuración actual del registro de consultas, podemos utilizar la siguiente sentencia:

SHOW VARIABLES LIKE "general\_log%";

Para activar este registro utilizando la consola *mysql*, utilizaríamos la sentencia a continuación:

SET global general\_log = on;

No obstante, y tal como se indicaba en el apartado dedicado a los archivos de registro, para que esta configuración sea permanente es necesario incluirla en el archivo de configuración de la instancia (normalmente, *my.ini* o *my.cnf*):

[mysqld] general\_log = on

Las principales desventajas de utilizar el registro de consultas para auditar los inicios de sesión son:

- Puede impactar sobre el rendimiento del servidor, ya que no se registran únicamente los inicios de sesión, sino absolutamente todas las consultas.
- Puede plantear problemas de privacidad, la que las sentencias registradas pueden contener información sensible sin cifrar.

![](_page_80_Picture_13.jpeg)

Por ello, siempre que sea posible, es recomendable utilizar un complemento que nos ofrezca un mayor control sobre los datos auditados.

### **3.3.2. Configuración de acceso remoto**

Casi todos los accesos que, por parte de los usuarios, se producen en un SGBD, lo hacen desde punto de acceso externo al servidor, bien en una intranet, bien a través de internet, ajustándose al tradicional modelo **cliente-servidor**. En este tipo de arquitectura, el papel del servidor es **pasivo**, ya que permanece a la espera de las peticiones de los clientes para procesarlas y devolver la correspondiente respuesta, mientras que papel de los clientes es **activo**, enviando peticiones al servidor y procesando la respuestas recibidas.

Debemos reseñar que, a la hora de indicar rutas en nuestras sentencias, es necesario reemplazar las contrabarras (\) por barras (/), ya que *mysql* está programado para interpretar la notación de estilo UNIX.

### Para + info

**2.6.2.** *Registro de consultas*

Visita las páginas Las comunicaciones entre el servidor y los clientes se realizan, en este contexto, mediante los protocolos definidos por la pila TCP/IP, donde las máquinas, o **nodos**, pueden identificarse utilizando una dirección IP, y un puerto TCP. La combinación de ambos es lo que denominamos socket de red; por ejemplo, *192.168.1.10:3456* puede utilizarse programáticamente para conectarse con el nodo en la dirección *192.168.1.10* a través del puerto *3456*.

En MySQL, las comunicaciones entre clientes y servidores se realizan mediante un protocolo implementado por los conectores, el proxy y las comunicaciones entre el servidor maestro y los servidores de replicación de MySQL. Este protocolo proporciona compresión y cifrado SSL de los datos, y contempla dos fases, una de conexión, donde se intercambian los datos de autenticación, y otra de instrucciones, en donde se aceptan y ejecutan las peticiones de los clientes.

Por otra parte, y en sistemas de tipo Unix, las comunicaciones que se dan entre los diferentes procesos internos de MySQL (denominadas IPC, del inglés *interprocess communications*) se realizan mediante un archivo *socket* denominado *mysqld.sock*, que usualmente se ubica en el directorio */var/run/mysqld/*. Estos *sockets* IPC (también denominados *sockets de dominio Unix*), cuya dirección es el mismo archivo *socket* local, permiten canalizar las comunicaciones entre los procesos dentro de un mismo anfitrión, y, dado que no requieren de un protocolo subyacente (como el TCP o el UDP), son más eficientes que los de red.

En el caso de Windows, en lugar de archivos *socket* podemos utilizar tuberías con nombre, o *named pipes*, siempre y cuando hayamos habilitado previamente la variable de sistema *named\_pipe*. La ruta a la tubería por defecto para el servidor MySQL es \\.\*pipe*\*MySQL* (deberemos especificar esta ruta en el apartado correspondiente a la dirección del anfitrión, dentro de la aplicación desde la que deseemos establecer la conexión con el servidor).

### Para + info

Una técnica que se emplea, en las aplicaciones basadas en la filosofía cliente-servidor, para gestionar las comunicaciones entre procesos, son las llamadas de procedimiento remoto o RPC (*Remote Procedure Call*). Así, cuando los clientes realizan sus peticiones, son las RPC las encargadas de traducir y enviar los mensajes a los servidores de destino.

Para habilitar las tuberías en el archivo de configuración de MySQL (*my.ini* o *my.cnf*), incluiremos las siguientes líneas:

[mysqld] enable-named-pipe socket=MYSQL

### **Cifrado de datos y conexiones seguras**

Para proteger los datos que se transmiten entre clientes y servidores a través de una red, se utilizan técnicas de criptográficas para cifrar la información, de forma que resulte imposible descifrarla sin contar con la correspondiente clave.

Sin embargo, el nivel de seguridad obtenido varía en función del sistema de cifrado que implementemos; cada método tiene sus características particulares en relación con el tipo de claves de cifrado utilizadas, el tamaño de los paquetes de datos o el impacto sobre el rendimiento del sistema.

En primer lugar, debemos saber que la clave de cifrado (una cadena de bits aleatoria lo más larga, única e impredecible que sea posible) es el factor que determina la fortaleza de un algoritmo de cifrado.

Los sistemas de **clave única** son los más seguros, pero dependen de que la **clave maestra** o fija, a partir de la cual se generan claves distintas para cada transacción, no se haga nunca pública. Este es el tipo de cifrado adoptado, en las dos últimas décadas del siglo pasado, por las entidades financieras y crediticias para cifrar los PIN de las tarjetas de débito o crédito.

El cifrado llamado de **clave simétrica** o secreta utiliza también una sola clave, aunque en este caso la conocen tanto el emisor como el receptor de la información, por lo que también se lo conoce como cifrado de clave compartida. Se trata de un método más simple, por lo que, en consecuencia, resulta también más rápido, aunque también menos seguro que el de clave única.

Finalmente, los algoritmos de **cifrado asimétrico** utilizan dos claves conectadas matemáticamente en lugar de una sola. La clave que se utiliza para cifrar los datos es pública (lo que se conoce como infraestructura de clave pública, o PKI por sus siglas en inglés). La otra clave, que es privada, es la que se requiere para descifrar los datos. La ventaja de este sistema es que evita la transmisión de una clave compartida —lo que hace posible, entre otras cosas, la firma electrónica de documentos—, pero es el más lento de todos los sistemas.

Uno de los algoritmos de cifrado más populares es el AES (*Advanced Encryption Standard*, es decir, estándar de cifrado avanzado). Se trata de un método de clave simétrica que permite cifrar paquetes de datos de 128 bits usando una clave de 128,192 o 256 bits de longitud (a más larga, más segura).

### Para + info

Cuando las comunicaciones se establecen a través de internet, se utilizan protocolos de conexión seguros, como SSL o TLS, que se basan en estas técnicas criptográficas. En el caso del HTTPS, por ejemplo, se utiliza una clave simétrica para cifrar el contenido de los mensajes, y una clave pública para transmitir dicha clave. De esta forma se consigue que la parte más larga —la propia página web—, se cifre y descifre de la forma más eficiente posible, al tiempo que se refuerza la seguridad utilizando el cifrado asimétrico para la parte más sensible, que es la clave compartida.

MySQL permite, por defecto, las conexiones cifradas con SSL, aunque no son obligatorias salvo que se habilite la variable de sistema *require\_ secure\_transport*. Por otra parte, para definir los archivos de certificado y clave necesarios para permitir las conexiones cifradas de los clientes, se utilizan las siguientes variables:

- **ssl\_ca**: ruta al certificado de autoridad.
- **ssl\_cert**: ruta al certificado de clave pública del servidor.
- **ssl\_key**: ruta al archivo de clave privada del servidor.

Podríamos, por ejemplo, incluir las siguientes líneas en el archivo de configuración de MySQL:

[mysqld] ssl\_ca=ca.pem ssl\_cert=server-cert.pem ssl\_key=server-key.pem require\_secure\_transport=ON

Los archivos especificados deben estar en formato PEM y hallarse en el directorio de datos. En caso de no encontrarlos, el servidor continuará con su ejecución normal, aunque sin admitir conexiones cifradas.

![](_page_83_Picture_7.jpeg)

### Para + info

La **capa de** *sockets* **seguros** o *Secure Sockets Layer* (SSL) y la tecnología a la que reemplaza —llamada *seguridad de capa de transporte* o *Transport Layer Security* (TLS)— emplean criptografía de clave pública, y requieren de un certificado de autoridad (CA) para verificar la identidad de un servidor en internet. Dicho certificado debe emitirse por una entidad de confianza, y se cifra utilizando sistemas criptográficos como el ECC, el RSA o el DSA. El programa cliente es el encargado de comprobar la validez de las credenciales antes de iniciar la sesión SSL o TLS cifrada con el servidor.

### **Interoperabilidad entre sistemas de bases de datos**

En aquellas aplicaciones que necesitan acceder a diferentes fuentes de datos, o que requieren ser totalmente independientes de las bases de datos con las que se conectan, suele utilizarse una interfaz de programación estandarizada llamada ODBC (*Open Database Connectivity*).

Se trata de una API que utiliza el SQL como vía de acceso a las bases de datos, por lo que puede utilizarse para conectar con cualquier SGBD basado en este lenguaje.

![](_page_84_Picture_4.jpeg)

En MySQL, el soporte para ODBC se proporciona a través de un conector compatible con el protocolo MySQL, que es el encargado de gestionar todas las operaciones necesarias para que los clientes puedan acceder a las bases de datos, incluyendo la comunicación con los controladores ODBC del sistema operativo anfitrión y la resolución de DSN.

![](_page_84_Picture_10.jpeg)

### Para + info

Un protocolo de aplicación específicamente diseñado para el acceso a bases de datos es el *Remote Database Access (RDA)*, publicado en 1993 por la International Organization for Standardization (ISO).

En él se incluyen los mecanismos necesarios para gestionar las peticiones de clientes a servidores, así como para el transporte de los datos solicitados y la gestión de las transacciones de la base de datos.

Sin embargo, y a pesar de poder implementarse sobre conexiones de red TCP/IP estándar, el RDA no ha conseguido todavía obtener el apoyo de los principales proveedores de SGBD.

Los **nombres de fuentes de datos** o *Data Source Names*  (DSN) son un mecanismo estandarizado que permite a una aplicación ODBC referenciar, a través de una cadena, no solo a un anfitrión de BD o a una BD en particular, sino también al controlador de BD y, opcionalmente, toda la información relacionada con la autenticación de la conexión.

En Windows, podemos instalar el conector ODBC mediante el propio instalador de MySQL, tal como vimos en el apartado 2.3, aunque también puede obtenerse como paquete de instalación MSI independiente. El conector ofrece la posibilidad de definir la conexión a través de numerosos parámetros, cuya configuración podemos realizar, bajo Windows, utilizando el Administrador de fuentes de datos ODBC (ODBC Data Source Administrator). En Windows Server, encontraremos esta herramienta en *Inicio > Herramientas administrativas de Windows > Orígenes de datos ODBC*. Los pasos a seguir para configurar una conexión ODBC son los siguientes:

- 1. En la ventana del *Administrador de origen de datos ODBC*, vamos a la pestaña *DSN de usuario*, *DSN de sistema o DSN de archivo*, según sea el caso, y pulsamos el botón *Agregar*.

![](_page_85_Picture_4.jpeg)

- 2. En la ventana *Crear nuevo origen de datos*, escogemos entre el controlador ANSI o Unicode de MySQL ODBC, según nuestras necesidades, y pulsamos el botón *Finalizar*.

![](_page_85_Picture_6.jpeg)

- 3. En la ventana *MySQL Connector/ODBC Data Source Configuration*, completamos los campos requeridos. En esta ocasión crearemos un DSN para nuestra base de datos *filmoteca*.

Debemos tener en cuenta que el usuario que utilicemos para establecer la conexión debe tener algún privilegio concedido sobre la base de datos en cuestión. Para comprobarlo, seleccionamos la BD en la lista desplegable *Database*, y pulsamos el botón *Test*.

- 4. Para acceder a la configuración avanzada de la fuente de datos, pulsamos el botón *Details* y seleccionamos la pestaña apropiada. De esta forma podremos, por ejemplo, configurar todos los parámetros relativos al cifrado SSL, en caso de querer utilizarlo. Para dar por finalizada la configuración, pulsaremos el botón *OK*.

- 5. Para poner a prueba la configuración realizada podemos utilizar cualquier aplicación compatible con ODBC. Por ejemplo, el kit de desarrollo Microsoft Data Access Components (MDAC) incluye las herramientas *odbct32.exe* y *odbct32w.exe* para probar conexiones ODBC ANSI y Unicode, respectivamente.

![](_page_87_Picture_2.jpeg)

### **3.3.3. Normativa sobre protección de datos**

El personal encargado de la gestión de bases de datos, y en particular aquellos que desempeñan el rol de administradores de seguridad, deben proteger y velar por la integridad de todos los archivos almacenados en el sistema que pudieran contener datos personales o de naturaleza sensible. Por ello, es importante que los administradores de SGBD conozcan las principales regulaciones que establecen las leyes en materia de protección de datos, y que, a partir de ellas, adopten las medidas necesarias para garantizar su cumplimiento.

### **Marco regulatorio vigente**

La legislación actual relativa a la protección de datos se basa en el **Reglamento (UE) 2016/679** del Parlamento europeo y del Consejo, de 27 de abril de 2016, relativo a la protección de las personas físicas en lo que respecta al tratamiento de datos personales y a la libre circulación de estos datos, complementada, en España, por dos leyes orgánicas: la **Ley Orgánica 3/2018**, de 5 de diciembre, de Protección de Datos Personales y garantía de los derechos digitales (BOE, 6 de diciembre de 2018), y **la Ley Orgánica 15/1999**, de 13 de diciembre, de Protección de Datos de carácter personal (BOE, 14 de diciembre de 1999).

![](_page_88_Picture_1.jpeg)

A partir de la normativa europea, se elabora el actual **Reglamento General de Protección de Datos (RGPD)**, vigente desde el 25 de mayo de 2018, y en él se definen los derechos de los ciudadanos con respecto de sus datos personales, y las obligaciones que sobre ellos adquieren el personal y las entidades encargados de su gestión.

Estos derechos son los siguientes:

- **Derecho de acceso**: derecho a saber si nuestros datos personales van a ser tratados y, en caso afirmativo, a obtener una copia de ellos. Si así fuera, sería también necesario informar al interesado acerca de la finalidad y destino de los datos tratados, de su periodo de conservación, y de cualquier otro proceso automatizado que se fuera a ejercer sobre ellos, como la confección de perfiles comerciales.
- **Derecho de rectificación**: derecho a pedir al responsable del tratamiento de los datos la rectificación de todos aquellos que fueran inexactos.
- **Derecho de oposición**: derecho del interesado a oponerse a que se realice cualquier tratamiento de sus datos personales, sin importar si el objeto del tratamiento es legítimo o, incluso, de interés público (salvo en casos excepcionales).
- **Derecho de limitación**: derecho a que se suspenda el tratamiento de los datos en tanto que se verifica la legitimidad de una reclamación.
- **Derecho de supresión**: derecho del interesado a que se eliminen sus datos personales. Solo podría denegarse si ello implicara un perjuicio mayor en aspectos como la libertad de expresión e información, la investigación científica y otras cuestiones de interés público.

- 1. Reglamento (UE) 2016/679.
- 2. Ley Orgánica 3/2018.
- 3. Ley Orgánica 15/1999.

![](_page_88_Picture_3.jpeg)

![](_page_88_Picture_4.jpeg)

![](_page_88_Picture_5.jpeg)

**1** [bit.ly/3igjjqQ](http://bit.ly/3igjjqQ) **2** [bit.ly/3GMei3k](http://bit.ly/3GMei3k) **3** bit.ly/3ALy8I5

- **Derecho de portabilidad**: derecho a recibir una copia de los datos personales en un archivo electrónico estructurado, de uso común, de lectura mecánica e interoperable.

![](_page_89_Picture_2.jpeg)

En España, el organismo encargado de velar por el ejercicio —que debe ser siempre gratuito— y por el respeto a estos derechos, es la Agencia Española de Protección de Datos (AEPD). Sin embargo, son los responsables del tratamiento de dichos datos quienes están obligados a informar a los interesados acerca de sus derechos y de las vías de las que disponen para ejercitarlos.

Esta información debe facilitarse, siempre que sea posible, por medios electrónicos, y la respuesta a toda solicitud debe producirse en un plazo de uno a tres meses, dependiendo de la complejidad de la petición.Para hacer un poco más sencillo el trabajo de los responsables del tratamiento de datos, la AEPD dispone de herramienta en línea llamada *Facilita*.

 A pesar de que no garantiza el pleno cumplimiento del RPGD, supone un buen punto de partida para ajustar a la ley las directivas y procedimientos relativos a la protección de datos cuando los riesgos que se hubieran valorado son bajos, como pudiera ser el caso de una BD de clientes, proveedores o de recursos humanos.

El RGPD ofrece libertad a los responsables del tratamiento de datos para determinar, a partir de un análisis de riesgos previo, las medidas técnicas y organizativas necesarias para garantizar su seguridad. Estas deberán ser proporcionales, en complejidad y sofisticación, al valor de la información a proteger. En este sentido, los SGBD contemplan mecanismos que permiten controlar los accesos locales y remotos, y el nivel de acceso a los datos permitido según el perfil definido para cada usuario.

**3.1.** *Gestión de usuarios y permisos en MySQL.*

*Facilita es la herramienta en línea de la AEPD para generar documentos de utilidad en el tratamiento de datos de bajo riesgo.*

Gracias a Facilita podemos generar diversos documentos adaptados a nuestro caso en particular, como una relación de las cláusulas informativas que deberíamos incluir en los formularios de captación de datos personales, las cláusulas a contemplar en el contrato de un responsable de tratamiento de datos, o una relación de medidas de seguridad recomendadas por la AEPD, entre otros.

![](_page_90_Picture_2.jpeg)

### **Tratamiento de datos personales**

Los principios generales que regulan específicamente el tratamiento de los datos personales, vienen recogidos en el artículo 5 del RPGD; en líneas generales, son los siguientes:

- El tratamiento de datos personales se realizará de forma lícita, leal y transparente de cara al interesado.
- Los datos personales solo podrán recogerse y tratarse con fines determinados, explícitos y legítimos.
- Únicamente pueden captarse datos que se consideren adecuados, pertinentes y limitados a finalidad, según el principio de minimización de datos.
- Los datos deberán ser exactos y estar debidamente actualizados.
- Los datos personales no pueden mantenerse por más tiempo del que fuera necesario según su finalidad, excepto cuando esta sea de interés público o de investigación científica, histórica o estadística.
- Debe garantizarse un nivel de seguridad adecuado, incluyendo la protección contra su tratamiento no autorizado o ilícito, pérdida, destrucción o daño accidental.
- Debe existir una persona responsable del tratamiento de datos personales, cuya misión será la de velar por el cumplimiento de estas normas según el principio de responsabilidad proactiva.

### Para + info

Enlace a la herramienta *Facilita* de la Agencia Española de Protección de Datos:

[bit.ly/3VirUaw](http://bit.ly/3VirUaw)

![](_page_90_Picture_6.jpeg)

# Tema 3. Acceso a la información

### **Gestión de archivos y registro de actividades**

Según la normativa, existen dos circunstancias en las que deberá documentarse adecuadamente cualquier operación de tratamiento de datos en la que se manejen datos personales:

- 1. Cuando la organización tenga más de 250 trabajadores.
- 2. Cuando concurra cualquiera de las siguientes circunstancias: –Que exista riesgo sobre los derechos y libertades de los interesados. –Que la información personal incluya datos como el origen étnico o racial del interesado, opiniones políticas, convicciones religiosas o filosóficas, afiliación sindical, datos genéticos o biométricos, datos relativos a la salud, condenas e infracciones penales, o datos concernientes a la orientación sexual de la persona. –Que el tratamiento no sea ocasional.

Entre las operaciones habituales destinadas a preservar la seguridad e integridad de la información se cuentan la realización de **copias de seguridad periódicas** y la **protección de los equipos** de almacenamiento y procesamiento de los datos (en particular, aquellos conectados a una red y a Internet, así como de los dispositivos móviles). En tales casos, y si se dan las circunstancias arriba mencionadas, los responsables del tratamiento de los archivos deberán crear y mantener un **registro de actividades de tratamiento**.

El propósito de este registro es documentar el flujo de información de carácter sensible dentro de los sistemas de la organización, y substituye a la antigua obligación de inscribir los archivos de datos personales en un Registro General de Protección de Datos.

El registro de actividades debe contemplar, obligatoriamente, el siguiente conjunto de datos:

- Identificación y datos de contacto del responsable del tratamiento.
- Finalidad del tratamiento.
- Descripción de los interesados y de los tipos de datos recabados.

- • Definición de los destinatarios de la información.
- Transferencias internacionales de los datos (si las hubiera).
- Plazos previstos para la supresión de datos (si procediera).
- Descripción de las medidas de seguridad adoptadas para la protección de los datos.

### Para + info

El RGPD establece, en sus artículos 33 y 34, los procedimientos de actuación cuando una brecha de seguridad pueda causar daños y perjuicios a los interesados de los datos comprometidos. En estos casos, se deberá informar a la AEPD acerca de las circunstancias de esta brecha en las 72 horas siguientes a su detección. Además, cuando los daños fueran de especial gravedad, será necesario informar también a todas aquellas personas o entidades que hubieran podido verse afectadas.
