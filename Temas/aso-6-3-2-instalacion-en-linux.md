# **6.3.2. Instalación en Linux**

CUPS es el sistema de impresión que, por defecto, se instala en la mayor parte de distribuciones Linux. Para comprobar si el servicio está funcionando, utilizaremos la siguiente instrucción:

sudo systemctl status cups

A continuación, procederemos de la siguiente manera:

- 1. Abrimos para edición el archivo de configuración de CUPS:

sudo nano /etc/cups/cupsd.conf

- 2. Realizamos el siguiente cambio en el archivo, de forma que CUPS no solo escuche las peticiones del anfitrión local, sino de cualquier dirección accesible dentro de la red:

Los servidores de impresión basados en Windows Server 2019 y 2022 solo admiten el uso de impresoras con controladores de tipo 3 o tipo 4, aunque se recomienda utilizar, si es posible, únicamente este último tipo. Los controladores de tipo 4 suelen venir incluidos en el propio sistema operativo o se descargan desde Windows Update, mientras que los de tipo 3 los proporciona el fabricante del dispositivo.

Atención

- 3. Agregamos *Allow from all* a la directiva de acceso al servidor, lo cual permitirá que cualquier cliente pueda acceder a la interfaz web de CUPS:

<Location />

 Allow from all Order allow,deny

</Location>

- 4. Guardamos el archivo y reiniciamos el servicio:

sudo systemctl restart cups.service
