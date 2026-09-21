# **2.2. Escoger la versión de MySQL**

Como ya se ha comentado, en esta obra utilizaremos **MySQL Community Server** como base y ejemplo de los contenidos prácticos, en concreto la versión **8.0.31**.

Desde la web para desarrolladores de MySQL tendremos acceso a la descarga del programa para cada uno de los sistemas operativos soportados, ya sea comprimidos en formato ZIP o TAR, o bien como paquete instalación.

En el caso de Linux, disponemos de los paquetes DEB para distribuciones basadas en Debian y superiores (como Ubuntu), y RPM para SUSE, RedHat y derivadas. En el caso de Windows, se proporciona un paquete de instalación MSI compatible con las siguientes versiones de 64 bits: Microsoft Windows 2012 Server R2, Microsoft Windows 2016 Server, Microsoft Windows 2019 Server, Microsoft Windows 2022 Server, Microsoft Windows 10 y Microsoft Windows 11.

![](_page_33_Picture_5.jpeg)

### Para + info

En el siguiente enlace puede encontrarse el listado de las plataformas soportadas por MySQL:

[bit.ly/3frJLNb](https://bit.ly/3frJLNb)

![](_page_33_Picture_9.jpeg)

El paquete de instalación MSI de MySQL Community Server para Windows puede descargarse desde el siguiente enlace:

[bit.ly/3U4o2tA](https://bit.ly/3U4o2tA)

![](_page_33_Picture_12.jpeg)

### **2.3. Instalación y configuración básica de MySQL**

### **2.3.1. Asistentes de instalación <sup>y</sup> configuración inicial**

En nuestro caso, plantearemos uno de los escenarios de instalación de MySQL habituales en el ámbito empresarial, utilizando como plataforma una instancia de Microsoft Windows 2022 Server Standard, versión 21H2.

- 1. Tras hacer doble clic en el archivo MSI que hemos descargado desde la web de MySQL, el instalador nos invita a escoger el tipo de instalación que vamos a realizar: para equipos de desarrollo, únicamente como SGBD dedicado, cliente de SGBD, instalación completa o personalizada.

Para instalar ciertos productos es necesario que el equipo cumpla los requisitos necesarios. Por ejemplo, el componente MySQL for Visual Studio requiere de Visual Studio, versión 2015 o superior, mientras que el conector para Python requiere haber instalado una versión de 64 bits de Python a partir de la 3.7. En cualquier caso, los productos con requerimientos insatisfechos no se instalarán.

- 2. Antes de proceder con la instalación, se nos mostrará el listado de los productos que se van a instalar, según el tipo de configuración deseada.

Al finalizar, podremos comprobar si alguno de los productos seleccionados no se instaló correctamente, y consultar un registro detallado que nos permitirá diagnosticar el problema (botón *Show*/ *Hide Details*).

- 3. A continuación, se ejecutará un asistente de configuración para los productos que lo requieran; en nuestro caso, vamos a ver los pasos de configuración relativos a MySQL Server 8.0.31.

En la primera ventana del asistente deberemos escoger la configuración de servidor que mejor se adecúe a nuestras necesidades. Esta elección determinará la cantidad de recursos del sistema —en particular, de la memoria— que se asignarán, por defecto, a la instancia del SGBD. Aquí también podremos configurar las opciones de conectividad (protocolos y puertos), y activar la casilla que nos permitirá acceder a las opciones de registro y algunas otras opciones avanzadas de configuración.

A continuación, podemos escoger entre dos métodos de cifrado para autenticación, el mejorado (por defecto) y el legado (para aplicaciones incompatibles con los conectores y controladores más recientes).

- 4. En la siguiente pantalla indicaremos la contraseña para la cuenta raíz (*root*), y podremos añadir cuantos usuarios necesitemos.

A la hora de crear los usuarios, podemos optar por una amplia variedad de roles: administrador de copias de seguridad, diseñador de BD, gestor de instancia, administrador de replicación, etc.

![](_page_36_Picture_4.jpeg)

- 5. Es recomendable configurar el servidor de MySQL como servicio de Windows, bajo una cuenta de sistema estándar y con inicio automático en el inicio de sesión. En esta ventana podremos editar el nombre que va a tener este servicio, que, por omisión, es *MySQL80*.

También podemos dejar que el instalador configure los permisos de los archivos del servidor para que los administradores tengan pleno acceso a ellos. De todas formas, podremos administrar los permisos de forma manual tras haberse completado la instalación.

- 6. Si hemos escogido la configuración de las opciones de registro, podremos activar y desactivar los diferentes registros disponibles (de errores, general, de consultas lentas y binario), así como definir la ruta y el nombre de cada uno de ellos.

![](_page_37_Figure_3.jpeg)

- 7. Las opciones avanzadas nos permiten cambiar el identificador del servidor y si los nombres de las tablas conservarán las mayúsculas y minúsculas, o se convertirán a minúsculas.

Por último, aplicamos las configuraciones que hayamos escogido pulsando el botón *Execute*. En la pestaña *Log* podremos ver el registro de todas las operaciones realizadas por el asistente. Una vez completada la operación, concluimos con la instalación del servidor pulsando el botón *Finish*.

- 8. Si hemos seleccionado la instalación de muestras y ejemplos, tendremos que proporcionar la contraseña de la cuenta raíz para conectar el asistente con nuestra instancia de MySQL.

- 9. Una vez completada la instalación de todos los productos, podemos copiar el registro completo de las operaciones realizadas por los asistentes al portapapeles, lo cual nos permitirá pegarlo en un documento de texto para su almacenamiento y revisión posterior. De esta forma, quedará convenientemente documentado el proceso de instalación y configuración inicial de MySQL.

10. La última ventana también nos permite iniciar automáticamente MySQL Workbench (la interfaz de administración gráfica integrada) y MySQL Shell (*mysqlsh*, una evolución del tradicional cliente de líneas de instrucción *mysql*). De esta forma, podremos comprobar si la instalación ha sido, efectivamente, exitosa.

![](_page_39_Picture_3.jpeg)

### **2.3.2. Editar los parámetros de configuración**

Por defecto, las opciones relativas a MySQL Server se almacenan en el archivo *my.ini*, ubicado en *C:\ProgramData\MySQL\MySQL Server 8.0*. Contiene dos secciones, la sección que leen las aplicaciones cliente bajo la etiqueta [*client*], y la opciones del servidor bajo la etiqueta [*mysqld*]. Este archivo es editable de forma manual usando cualquier editor de texto simple, como el Bloc de notas.

Por otra parte, tanto para aplicar los cambios que hayamos podido realizar manualmente en este archivo configuración, como para realizar algunas operaciones administrativas, a menudo será necesario detener y, posteriormente, reanudar la ejecución de MySQL. Dado que, probablemente, habremos configurado MySQL como servicio de Windows, podemos realizar esta operación mediante la siguiente instrucción en una ventana de consola de Windows con privilegios de administrador (para invocarla, pulsamos la combinación de teclas *Windows+R* y escribimos *cmd* en la ventana *Ejecutar*):

### > net stop mysql80

El nombre del servicio a detener es el que le habremos dado durante la instalación y configuración inicial de MySQL (paso 5 del apartado 2.3.1 anterior), en nuestro caso, *mysql80*.

Para reiniciar el servicio, utilizaremos siguiente instrucción:

> net start mysql80

Otra alternativa consiste en utilizar una ventana de PowerShell para introducir las instrucciones. Para ello, hacemos clic derecho sobre el icono del menú Inicio, y seleccionamos la opción *Windows PowerShell*  (*Administrador*).

Obviamente, siempre podemos usar el complemento Servicios de la consola de administración de Microsoft (MMC), *services.msc*, para detener, pausar y reanudar este servicio, así como para configurar su tipo de inicio.

No obstante, si trabajamos habitualmente con MySQL Workbench, nos resultará más sencillo utilizar su interfaz gráfica para este propósito, así como para editar de forma más cómoda el archivo de configuración *my.ini*.

Dependiendo de la versiones del SGBD y del sistema operativo instaladas, para que la conexión con el servicio de MySQL funcione correctamente desde MySQL Workbench puede ser necesario cambiar la configuración de idioma.

Así pues, si obtenemos un mensaje de error al intentar administrar nuestra instancia local del MySQL, haremos lo siguiente: abriremos el *Panel de control* e iremos a *Reloj y Región* > *Región*, entraremos en la pestaña *Administrativo* y pulsaremos el botón *Cambiar configuración regional del sistema*.

Esto abrirá la ventana *Configuración regional*, donde debemos marcar la casilla *Versión beta: Use UTF-8 Unicode para la compatibilidad de idioma en todo el mundo*.

### Atención

*Activación de UTF-8 Unicode para compatibilidad de idioma.*

- 1. La primera vez que abramos MySQL Workbench, veremos la instancia local MySQL80 que se creó durante la instalación del servidor. Si hacemos clic sobre ella, se abrirá el diálogo de conexión donde tendremos que indicar la contraseña del usuario raíz (si el entorno es de confianza y la información a tratar no es de carácter sensible, podemos guardarla para no tener que introducirla en cada sesión).

![](_page_41_Picture_2.jpeg)

- 2. Para comprobar que la conexión funciona correctamente, hacemos clic en *Server Status*, la primera opción en la sección *MANAGEMENT* del panel *Administration* del navegador, en el lateral izquierdo de la ventana. Esto nos ofrecerá una vista resumen del tráfico de la BD, de las características disponibles, y de datos como los directorios utilizados, la configuración de replicación y las configuraciones de seguridad del servidor.

![](_page_41_Picture_4.jpeg)

- 3. Para detener el servidor o ponerlo fuera de línea, disponemos de los botones *Stop Server* y *Bring Offline* respectivamente, a los que

podemos acceder desde la opción *Startup* / *Shutdown* del apartado *INSTANCE* del panel de administración del navegador.

![](_page_42_Picture_2.jpeg)

- 4. Para acceder, finalmente, al archivo de opciones, haremos clic en *Options File*, dentro de la misma sección *INSTANCE*. Desde este panel podremos manejar cómodamente todos los valores del archivo de configuración *my.ini*.

El panel se divide en diferentes pestañas, relativas a los distintos aspectos de la configuración del servidor. En la primera de ellas, *General*, podemos configurar aspectos tan importantes como activar y desactivar el programador de eventos (*event-scheduler*), activar y desactivar el modo de confirmación automática (*autocommit*), el uso de la memoria, las rutas de los directorios, el uso exclusivo de minúsculas en los nombres de las tablas (*lower\_case\_table\_names*), y los conjuntos de caracteres por defecto (sección *International*).

![](_page_42_Picture_5.jpeg)

- 5. En la pestaña *Logging* podremos configurar las opciones de registro de auditoría (*audit-log*), de consultas lentas (*slow\_query\_log\_file*), y otros registros generales y avanzados.

- 6. Bajo la pestaña *Networking* encontraremos todas las opciones relativas a las conexiones de red, como el tamaño de los paquetes de envío y recepción (*max\_allowed\_packet*), los tiempos máximos de espera (*Timeout Settings*), las opciones relativas a las conexiones cifradas (*SSL*), el número máximo de conexiones permitidas (*max\_ connections*), y el puerto TCP a utilizar (*port*), entre otras muchas.

- 7. En la pestaña dedicada a la seguridad, *Security*, podremos configurar todo lo relativo a los servidores LDAP y otras muchas opciones de los mecanismos de autenticación utilizados, así como características generales de seguridad.

- 8. Podemos aplicar las modificaciones que hayamos realizado mediante el botón *Apply*, o descartarlas con *Discard*. Al aplicarlas, podremos revisar los cambios que se realizarán en el archivo *my.ini*, así como obtener una vista previa de él pulsando el botón *View File Preview*. Esto nos permitirá realizar más cambios, de forma manual, antes de aplicarlos.

![](_page_44_Picture_4.jpeg)

### Para + info

El **LDAP** (*Lightweight Directory Access Protocol*, o protocolo ligero de acceso a directorios) puede emplearse para recuperar los datos de los usuarios de un SGBD almacenada en un servidor LDAP. En el caso de MySQL, podemos utilizar el método de autenticación LDAP para obtener la información, credenciales y grupo de los usuarios.

Ponte a prueba

**¿Cómo se denomina el archivo en el que se almacenan, por omisión, las opciones relativas a MySQL Server?**

- a) mysql.cnf
- b) mysql.ini
- c) my.ini
- a) mysqld

