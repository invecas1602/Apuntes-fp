# **4.5.2. Apt-cacher**

![](_page_128_Picture_2.jpeg)

En redes con muchos clientes, Apt-cacher puede recortar significativamente el tiempo y la ocupación de ancho de banda dedicados a las actualizaciones de software. Además, gracias a algunas funciones adicionales, como la replicación de repositorios y el filtrado de paquetes, es una herramienta útil para gestionar las actualizaciones en una red basada en Debian.

A continuación se detallan los pasos necesarios para implementar Apt-cacher en una red con máquinas basadas en múltiples distribuciones, como Debian y Ubuntu, para lo cual usaremos un servidor con Ubuntu 22.04:

- 1. Instalamos Apt-cacher y el servidor web Apache:

sudo apt install apt-cacher apache2

Durante la instalación se nos solicitará el modo del servicio Apt-cacher; seleccionaremos *demonio* para cargarlo como servicio del sistema.

- 2. Abrimos con *nano* el archivo */etc/default/apt-cacher* y añadimos el siguiente parámetro:

autostart 1

- 3. Reiniciamos Apache:

sudo service apache2 restart

- 4. Probamos si funciona Apt-cacher cargando en el navegador la siguiente página:

**Apt-cacher** es un servidor para APT (*Advanced Package Tool,* o herramienta avanzada de paquetes), el gestor de paquetes que utilizan las distribuciones Linux basadas en Debian. Como tal, su misión es almacenar en caché los paquetes de actualización relativos a dicha distribución para que todos los clientes de una red local puedan descargarlos sin tener que salir a Internet.

- 5. El archivo de configuración de Apt-cacher es */etc/apt-cacher/ apt-cacher.conf,* donde podremos adaptar los parámetros del servicio a nuestro entorno de trabajo. No obstante, una posible configuración básica sería la siguiente:
- Abrimos el archivo con *nano* y añadimos las siguientes tres líneas:

allowed\_hosts = \* distinct\_namespaces = 1 installer\_files\_regexp = ^(?:vmlinuz|linux| initrd\.gz|changelog|NEWS.Debian|[a-z]+ \.tar\.gz(?:\.gpg)?|UBUNTU\_RELEASE\_NAMES \.tar\.gz(?:\.gpg)?|(?:Devel|EOL) ?ReleaseAnnouncement(?:\.html)?|meta-release (?:-lts)?(?:-(?:development|proposed))?)\$

- Cambiamos la dirección de correo administrativo (*admin\_email*).
- 6. Reiniciamos Apt-cacher:

sudo service apt-cacher restart

- 7. Importamos los paquetes existentes (de haberlos) con la siguiente instrucción:

sudo /usr/share/apt-cacher/apt-cacher-import.pl -l /var/cache/apt/archives

- 8. Alternativamente, podemos utilizar una imagen ISO de nuestra distribución para importar todos sus paquetes, lo que acelerará el proceso al no tener que descargarlos de Internet (adaptaremos las rutas de la imagen y del punto de montaje a nuestra configuración de equipo):

sudo mount -o loop /home/usuario/imagen.iso /media/cdrom0 sudo /usr/share/apt-cacher/apt-cacher-import.pl -R -r /media/cdrom0

- 9. Finalmente, configuramos Apt para que utilice el caché; primero, creamos con *nano* un fragmento de configuración, y a continuación añadimos el parámetro *Acquire* que apunta a nuestro proxy (asumimos aquí que *ilerna-PC* es el nombre del servidor, el cual podemos reemplazar por su dirección IP):

sudo nano /etc/apt/apt.conf.d/01proxy Acquire::http::Proxy "http://ilerna-PC:3142";

Utilizaremos este mismo método en todos los clientes de nuestra red.

- 10. Probamos actualizar la lista de paquetes con *sudo apt update.* Si no obtenemos ningún error significa que Apt-cacher está funcionando correctamente y podemos actualizar el sistema con s*udo apt upgrade* o *sudo apt dist-upgrade.*

Conclusiones La elección y uso correcto de las herramientas y técnicas para la gestión del acceso remoto es fundamental en los entornos empresariales actuales, donde es frecuente el teletrabajo y se requiere que los administradores manejen un cada vez mayor parque móvil de dispositivos conectados en red. De la administración eficaz de estos servicios depende, en gran medida, la seguridad de los datos y los sistemas de la organización, y por ello debemos dedicar especial atención a implementar mecanismos de autenticación reforzados y unas directivas de seguridad y control de acceso adecuadas.

![](_page_130_Picture_5.jpeg)

**ADMINISTRACIÓN DE SERVIDORES DE APLICACIONES**

Las tecnologías actuales proporcionan a los servidores la potencia de proceso necesaria para ejecutar múltiples instancias de una misma aplicación, y el progresivo aumento en el ancho de banda de red permite a los equipos acceder remotamente a estas aplicaciones prácticamente en tiempo real. El papel de estos servidores de aplicaciones va incluso más allá: no solo fortalecen la seguridad de la red, ya que las aplicaciones se instalan, actualizan y aseguran de forma centralizada, sino que también contribuyen a recortar gastos, pues los costes del despliegue suelen ser inferiores a instalar las aplicaciones en cada equipo.

En esta unidad identificaremos diferentes tipos de servidores de aplicaciones, así como las técnicas y productos relacionados, aunque centrándonos en los Servicios de Escritorio remoto como plataforma para publicar aplicaciones dentro de un dominio del Directorio Activo.
