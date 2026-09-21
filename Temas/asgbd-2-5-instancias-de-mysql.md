# **2.5. Instancias de MySQL**

Es posible tener funcionando de forma concurrente varias instancias del servidor de BD, a condición de que cada una utilice un puerto TCP/IP distinto. A continuación, veremos cómo inicializar y ejecutar una nueva instancia de MySQL Server, usando para ello la consola de Windows.

Una vez creada, es posible utilizar el Programador de tareas para hacer que esta instancia se ejecute automáticamente —ya sea durante el inicio de sesión, o como respuesta a cualquier otro evento—, o bien ejecutarla como servicio de Windows.

- 1. En primer lugar, crearemos un directorio donde almacenaremos la configuración y los datos de esta segunda instancia de MySQL. En nuestro ejemplo, utilizaremos *C:\instancia2* como ruta del directorio base. Abrimos la consola de Windows (*cmd*) e introducimos la siguiente instrucción:

> md C:\instancia2

- 2. A continuación, en la misma ventana, inicializamos la instancia:

> mysqld --initialize-insecure --basedir=C:\instancia2

Hemos utilizado la opción *initialize-insecure* para que el usuario *root* no tenga, inicialmente, contraseña, aunque se la asignaremos posteriormente utilizando el monitor *mysql*. Si utilizamos la opción *initialize*, se asignará a *root* una contraseña temporal, que deberemos o cualquier otro programa para la edición de textos simples, cambiar, de igual manera, usando *mysql*, antes de que se nos permita establecer una conexión con la instancia.

- 3. Seguidamente, será necesario crear, dentro del directorio base —*C:\instancia2* en nuestro ejemplo—, y utilizando el Bloc de notas, un archivo de configuración al que llamaremos *my.cnf.* En este archivo copiaremos las siguientes líneas:

[mysqld] datadir = C:/instancia2/data port = 3308

En esta ocasión hemos optado por el puerto 3308, de manera que no coincida con el puerto por defecto, el 3306, que es el que corresponde a nuestra instancia local inicialmente configurada durante la instalación de MySQL.

- 4. Para arrancar la nueva instancia, utilizaremos la instrucción *mysqld* especificando la ruta del archivo de configuración recién creado:

> mysqld --defaults-file=C:\instancia2\my.cnf --console

La opción *console* hará que se nos muestren los mensajes de MySQL en la ventana de la consola, lo cual nos será útil a la hora de diagnosticar posibles errores.

- 5. Sin cerrar la ventana de consola donde se está ejecutando el servidor (si lo hiciéramos, el servidor se detendría), abrimos una nueva ventana de Símbolo del sistema y ejecutamos el monitor *mysql* sobre el puerto 3308:

> mysql -h localhost -u root --port=3308

- 6. Finalmente, asignaremos o cambiaremos la contraseña al usuario *root*:

ALTER USER 'root'@'localhost' IDENTIFIED BY 'nueva\_contraseña';

- 7. A partir de este momento, podemos conectarnos con las dos instancias de MySQL, mediante el monitor *mysql*, utilizando las siguientes instrucciones:

> mysql -h localhost -u root -p*contraseña*

> mysql -h localhost -u root -p*nueva\_contraseña* --port=3308

La primera de las instancias se está ejecutando en el puerto por defecto (3306), por lo que no es necesario especificarlo como opción de *mysql*.

- 8. Para facilitar la gestión de esta instancia, podemos crear una nueva conexión en MySQL Workbench. Hacemos clic sobre el botón con el signo *+* junto a MySQL Connections, en el panel de bienvenida de la herramienta, y en la ventana *Setup New Connection*, especificamos el nombre de la conexión, el puerto y, si lo deseamos, almacenamos la contraseña mediante el botón *Store in vault* para que no se nos pregunte cada vez que nos conectemos.
- 9. No debemos olvidar especificar la ruta al archivo de configuración (*C:\instancia2\my.cnf*) en el campo *Configuration File* de la pestaña *System Profile*, así como, en el caso de haberse configurado la ejecución de la instancia como servicio de Windows, el nombre de dicho servicio en el campo *Windows Service Name*.

- 10. Para comprobar si la instancia está funcionando y la conexión está correctamente configurada, hacemos clic en el botón *Test Connection*. 11.Pulsamos el botón *OK*, y veremos cómo la nueva conexión ha aparecido ya bajo *MySQL Connections*.

### Para + info

![](_page_52_Picture_3.jpeg)

Para configurar la ejecución de una instancia como servicio de Windows, utilizaremos la opción install de *mysqld*. En nuestro ejemplo, ejecutaríamos la siguiente instrucción en una consola de Windows (*cmd*):

> mysqld --install MySQL81 --defaults-file=C:\inst2\my.cnf

Esto creará un nuevo servicio llamado *MYSQL81* (puede tener cualquier otro nombre), configurado para iniciarse, de forma automática, usando el archivo de configuración *my.cnf* almacenado en el directorio *c:\inst2*. Si prefiriésemos que el servicio fuera de ejecución manual, utilizaríamos la opción *install-manual*.

Por otra parte, para eliminar este servicio usaríamos la siguiente instrucción:

> mysqld --remove MySQL81
