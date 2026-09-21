# **7.4.2. Configuración de GlusterFS**

En este paso a paso, partimos de dos servidores basados en Debian en los que tenemos agregados sendos discos duros que queremos clusterizar con GlusterFS. Cada servidor está equipado con dos adaptadores de red, uno con salida a Internet (10.0.1.x), y otro configurado en una red exclusivamente para uso interno (192.168.0.1 para el equipo llamado *cluster01*, y 192.168.0.2 para *cluster02*). Este último adaptador es el que utilizaremos con GlusterFS.

Para ello, seguiremos los pasos que se indican a continuación:

- 1. Tras actualizar el sistema, nos aseguramos de haber obtenido los paquetes que vamos a necesitar para poder instalar el software de GlusterFS en nuestro sistema:

sudo apt install gnupg2 apt-transport-https software-properties-common

- 2. A continuación, añadimos el repositorio de GlusterFS:

curl https://download.gluster.org/pub/gluster/glusterfs /10/rsa.pub | gpg - dearmor > /usr/share/keyrings/glusterfs-archive -keyring.gpg DEBID=\$(grep 'VERSION\_ID=' /etc/os-release | cut -d '=' -f 2 | tr -d '"') DEBVER=\$(grep 'VERSION=' /etc/os-release | grep -Eo '[a-z]+') DEBARCH=\$(dpkg --print-architecture) echo "deb [signed-by=/usr/share/keyrings/glusterfs -archive-keyring.gpg arch=64] https://download.gluster.org/pub/gluster/glusterfs/ LATEST/Debian/\${DEBID}/\${DEBARCH}/apt \${DEBVER} main" | sudo tee /etc/apt/sources.list.d/gluster.list

La forma de agregar el repositorio puede diferir en función de la distribución que estemos utilizando. Por ejemplo, si esta soporta el uso de repositorios personales (PPA), como es el caso de Ubuntu y derivados, podemos agregar el repositorio utilizando una única instrucción:

sudo add-apt-repository ppa:gluster/glusterfs-5

- 3. Una vez configurado el repositorio, ya podemos proceder a instalar y activar GlusterFS:

sudo apt update sudo apt install glusterfs-server sudo systemctl enable glusterd

Podemos comprobar si el servidor GlusterFS funciona con la siguiente instrucción:

systemctl status glusterd

- 4. Editamos los archivos */etc/hosts* en cada equipo agregando las líneas siguientes (será necesario modificarlas en función de los nombres de anfitrión y direcciones IP particulares de cada escenario):

192.168.0.1 cluster01 192.168.0.2 cluster02

- 5. En el equipo que queremos configurar como primer nodo de GlusterFS (*cluster01,* en nuestro caso), ejecutamos la siguiente instrucción para agregar el segundo nodo (*cluster02*):

sudo gluster peer probe cluster02

Si la operación ha tenido éxito, veremos el siguiente mensaje:

peer probe: success

Lo verificamos con la siguiente instrucción:

sudo gluster peer status

- 6. Es el momento de agregar los medios que vamos a utilizar a un volumen distribuido que, en nuestro caso, denominaremos *datos*. Suponiendo que están montados en */media/Datos1* para el servidor *cluster01,* y en */media/Datos2* para *cluster02*, tendremos que usar la siguiente instrucción:

gluster volume create datos replica 2 cluster01:/Datos1/br0 cluster02:/Datos2/br0

Los volúmenes de GlusterFS se denominan *bricks* y deben tener su propio punto de montaje, de ahí que lo montemos en */Datos1/br0* y */Datos2/br0.* Es importante que los discos físicos que vayamos a utilizar se monten automáticamente durante el inicio del sistema, para lo cual tendremos que haberlos incluido en */etc/fstab.*

Por otra parte, y dado que estamos utilizando únicamente dos volúmenes distribuidos, veremos un mensaje de advertencia acerca de la posibilidad de un escenario *split-brain*, en el cual dos o más copias de un mismo archivo difieran. Esto puede suceder, por ejemplo, cuando se pierde la conexión entre los dos *bricks,* de forma que los cambios en los archivos de un servidor no se replican en el otro. Solventar esta situación implica una parada del sistema y la pérdida temporal de disponibilidad, por lo que, siempre que sea posible, se recomienda utilizar, al menos, 3 *bricks.*

- 7. El siguiente paso es iniciar el volumen *datos* para empezar a acceder a los archivos:

Para comprobar el estado de los volúmenes, usamos la siguiente orden:

sudo gluster volume status

En nuestro caso, aparecen los dos *bricks* que hemos agregado anteriormente:

Brick cluster01:/Datos1/br0

Brick cluster02:/Datos2/br0

Junto a cada entrada veremos el puerto TCP que se está utilizando, si está o no en línea, y su Pid. Para acceder a más información acerca del volumen, ejecutamos la siguiente instrucción:

sudo gluster volume info

El *Status* debe ser *Started.*

- 8. Para restringir el acceso al volumen a los equipos de la red interna, ejecutamos lo siguiente:

sudo gluster volume set datos auth.allow 192.168.0.\*

- 9. Para comprobar que los archivos se replican correctamente, instalaremos el software cliente en un equipo con acceso a la intranet:

sudo apt install gluster-client

- 10. A continuación, crearemos un directorio que nos sirva como punto de montaje y montaremos ahí el volumen *datos* con sistema de archivos *glusterfs*:

sudo mkdir /datoscli

sudo mount.glusterfs cluster01:/datos /datoscli

- 11. Para que el montaje sea persistente entre reinicios, en nuestro caso deberemos añadir la siguiente línea en */etc/fstab*:

cluster01:/datos /datoscli glusterfs defaults,\_netdev 0 0

- 12. Finalmente, creamos un archivo nuevo en /*datos*, y comprobamos que exista en */media/Datos1/br0* (*cluster01*) y */media/Datos1/br0* (*cluster02*):

sudo touch /datos/prueba

![](_page_230_Picture_1.jpeg)
