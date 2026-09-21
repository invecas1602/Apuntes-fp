# **4.1. Guiones para intérpretes de órdenes**

Una parte importante del trabajo de un administrador de SGBD consiste en realizar tareas de mantenimiento que, por propia naturaleza, son repetitivas. Por este motivo, se hace imprescindible el uso de herramientas que permitan automatizar este tipo de trabajos. Por un lado, y como veremos más adelante en este capítulo, contamos con el programador de eventos del propio sistema gestor, con el que es posible automatizar la ejecución de procedimientos almacenados, pero también es posible utilizar guiones para el intérprete de órdenes del sistema operativo subyacente.

![](_page_94_Picture_3.jpeg)

Dado que muchas tareas relacionadas con la administración de sistemas consisten en la ejecución de varias líneas de órdenes, los emuladores de terminal tienen la capacidad de procesar guiones o *scripts*, archivos en los que se almacena la secuencia de órdenes a ejecutar, y que podemos editar con cualquier procesador de textos simples. En el caso del Símbolo del sistema, estos archivos se denominan "de procesamiento por lotes", y llevan la extensión .bat, mientras que, en PowerShell, los guiones se identifican mediante la extensión *.ps1*. En cuanto a Linux, los *scripts* para bash, que es uno de los *shells* más utilizados, llevan por extensión *.sh*.

Los guiones de bash deben empezar con una línea que defina la ruta del intérprete a utilizar para la ejecución del script; por ejemplo:

### > #!/bin/bash

Además, deberemos hacer ejecutables los archivos *.sh* creados con nuestro editor de textos simples:

Un **intérprete de órdenes** es un programa que sirve para dar instrucciones escritas al sistema operativo siguiendo una sintaxis preestablecida. Las órdenes se teclean en una interfaz de línea de órdenes (en inglés, *command-line interface*, CLI), implementada a través de un emulador de terminal o *shell*. En Linux contamos con una variedad de emuladores de terminal, entre los que se cuentan Bourne Shell (sh), Debian Almquist Shell (dash), Bourne Again Shell (bash) y Friendly Interactive Shell (fish), mientras que para Windows tenemos el Símbolo del sistema (cmd) y Windows PowerShell.

![](_page_94_Picture_5.jpeg)

Aunque para elaborar un *script* no se necesita ningún programa especial al margen de los editores de textos incluidos en los diferentes sistemas operativos, en Linux existen herramientas que nos pueden ayudar a realizar tareas específicas sobre ciertos archivos, como los que resultan de una tubería. Entre ellos podemos citar SED, con el que se pueden filtrar textos y realizar transformaciones, como sustituciones y eliminaciones, y Gawk, que permite buscar patrones de cadenas de texto y ejecutar una determinada acción ante cualquier coincidencia.

### Para + info

### > chmod +x mi\_guion.sh

Para ejecutar el guion, utilizaremos la siguiente sintaxis:

### > ./mi\_guion.s

En el caso de PowerShell, Windows no permite su ejecución haciendo doble clic sobre ellos, siendo necesario hacer clic derecho sobre el archivo *.ps1* y escoger la opción *Ejecutar con PowerShell* en el menú contextual. También podemos ejecutar guiones en el mismo entorno de PowerShell utilizando la siguiente sintaxis:

### > .\mi\_guion.ps1

Las funciones de PowerShell son muy extensas y, en muchos casos, complejas, aunque el propio entorno de PowerShell ofrece diversas funciones de ayuda como completar las órdenes usando el tabulador, la instrucción *Get-Command* para listar todas las órdenes disponibles, y una sintaxis más clara y comprensible que la que nos proporciona el Símbolo del sistema.

Como en el caso de Linux, podemos editar los guiones de PowerShell utilizando cualquier procesador de textos, pero existe una herramienta de edición específica, denominada Integrated Scripting Environment (ISE), que proporciona funciones de ejecución y depuración avanzadas, y que se carga cuando seleccionamos la opción Editar en el menú contextual del archivo.

![](_page_95_Picture_8.jpeg)

![](_page_95_Figure_9.jpeg)

Aunque el sistema no permite la ejecución directa de guiones Power-Shell, sí podemos utilizar una instrucción de Símbolo del sistema para ejecutarlos con la opción *-file* de *powershell.exe*:

> powershell -file "mi\_guion.ps1"

Esto hace posible programar la ejecución periódica de guiones de PowerShell, de forma muy sencilla, utilizando el Programador de tareas.

### **PowerShell y el conector .NET para MySQL**

El instalador de MySQL incluye un conector para .NET que permite utilizar PowerShell para interactuar con nuestras bases de datos. De esta forma, es posible utilizar PowerShell para elaborar guiones que ejecuten consultas de forma programada.

