# **7.3.1. Configuración de Samba**

Samba es uno de los mecanismos para compartir archivos más utilizados en entornos de red heterogéneos en los que predominan los equipos basados en Windows, ya que el protocolo CIFS es una implementación del SMB nativa de los sistemas de Microsoft.

En este tutorial, veremos cómo configurar una carpeta compartida con Samba en Windows Server, y cómo acceder a ella desde clientes Windows y Linux.

- 1. Abrimos el Administrador del servidor y vamos a *Servicios de archivos y de almacenamiento* > *Recursos compartidos* donde, en el menú desplegable *TAREAS*, seleccionamos *Nuevo recurso compartido*.

![](_page_205_Picture_6.jpeg)

- 2. En el apartado *Seleccionar perfil* del *Asistente para nuevo recurso compartido*, seleccionamos *Recurso compartido SMB - Rápido.*

- 3. Escribimos la ruta a la carpeta que queremos compartir o la buscamos con el botón *Examinar.*

- 4. Escribimos el nombre del recurso compartido, que quedará reflejado en la ruta de acceso remoto a la carpeta (en nuestro ejemplo, *\\Servidor02\ArchivosSMB*).

- 5. Si la carpeta no es pública, habilitaremos la enumeración basada en el acceso, que sirve para ocultar los archivos y carpetas para los cuales los usuarios no tengan permisos de acceso. En caso contrario, dejaremos esta opción desactivada para que todos los usuarios puedan acceder a todo el contenido.

- 6. En el apartado *Permisos,* vemos que *Todos* tienen el control total del recurso compartido. Si lo deseamos, podemos cambiar esto pulsando el botón *Personalizar permisos* y editando las entradas de permiso en la pestaña *Compartir* de la *Configuración de seguridad avanzada* para la carpeta compartida.

- 7. Revisamos los parámetros de configuración escogidos y confirmamos la creación del recurso pulsando el botón *Crear*.

- 8. La carpeta compartida aparecerá en los recursos de Red relativos al servidor en el Explorador de archivos de cualquier cliente conectado al dominio. También podemos acceder directamente mediante su nombre de recurso de red (*\\Servidor02\ArchivosSMB*).

- 9. En clientes Linux, debemos asegurarnos de haber instalado el paquete *cifs-utils*:

sudo apt install cifs-utils

- 10. Creamos una carpeta para montar el recurso, y editamos el archivo */etc/fstab*, añadiendo una entrada con formato similar a esta:

//10.0.1.125/ArchivosSMB /home/usuario/samba cifs username=usuario,password=contraseña,user 0 0

La primera parte de la entrada (*//10.0.1.125/ArchivosSMB*), es la dirección del recurso compartido; la siguiente (*/home/usuario/samba*), la ruta a la carpeta de montaje que hemos creado. Es necesario especificar, además, un nombre de usuario y contraseña válidos para acceder a la carpeta compartida con Samba, ya que, por defecto, en SMB2 y SMB3 los accesos con cuentas de invitado están desactivados por seguridad.

Esto montará la carpeta compartida en el inicio de sesión. Si preferimos montarla solo cuando la necesitemos, podemos añadir la opción *noauto* y hacerlo de forma manual desde el intérprete de órdenes con *mount /home/usuario/samba*:

//10.0.1.125/ArchivosSMB /home/usuario/samba cifs username=usuario,password=contraseña,noauto,user 0 0
