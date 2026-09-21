# **4.3. Escritorio remoto**

![](_page_114_Picture_2.jpeg)

En Windows Server, el Escritorio remoto está implementado bajo el nombre de Terminal Server o Servicios de Escritorio remoto (*Remote Desktop Services*, RDS), dependiendo de la versión del sistema. Su principal diferencia con respecto a la versión para ordenadores de escritorio es que Servicios de Escritorio remoto hace posible el acceso de múltiples usuarios a una misma máquina, mientras que el Escritorio remoto está diseñado para permitir a un solo usuario acceder a un único equipo dentro de la red.

Dado que, en un entorno profesional de administración de sistemas, lo más habitual es trabajar con múltiples usuarios en una arquitectura cliente-servidor, nos centraremos en la configuración básica de Servicios de Escritorio remoto para acceder a un servidor basado en Windows Server 2022 desde múltiples equipos con Windows 11.

En primer lugar, para configurar Servicios de Escritorio remoto en el servidor, realizaremos los pasos siguientes:

- 1. Agregamos el rol de Servicios de Escritorio remoto (RDS) en el servidor utilizando el Administrador del servidor: *Administrar* > *Agregar roles y características.* Como tipo de instalación seleccionaremos *Instalación de Servicios de Escritorio remoto.* Como tipo de implementación, seleccionaremos *Inicio rápido,* y como escenario de implementación, podemos optar entre sesiones de usuario (modelo clásico) o escritorios virtuales, siempre que el servidor cuente con las características necesarias para la gestión de máquinas virtuales.

El **Escritorio remoto** (*Remote Desktop*) es una función integrada en Windows que permite a sus usuarios conectarse a través de una red con otra instalación de Windows y controlarla remotamente. Esta característica utiliza el protocolo RDP para iniciar la sesión y transferir datos de forma segura, y facilita el trabajo a distancia con las aplicaciones y los recursos del equipo remoto.

> Para poder instalar los Servicios de Escritorio remoto, es necesario que el servidor esté unido a un dominio del Directorio Activo. Consulta el apartado *6.3.1. Directorio Activo* para revisar las instrucciones, paso a paso, del proceso de instalación de los *Servicios de dominio de Active Directory.*

#### Atención

- 2. La herramienta de configuración de Servicios de Escritorio remoto, que encontraremos en el panel izquierdo del Administrador del servidor, nos permitirá editar las características y propiedades de nuestro despliegue. Lo primero que debemos hacer es agregar nuestro servidor a la función *Administración de licencias de Escritorio remoto.*

![](_page_115_Diagram_2.jpeg)

- 3. Ahora ya podemos hacer clic derecho en *Administración de licencias de Escritorio remoto* y escoger la opción *Seleccionar el modo de la Administración de licencias de Escritorio remoto.* Esto nos permitirá configurar la implementación: puerta de enlace (de ser necesario), modo de administración (por dispositivo o por usuario) y certificados.

- 4. A continuación, podremos ya instalar licencias de Escritorio remoto. Para ello, seleccionamos el menú Herramientas del Administrador del servidor, opción *Remote Desktop Services* > *Administrador de licencias de Escritorio remoto.* Aquí, desplegamos la lista *Todos los servidores,* hacemos clic derecho sobre nuestro servidor, y seleccionamos la opción *Activar servidor.*

Esto iniciará el asistente para activar servidor, donde dejaremos el modo de conexión por defecto (automática), indicaremos la información corporativa que se nos vaya solicitando, e iniciaremos el asistente para instalar licencias.

![](_page_116_Picture_2.jpeg)

- 5. El asistente para activar servidor necesita que se le indique el programa de licencias que se va a utilizar, ya que los clientes que se conecten al servidor deberán contar con una licencia de acceso cliente (*Client Access License* o CAL). Estas licencias se adquieren por usuario o por máquina, según el modo de administración escogido anteriormente. Si todavía no disponemos de CAL, simplemente cancelaremos el asistente, ya que podremos agregarlas en el futuro. Contamos con un periodo de gracia de 120 días para adquirir estas licencias, tras el cual los Servicios de Escritorio remoto dejarían de funcionar.

![](_page_116_Picture_5.jpeg)

- 6. A continuación, en el *Administrador de licencias de Escritorio remoto*, hacemos clic derecho sobre nuestro servidor y seleccionamos *Revisar configuración.* Veremos que nos queda por agregar el servidor al grupo *Servidores de licencias de Terminal Server.* Para ello, pulsaremos el botón *Agregar a grupo* y el servicio *Administración de licencias de Escritorio remoto* desde la herramienta Servicios del sistema (*services.msc*).

- 7. En este punto ya podemos especificar qué equipos o usuarios pueden conectarse al servidor. En el Administrador del servidor, dentro de Servicios de Escritorio remoto, abrimos *QuickSessionCollection*  y, en el desplegable *TAREAS,* escogemos *Editar propiedades.* Esto nos permitirá definir la configuración de una *Colección de sesiones*  donde se especifican, entre otros detalles —nivel de seguridad, equilibrio de carga, opciones de cliente y carpetas de usuario—, los referentes a los grupos de usuarios que podrán conectarse mediante Escritorio remoto. Por defecto se agregan todos los usuarios del dominio, pero normalmente se crea un grupo específicamente para RDS. El tipo de dicho grupo deberá ser *Seguridad.*

- 8. Para acceder al servidor desde Windows 11, simplemente iniciamos la herramienta de Conexión a Escritorio remoto y facilitamos la IP del servidor y las credenciales de acceso.

![](_page_118_Picture_3.jpeg)

- 9. Si no hemos instalado unos certificados de confianza, aparecerá un mensaje de advertencia, que podremos omitir para establecer la conexión.
