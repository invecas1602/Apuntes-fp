# **2.6. Archivos de registro en MySQL**

MySQL Server puede registrar sus actividades en diferentes archivos, según la naturaleza de las operaciones a registrar:

Ninguno de estos registros, o *logs* en inglés, están activados por defecto, con la excepción del registro binario, y en los sistemas Windows, del registro de errores. A no ser que especifiquemos lo contrario, los archivos correspondientes a los registros activos se escribirán en el directorio de datos.

Por otra parte, podemos volcar, es decir, cerrar y reabrir estos registros (o, en algunos casos, alternar a un archivo de registro nuevo), ya sea mediante la sentencia *FLUSH LOGS*, o bien desde la consola de Windows (*cmd*), usando la instrucción *mysqladmin* con el argumento *flush-logs*; por ejemplo:

> mysqladmin -h localhost -u root -p flush-logs

### **2.6.1. Registro de errores**

El registro de errores contiene los mensajes relacionados con el inicio y el cierre de *mysqld*, así como todos los mensajes de diagnóstico relativos a errores o advertencias que puedan lanzarse durante la ejecución de MySQL.

Por defecto, este registro se almacena en el directorio de datos de la instancia en ejecución, en un archivo llamado *nombre\_de\_anfitrión.err* (por ejemplo, *Servidor01.err*).

| Tipo de registro    | Información registrada                        |
|---------------------|-----------------------------------------------|
| Registro de errores | Problemas en el inicio, ejecución o detención |
|                     | de mysqld                                     |
| Registro binario    | Sentencias que alteran datos (también         |
| ( relay )           |                                               |
| Registro de DDL     | Operaciones de metadatos efectuadas por       |

Esta configuración puede cambiarse ejecutando *mysqld* con las opciones *--log-error* para especificar una ruta y nombre de archivo distinto, y *--console* para que todos los errores se vuelquen en la consola del sistema:

> mysql -h localhost -u root -p --log-error=C:\registros\instancia1\_errores.err

> mysql -h localhost -u root -p --console

La variable de sistema *log\_error\_services* controla los componentes de registro que se activarán para registrar los errores, que, por defecto, son *log\_filter\_internal* y *log\_sink\_internal*. El primero es un filtro de errores simple basado en la prioridad de los eventos y los códigos de error. El segundo es el componente que se encarga de volcar los errores procedentes del filtro anterior en el archivo de registro o en la consola.

### **2.6.2. Registro binario**

Las operaciones capaces de alterar los datos en las BD, es decir, las que se emplean en la creación de tablas y la inserción, modificación o eliminación de los registros, se recopilan en el registro binario, junto con el tiempo consumido por cada una de ellas.

La variable del sistema que permite activar o desactivar el registro binario es *log\_bin*, y, por defecto, su valor es *ON* (habilitada), excepto si se utiliza *mysqld* para inicializar una nueva instancia, en cuyo caso deberá usarse la opción *--log-bin* en tiempo de ejecución (o, una vez más, dentro del archivo de configuración de la instancia).

Las **instrucciones de la consola de Windows (cmd)** aparecen siempre precedidas por el símbolo >, y deben escribirse en una única línea antes de pulsar la tecla Entrar.

Si, como en el caso del bloque anterior, fuera necesario dividir una instrucción en dos o más líneas, la segunda línea y subsiguientes aparecerán desplazadas dos espacios a la derecha para denotar que son continuación de la primera.

Esta misma norma rige para las sentencias SQL, con la diferencia

de que estas no van precedidas por ningún símbolo,

pero deben cerrarse, según requiere MySQL,

con un punto y coma (;).

Atención

También es posible desactivar el registro binario, al ejecutar el servicio, mediante las opciones *--skip-log-bin* o *--disable-log-bin*.

El registro binario se almacena en el directorio de datos como *nombre\_de\_anfitrión-bin*. Como en el caso de los otros registros, podemos especificar una ruta y nombre distintos usando la opción *--log-bin*:

> mysql -h localhost -u root -p --log-bin=C:\registros\instancia1-bin

Dado que MySQL cierra este registro cuando se detiene, y crea uno nuevo cuando se inicia otra vez, a cada archivo de registro binario le asigna una extensión numérica, que se irá incrementando, de forma correlativa, con cada reinicio.

Otra circunstancia en la que el servidor cerrará y abrirá un nuevo registro binario, es cuando este alcance el tamaño especificado por la variable del sistema *max\_binlog\_size*, así como también cuando realicemos un volcado de los registros.

Por este motivo, MySQL almacena un índice de los registros binarios en un archivo del mismo nombre, pero con la extensión *.index*, aunque es posible especificar un nombre distinto usando la opción *--log-bin-index*.

Podemos eliminar todos o una parte de los registros binarios usando las sentencias *RESET MASTER* (todos), *PURGE BINARY LOGS* (todos salvo el más reciente), *PURGE MASTER LOGS TO nombre\_de\_archivo* (todos hasta un registro determinado) y PURGE MASTER LOGS BEFORE *fecha-hora* (todos hasta el momento especificado). Además, mediante la variable *expire\_logs\_days* podemos establecer un periodo de días, transcurrido el cual, los registros serán automáticamente eliminados.

#### Para + info

Los **archivos de registro binario** cobran especial importancia a la hora de efectuar ciertas operaciones de recuperación de datos; por ejemplo, si restauramos los datos de una BD, MySQL Server puede usar este registro para repetir las operaciones que se hubieran efectuado después de realizar la copia de respaldo de la que proceden los datos recuperados. También proporciona el registro de los cambios en los datos que se emplean durante las operaciones de replicación, con el fin de que los datos de las réplicas experimenten los mismos cambios que se hayan realizado en el servidor de origen.

### **2.6.3. Registro de consultas**

El registro general de consultas de MySQL permite conservar un histórico de las consultas que se han realizado en cada instancia del servidor. Esto puede resultar útil para recopilar información estadística acerca de las consultas más realizadas y optimizar, en su caso, el rendimiento de las tablas con una mayor utilización.

Por defecto, MySQL almacena este registro en su directorio de datos bajo el nombre de *nombre\_de\_anfitrión.log*, pero, para activarlo, deberemos ejecutar *mysqld* con la opción *--general-log* (o bien, incluir esta opción en el archivo de configuración de inicio):

> mysql -h localhost -u root -p --general-log

Para desactivar este registro, utilizaremos la opción *--general-log=0*. Además, si queremos cambiar la ruta o el nombre del registro, podemos lograrlo con la opción *--general-log-file*:

> mysql -h localhost -u root -p --general-log-file=C:\registros\instancia1.log

Otra posibilidad es que este registro se almacene en una tabla, dentro del esquema del sistema, en lugar de en un archivo. Para este fin, usaremos la variable de sistema *--log\_output*, que puede contener como valor *FILE* (archivo), *TABLE* (tabla) y *NONE* (desactiva el registro de consultas). También podemos realizar esta configuración en tiempo de ejecución:

> mysql -h localhost -u root -p --log-output=TABLEº

### **3.1. Gestión de usuarios y permisos en MySQL**

Un aspecto esencial del trabajo de un administrador de SGBD es el de gestionar los puntos de acceso al sistema y garantizar su seguridad. Esta labor conlleva, básicamente, tres tareas:

- **Dar de alta y mantener una BD** de los usuarios que podrán acceder al sistema.
- Aplicar y garantizar el **cumplimiento de las directivas** de contraseñas.
- Asignar a los usuarios los **permisos necesarios** para acceder, desde un lugar determinado, a ciertos objetos del sistema, lo cual les permitirá, a su vez, realizar sobre ellos las acciones que tuvieran expresamente autorizadas.

Así pues, es el **administrador de usuarios** el que se encarga de gestionar quién puede conectarse al SGBD, desde dónde, a qué bases de datos y con qué tipo de privilegios —qué es lo que puede y no puede hacer—, tanto sobre dichos datos, como sobre la configuración del propio SGBD.

No cabe duda, por tanto, que diseñar y mantener una directiva de accesos adecuada es fundamental a la hora de garantizar la seguridad del sistema y de los datos almacenados en las BD que contiene.

### **3.1.1. Control de accesos en MySQL**

El control de los accesos al SGBD por parte de los usuarios implica, en MySQL, dos operaciones distintas:

- 1. **Comprobación de la conexión**: se autentifica al usuario mediante un nombre de usuario y una contraseña, acompañado del identificativo del anfitrión desde el que se inicia la conexión (esto es, el nombre de la máquina o su dirección IP).
- 2. **Comprobación de la solicitud**: se consulta a qué objetos tiene acceso el usuario y qué tipo de operaciones puede realizar sobre ellos.

### **Fase 1: comprobación de la conexión**

Durante la primera fase se acepta o se rechaza la conexión dependiendo, en primer lugar, de si se han proporcionado las credenciales adecuadas y, en segundo término, de si la cuenta en cuestión está abierta (*unlocked*), o cerrada bajo llave (*locked*), en cuyo caso de deniega.

Los datos de la máquina anfitrión y el nombre de usuario a comprobar están almacenados en las columnas *Host* y *User* de las **tablas de permisos** del SGBD, bien a nivel administrativo global (tabla *user* en la BD de sistema *mysql*, a la que podemos referirnos también como *mysql.user*), bien a nivel de base de datos (tabla *db*). En este último caso, se guarda el nombre de la base de datos sobre la que se detentan los permisos en una columna llamada *Db*.

En estas tablas se almacenan, a su vez, las credenciales —una contraseña, por ejemplo—, en la columna *authentication\_string* (MySQL usará el complemento especificado en la columna *plugin* para interpretar correctamente dichas credenciales), y la configuración de cierre bajo llave, en la columna *account\_locked* de la misma tabla.

Además de las mencionadas, existen muchas otras columnas que determinan los privilegios, la seguridad y límites de acceso a recursos de las cuentas de usuario:

- **Privilegios (***user* **y** *db***)**: permisos para ejecutar cláusulas como *SELECT* (columna *Select\_priv*), *INSERT* (*Insert\_priv*), *UPDATE* (*Update\_priv*), *DELETE* (*Delete\_priv*), *DROP* (*Drop\_priv*) o *GRANT* (*Grant\_priv*), entre otros muchos. La tabla *db* cuenta con menos columnas que la tabla user, al no ser necesarios ciertos permisos administrativos, como el de la gestión de usuarios y roles, entre otros.
- **Seguridad (***user***)**: tipo de SSL (columna *ssl\_type*), cifrado de SSL (*ssl\_cipher*), contraseña expirada (*password\_expired*), reutilización de contraseñas (*Password\_reuse\_history* y *Password\_reuse\_time*), etc.
- **Control de recursos (***user***)**: número máximo de consultas (*max\_questions*), actualizaciones (*max\_updates*) y conexiones (*max\_connections*) por hora, así como el número máximo de conexiones simultaneas al servidor (*max\_user\_connections*).

### **Fase 2: comprobación de la solicitud**

Una vez autorizada la conexión, MySQL comprueba, para cada petición que se realice a través de ella, **qué operación** se pretende realizar y si el usuario tiene los **privilegios necesarios** para ejecutarla.

Estos privilegios pueden residir en cualquiera de las tablas de privilegios del sistema que, además de las ya mencionadas *user* (privilegios globales permanentes) y *db* (privilegios sobre BD específicas), incluyen *global\_grants* (privilegios globales dinámicos que se registran o desregistran, en tiempo de ejecución, por los componentes que los definen), *tables\_priv* (privilegios específicos sobre las tablas de una determinada BD), *columns\_priv* (privilegios específicos sobre las columnas de una determinada tabla) y *procs\_priv* (privilegios específicos sobre rutinas).

Para determinar el alcance de un permiso podemos usar, por norma general, los comodines % (reemplaza a cualquier carácter) y \_ (reemplaza un solo carácter), teniendo en cuenta las siguientes reglas:

- Un usuario en blanco ('') equivale al usuario anónimo.
- No se pueden usar comodines en los nombres de usuario.
- Un valor de anfitrión en blanco o con el comodín % equivale a cualquier anfitrión.
- Un valor de BD en blanco o con el comodín % equivale a cualquier BD.
- En las tablas *tables\_priv, columns\_priv y procs\_priv*, las columnas *Db*, *Table\_name, Column\_name* y *Routine\_name* no se pueden dejar en blanco, así como tampoco pueden contener comodines.

Para determinar si una operación se permite o no, MySQL primero ordena las tablas de permisos, colocando los valores más específicos en los primeros lugares, y los menos específicos al final de la lista. El procedimiento es, en líneas generales, el siguiente:

- Si se requiere un privilegio ex clusivamente administrativo, el servidor comprueba únicamente las correspondencias en las tablas *user* y *global\_grants*. Para que la operación se permita:
- 1. Debe localizarse una coincidencia de nombre de usuario (*User*) y anfitrión (*Host*).
- 2. La columna que corresponda al permiso requerido debe tener el valor 'Y' (sí).
- Si el privilegio no es únicamente global, se leen las tablas *user* y *db*, y se ordena esta última por anfitrión (*Host*), base de datos (*Db*) y usuario (*User*). El servidor lee la tabla *user* y comprueba, como en el caso anterior, si hay una coincidencia y si la operación está permitida:
- 1. Si el usuario y anfitrión no coinciden con ningún registro en la tabla *user*, se deniega la conexión.
- 2. Si hay coincidencia, pero la operación no está permitida en *user*:
  - a. Se busca una coincidencia en las columnas *Host*, *User* y *Db* de la tabla *db*; en caso de haberla, se añaden todos los permisos de dicha tabla a los de la tabla *user*, y se vuelve a comprobar las coincidencias.
  - b. Si los permisos recopilados no permiten la operación solicitada (es posible que el usuario tenga asignados diferentes permisos

sobre distintas tablas en una o varias BD), se comprueban, con idéntico proceder y de manera sucesiva, las tablas *tables\_priv*, *columns\_priv* y *procs\_priv*. El resultado final (se aprueba o se deniega la operación) vendrá determinado por la combinación de todos los privilegios concedidos al usuario en cuestión.

### **3.1.2. Gestión de cuentas de usuario**

El administrador de usuarios puede usar las siguientes sentencias para para crear, modificar y eliminar cuentas de las tablas de sistema de MySQL:

| Sentencia   | Descripción                                |
|-------------|--------------------------------------------|
| ALTER USER  | Modifica las propiedades de las cuentas de |
| RENAME USER | Cambia el nombre de usuario y anfitrión de |
| DROP USER   | Elimina usuarios de MySQL.                 |

### **Crear un usuario**

La sentencia *CREATE USER* crea una nueva fila en la tabla de sistema *mysql.user*. El único dato imprescindible para ejecutar esta sentencia es el nombre de usuario. Cualquier otra propiedad sin especificar, adoptará su valor por defecto:

| Propiedad           | Valor por defecto |
|---------------------|-------------------|
| Anfitrión           | %                 |
| Rol                 | Ninguno.          |
| Opciones SSL/TLS    | Ninguna.          |
| Límites de recursos | Sin límites.      |
| Cierre bajo llave   | Sin cerrar.       |

![](_page_62_Picture_1.jpeg)

Supongamos que queremos crear un usuario llamado *leonardo*. La forma más simple de la sentencia *CREATE USER* sería la siguiente:

CREATE USER 'leonardo';

Si tecleamos esto en una ventana cliente de *mysql* y, a continuación, ejecutamos la sentencia *SELECT User*, *Host FROM mysql.user*, obtendremos el listado de registros de la tabla global de usuarios mostrando las columnas *User* y *Host*:

|               | +------------------+-----------+             |
|---------------|----------------------------------------------|
| User          | Host   +------------------+-----------+      |
| leonardo      | %     mysql.infoschema   localhost           |
| mysql.session | localhost                                    |
| mysql.sys     | localhost                                    |
| root          | localhost   +------------------+-----------+ |

Como vemos, al no especificar ningún anfitrión, se ha reemplazado el valor de esta columna por el comodín % (cualquiera). Esto permitiría al nuevo usuario conectarse al SGBD desde cualquier anfitrión.

Si queremos ver todas las propiedades relativas a una cuenta en particular (en este caso, las correspondientes al usuario *leonardo*), ejecutaremos la siguiente sentencia:

#### Para + info

Los **administradores de usuarios (UserAdmin)** requieren de los privilegios globales para la ejecución de sentencias *CREATE USER* (*Create\_user\_priv*), que permite crear cuentas y reiniciar contraseñas, y *RELOAD* (*Reload\_priv*), que permite la ejecución de las sentencias de volcado (*FLUSH*) y la recarga de las tablas de privilegios. En términos generales, todas las cuentas con el privilegio *CREATE USER* pueden también modificar y eliminar usuarios.

El asterisco (\*) es el comodín que representa todas las columnas de la tabla, y con la cláusula *WHERE* filtramos los resultados según el valor especificado para la columna *User*.

Tal como hemos comentado, el administrador de usuarios puede establecer, en la misma sentencia de creación de la cuenta, ciertas propiedades básicas; las más habituales son el anfitrión desde donde se debe conectar el nuevo usuario, y una contraseña:

CREATE USER 'miguel'@'localhost' IDENTIFIED BY 'Contra12345<';

En esta ocasión, se especifica el nombre de anfitrión desde donde puede conectarse el nuevo usuario (*localhost*) y se le asigna la contraseña *Contra12345<*.

Dado que podemos configurar las propiedades de la cuenta en el mismo momento de su creación, las sentencias *CREATE USER* pueden ser relativamente extensas, al ofrecer la posibilidad de incluir diversos parámetros. Además, es posible crear varias cuentas en el mismo proceso si incluimos varios usuarios separados por comas, especificando para cada uno de ellos su anfitrión y sus opciones de autenticación. Tomemos, por ejemplo, la siguiente sentencia:

|    | 1 CREATE USER                         |
|----|---------------------------------------|
| 2  | leonardo@localhost                    |
| 3  | IDENTIFIED WITH mysql_native_password |
| 4  | BY RANDOM PASSWORD,                   |
| 5  | miguel@10.0.1.20                      |
| 6  | IDENTIFIED BY RANDOM PASSWORD         |
| 7  | REQUIRE SSL                           |
| 8  | WITH MAX_CONNECTIONS_PER_HOUR 25      |
| 9  | MAX_QUERIES_PER_HOUR 250              |
| 10 | MAX_UPDATES_PER_HOUR 50               |
| 11 | MAX_USER_CONNECTIONS 5                |
| 12 | PASSWORD EXPIRE                       |
| 13 | PASSWORD EXPIRE INTERVAL 365 DAY      |
| 14 | PASSWORD HISTORY 5;                   |

Podemos desglosarla en los siguientes bloques:

- 1. **Nombre, anfitrión y autenticación de cada usuario (separados por comas):**
  - a. Se define un usuario llamado *leonardo*, en el anfitrión *localhost* y autenticado (*IDENTIFIED*) utilizando una contraseña de tipo MySQL nativa (*WITH mysql\_native\_password*) definida al azar (*BY RANDOM PASSWORD*).

- b. Se define un usuario llamado *miguel*, con acceso permitido desde la máquina con dirección IP *10.0.1.20* y autenticado mediante una contraseña aleatoria usando el complemento de autenticación por defecto.

### 2. **Propiedades comunes a ambas cuentas:**

- a. Requieren de una conexión segura mediante SSL (*REQUIRE SSL*).
- b. Se les configura los siguientes límites de acceso a los recursos (*WITH*): 25 conexiones por hora (*MAX\_CONNECTIONS\_PER\_HOUR*). 250 consultas por hora (*MAX\_QUERIES\_PER\_HOUR*). 50 actualizaciones por hora (*MAX\_UPDATES\_PER\_HOUR*). Un máximo de 5 conexiones simultáneas (*MAX\_USER\_CON-NECTIONS*).
- c. Opciones de contraseña: La contraseña aleatoria asignada expira de inmediato (*PASSWORD EXPIRE*), por lo que se debe cambiar en el primer inicio de sesión. Las contraseñas expiran al cabo de 365 días (*PASSWORD EXPI-RE INTERVAL*). Se veta la reutilización de las 5 contraseñas previas (*PASSWORD HISTORY*).

Los diferentes bloques de las sentencias *CREATE USER* deben conservar el orden establecido por su sintaxis, que es la siguiente:

CREATE USER [IF NOT EXISTS] usuario [opción\_de\_autenticación] [, usuario [opción\_de\_autenticación]] ... DEFAULT ROLE rol [, rol] ... [REQUIRE {NONE | opción\_tls [[AND] opción\_tls] ...}] [WITH opción\_de\_recursos [opción\_de\_recursos] ...] [opción\_de\_contraseña | opción\_de\_cierre] ... [COMMENT 'comentario' | ATTRIBUTE 'objeto\_json']

Debemos tener presente que las **cuentas recién creadas** no tienen ningún privilegio concedido, por lo que, de entrada, son incapaces de acceder a los recursos del SGBD.

### Atención

#### Para + info

En la sección 13.7.1.3 del manual de referencia en línea de MySQL se puede consultar al detalle la sintaxis de las sentencias *CREATE USER* y todas sus posibles opciones:

[bit.ly/3hHFdTl](http://bit.ly/3hHFdTl)

![](_page_64_Picture_7.jpeg)

### **Modificar y eliminar usuarios**

La sentencia *ALTER USER* se utiliza para modificar las cuentas de MySQL, y adopta la misma sintaxis básica que la sentencia *CREATE USER*:

ALTER USER [IF EXISTS] usuario [opción\_de\_autenticación] [, usuario [opción\_de\_autenticación]] ... DEFAULT ROLE rol [, rol] ... [REQUIRE {NONE | opción\_tls [[AND] opción\_tls] ...}] [WITH opción\_de\_recursos [opción\_de\_recursos] ...] [opción\_de\_contraseña | opción\_de\_cierre] ... [COMMENT 'comentario' | ATTRIBUTE 'objeto\_json']

Cualquier propiedad no incluida explícitamente en la sentencia *ALTER USER*, retendrá sus valores actuales.

![](_page_65_Picture_5.jpeg)

Un posible ejemplo de sentencia *ALTER USER* sería el siguiente:

1 ALTER USER leonardo@localhost 2 IDENTIFIED BY 'Contra54321>' 3 PASSWORD EXPIRE INTERVAL 200 DAY 4 FAILED\_LOGIN\_ATTEMPTS 3 PASSWORD\_LOCK\_TIME 2 5 COMMENT 'Representante de ventas EMEA';

Mediante esta sentencia modificamos la contraseña del usuario, su periodo de validez, el número de intentos de inicio de sesión fallidos permitidos y los días que permanecerá bloqueada la cuenta en caso de haber superado dicho límite, y, por último, agregamos un comentario. *ALTER USER* soporta diversas opciones a la hora de modificar las contraseñas de usuario. Es posible, por ejemplo, asignar una nueva contraseña primaria, pero retener la anterior como contraseña secundaria:

1 ALTER USER leonardo@localhost 2 IDENTIFIED BY 'nueva\_contraseña' 3 RETAIN CURRENT PASSWORD;

### Para + info

*CREATE USER* y *ALTER USER* difieren en el uso de *IF EXISTS* e *IF NOT EXISTS*, que se usan para evitar que se produzca un error si el usuario a crear ya existe o si la cuenta a modificar no existe. En *CREATE USER*, la operación solo se ejecuta en el caso de que el usuario no exista (*IF NOT EXISTS*), mientras que en *ALTER USER*, solo se llevará a cabo si el usuario existe (*IF EXISTS*).

Posteriormente, se podría descartar esta segunda contraseña con la siguiente sentencia:

ALTER USER leonardo@localhost DISCARD OLD PASSWORD;

Por otra parte, a la hora de modificar las contraseñas de usuario contamos también con la sentencia *SET PASSWORD* —aunque, por lo general, se prefiere *ALTER USER*—, así como con la opción *password* de la instrucción *mysqladmin*; por ejemplo:

> mysqladmin -u leonardo -h localhost password "nueva\_contraseña"

Si lo que deseamos es cambiar el propio nombre de usuario o de anfitrión de una cuenta, utilizaremos la sentencia *RENAME USER*; por ejemplo:

RENAME USER leonardo@localhost TO leo@10.0.1.30;

Si se omite el nombre de anfitrión, este se cambiará por el carácter comodín %.

Por último, para eliminar una o más cuentas de usuario, junto con todos sus privilegios, contamos con la sentencia *DROP USER*:

DROP USER leonardo@localhost, miguel@10.0.1.20;

### Para + info

Los **comentarios y atributos de los usuarios** se almacenan como objetos JSON en la tabla *INFORMATION\_SCHEMA*. *USER\_ATTRIBUTES*. Por lo tanto, para revisarlos, podemos usar la siguiente sentencia:

1 SELECT \* 2 FROM INFORMATION\_SCHEMA.USER\_ATTRIBUTES 3 WHERE USER='nombre\_de\_usuario' 4 AND HOST='nombre\_de\_anfitrión';

### **3.1.3. Gestión de permisos y roles**

Los administradores de seguridad son los responsables de conceder y retirar privilegios a los usuarios del SGBD, para lo cual se utilizan las sentencias *GRANT* y *REVOKE*. De igual forma, son los encargados de la gestión de roles mediante las sentencias *CREATE ROLE* y *DROP ROLE*.

### **Gestión de privilegios**

*GRANT* se utiliza para asignar privilegios o roles, pero no ambos en una misma sentencia. Estos permisos pueden ser globales o referirse a diferentes objetos del sistema: una o varias bases de datos, tablas, columnas, rutinas almacenadas o usuarios proxy. La sintaxis de esta instrucción es la siguiente:

GRANT tipo\_de\_privilegio [(lista\_de\_columnas)] [, tipo\_de\_privilegio [(lista\_de\_columnas)]] ... ON [tipo\_de\_objeto] nivel\_de\_privilegio TO usuario\_o\_rol [, usuario\_o\_rol] ... [WITH GRANT OPTION] [AS usuario [WITH ROLE DEFAULT | NONE | ALL | ALL EXCEPT rol [, rol] ... | rol [, rol] ... ] ]

![](_page_67_Picture_6.jpeg)

### Para + info

En la sección 13.7.1.6 del manual en línea de MySQL se puede consultar al detalle la sintaxis de la sentencia *GRANT* y todas sus posibles opciones. En las tablas 13.11 y 13.12 de dicha sección se recogen, a su vez, todos los tipos de privilegios estáticos y dinámicos que pueden especificarse en las sentencias *GRANT* y *REVOQUE*.

### [bit.ly/3ELhGtT](http://bit.ly/3ELhGtT)

![](_page_67_Picture_10.jpeg)

Así pues, en su formulación más básica, en la sentencia *GRANT* deben figurar el permiso o permisos a conceder, el objeto sobre el cual se conceden y el usuario o rol al cual se le conceden. Por ejemplo, para conceder todos los permisos sobre todas las bases de datos de MySQL, usaremos una sentencia como la siguiente:

GRANT ALL ON \*.\* TO leonardo@localhost;

También podemos conceder permisos concretos sobre objetos determinados. Por ejemplo, para otorgar permisos de selección e inserción, sobre una base de datos llamada *filmoteca*, al usuario *leonardo@localhost*, utilizaríamos la siguiente sentencia:

GRANT SELECT, INSERT ON filmoteca.\* TO leonardo@localhost;

De la misma forma, para gestionar privilegios sobre tablas concretas (por ejemplo, la tabla actores de la BD *filmoteca*), utilizamos la misma sintaxis:

GRANT SELECT, INSERT ON filmoteca.actores TO leonardo@localhost;

Sin embargo, cuando los permisos son sobre columnas concretas dentro de una tabla, es necesario explicitarlas entre paréntesis a continuación del tipo de permiso a conceder. En nuestro ejemplo anterior, si queremos conceder permisos para insertar y actualizar datos en las columnas nombre y apellido de la tabla anterior, usaremos la siguiente sentencia:

GRANT INSERT (nombre, apellido), UPDATE (nombre, apellido) ON filmoteca.actores TO leonardo@localhost;

En lo relativo a las rutinas —procedimientos y funciones almacenados—, puede concederse el privilegio para crearlas y para ejecutarlas:

GRANT CREATE ROUTINE ON filmoteca.\* TO leonardo@localhost;

GRANT EXECUTE ON PROCEDURE filmoteca.miproc TO leonardo@localhost;

Por último, para traspasar todos los privilegios de un usuario (por ejemplo, *leonardo@localhost*) a otro usuario que adopta el papel de representante o proxy (en nuestro ejemplo, *miguel@10.0.20*), podemos utilizar la sentencia siguiente:

Podemos conocer los permisos asignados a un usuario utilizando la sentencia *SHOW GRANTS*:

SHOW GRANTS FOR leonardo@localhost;

Para retirar privilegios o roles a cuentas de usuario o a otros roles, los administradores de seguridad pueden utilizar una sentencia *REVOKE*. Si sintaxis es similar a la de *GRANT*:

REVOKE [IF EXISTS] tipo\_de\_privilegio [(lista\_de\_columnas)] [, tipo\_de\_privilegio [(lista\_de\_columnas)]] ... ON [tipo\_de\_objeto] nivel\_de\_privilegio FROM usuario\_o\_rol [, usuario\_o\_rol] ... [IGNORE UNKNOWN USER]

Como vemos, podemos utilizar la opción *IF EXISTS* para evitar un mensaje de error en el caso de que el usuario o rol sobre el que queremos actuar exista, pero carezca de los privilegios o roles que se desean retirar. También podemos eludir el error, en el caso de que el usuario o rol sobre el que actúa la sentencia no existiera, añadiendo la opción *IGNORE UNKNOWN USER*.

Utilizando nuestro ejemplo anterior, para retirar los permisos de selección e inserción sobre las tablas de la BD *filmoteca* al usuario *leonardo@ localhost*, utilizaríamos la siguiente sentencia:

REVOKE SELECT, INSERT ON filmoteca.\* FROM leonardo@localhost;

![](_page_69_Picture_8.jpeg)

### Para + info

Dado que, para revocar permisos, un administrador debe contar con el privilegio *GRANT OPTION*, así como con todos los privilegios que desea retirar, para revocar todos los permisos de dicho usuario deberemos utilizar la siguiente sintaxis:

REVOKE ALL PRIVILEGES, GRANT OPTION FROM usuario\_o\_rol [, usuario\_o\_rol] ...

Para ejecutar esta sentencia, es necesario contar con el privilegio global *CREATE USER*.

### **Gestión de roles**

Un rol no es más que una colección de privilegios. Existen diversos roles predeterminados en MySQL, pero es posible crear roles con conjuntos de privilegios personalizados.

Para crear nuevos roles se utiliza la sentencia *CREATE ROLE*:

CREATE ROLE [IF NOT EXISTS] rol [, rol] ...

Por ejemplo, la siguiente sentencia creará los roles *comercial* y *desarrollador*:

CREATE ROLE comercial, desarrollador;

Por otra parte, la sentencia *DROP ROLE* —que adopta la misma sintaxis básica que *CREATE ROLE*— se utiliza para eliminar roles:

DROP ROLE comercial, desarrollador;

De esta sintaxis podemos inferir fácilmente que un rol recién creado carece de privilegios: estos se tienen que conceder explícitamente. Y, como ya hemos mencionado, es la sentencia *GRANT* la que se utiliza para este fin; por ejemplo, la sentencia a continuación añade el privilegio de inserción sobre la BD *filmoteca* al rol denominado *rol1*:

GRANT INSERT ON filmoteca.\* TO rol1;

Una vez dotados de privilegios, podemos ya usar *GRANT* para asignar uno o varios roles, a uno o diversos usuarios o roles:

GRANT rol1, rol2 TO leonardo@localhost, miguel@10.0.1.20;

La sentencia anterior asigna los roles *rol1* y *rol2* a los usuarios *leonardo@localhost* y *miguel@10.0.1.20.* Si quisiéramos asignar todos los privilegios de un rol a otro rol, utilizaríamos la misma sintaxis básica:

GRANT rol1 TO rol2;

Para conocer qué roles están activos para la sesión actual, podemos usar la función *CURRENT\_ROLE()*, de esta forma:

Por otra parte, para retirar roles utilizamos la sentencia *REVOKE*:

REVOKE rol1, rol2 FROM leonardo@localhost, miguel@10.0.1.20;

REVOKE rol1 FROM rol2;

Es importante tener presente que, para que los roles asignados a un usuario se hagan efectivos, deben activarse previamente utilizando las sentencias *SET ROLE* (aplica los roles especificados al usuario que ha iniciado la sesión) y *SET DEFAULT ROLE* (aplica uno o varios roles por defecto cada vez que los usuarios especificados inician la sesión).

Por ejemplo, para asignar los roles *comercial* y *desarrollador* a *leonardo@localhost*, y que todos los roles asignados a él se activen cada vez que dicho usuario inicie sesión, emplearíamos las siguientes cláusulas:

GRANT comercial, desarrollador TO leonardo@localhost;

SET DEFAULT ROLE ALL TO leonardo@localhost;

Si no queremos tener que ir activando explícitamente los roles asignados a cada cuenta, podemos habilitar la variable del sistema *activate\_all\_roles\_on\_login*, que instruye a MySQL para que active todos los roles asignados a las cuentas durante su inicio de sesión. Si esta variable está desactivada, solo se activarán los roles que hayamos designados como activos por defecto usando *SET DEFAULT ROLE*.

![](_page_71_Picture_9.jpeg)

#### Para + info

Es posible hacer que algunos roles se concedan siempre a todas las cuentas si incluimos la variable *mandatory\_roles* en el archivo de configuración inicial (*my.cnf*); por ejemplo:

[mysqld] mandatory\_roles='rol1,rol2'

También podemos hacer persistentes estos roles obligatorios con la siguiente sentencia:

SET PERSIST mandatory\_roles = 'rol1,rol2';

En cualquiera de los dos casos, lograremos que los roles (llamados *rol1* y *rol2* en nuestro ejemplo) se concedan siempre a todas las cuentas, por lo que no será necesario hacerlo de forma explícita. Sin embargo, como en el caso de cualquier rol, los roles obligatorios no entrarán en efecto hasta que sean activados.

![](_page_72_Diagram_0.jpeg)
