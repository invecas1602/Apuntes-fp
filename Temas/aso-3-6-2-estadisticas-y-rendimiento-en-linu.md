# **3.6.2. Estadísticas y rendimiento en Linux**

Como es propio de Linux, en este sistema disponemos de múltiples opciones para monitorizar el rendimiento del equipo y generar estadísticas para poder tratarlas con diferentes aplicaciones. Como herramienta para el emulador de terminal contamos, por ejemplo, con *nmon* (*sudo apt install nmon*), que puede monitorizar los recursos del sistema y exportar los datos recopilados en formato CVS para poder importarlos a una hoja de cálculo o base de datos. Por ejemplo, para registrar las estadísticas cada 30 segundos, la instrucción sería:

nmon -f -s 30

Esto generará un documento en el directorio desde donde estemos ejecutando el monitor con la extensión *.nmon* que se irá actualizando cada medio minuto, aunque no veremos ninguna información en pantalla. En cambio, si ejecutamos simplemente la orden *nmon*, se iniciará la herramienta en un modo de texto interactivo en el que podremos cambiar los datos mostrados mediante la pulsación de teclas; por ejemplo, para ver el rendimiento de la CPU, los discos y la memoria, pulsaríamos las teclas *c*, *d* y *m*.

![](_page_96_Figure_0.jpeg)

Si lo que buscamos es una alternativa para el entorno gráfico, una opción sencilla pero efectiva es Monit (*sudo apt install monit*). La herramienta se configura con un archivo de control denominado *monitrc* que encontraremos en */etc/monit.* Monit se puede gestionar usando una cómoda interfaz web, pero para ello tendremos que editar *monitrc* y añadir las siguientes líneas:

set httpd port 2812 allow localhost allow admin:monit allow @monit allow @users readonly

Con esto configuramos el puerto 2812 para acceder a la interfaz web mediante la dirección de *loopback* (*127.0.0.1* o *localhost*), asignamos un nombre y contraseña de administración (*admin:monit*), y permitimos a los usuarios del grupo *monit* realizar operaciones de lectura/ escritura, y a los del grupo *users* de solo lectura. Podemos adaptar estos parámetros a nuestras necesidades, e incluso añadir varios servicios para monitorizarlos de manera específica.

Tras esto, iniciaremos el servicio de la herramienta con:

sudo /etc/init.d/monit start

Abrimos un navegador, y vamos a la dirección *http://localhost:2812*, donde se nos solicitará el correspondiente nombre de usuario y contraseña de administración.

*Estadísticas del sistema en nmon.*

![](_page_98_Picture_8.jpeg)

Una vez comprobada la correcta instalación de la instancia de Monit, podemos descargar M/Monit para administrarla. Para ello, iremos a la web *https://mmonit.com* y descargaremos la versión adecuada para nuestro sistema (en el caso de Debian, *linux-x64*). Descomprimiremos el programa y lo iniciaremos ejecutando *mmonit/bin/mmonit*. Por último, iremos a *http://localhost:8080/* en nuestro navegador, y utilizaremos *admin* como nombre de usuario y *swordfish* como contraseña para entrar en la interfaz de M/Monit.

No obstante, para que M/Monit reconozca nuestra instancia de Monit, tendremos que editar una vez más el archivo *monitrc*, y añadir lo siguiente:

set eventqueue basedir /var/monit slots 1000 set mmonit http://admin:swordfish@localhost:8080/collector

Reiniciamos el servicio (*sudo /etc/init.d/monit restart*) y ya podremos administrar la instancia local de Monit desde M/Monit.

M/Monit ofrece muchas posibilidades a la hora de monitorizar sistemas, ya que cuenta con una estructura de informes y alertas, soporte para SSL y envío de notificaciones por correo electrónico o mediante un servidor Jabber.

*Estadísticas del sistema en M/Monit.*
