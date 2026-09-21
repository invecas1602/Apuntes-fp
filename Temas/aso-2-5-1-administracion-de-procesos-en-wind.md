# **2.5.1. Administración de procesos en Windows**

En Windows, disponemos de las siguientes órdenes para la administración de procesos:

- **Tasklist / Get-Process**: devuelve la lista de procesos en ejecución, tanto del equipo local como de un sistema remoto. También permite utilizar diferentes filtros para mostrar únicamente los procesos que cumplan determinadas condiciones. Por ejemplo, para mostrar los procesos en ejecución que pertenecen al usuario Juan Cerro, ejecutaríamos la siguiente instrucción:

### TASKLIST /FI "USERNAME eq Juan" /FI "STATUS eq running"

Como vemos, */FI* es el parámetro que precede a un filtro, expresión entrecomillada que contiene: un nombre de filtro (*USERNAME, STATUS,* etc.), un operador (en este caso, *eq*, que significa 'equivale') y un valor válido según el tipo de filtro seleccionado. *Get-Process* es el *cdmlet* para PowerShell que cumple, básicamente, el mismo cometido que *tasklist*.

- **Start / Start-Process**: se utiliza para ejecutar un programa, y resulta de utilidad para asignarle manualmente una determinada prioridad, un uso determinado de la memoria o del procesador, y la arquitectura de máquina, entre otros parámetros. Por ejemplo, para iniciar el Bloc de notas en una ventana maximizada y con una prioridad por encima de la normal, utilizaríamos la siguiente instrucción:

- **Taskkill / Stop-Process**: ocasiona la detención inmediata de un proceso. Al igual que *tasklist*, admite el uso de filtros para terminar procesos que cumplan determinadas condiciones. Podemos usarla, por ejemplo, para terminar, de manera forzada (*/F*), todos los procesos con un PID mayor o igual a 1000:

### TASKKILL /F /FI "PID ge 1000"

- **Sc**: se utiliza para comunicarse con el Administrador de control de servicios y con los servicios de Windows. Mediante las diversas órdenes que contempla, nos permite consultar el estado del servicio (*query*), iniciarlo (*start*), pausarlo (*pause*), detenerlo (*stop*), crear un nuevo servicio (*create*), eliminarlo (*delete*), o consultar su configuración (*qc*), entre otras muchas opciones. Por ejemplo, para enumerar los servicios de controladores activos, podemos utilizar la siguiente instrucción:

### SC query type=driver

En el caso de PowerShell contamos con varios *cmdlets* independientes que nos permiten gestionar los servicios, como *Get-Service, Set-Service, Start-Service, Restart-Service, Suspend-Service* y *Stop-Service.*

En cuanto a las herramientas gráficas, contamos con el **Administrador de tareas** para gestionar todos los procesos, y con el complemento **Servicios** para gestionar específicamente este tipo de procesos a través de la consola de administración de Microsoft.

El Administrador de tareas organiza de forma clara y dinámica toda la información relativa a los procesos en ejecución y al porcentaje de los recursos de CPU, memoria, GPU, almacenamiento y red asignados a ellos en cada momento. También nos permite detener los procesos o ponerlos en modo eficiente, que reduce la prioridad de los procesos y, por lo tanto, el perfil energético. Además, activando la columna Anunciante podremos saber, en la mayor parte de los casos, si se trata de un proceso del sistema (Microsoft Corporation) o de una instancia de un programa de terceros.

![](_page_44_Picture_14.jpeg)

#### Para + info

Para consultar las opciones disponibles de cada instrucción y su sintaxis, utiliza /? como parámetro de la orden (por ejemplo, *SC /?).* En cuanto al uso de los *cmdlets* para Power-Shell, puedes obtener indicaciones acerca de su sintaxis en los siguientes enlaces:

**1** http://bit.ly/3G8xLdw

![](_page_44_Picture_7.jpeg)

**2** http://bit.ly/436rb10

![](_page_44_Picture_11.jpeg)

El Administrador de tareas también nos permite acceder a la lista de servicios en ejecución, desde donde podremos detenerlos, iniciarlos o reiniciarlos, pero para poder configurar cada uno de los servicios, tendremos que abrir la herramienta de administración de servicios. Podemos hacerlo desde la opción presente en el propio Administrador de tareas, o bien ejecutando la orden *services.msc*.

La herramienta de administración de servicios nos muestra la lista de los servicios instalados, su descripción (si la tienen), el estado de ejecución, su tipo de inicio y la cuenta de usuario que proporciona los permisos administrativos a cada uno de ellos.

*Administrador de tareas de Windows.*

Desde esta vista podemos iniciar, detener, pausar, reanudar y reiniciar los servicios (si estos lo permiten), y haciendo doble clic sobre cada uno, acceder a su diálogo de *Propiedades*.

En la pestaña *General* podremos configurar el tipo de inicio del servicio:

- **Automático**: el servicio lo inicia el sistema u otro servicio de forma automática.
- **Automático (inicio retrasado)**: el servicio se inicia después de que Windows se haya cargado por completo.
- **Manual**: es una aplicación o función iniciada por un usuario la que inicia el servicio.
- **Manual (desencadenar inicio)**: el servicio sólo se iniciará si no hay demasiados servicios en ejecución.
- **Deshabilitado**: el servicio no se iniciará.

En la pestaña *Inicio de sesión* podremos seleccionar la cuenta de usuario asociada al servicio, mientras que en *Recuperación* podremos determinar cómo responderá el sistema ante un error en el servicio. Finalmente, en *Dependencias* veremos de qué otros servicios, controladores o componentes del sistema depende la correcta ejecución del servicio.

*Propiedades de un servicio.*