### **2.3.3. Variables del servidor**

Ya hemos visto cómo, mediante una variable definida por el usuario, es posible almacenar un valor utilizando una sentencia y referirnos a dicho valor en otra sentencia distinta. De la misma forma, el servidor de MySQL almacena valores en variables para poder realizar sus operaciones internas.

### **Variables de sistema**

El funcionamiento de MySQL, incluyendo el de ciertos componentes o complementos, viene determinado por las variables de sistema. Las variables de sistema pueden ser de dos tipos, según su alcance:

- **Globales**: afectan al comportamiento del servidor en general.
- **De sesión**: únicamente afectan a conexiones de cliente individuales.

Cada una de estas variables tiene un valor por defecto, pero podemos cambiarlo, durante el arranque del servidor, mediante el uso de un archivo de configuración, así como también, en algunos casos, añadiendo modificadores a instrucciones de terminal.

Por ejemplo, en el caso de la variable *max\_allowed\_packet* que mencionamos en el punto anterior, para iniciar MySQL estableciendo su valor en 512 KB podemos utilizar la siguiente instrucción en una ventana de la consola de Windows (*cmd*):

### > mysqld --max-allowed-packet=512K

Observemos cómo las opciones van siempre precedidas de dos guiones, y también que, en este caso, a la hora de escribir el nombre de la variable como opción de la instrucción podemos utilizar los guiones normales y bajos de manera indistinta (es decir, *max\_connections* es igual que *max-connections*).

