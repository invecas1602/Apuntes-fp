# **4.2.2. Servidores Telnet y SSH**

Normalmente, los servidores Telnet y SSH se utilizan, en entornos Windows, para acceder remotamente a un servidor desde cualquier ordenador conectado a la red.

#### **Instalar el servidor OpenSSH**

En Windows Server 2022, el servidor SSH viene habilitado por defecto, por lo que no es necesario realizar ninguna configuración en el equipo para poder conectarse desde un cliente remoto. Sin embargo, en máquinas con versiones de Windows para ordenadores de escritorio, sí será necesario instalar el servidor OpenSSH manualmente. En Windows 11, esto se realiza desde *Configuración > Aplicaciones > Características opcionales*, botón *Ver características.*

En Linux tendremos también que instalar y configurar el servidor OpenSSH. En el caso de Debian 11, usaremos las siguientes instrucciones para habilitarlo:

sudo apt install openssh-server sudo systemctl start ssh

Si queremos que se ejecute como servicio desde el arranque del sistema, deberemos activarlo con la siguiente orden:

sudo systemctl enable ssh

A partir de este punto, es posible acceder al equipo mediante SSH usando las credenciales de cualquier usuario del sistema.

Si queremos reforzar la seguridad, podemos generar, en la máquina cliente, un par de claves RSA pública y privada (pulsaremos la tecla *Entrar* para aceptar todas las opciones por defecto):

Por defecto, el servicio OpenSSH se instala, en Windows, configurado para iniciarse de forma manual, lo cual podemos hacer desde el complemento *Servicios*  (*services.msc*). Por tanto, si queremos que se ejecute automáticamente durante el inicio de sesión, deberemos configurar el servicio *OpenSSH SSH Server* para iniciarse automáticamente.
