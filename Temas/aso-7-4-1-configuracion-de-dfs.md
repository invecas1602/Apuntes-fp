# **7.4.1. Configuración de DFS**

En este tutorial utilizaremos dos servidores Windows Server: 2022 y Windows Server 2019, unidos al dominio *midominio.local.* El servidor con Windows Server 2022 (*Servidor01*) es, en este caso, el que actúa como controlador de dominio, y en él habremos instalado y configurado adecuadamente los servicios del Directorio Activo y de servidor DNS.

Para añadir los servicios de almacenamiento distribuido DFS al servidor que no actúa como controlador de dominio (denominado, en nuestro caso, *Servidor02*), iniciaremos sesión con un perfil de administrador de dominio, y haremos lo siguiente:

- 1. En *Servidor02*, abrimos el Administrador del servidor y, en el menú *Administrar*, seleccionamos *Agregar roles y características*. Como *Tipo de instalación*, seleccionamos *Instalación basada en características o en roles.*
- 2. Tras seleccionar el servidor local, en el apartado *Roles de servidor,* abrimos *Servicios de archivos y almacenamiento > Servicios de iSCSI y archivo* y marcamos *Espacios de nombres DFS*, lo cual agregará, a su vez, el servicio de *Servidor de archivos*. Hacemos clic en *Agregar características* y, a continuación, en *Siguiente.*

- 3. Saltamos el apartado *Características* y, en *Confirmación*, pulsamos el botón *Instalar.*

- 4. Una vez instalados los servicios, debemos configurar el espacio de nombres DFS. Para ello, abrimos el menú *Herramientas* en el Administrador del servidor y escogemos *Administración de DFS.* En la consola de administración, seleccionamos *Espacios de nombres* y, en el panel *Acciones*, hacemos clic sobre *Nuevo espacio de nombres.*

![](_page_214_Picture_5.jpeg)

- 5. En el primer paso del *Asistente para crear nuevo espacio de nombres,* indicamos el nombre del servidor que lo hospedará, en nuestro caso, *Servidor02.*

![](_page_214_Picture_9.jpeg)

- 6. Especificamos la denominación del espacio de nombres; en nuestro caso, utilizaremos *datosdfs*. A continuación, pulsamos el botón *Editar configuración.*

![](_page_215_Picture_3.jpeg)

- 7. Aquí podemos cambiar la ruta de acceso a la carpeta compartida y los permisos que los usuarios tendrán sobre ella. Podemos escoger cualquiera de las opciones según nuestras necesidades, o personalizar los permisos.

- 8. Como tipo de espacio de nombres, podemos escoger basarlo en el dominio o que sea independiente.

![](_page_216_Picture_2.jpeg)

- 9. Tras revisar el resumen de nuestras elecciones, pulsamos el botón *Crear* para finalizar el asistente. Nuestro espacio de nombres se habrá creado, según la configuración particular utilizada en este tutorial, en *\\midominio.local\datosdfs.*

![](_page_216_Picture_5.jpeg)

- 10. El siguiente paso consiste en configurar los recursos de almacenamiento compartidos. Para ello, en el Administrador del servidor, vamos a *Servicios de archivos y de almacenamiento > Recursos compartidos*, donde hacemos clic sobre el desplegable *TAREAS*, y seleccionamos *Nuevo recurso compartido.*

![](_page_217_Picture_1.jpeg)

- 11. En el primer paso del asistente para *Nuevo recurso compartido*, seleccionamos un perfil SMB, si trabajamos en un entorno Windows, o NFS si el entorno es heterogéneo, con equipos basados en sistemas Unix, como Linux o macOS. A efectos de este tutorial, escogeremos la primera de las opciones, *Recurso compartido SMB - Rápido.*

![](_page_217_Picture_3.jpeg)

- 12. Seleccionamos la ubicación del recurso compartido, en nuestro caso, el volumen con la letra de unidad *E:*.

![](_page_217_Picture_6.jpeg)

- 13. A continuación, escogemos un nombre para el recurso compartido. Las rutas local y remota se actualizarán según la denominación especificada.

![](_page_218_Picture_3.jpeg)

- 14. En el siguiente paso podremos habilitar el cifrado del acceso a los datos (recomendable si se van a compartir fuera de la intranet), el almacenamiento en caché y la enumeración basada en el acceso, que oculta aquellos archivos y carpetas sobre los que los usuarios no tengan permisos.

![](_page_218_Picture_5.jpeg)

- 15. En el diálogo *Permisos* podemos personalizarlos haciendo clic en el botón correspondiente. Por defecto se autorizan los administradores y usuarios del equipo, pero podemos crear un grupo de seguridad en el controlador de dominio (*UsuariosDFS,* por ejemplo) para restringir el acceso a este recurso. Para ello, desactivaremos la herencia, de forma que los permisos deban configurarse de forma explícita, eliminamos las dos entradas correspondientes a *Usuarios*, y añadimos el permiso para el grupo *UsuariosDFS.*

![](_page_219_Picture_2.jpeg)

- 16. Hacemos clic en *Permisos avanzados* y revisamos los correspondientes a la creación y eliminación de archivos y carpetas, que activaremos o no según nuestras necesidades. También podemos agregar alguna condición para limitar los accesos. Aplicamos y aceptamos la configuración de permisos antes de progresar en el asistente.

![](_page_219_Picture_5.jpeg)

- 17. El último diálogo muestra un resumen de la configuración escogida. Tras revisarlo, si estamos conformes pulsaremos el botón *Crear*.

