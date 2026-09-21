# **1.3.1. Directorio Activo**

Para realizar una instalación básica del Directorio Activo en Windows Server 2022 (versión 21H2), seguiremos los pasos que se indican a continuación:

- 1. En el Panel del *Administrador del servidor,* hacemos clic sobre la *opción Agregar roles y características* del menú *Administrar.*
- 2. En la ventana del *Asistente para agregar roles y características,*  optamos por la opción por defecto, *Instalación basada en características o en roles* y, tras seleccionar un servidor de la lista *Grupo*

![](_page_19_Picture_7.jpeg)

*de servidores*, activamos la casilla *Servicios de dominio de Active Directory* en el apartado *Roles de servidor.* Este rol tiene una serie de dependencias que el asistente seleccionará automáticamente para su instalación, lo cual confirmaremos pulsando el botón *Agregar características.* A partir de este punto, iremos haciendo

![](_page_20_Picture_2.jpeg)

clic en *Siguiente* hasta llegar al final del asistente, confirmando la operación mediante el botón *Instalar.*

- 3. Cuando el proceso de instalación concluya, cerraremos el asistente y abriremos el menú de notificaciones del panel, donde haremos clic en el enlace *Promover este servidor a controlador de dominio,* lo cual iniciará el *Asistente para configuración de Servicios de dominio de Active Directory.*
- 4. En la primera sección del asistente, *Configuración de implementación,* deberemos indicar si estamos agregando un DC a un dominio que ya existe, si estamos agregando un nuevo dominio a un bosque existente, o si estamos creando un nuevo bosque. En los dos primeros casos, es necesario que la configuración DNS sea correcta para que el asistente pueda localizar y conectarse al dominio o al bosque existente; además, tendremos que usar las credenciales de administrador de dicho dominio (*dominio\Administrador*). Si, por el contrario, optamos por crear un bosque, el nuevo dominio será también el dominio raíz de un nuevo árbol dentro del nuevo bosque. En el supuesto de tener registrado un dominio en Internet, lo pondremos como nombre del dominio raíz (por ejemplo, *midominio.es*). Si se trata de un dominio en una intranet, utilizaremos siempre la terminación *.local,* por ejemplo, *midominio.local.*

- 5. En la siguiente sección, *Opciones del controlador de dominio,*  podemos escoger el nivel de compatibilidad del bosque con otras ediciones de Windows Server, las capacidades del controlador de dominio de nuestro servidor y la contraseña que, obligatoriamente, debemos establecer para el modo de restauración de servicios de directorio o DSRM. El Directorio Activo requiere de un DNS, por lo que, si no tenemos uno en la red, deberemos dejar activada esta

casilla. En este caso, tampoco será necesario crear una delegación DNS en el apartado *Opciones DNS.*

- 6. En el caso de que estemos añadiendo un nuevo DC a un dominio, en *Opciones adicionales* podremos escoger desde qué DC se realizará la replicación. Si estuviéramos creando un nuevo bosque, aquí podremos cambiar el nombre NetBIOS de la máquina. En cualquiera de los casos, en Rutas de acceso podremos personalizar

![](_page_22_Picture_1.jpeg)

los directorios donde se almacenan la base de datos y los archivos de registro (por defecto, *C:\WINDOWS\NTDS*) y la carpeta *SYSVOL* 

![](_page_22_Picture_3.jpeg)

#### (*C:\WINDOWS\SYSVOL*).

- 7. Tras revisar la configuración realizada, se efectuará una comprobación de los requisitos previos para la promoción del servidor a controlador de dominio y se nos informará de cualquier circunstancia que pueda afectar al funcionamiento del controlador. Si la operación de comprobación da un resultado positivo, el asistente nos invitará a completar la instalación pulsando el botón *Instalar,* con lo cual se realizarán los cambios necesarios y se reiniciará el equipo.
- 8. Tras el reinicio, veremos que se nos han añadido los dos nuevos roles, AD DS y DNS.