Existen determinadas variables, denominadas **dinámicas**, a las que también podemos cambiar el valor tras haber iniciado el servidor, es decir, en tiempo de ejecución. Para ello, utilizamos la sentencia SET en una consola de *mysql*, como por ejemplo la siguiente:

SET GLOBAL max\_connections = 100;

Debemos tener en cuenta que, cuando referimos a una variable en una sentencia de SQL, es obligatorio el uso de guiones bajos. Además, deberemos especificar el alcance del nuevo valor, pudiendo ser este global (*GLOBAL*), de sesión (*SESSION* o *LOCAL*), o, en algunos casos, persistente (*PERSIST* y *PERSIST\_ONLY*). Si no añadimos ningún modificador a la sentencia, se considerará, por omisión, que el valor es de sesión.

También podemos devolver, en tiempo de ejecución, una variable a su valor por defecto, utilizando la palabra clave *DEFAULT*:

SET GLOBAL max\_connections = DEFAULT;

Para saber el valor que tiene actualmente una variable, podemos utilizar la siguiente sentencia:

SHOW VARIABLES LIKE 'max\_connections';

Si no especificamos una variable, la sentencia *SHOW VARIABLES* nos listará todas las variables definidas, junto a sus respectivos valores.

Hay que tener en cuenta que las variables definidas dinámicamente como globales o de sesión, volverán a adquirir sus valores iniciales por defecto, o aquellos que se hayan indicado en los archivos de opciones, cuando reiniciemos el servidor, excepto si las hubiéramos definido como persistentes. En tal caso, se añadirán al archivo *mysqld-auto.cnf* en el directorio de datos de la instancia (por defecto, *C:\ProgramData\ MySQL\MySQL Server 8.0\Data\*), y se cargarán, como variables de sistema globales, en cada inicio del servidor.

