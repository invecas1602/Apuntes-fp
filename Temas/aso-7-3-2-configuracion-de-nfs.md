# **7.3.2. Configuración de NFS**

Samba es un servicio muy integrado en el ecosistema Windows pero, para compartir archivos en entornos de red heterogéneos, una opción a tener en cuenta es NFS, ya que su uso está más extendido en sistemas tipo Unix.

Para ilustrar una implementación típica de archivos compartidos en un ecosistema de red mixto, en este tutorial veremos cómo configurar un recurso compartido mediante NFS en Linux y cómo conectarnos a él en clientes tanto con Linux como con Windows 11.

En un servidor Linux (en nuestro caso vamos a usar una distribución basada en Debian), haremos lo siguiente:

- 1. Ejecutamos las siguientes instrucciones en un emulador de terminal:

sudo apt install nfs-kernel-server rpcbind

#### 2. A continuación, editamos el archivo */etc/exports*:

sudo nano /etc/exports

- 3. En este archivo se almacena la lista de sistemas de archivos que se exportarán a los clientes NFS. El formato de cada entrada es el siguiente:

ruta/carpeta/exportada IP\_servidor/longitud(parámetros)

Para nuestro ejemplo, habremos creado previamente una carpeta con *sudo mkdir /nfs.* Siendo 10.0.1.1 la dirección IP de nuestro servidor, podríamos configurar el recurso como sigue:

/nfs 10.0.1.1(rw,sync,no\_root\_squash,no\_subtree\_check)

Las opciones escogidas permiten la lectura y escritura en la carpeta especificada (*rw*); la respuesta a las peticiones solo cuando los cambios se hayan realizado en el almacenamiento (*sync*, más lenta pero más segura que *async*); que el perfil *root* de los clientes se trate como *root* del servidor (*no\_root\_squash*), y que no se compruebe si los archivos accedidos están en el árbol exportado (*no\_subtree\_check*) a efectos de mejorar el rendimiento.

Es necesario tener en cuenta que los UID y GID del usuario con el cual accedemos desde el equipo cliente deben coincidir con los del propietario de la carpeta compartida o bien, si el recurso exportado lo permite, podemos utilizar *root*.

Para obtener un listado de todas las opciones disponibles, podemos acudir a la correspondiente página de manual, *man exports.*

- 4. Tras guardar el archivo, ejecutamos lo siguiente:

sudo exportfs -va

sudo systemctl restart nfs-kernel-server

- 5. En el equipo cliente basado en Linux, instalamos el siguiente paquete, si no lo está ya:

sudo apt install nfs-common

- 6. Creamos una carpeta para acceder a los archivos compartidos (por ejemplo */home/usuario/nfs*) y editamos el archivo */etc/fstab*  añadiendo una entrada con formato similar al de esta:

10.0.1.1:/nfs /home/usuario/nfs nfs rw,noauto,user 0 0

Como ya habíamos visto en la configuración de Samba, la primera parte de la entrada (en este caso, *10.0.1.1:/nfs*) es la dirección del recurso compartido, y la siguiente (*/home/usuario/nfs*), la ruta a la carpeta de montaje que hemos creado. Si utilizamos la opción *noauto* la carpeta no se montará automáticamente en el inicio de sesión y tendremos que hacerlo manualmente con *mount /home/ usuario/nfs* (en este caso, podríamos usar también *mount ~/nfs*).

- 7. En un cliente con Windows, podemos instalar el cliente NFS mediante la siguiente instrucción de PowerShell:

Enable-WindowsOptionalFeature -FeatureName ServicesForNFS-ClientOnly, ClientForNFS-Infrastructure -Online -NoRestart

Si se trata de Windows Server, utilizaremos la siguiente instrucción en su lugar:

Install-WindowsFeature NFS-Client

- 8. Dado que es necesario proporcionar un UID y un GID para acceder al recurso compartido, y que Windows se basa en SID, es necesario mapear los identificativos de Linux correctamente. Para ello pueden seguirse diferentes métodos, dependiendo de si tanto el servidor como el cliente están o no unidos a un dominio con Directorio Activo.

Si ambos están dentro del dominio, entonces podemos utilizar el mapeado de identidades del Directorio Activo. En primer lugar, ejecutamos la siguiente instrucción para hacer que el cliente NFS pueda usar esta funcionalidad:

Set-NfsMappingStore -EnableADLookup \$True -ADDomainName "nombre\_del\_dominio"

A continuación, editaremos las propiedades del usuario en la consola *Usuarios y equipos de Active Directory,* no sin haber activado antes las *Características avanzadas* en el menú *Ver*. En la pestaña *Editor de atributos,* editaremos los atributos *uidNumber* y *gidNumber* para que coincidan con los autorizados, que podemos obtener ejecutando *id nombre\_usuario* en el emulador de terminal del servidor Linux.

Por último, montaremos el recurso con una letra de unidad, por ejemplo:

mount \\10.0.1.98\home\usuario\nfs U:

- 9. Una forma simple, aunque menos segura, de lograr esto en cualquier equipo, esté unido o no a un dominio, es ejecutar las siguientes instrucciones de PowerShell:

New-ItemProperty HKLM:\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion \Default -Name

AnonymousUID -Value 1000 -PropertyType "DWord"

New-ItemProperty

HKLM:\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion

\Default -Name

AnonymousGID -Value 1000 -PropertyType "DWord"

Será necesario reemplazar el número 1000 por el UID y GID del usuario propietario del recurso. Con esto estaremos mapeando los identificativos de usuario y grupo autorizados al usuario y grupo anónimos.

Tras reiniciar el equipo, para montar el recurso ejecutaremos, en esta ocasión, la siguiente orden:
