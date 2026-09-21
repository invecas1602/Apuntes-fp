# **2.5.2. Administración de procesos en Linux**

En Linux, podremos administrar los procesos y demonios desde cualquier emulador de terminal. A continuación efectuaremos un repaso de las principales herramientas con las que contamos para la gestión de procesos en Debian 11.

#### **ps**

Para interactuar con los procesos en Linux, la herramienta básica es *ps*. Por ejemplo, la siguiente instrucción nos mostrará la lista de todos los procesos en ejecución ordenados por PID:

ps -e

Podemos filtrar los resultados utilizando una tubería (representada mediante el símbolo |); en este caso, entubamos la salida de la instrucción *ps* a la entrada de *grep* (que busca patrones de caracteres en los archivos), indicando el nombre del proceso a filtrar. Por ejemplo:

#### ps -e | grep firefox

Esta orden nos mostrará únicamente las entradas del listado de procesos en ejecución que contengan la cadena de caracteres *firefox.*

Conocer el PID de un determinado proceso es necesario para poder utilizar determinadas instrucciones, como por ejemplo *pstree*, que nos muestra el árbol de subprocesos lanzados por un proceso dado.

#### **top**

Otra instrucción muy útil para la gestión de procesos es *top*, que, de forma muy similar al Administrador de tareas de Windows —aunque en modo texto—, nos muestra el estado de los procesos en tiempo real (prioridad y consumo de memoria y CPU) y nos indica el PID y el usuario que inició el proceso.

#### **nice**

Es posible abrir los procesos para que, según su nivel de prioridad, se ejecuten más rápida o más lentamente dependiendo de la carga actual del sistema. Para ello contamos con la instrucción *nice*, tras la cual especificaremos un número negativo o positivo (a menor valor, mayor prioridad) seguido del nombre del proceso en cuestión. La prioridad por defecto de un proceso cuando se crea es 0 (no definida). Por ejemplo, si queremos abrir una ventana de terminal de Gnome que se ejecute con menor prioridad (10), ejecutaremos:

nice -10 gnome-terminal

Si, por el contrario, queremos asignarle una prioridad más alta de lo normal (-10), tendremos que hacerlo con permisos de administrador:

sudo nice --10 gnome-terminal

#### **kill**

Para enviar una señal a los procesos se utiliza la instrucción *kill*. Existen gran cantidad de señales para esta instrucción, que podemos listar con *kill -l*, y a cada una corresponde un número que se puede utilizar en lugar del nombre de la señal. Entre las señales más interesantes están las siguientes:

- **TERM (15)**: finaliza limpiamente la ejecución de un proceso. Si no especificamos ninguna señal, se enviará esta por defecto.
- **HUP (1)**: recarga un proceso.
- **INT (2)**: interrumpe un proceso (equivale a pulsar Ctrl+C en una ventana de terminal).
- **KILL (9)**: fuerza la detención de un proceso.
- **STOP (19)**: pausa la ejecución de un proceso.
- **CONT (18)**: reanuda la ejecución de un proceso.

Por ejemplo, para finalizar de forma forzada el proceso de Firefox desde una ventana de terminal, primero averiguaríamos el PID del proceso (*ps -e | grep firefox*) y, suponiendo que este fuera 2979, lo detendríamos con la siguiente instrucción:

### kill -9 2979

Si queremos detener todas las instancias de un mismo proceso, podemos usar la instrucción *killall* seguido del nombre exacto del proceso:

#### **Carga de demonios con System V**

Los servicios de Linux se conocen también como *demonios* (*daemons*  en inglés), motivo por el cual muchas veces su nombre finaliza con la letra *d*.

Antiguamente se utilizaba el sistema denominado System V (o SysV), según el cual los servicios se cargaban durante el arranque ejecutando una serie de *scripts* siguiendo el orden de los niveles de ejecución (o *runlevels*), que proporcionan diferentes grados de funcionalidad dependiendo de la distribución utilizada. En la siguiente tabla se muestran los diferentes niveles de ejecución y su funcionalidad en Fedora, Slackware, Debian y distribuciones genéricas de Linux:

Según este sistema, en cada etapa se ejecutan los *scripts* contenidos en un directorio determinado ubicado en */etc: /etc/rc1.d* para los *scripts* con nivel de ejecución 1, */etc/rc2.d* para los de nivel 2, y así para cada nivel sucesivo. En sistemas basados en BSD, la mecánica es la misma, con la diferencia de que todos los *scripts* se ubican en la carpeta */etc/rc.d* bajo la denominación *rc.xx,* donde *xx* varía en función del nivel de ejecución.

