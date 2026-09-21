# **5.2.3. Puerta de enlace de Escritorio remoto**

![](_page_143_Picture_2.jpeg)

Para configurar la puerta de enlace de Escritorio remoto, hacemos lo siguiente:

- 1. Abrimos el Administrador del servidor y vamos a *Servicio de Escritorio remoto > Información general,* donde hacemos clic sobre el icono *Puerta de enlace de Escritorio remoto*. Esto iniciará el asistente que nos permitirá agregar el servidor puerta de enlace de entre los servidores disponibles en el cuadro *Grupo de servidores.*

![](_page_143_Picture_6.jpeg)

- 2. A continuación, debemos indicar el nombre del certificado SSL que se utilizará para cifrar las comunicaciones con los clientes. Este debe coincidir con el FQDN, es decir, el nombre de dominio completo del servidor RDS, por ejemplo, *rds.midominio.es.* Con esto ya podemos agregar el servicio de rol *Puerta de enlace de Escritorio remoto.*

La **puerta de enlace de Escritorio remoto** (en inglés, *RD Gateway*) proporciona acceso seguro mediante HTTPS a clientes de fuera de la red corporativa sin necesidad de utilizar una red privada virtual o VPN. De esta forma, utiliza el puerto 443 para establecer conexiones seguras, incluso a través de cortafuegos, abriendo puertos adicionales.

- 3. Tras completarse la instalación del servicio de rol, desplegamos la lista TAREAS y seleccionamos *Editar propiedades de la implementación*, donde seleccionamos *Certificados* en el panel izquierdo, y *Puerta de enlace de Escritorio remoto* en la lista de servicios de rol. Aquí podremos configurar todo lo relativo al certificado SSL. Si disponemos de un certificado emitido por una entidad de confianza, pulsaremos el botón *Seleccionar certificado existente*. En caso contrario, haremos clic en *Crear nuevo certificado.*

![](_page_144_Picture_2.jpeg)

- 4. Como nombre de certificado, indicaremos el FQDN anteriormente mencionado, así como una contraseña y una ruta de almacenamiento. Además, deberemos marcar la casilla que permite agregar el certificado a los equipos de destino. Pulsamos *Aceptar* y, seguidamente, *Aplicar*.

![](_page_144_Picture_5.jpeg)

- 5. Si el servidor en el que hemos instalado el servicio de rol de puerta de enlace es el mismo que desempeña el de *Acceso web de Escritorio remoto*, debemos asegurarnos de utilizar el mismo certificado para ambos. Para ello, escogeremos *Acceso web a Escritorio remoto* en la lista de servicios de rol y pulsaremos el botón *Seleccionar certificado existente*.

Indicaremos la ruta al certificado autogenerado previamente, su contraseña y, una vez más, permite agregar el certificado en destino. Pulsa *Aceptar* y, seguidamente, *Aplicar*, para realizar la asignación.

![](_page_145_Picture_3.jpeg)

- 6. Tras haber configurado la puerta de enlace, es necesario que configuremos adecuadamente los clientes para que puedan conectarse de forma segura. Para ello, abrimos la aplicación Conexión a Escritorio remoto (*mstsc.exe*), desplegamos *Mostrar opciones,* vamos a la pestaña *Opciones avanzadas* y pulsamos el botón *Configuración.* En la ventana de configuración de la conexión, escogemos *Usar esta configuración de servidor de puerta de enlace de Escritorio remoto,* indicando el FQDN del servidor de puerta de enlace y marcando la casilla *Usar mis credenciales de Puerta de enlace de Escritorio remoto para el equipo remoto.* Adicionalmente, si queremos usar la puerta de enlace también para direcciones locales, tendremos que desmarcar la casilla correspondiente, según se observa en la imagen.

![](_page_145_Picture_6.jpeg)

- 7. Regresamos a la pestaña *General,* indicamos el nombre del servidor de puerta de enlace y el usuario mediante el que queremos conectarnos al Escritorio remoto (por ejemplo, *usuario@midominio.local*) pulsando el botón *Conectar.*

- 8. Se abrirá la ventana *Escribir las credenciales,* donde se nos solicita la contraseña del usuario. Al aceptar, veremos un mensaje en el que se nos advierte que no se puede comprobar la identidad de la puerta de enlace. Para solventar este problema, pulsaremos el botón *Ver certificado.*
- 9. Abrimos la pestaña *Detalles del certificado* y pulsamos el botón *Copiar en archivo,* lo que iniciará el *Asistente para exportar certificados.* Escogeremos el formato a utilizar (la opción por defecto es válida) y especificaremos la ruta y el nombre de archivo en el que se almacenará el certificado. Pulsaremos *Finalizar* para exportar el certificado.

- 10. Seguidamente, iremos al lugar donde hemos almacenado el certificado y lo abriremos. En esta ocasión, podremos instalarlo haciendo clic en el botón *Instalar certificado.*

- 11. Seleccionamos la ubicación del almacén donde queremos instalar el certificado, en el del equipo local o en el del usuario actual.

- 12. En el diálogo siguiente, seleccionamos *Colocar todos los certificados en el siguiente almacén,* pulsamos *Examinar* y escogemos *Entidades de certificación raíz de confianza.* Pulsamos en *Finalizar* y se nos informará de que la importación se ha completado correctamente. Si ahora regresamos a la aplicación Conexión de Escritorio remoto y pulsamos en *Conectar*, tras introducir la contraseña del usuario ya podremos establecer la conexión de Escritorio remoto.

![](_page_147_Picture_8.jpeg)

- 13. Opcionalmente, mediante el uso de la puerta de enlace podemos limitar el acceso al Escritorio remoto por usuario. En este caso, lo más práctico es crear un grupo de seguridad (llamado, por ejemplo, *UsuariosRDS*) en Usuarios y equipos de Active Directory, e incluir en él todos los usuarios a los que se les permitirá la conexión.

Una vez hecho esto, desplegamos el menú *Herramientas* del Administrador del servidor y vamos a *Remote Desktop Services*  > *Administrador de puerta de enlace de Escritorio remoto.* En él, desplegamos el árbol del servidor, vamos a *Directivas* > *Directivas de autorización de recursos* y hacemos doble clic en *RDG\_AllDomainComputers.* Aquí, vamos a la pestaña *Grupos de usuarios* y pulsamos el botón *Agregar.*

![](_page_148_Picture_2.jpeg)

- 14. Agregamos el grupo *Usuarios RDS* y eliminamos el de *Usuarios del dominio.*

- 15. En la pestaña *Recurso de red,* podremos especificar a qué recursos de red tendrán acceso los usuarios. Por defecto pueden conectarse a los equipos del dominio, pero podemos seleccionar un grupo administrado por la puerta de enlace, o bien permitir que se conecten a cualquier recurso de red disponible.
