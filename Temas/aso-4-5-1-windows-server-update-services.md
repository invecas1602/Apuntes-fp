# **4.5.1. Windows Server Update Services**

![](_page_121_Picture_3.jpeg)

Entre las opciones que WSUS proporciona para gestionar las actualizaciones se incluyen la aprobación manual o automática de actualizaciones, la posibilidad de fijar fechas límite para su instalación y muchas otras que nos ayudarán a mantener el control de qué se actualiza, dónde y cuándo en nuestro entorno de red.

Para instalar los servicios de actualización en Windows 2022 realizaremos los siguientes pasos:

- 1. En el Administrador del servidor, abrimos el menú *Administrar* y escogemos *Agregar roles* y *características.* Como tipo de instalación dejamos marcada la opción *Instalación basada en características o roles*, y marcamos *Windows Server Update Services* en la lista de *Roles de servidor.*

**Windows Server Update Services** o **WSUS** es la herramienta de Microsoft que permite administrar las actualizaciones de Windows y todo el software relacionado dentro de un dominio. Utiliza los protocolos HTTP/HTTPS (en los puertos 8530 y 8531, respectivamente) para descargar las actualizaciones desde los servidores de Microsoft y comunicarse con los equipos clientes.

- 2. Aceptamos las opciones por defecto del asistente hasta llegar al apartado *Contenido,* donde es recomendable especificar la ubicación —una unidad NTFS con al menos 6 GB de espacio libre disponible— en la que se almacenarán todos los archivos de actualización. Con esto ya podemos proceder a la instalación de la característica.

- 3. Finalizada la instalación debemos configurar WSUS, para lo cual, lo primero es hacer clic en el enlace *Iniciar tareas posteriores a la instalación*, bien en la propia ventana de *Progreso de instalación,* bien abriendo la bandera de notificaciones del Administrador del servidor. Ahora podemos abrir el menú *Inicio > Herramientas administrativas de Windows,* y desde ahí ejecutar *Windows Server Update Services,* lo cual lanzará el asistente de configuración inicial. El primer paso del asistente consiste en seleccionar el servidor desde el que se van a descargar las actualizaciones. En nuestro caso, al ser el servidor WSUS principal, es necesario dejar activada la opción por defecto, *Sincronizar desde Microsoft Update*. Tras especificar el servidor proxy, de ser necesario, sincronizamos la información sobre las actualizaciones disponibles haciendo clic en el botón *Iniciar conexión.* Este proceso puede tomar una cantidad de tiempo considerable, dependiendo de nuestra configuración de red y la carga del servidor.

![](_page_122_Figure_4.jpeg)

- 4. El siguiente paso consiste en seleccionar los idiomas y productos para los cuales queremos gestionar las actualizaciones. Esta selección dependerá de cada dominio en particular, pero se recomienda escoger únicamente aquellos productos que sean pertinentes dentro de nuestro entorno para no dedicar recursos a la descarga y almacenamiento de actualizaciones innecesarias. Por defecto, se seleccionan todas las actualizaciones relativas a las diferentes versiones de Windows, pero podemos desmarcar todas las versiones que no existan en el dominio.

![](_page_123_Picture_2.jpeg)

- 5. A continuación especificaremos lo que WSUS denomina *clasificaciones*, que designan los diferentes tipos de actualización que podemos gestionar: actualizaciones críticas, de seguridad, paquetes de características, herramientas, etc. Una vez más, esta selección dependerá de las necesidades del entorno de trabajo.

![](_page_123_Picture_4.jpeg)

- 6. Por último, podemos programar la sincronización de actualizaciones para que se realice según una pauta de tiempo, o bien dejar activada la opción de actualización manual. Para reducir el tiempo que tarda cada proceso de sincronización, podemos distribuir la programación en dos o más sincronizaciones por día.

- 7. Al finalizar el asistente, marcaremos la casilla *Iniciar sincronización inicial.*

- 8. A partir de este momento podemos acceder a la herramienta de servicios de actualización (*Update Services*) desde el menú *Herramientas > Windows Server Update Services* del Administrador del servidor. Para editar las opciones de WSUS, desplegamos el árbol del servidor, en el panel izquierdo, y seleccionamos *Opciones.* Desde aquí también podremos liberar recursos relativos a actualizaciones antiguas utilizando el *Asistente para limpieza del servidor.*

- 9. Para que los equipos del dominio utilicen WSUS como proveedor de actualizaciones, es necesario configurar adecuadamente las directivas de grupo del controlador de dominio (normalmente será un servidor distinto al que hemos dedicado a WSUS). Para ello, abrimos el menú *Inicio > Herramientas administrativas de Windows* del controlador de dominio y seleccionamos *Administración de directivas de grupo* (*gpmc.msc*). A continuación, creamos una nueva directiva (llamada WSUS, por ejemplo) dentro de los *Objetos de directiva de grupo* del dominio. Podemos configurar diferentes GPO para los distintos equipos que forman parte del dominio según el grupo al que pertenezcan o los roles que tengan establecidos.

![](_page_125_Picture_2.jpeg)

- 10. Hacemos clic derecho sobre el nuevo GPO y escogemos la opción *Editar.* Esto abrirá el *Editor de administración de directivas de grupo* para este GPO en particular. Navegamos por *Configuración del equipo > Directivas > Plantillas administrativas > Componentes de Windows > Windows Update* para acceder al listado de directivas relativas al servicio de actualización de los equipos.

![](_page_125_Picture_4.jpeg)

- 11. Abrimos la directiva *Especificar la ubicación del servicio Windows Update en la intranet* y la habilitamos. El servicio de actualización se realiza mediante el protocolo HTTP o, idealmente, HTTPS si tenemos implementada la seguridad basada en SSL en un entorno de producción, por lo que, como dirección del servicio, indicaremos, por ejemplo, *http://Servidor01:8530* o *https://Servidor01:8531,*  asumiendo que *Servidor01* es el nombre del servidor donde hemos instalado WSUS. Indicaremos la misma dirección en el apartado del servidor de estadísticas y pulsaremos *Aceptar.*

- 12. Opcionalmente, podemos habilitar la directiva *Configurar actualizaciones automáticas* para configurar la forma en que los equipos reciben las actualizaciones. Por ejemplo, podemos definir que la descarga se notifique y se instale automáticamente de forma semanal. Vale la pena tomar un tiempo para explorar el resto de directivas y aplicar todas aquellas que se ajusten a nuestras necesidades.

- 13. El último paso es configurar el ámbito del GPO. Si hacemos doble clic sobre él en la herramienta de *Administración de directivas de grupo* veremos, en la pestaña *Ámbito,* que la configuración del GPO se aplica a los usuarios autentificados. Si queremos limitar su aplicación a un equipo o grupo de equipos del dominio, deberemos eliminar este filtro y añadir el equipo o grupo en cuestión mediante el botón *Agregar.* Finalmente, vinculamos la directiva al dominio arrastrándola al elemento padre del dominio (en nuestro caso, *midominio.local*).

![](_page_127_Picture_2.jpeg)

- 14. Para aplicar los cambios en la directiva y registrar de inmediato los servidores y clientes del dominio en WSUS, ejecutamos las siguientes instrucciones en una ventana de Símbolo del sistema (*cmd*):

gpupdate /force wuauclt /detectnow

wuauclt /reportnow

Los procesos de difusión y sincronización en el dominio suelen tardar de unos minutos a varias horas, en función del servicio que se esté desplegando, por lo que será necesario esperar a que los equipos implicados reciban la información necesaria antes de que podamos observar en ellos los cambios implementados.

### Atención