El nivel por defecto y los *scripts* que lo definen se configuran en el archivo */etc/inittab.* La sintaxis de las entradas que lo componen es la siguiente:

| Nivel | Linux genérico   | Fedora           | Slackware        | Debian           |
|-------|------------------|------------------|------------------|------------------|
| 0     | Parada           | Parada           | Parada           | Parada           |
| 1     | Modo monousuario | Modo monousuario | Modo monousuario | Modo monousuario |
| 4     | Sin uso          | Sin uso          |                  |                  |
| 6     | Reinicio         | Reinicio         | Reinicio         | Reinicio         |

#### Donde:

- **Id**: identificador único de la entrada.
- **Niveles**: uno o varios niveles de ejecución para los que la entrada es válida.
- **Acción**: acción a tomar para el proceso. Puede ser una de las siguientes:
  - *sysinit*: el proceso se inicia durante el arranque del sistema.
  - *wait*: el proceso se inicia y se espera hasta que finaliza antes de continuar con otros servicios.
  - *respawn*: el proceso se inicia y, si finaliza, se reinicia automáticamente.
  - *once*: el proceso se inicia una sola vez; cuando finaliza no se reinicia.
  - *boot*: el proceso se inicia durante el arranque del sistema, pero no durante un cambio de nivel de ejecución.
  - *off*: la entrada se ignora.
- **Proceso**: la línea de órdenes a ejecutar al iniciar el proceso (puede incluir argumentos y opciones).

Por ejemplo:

### 1:2345:respawn:/sbin/getty 38400 tty1

Esta entrada especifica el inicio del proceso *getty* —responsable de requerir a los usuarios sus credenciales de inicio de sesión— en *tty1* y para los niveles de ejecución 2, 3, 4 y 5. Además, fuerza que, si por cualquier motivo este proceso finaliza, se reinicie automáticamente.

![](_page_50_Picture_7.jpeg)

En Linux, un **TTY** (abreviatura del inglés *teletype,* teletipo) es un dispositivo terminal, ya sea físico, como una consola conectada a través de un puerto serie, o virtual, denominado emulador de terminal, como *gnome-terminal*. Cada TTY se identifica mediante un número único; por ejemplo, el primer terminal virtual suele ser *tty1*, el segundo, *tty2*, y así sucesivamente. Para alternar entre terminales, utilizamos las combinaciones de teclas de *Ctrl+Alt+F1* a *Ctrl+Alt+F6.* Podemos utilizar los terminales para realizar tareas administrativas como ejecutar órdenes y gestionar los recursos del sistema.

Para cambiar el modo de ejecución, utilizamos la instrucción *init*. Por ejemplo, con *init 1* entraremos en el modo monousuario, y con *init 6* reiniciaremos el sistema. Cuando esto sucede, se finalizan todos los procesos que no estuvieran especificados en el nuevo nivel de ejecución. Finalmente, podemos cambiar el nivel de arranque por defecto editando la línea con *initdefault* en */etc/inittab*. Por ejemplo, con *id:3:initdefault,* el nivel por defecto será el 3 (de texto), en lugar del nivel gráfico.

#### **Carga de demonios con Upstart**

Upstart es un sistema más moderno que reemplaza al tradicional de System V como mecanismo de carga de servicios. Upstart permite definir trabajos personalizados para realizar una tarea determinada, como lo es el inicio de un demonio. Los archivos de configuración de dichos trabajos se almacenan, con la extensión *.conf,* en el directorio */etc/init,*  y definen todas las propiedades de cada uno de ellos, incluyendo su nombre, descripción y las instrucciones necesarias para iniciar el demonio en cuestión.

Por ejemplo, para iniciar el servidor HTTP Apache, podríamos usar la siguiente configuración de trabajo para Upstart, almacenada como *apache2.conf:*

description "Servidor HTTP Apache" author "Juan Rubio" start on runlevel [2345] stop on runlevel [016] exec /usr/sbin/apache2 -k start

Aquí, el servicio se inicia cuando el sistema entra en los niveles de ejecución 2, 3, 4 o 5, y se detiene cuando entra en los niveles 0, 1 o 6. La línea *exec* especifica la orden necesaria para iniciar el demonio, en este caso, */usr/sbin/apache2 -k start.*

Los archivos de configuración de trabajos se cargan en Upstart mediante la orden *initctl*; en nuestro ejemplo:

sudo initctl start apache2

Por otra lado, para cambiar el nivel de arranque en Upstart, empleamos la variable de entorno *DEFAULT\_RUNLEVEL*. Para modificar su valor, editaremos el archivo */etc/init/rc-sysinit.conf*; por ejemplo:

#### **Carga y gestión de demonios con systemd**

La mayor parte de las distribuciones de Linux utilizan hoy **systemd** como método de carga y administración de servicios. Se trata de un sistema compuesto por herramientas, demonios y bibliotecas que aprovecha las arquitecturas multiprocesador y multinúcleo para optimizar la carga del sistema.

Una de las principales diferencias de Systemd con respecto a SysV y Upstart es que no emplea niveles de ejecución, sino un sistema más flexible y dinámico basado en conjuntos de servicios denominados *destinos*. Estos destinos son los que deben iniciarse o detenerse con el fin de alcanzar un estado determinado del sistema, como arrancarlo, entrar en su interfaz gráfica o apagarlo. Los enlaces simbólicos a los destinos se agrupan en el directorio */etc/systemd/system/*, y apuntan a los archivos de unidad que contienen la descripción y los servicios a iniciar de cada destino.

En Debian 11, el destino por omisión que especifica el estado del sistema al completarse el proceso de arranque está en */etc/systemd/system/ default.target*, aunque se trata de un enlace simbólico al destino real, que encontraremos en */lib/systemd/system/*. Para saber cuál es este destino, podemos usar la orden *systemctl*:

systemctl get-default

Para cambiar el destino por defecto, podemos usar la siguiente instrucción:

sudo systemctl set-default multi-user.target

Con esta orden, después de reiniciar la máquina, el sistema arrancaría en un destino equivalente al nivel de ejecución 3 (consola de texto multiusuario).

Para regresar al modo gráfico por defecto, utilizaremos la orden siguiente:

sudo systemctl set-default graphical.target

Por otra parte, una de las claves de *Systemd* radica en el concepto de *unidad*. Las unidades son archivos que se ubican en */etc/systemd/ system* y */usr/lib/systemd/system,* y cuya naturaleza puede ser muy diversa: servicios (*.service*), puntos de montaje (.*mount*), dispositivos (.*device*), un destino (.*target*), etc.

Para ver todas las unidades disponibles usaremos la instrucción:

Para conocer las que el sistema ha intentado cargar, usaremos simplemente la instrucción *systemctl.* No obstante, puede resultar más práctico obtener únicamente el listado de un determinado tipo de unidad mediante el uso del parámetro *type.* De este modo, para obtener un listado de todos los servicios que se han intentado cargar, podemos utilizar la siguiente orden:

#### systemctl --all --type=service

En el listado se marcarán con un punto de color los servicios con problemas (en amarillo los no encontrados, en rojo los que hayan dado algún error), y se nos indicará en qué estado de actividad están, ofreciéndonos, además, una descripción de cada uno de ellos.

Para obtener un listado de exclusivamente aquellas unidades que hubieran dado error, podemos usar la instrucción:

#### systemctl --failed

Para habilitar una unidad, usaremos systemctl enable, seguido del nombre de dicha unidad. Si, por el contrario, queremos deshabilitar un servicio, utilizaremos *disable*; por ejemplo:

### systemctl disable bluetooth

Para iniciar un servicio de forma manual usaremos *start*, o *stop* si queremos detenerlo, y *restart* para reiniciarlo:

*Listado de los servicios con systemctl.*

Si queremos conocer el estado de un servicio, utilizaremos *status*:

![](_page_54_Picture_2.jpeg)

systemctl status cron

Finalmente, podremos saber si un servicio en particular está habilitado (*enabled*) o no (*disabled*) para iniciarse durante el arranque:

### systemctl is-enabled cron

Una buena opción para gestionar de una forma más visual las unidades de Systemd desde una ventana de terminal es *chkservice*. Esta herramienta puede instalarse actualmente, en Debian 11, desde el repositorio Unstable (*deb* <http://ftp.us.debian.org/debian> *sid main*), y permite habilitar o deshabilitar unidades pulsando la tecla *espacio*, e iniciarlas y detenerlas usando la tecla *s*.

La herramienta también muestra las unidades estáticas (*s*) y enmascaradas (*-m-*). Las estáticas dependen de otras unidades para iniciarse (es decir, se habilitan como dependencias), y las enmascaradas impiden su utilización incluso si es para satisfacer una dependencia.