Por ejemplo, para conectar con la base de datos *filmoteca* que hemos venido utilizando como ejemplo práctico, incluiríamos en nuestro guion las siguientes líneas (cambiando la ruta por la que corresponda según la versión de MySQL y del conector que estemos usando):

> Add-Type -Path 'C:\Program Files (x86)\MySQL\Connector NET 8.0 \Assemblies\v4.8\MySql.Data.dll' > \$Conexion = [MySql.Data.MySqlClient.MySqlConnection]@ {ConnectionString='server=localhost;uid=leonardo; pwd=contraseña;database=filmoteca'}

En la primera línea estamos indicando la ubicación de la biblioteca que se encarga de la conexión con la BD, mientras que en la segunda definimos la cadena de conexión, en la que es necesario indicar el servidor (*server*), el usuario con permisos de acceso (*uid*), su contraseña (*pwd*) y la base de datos (*database*). Si hemos especificado correctamente los datos de la conexión, podremos abrirla sin que se produzca un mensaje de error:

> \$Conexion.Open()

Para facilitarnos el manejo de bases de datos con MySQL, existen módulos de PowerShell que simplifican la ejecución de las operaciones más habituales. Uno de ellos es el que podemos encontrar en la dirección *<https://github.com/adbertram/MySQL>*. Básicamente, los módulos son colecciones de guiones de PowerShell (llamados también *cmdlets*) que pueden ejecutarse como si fueran órdenes. Para ejemplificar su uso, escribiremos un guion que ejecute *SELECT* \* sobre la tabla *películas* de la base de datos *filmoteca*.

![](_page_97_Picture_1.jpeg)

Para instalar el módulo, lo descargaremos desde su repositorio, lo descomprimiremos en la carpeta de módulos (por defecto, *C:\Program Files\WindowsPowerShell\Modules*), y editaremos el nombre de la carpeta como MySQL, todo ello desde PowerShell:

> Invoke-WebRequest -Uri https://github.com/adbertram/MySQL/archive/master.zip -OutFile 'C:\MySQL.zip' > Expand-Archive -Path C:\MySql.zip -DestinationPath 'C:\Program Files\WindowsPowerShell\Modules' > Rename-Item -Path "C:\Program Files\WindowsPowerShell\ Modules\MySql-master" -NewName MySQL

A continuación, creamos un nuevo archivo de guion usando ISE o un editor de textos. En primer lugar, para utilizar el módulo MySQL lo importaremos con la siguiente orden:

Import-Module -Name MySQL

Seguidamente, usaremos el *cmdlet Connect-MySqlServer*:

Connect-MySqlServer -Credential \$cred -ComputerName 'localhost' -Database filmoteca

Este nos solicitará el nombre de usuario y la contraseña con el cual queremos establecer la conexión. Se trata de una forma mucho más segura de pasar las credenciales al conector, ya que se utiliza, para ello, el *cmdlet Get-Credential*.

Una vez conectados a la base de datos, ejecutamos la consulta con el *cmdlet Invoke-MySqlQuery*:

Invoke-MySqlQuery -Query 'SELECT \* FROM películas'

En contrapartida, para obtener los mismos resultados, aunque sin recurrir a módulos de terceros, tendríamos que utilizar el siguiente guion:

 1 Add-Type -Path 'C:\Program Files (x86)\MySQL\Connector NET 8.0\ Assemblies\v4.8\MySql.Data.dll' 2 \$Conexion = [MySql.Data.MySqlClient.MySqlConnection]@{ConnectionString= 'server=localhost;uid=leonardo;pwd=contraseña;database=filmoteca'} 3 \$Conexion.Open() 4 \$Orden = New-Object MySql.Data.MySqlClient.MySqlCommand 5 \$Adaptador = New-Object MySql.Data.MySqlClient.MySqlDataAdapter 6 \$Datos = New-Object System.Data.DataSet 7 \$Orden.Connection = \$Conexion 8 \$Orden.CommandText = 'SELECT \* FROM películas' 9 \$Adaptador.SelectCommand = \$Orden 10 \$NumDatos = \$Adaptador.Fill(\$Datos, "datos") 11 Foreach(\$Registro in \$Datos.tables[0]) 12 {Write-Host "idPelícula :"\$Registro.idPelícula"`r`ntítulo :" \$Registro.título"`r`naño :"\$Registro.año"`r`npaís :" \$Registro.país"`r`ndirector :"\$Registro.director"`r`nidGénero :" \$Registro.idGénero"`r`n"} 13 \$Conexion.Close()
