# **4.4. Herramientas gráficas externas para la administración remota**

Para acceder remotamente a cualquier ordenador desde un entorno gráfico, podemos utilizar un software de terceros compatible con el protocolo VNC. Por ejemplo, podríamos configurar un servidor Linux para poder acceder a él desde un ordenador con Windows 11. En Linux podemos escoger entre varios servidores, como Vinagre, Krdc, RealVNC, TightVNC o TigerVNC que es el que nosotros, en esta ocasión, vamos a utilizar. El procedimiento es el siguiente:

- 1. En primer lugar, instalamos los paquetes necesarios: el entorno de escritorio ligero Xfce y TigerVNC. En esta ocasión lo haremos en Ubuntu 22.04, pero el procedimiento debería ser muy similar en cualquier distribución basada en Debian.

sudo apt updatesudo apt

install xfce4 xfce4-goodies

sudo apt install tigervnc-standalone-server

Durante el proceso se nos solicitará el gestor de sesiones predeterminado: pulsaremos *Entrar* para aceptar la opción por defecto.

- 2. Establecemos una contraseña de acceso de entre 6 y 8 caracteres —opcionalmente podremos crear una contraseña que solo permitirá ver el escritorio, pero no interactuar con él— y creamos los archivos de configuración iniciales con la siguiente instrucción:

#### vncserver

Si más adelante necesitamos cambiar la contraseña, podremos hacerlo mediante la orden *vncpasswd.*

- 3. Para crear o modificar el archivo de configuración, primero detenemos el servidor VNC (especificamos para ello el puerto de pantalla, en nuestro caso, :1), y luego abrimos para edición el archivo *~/.vnc/xstartup*:

vncserver -kill :1

nano ~/.vnc/xstartup

Tengamos en cuenta que, a la hora de conectarnos desde un equipo remoto, deberemos utilizar el puerto de red 5901, que es el que corresponde al puerto de pantalla :1. Si creásemos más instancias del servidor VNC (:2, :3, etc.), tendríamos que cambiar, en consecuencia, el número de puerto de red: 5902, 5903, etc.

A continuación, añadiremos las siguientes líneas al archivo de configuración (si existen otras líneas, las comentaremos con #):

#!/bin/shunset SESSION\_MANAGER unset DBUS\_SESSION\_BUS\_ADDRESS /usr/bin/startxfce4 [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup [ -r \$HOME/.Xresources ] && xrdb \$HOME/.Xresources x-window-manager &

El contenido de este archivo puede cambiar en función de la distribución y el servidor VNC escogidos, por lo que se recomienda revisar la documentación disponible a este respecto.

- 4. Guardamos el archivo y nos aseguramos de que es ejecutable:

chmod +x ~/.vnc/xstartup

- 5. Ahora podemos reiniciar el TigerVNC para poner a prueba nuestra configuración desde el propio servidor:

vncserver -localhost no :1

Podemos utilizar cualquier cliente para conectar con el servidor VNC indicando la dirección IP del servidor y el puerto de red correspondiente, por ejemplo *10.0.1.57:5901.*

Recibiremos un aviso de que la conexión no es segura, y se abrirá el escritorio Xfce. Una vez hayamos constatado el correcto funcionamiento de TigerVNC, lo cerramos y lo abrimos de nuevo, esta vez sin parámetros adicionales, por lo que, en adelante, se requerirá de autenticación remota para acceder desde otra máquina de la red:

vncserver -kill :1 vncserver

- 6. VNC utiliza SSH como protocolo de autenticación remota, por lo que, antes de intentar la conexión desde Windows 11, tendremos que haber instalado el servidor SSH en el servidor Linux tal como se explica en el apartado *4.2.2.* Además, será necesario crear un túnel SSH, en una ventana de Símbolo del sistema (*cmd*) abierta en el equipo cliente con Windows, mediante la siguiente instrucción (suponiendo que la IP del servidor sea *10.0.1.57*):

ssh -L 59000:localhost:5901 -C -N -l starbuck 10.0.1.57

Probamos de nuevo a acceder remotamente, esta vez cambiando la dirección en nuestro software cliente VNC, por *localhost:59000.*
