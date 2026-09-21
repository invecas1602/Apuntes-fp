# **5.2.1. Licencias: tipos y características**

Como ya vimos en el apartado *4.3. Escritorio remoto*, los Servicios de Escritorio remoto requieren de licencias que cubran el software que se utiliza para proporcionar los diferentes servicios dentro del dominio.

*Programas publicados en la página de acceso web de RD.*

El navegador Microsoft Edge no podrá cargar la página de acceso web a Escritorio remoto si el certificado SSL no existe o no es compatible con Chrome (el error producido es *ERR\_SSL\_KEY\_USAGE\_IN-COMPATIBLE*). Para solventar este problema, en la configuración de Edge, vamos al apartado *Navegador predeterminado* y, en el desplegable, seleccionamos *Permitir*. A continuación, agregamos la dirección de acceso web (por ejemplo*, https:// servidor01.midominio. local/rdweb*) a las páginas que se abrirán en el modo de Internet Explorer.

Para + info

Para un administrador de sistemas, es importante conocer cuáles son las diferentes alternativas y cómo se diferencian entre sí, por lo que vamos a detenernos aquí sobre este punto.

Microsoft proporciona dos modelos generales de licencias: el de *licencias de administrador de servidor* o ML (del inglés *Management License*), que contempla licencias de administración para servidores y para clientes, y el de *licencias de acceso al cliente* o CAL (del inglés *Client Access License*) que, como su nombre indica, incluye únicamente licencias de cliente.

![](_page_138_Picture_3.jpeg)

#### Las licencias de cliente de Microsoft son:

- **CAL de dispositivo**: licencias que cubren los equipos que se conectan al servidor. Cada dispositivo requiere de su propia CAL, que será válida para todos los usuarios del equipo. Este tipo de CAL es adecuada para entornos donde existen dispositivos compartidos por diferentes usuarios, como es el caso de las organizaciones que distribuyen el trabajo por turnos, ya que su administración resultará más sencilla y económica.
- **CAL de usuario**: van ligadas a los propios usuarios, los cuales podrán utilizarlas en cualquier dispositivo de la organización. Este tipo de licencias son ideales para entornos donde existen más equipos que usuario, o cuando los usuarios son itinerantes y necesitan poder acceder a la red corporativa desde una variedad de equipos remotos.
- **ML de dispositivo**: se basa en los llamados entornos de sistema operativo (en inglés OSE, por *Operating System Environment*); en concreto, este tipo de licencia permite a cualquier usuario administrar cualquier OSE desde un dispositivo en particular. Los OSE son otra forma de referirse a las máquinas conectadas a la red, solo que incluyen las máquinas virtuales.

Una **licencia de servidor** autoriza el uso de un sistema operativo de servidor en un equipo de red, lo que conlleva automáticamente los derechos de administración de la propia red y de instalación del software cliente necesario para conectar los equipos a ella. Por su parte, los equipos o los usuarios necesitan contar con una licencia de cliente para poder acceder a los servicios proporcionados por dicha red.

Por ejemplo, si administramos dos servidores Hyper-V con tres y dos máquinas virtuales basadas en Windows, en total estaremos sumando siete OSE. Otra diferencia importante de este tipo de licencias con respecto a las CAL consiste en que las ML se gestionan desde un servidor de administración de licencias central utilizando un producto como System Center, el cual se encarga de gestionar todos los OSE y las ML de la red.

- **ML por usuario**: permiten a un usuario en particular acceder a cualquiera de los OSE administrados desde cualquier dispositivo.
- **ML por OSE**: permiten a cualquier usuario de la red acceder a un OSE en particular desde cualquier dispositivo.

Por su parte, las licencias de servidor de Microsoft se dividen en:

- **Licencias de EC**: para los usuarios que no pertenecen a la organización, Microsoft dispone de un modelo alternativo (y más económico) a la adquisición de CAL de usuario: las licencias de conector externo o EC (del inglés *External Connector*), que permiten el acceso a cualquier número de usuarios externos siempre y cuando se produzca en beneficio del licenciatario y no del usuario externo. Como en el caso de las CAL de dispositivo, cada servidor físico al que acceden usuarios externos necesita una sola licencia de EC (además de la que corresponde al propio servidor), con independencia del número de usuarios que se conecten a él.
- **Licencias de servidor especializado**: algunos productos, como Windows Server Essentials, pueden tener su propia licencia y normalmente no requieren de CAL adicionales. Además, se permite ejecutar la instancia del sistema en un OSE virtual o físico, aunque según el producto pueden existir derechos de uso más específicos.
- **Licencias por núcleo**: cuando el software de servidor se ejecuta en un OSE físico, es necesario otorgar licencias a todos los núcleos físicos de su CPU. Para determinar el número de licencias necesario se suma el total de núcleos físicos de cada procesador y se multiplica por el factor de núcleo adecuado. Por ejemplo, en una máquina con dos procesadores de dos núcleos necesitaremos ocho licencias (cuatro núcleos en total multiplicados por dos núcleos por procesador). En este modelo tampoco se requieren las CAL.
- **ML de servidor**: se emplean cuando el OSE administrado es un servidor, y pueden ser de dos tipos:
  - System Center Datacenter: para entornos altamente virtualizados.

### **5.2.2. Administración básica de sesiones, usuarios y procesos**

Para administrar las sesiones de Escritorio remoto y los procesos que se ejecutan en el contexto de cada una de ellas, disponemos de una amplia variedad de instrucciones que podemos ejecutar en una ventana de PowerShell.

En primer lugar, si queremos conocer qué sesiones están abiertas, podemos usar la siguiente instrucción, indicando el nombre de anfitrión del servidor Agente de conexión; por ejemplo:

Get-RDUserSession -ConnectionBroker "Servidor01.midominio. local"

Obtendremos de esta forma los nombres de los usuarios que han abierto la sesión remota y su identificador unificado de sesión. Una vez hemos obtenido este identificador, podemos referirnos a él para administrar cada una de las sesiones abiertas.

Por ejemplo, para saber qué procesos están abiertos en una determinada sesión (por ejemplo, la número 2), podemos utilizar la siguiente instrucción:

#### Para + info

Visita la siguiente página web para conocer más acerca de las diferentes modalidades de licencias de Microsoft:

https://bit.ly/3NqJZCP

![](_page_140_Picture_8.jpeg)

#### query process /ID:2

De la misma forma, podemos utilizar el identificador de sesión para enviar un mensaje al usuario conectado, empleando para ello el *cmdlet Send-RDUserMessage*; por ejemplo:

Send-RDUserMessage -HostServer "Servidor01.midominio.local" -UnifiedSessionID 2 -MessageTitle "Mensaje del administrador" -MessageBody "Por favor, guarde su trabajo. El servidor se va a detener dentro de 15 minutos por labores de mantenimiento."

![](_page_141_Picture_4.jpeg)

Si queremos detener un proceso en particular, podemos utilizar la orden *taskkill*, indicando simplemente el identificador de proceso (PID) que obtuvimos con la instrucción *query* (utiliza la opción /F para forzar el cierre el proceso):

![](_page_142_Picture_1.jpeg)

### taskkill /F /PID 2140

Una forma más accesible de administrar algunos aspectos de la sesión remota como la finalización de tareas, el envío de mensajes y el cierre de la sesión, es utilizar la pestaña *Usuarios* del Administrador de tareas del servidor RDS. En ella veremos los usuarios conectados y la lista de los procesos que tienen abiertos:

Para detener un determinado proceso, basta con hacer clic derecho sobre él y escoger la opción *Finalizar tarea.* Para gestionar las opciones relativas a la conexión y desconexión del usuario, el cierre de la sesión y el envío de mensajes, haremos clic derecho sobre el usuario y escogeremos la opción que proceda en el menú contextual.

Existen también herramientas de terceros que nos pueden facilitar el trabajo con las sesiones remotas, y que amplían las posibilidades de la instrumentación incluida en Windows. Por ejemplo, Remote Desktop Commander, de RDPSoft, dispone de un modo gratuito que permite obtener una visión general de las sesiones, los usuarios y los procesos, así como administrarlos de forma centralizada. Además, si utilizamos la versión comercial, podremos obtener todo tipo de informes y estadísticas de uso y carga de trabajo.

#### Para + info

Para obtener una lista completa de los *cmdlets*  para administrar RDS, consulta la siguiente página web:

https://bit.ly/3AlKOF9

![](_page_142_Picture_8.jpeg)