- 18. A continuación, abrimos el explorador de archivos y vamos a la carpeta compartida (en nuestro caso, *E:\Shares\ArchivosDFS*), donde crearemos un nuevo archivo de texto al que llamaremos *Prueba*. Seguidamente, regresamos a la consola *Administración de DFS,*  hacemos clic derecho en el espacio de nombres que hemos creado (en nuestro caso, *\\midominio.local\datosdfs*), y escogemos la opción *Nueva carpeta.*

![](_page_220_Picture_2.jpeg)

- 19. Le daremos un nombre a la carpeta (por ejemplo, *archivosdfs*) y pulsaremos *Agregar*. Indicaremos la ruta de acceso de la carpeta compartida y, finalmente, pulsaremos *Aceptar*. Podemos agregar tantas carpetas como deseemos.

Si ahora iniciamos sesión en un cliente del dominio con cualquier usuario dentro del grupo *UsuariosDFS* y, en el explorador de archivos, vamos a la dirección *\\Servidor02\ArchivosDFS*, podremos leer, editar o eliminar el archivo *Prueba* según los permisos que tengamos otorgados.

#### **Activar la replicación DFS**

Para activar la replicación DFS en nuestro dominio de pruebas, *midominio.local*, necesitaremos instalar estos servicios en un mínimo de dos servidores. Para ello, seguiremos estos pasos en ambos equipos (denominados, en nuestro entorno, *Servidor01* y *Servidor02*):

- 1. Abrimos el Administrador del servidor y, en el menú *Administrar,*  seleccionamos *Agregar roles y características.* Como *Tipo de instalación,* seleccionamos *Instalación basada en características o en roles.*

- 2. Tras seleccionar el servidor local, en el apartado *Roles de servidor,* abrimos *Servicios de archivos y almacenamiento* > *Servicios de iSCSI y archivo*, y marcamos *Replicación DFS*. Hacemos clic en *Agregar características* y, a continuación, en *Siguiente*. Obviamos el apartado *Características* y, en *Confirmación*, pulsamos el botón *Instalar.*

- 3. Recordemos que, en el servidor miembro *Servidor02*, habíamos creado ya una carpeta compartida accesible en la dirección *\\Servidor02\ArchivosDFS*. En esta ocasión, procederemos a crear un recurso compartido en el equipo que hemos añadido para replicación. Por lo tanto, en el Administrador del servidor de

*Servidor01,* vamos a *Servicios de archivos y de almacenamiento > Recursos compartidos* y hacemos clic sobre el desplegable *TA-REAS*, donde seleccionaremos *Nuevo recurso compartido.*

![](_page_222_Picture_2.jpeg)

- 4. En este punto, realizaremos los pasos del 11 al 19 del paso a paso anterior, aunque cambiaremos el nombre y ruta de la carpeta replicada (por ejemplo, *D:\CopiaDFS\ArchivosDFS\_Rpl*), con lo que la ruta remota al recurso quedará configurada como *\\Servidor01\ archivosdfs\_rpl.* En cuanto a los permisos, en este caso no será necesario efectuar ningún cambio, de manera que podemos dejar los que se configuran por defecto.

![](_page_222_Picture_4.jpeg)

- 5. A continuación, en *Servidor02*, abrimos el menú *Herramientas* en el Administrador del servidor y escogemos *Administración de DFS*. En la consola de administración, seleccionamos *Espacios de nombres > \\midominio.local\datosdfs > archivosdfs* (o cualquier otro recurso que queramos replicar) y hacemos clic derecho sobre esta entrada. En el menú contextual, seleccionamos *Agregar destino de carpeta.*

![](_page_223_Picture_1.jpeg)

- 6. En el diálogo *Buscar carpetas compartidas*, seleccionamos la carpeta que hemos creado en *Servidor01: archivosdfs\_rpl*.

- 7. Nos aparece un diálogo de confirmación para crear automáticamente un grupo de replicación (el grupo de equipos que participan en la replicación de una o varias carpetas compartidas), al cual respondemos de forma afirmativa.

- 8. En el *Asistente para replicación de carpeta*, avanzamos hasta el diálogo *Miembro principal* donde, en nuestro caso, seleccionamos *Servidor02*, que es donde se ha configurado la carpeta compartida original.

- 9. El siguiente paso nos permite seleccionar una topología de conexiones entre los equipos miembros del grupo de replicación. La topología *Concentrador y radio* solo está disponible cuando existen tres o más miembros dentro del grupo.

- 10. A continuación podemos configurar una programación para la realización de las réplicas, o bien dejar la opción por defecto, que es la réplica continua. En este caso, si queremos restringir los recursos dedicados a este servicio, podemos limitar el ancho de banda disponible para la réplica.

#### 11. Revisamos la configuración y pulsamos el botón *Crear*.

![](_page_225_Picture_3.jpeg)

- 12. El nuevo grupo de replicación aparecerá bajo la raíz *Replicación*  en la consola *Administración de DFS.* A partir de este punto, los archivos contenidos en cualquiera de las dos carpetas compartidas se replicarán en la otra.

![](_page_225_Picture_5.jpeg)

- 13. Si comprobamos los permisos de la carpeta que hemos creado en *Servidor01*, veremos que se han modificado automáticamente para que coincidan con los de la carpeta principal en *Servidor02*.

![](_page_225_Picture_8.jpeg)

- 14. Si queremos auditar los procesos de replicación dentro de un grupo en particular, podemos crear un informe haciendo clic derecho sobre dicho grupo y seleccionando *Crear informe de diagnóstico.*

![](_page_226_Picture_2.jpeg)

- 15. Disponemos de dos tipos de informe: de *mantenimiento* y de *propagación*. Además, desde aquí podemos lanzar una prueba de propagación para comprobar el correcto funcionamiento del servicio.