Para añadir a este archivo un nuevo valor de variable persistente sin modificar dicha variable de inmediato, se utiliza la palabra clave *PER-SIST\_ONLY*. Para eliminar una variable de *mysqld-auto.cnf*, usaremos la sentencia *RESET PERSIST*, seguida del nombre de la variable:

RESET PERSIST max\_connections;

Si no se especifica ninguna variable en particular, la sentencia *RESET PERSIST* eliminará todas las variables presentes en *mysqld-auto.cnf*.

### **Variables de estado**

Las variables de estado almacenan información acerca del estado de funcionamiento del servidor, como el número de conexiones abortadas, la cantidad y número de errores de conexión registrados, el número de archivos temporales creados, entre otros muchos datos.

Estas variables pueden ser también globales (contienen el valor agregado de todas las sesiones) o de sesión; podemos obtener un listado de todas ellas mediante la siguiente sentencia:

SHOW [GLOBAL | SESSION] STATUS;

Como en el caso de las variables de sistema, podemos utilizar *LIKE* para mostrar el valor de una variable en concreto:

SHOW STATUS LIKE 'aborted\_clients';

### Para + info

Para administrar los valores de variable globales y persistentes normalmente es necesario usar un perfil con privilegios de tipo *SUPER*. Por el contrario, cualquier usuario puede, generalmente, cambiar el valor de una variable de sesión, exceptuando aquellas que pudieran tener algún efecto fuera de la propia sesión.

Ponte a prueba

**¿Qué sentencia utilizaríamos para establecer globalmente en 500 el valor de la variable** *max\_connections***, cada vez que se reinicia MySQL, sin alterar su valor actual?**

- a) mysqld GLOBAL --max-connections=500;
- b) SET GLOBAL max\_connections = 500;
- c) SET PERSIST max\_connections = 500; d)SET PERSIST\_ONLY max-connections = 500; e)Ninguna es correcta.

Cuando sea posible utilizar opciones alternativas en una instrucción o sentencia, las indicaremos todas entre corchetes y separándolas mediante una barra vertical; por ejemplo, *SHOW [GLOBAL | SESSION] STATUS* significa que la sentencia admite dos posibles formulaciones, *SHOW GLOBAL STATUS* y *SHOW SESSION STATUS*.

### Atención
