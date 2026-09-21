# **3.4.2. Sistemas de archivos**

Si bien las particiones constituyen la forma más básica de organizar los datos en una unidad de disco, sin la existencia de un sistema de archivos con el que darles formato seríamos incapaces de trabajar de forma efectiva con ellos. Es este sistema el que nos facilita el acceso a esos datos en forma de archivos, el que proporciona a dichos archivos su conjunto de atributos, y el que nos permite organizarlos convenientemente dentro de directorios y subdirectorios.

#### **Sistemas de archivos de Windows**

Microsoft ha venido desarrollando diferentes sistemas de archivos propios para sus sistemas operativos, y actualmente ofrece tres posibilidades a la hora de dar formato a un disco: FAT32, exFAT y NTFS. Además, está desarrollando el ReFS, un nuevo sistema orientado al manejo de grandes volúmenes de datos en entornos empresariales y de servidores.

En los sistemas Windows, los discos de arranque con GPT cuentan con una partición especial denominada MSR (*Microsoft Reserved*), a la que asignan entre 16 y 32 MB si la unidad es de tamaño inferior a 16 GB, y 128 MB si su capacidad es mayor. Su principal función es la de servir como espacio de almacenamiento para programas que suelen escribir datos en sectores ocultos del disco, ya que estos no están admitidos por la especificación UEFI. Por este motivo, la MSR no recibe ningún identificador de partición y no puede almacenar datos de usuario.

#### Para + info

- **FAT32**: el sistema FAT, del inglés *File Allocation Table*, es decir, tabla de asignación de archivos, consiste en un directorio de archivos y una lista enlazada de unidades de asignación compuestas por conjuntos de sectores contiguos del disco, o clústeres de disco. El directorio contiene el nombre de los archivos —formados por un máximo de 8 caracteres y una extensión de 3 caracteres—, su tamaño, fecha de creación y ubicación del clúster inicial donde se almacenan, y la FAT indica la localización de los clústeres sucesivos hasta recuperar todas las piezas del archivo, que no tienen por qué estar almacenadas de forma secuencial. FAT32 es la versión de 32 bits de este sistema. Admite el uso de 4 atributos de archivo —solo lectura, sistema, modificado y oculto—, y soporta discos duros de hasta 2 TB, aunque el tamaño máximo de una partición está limitado a 2 GB bajo MS-DOS y a 4 GB bajo Windows. La versión del sistema FAT más reciente, exFAT (*Extended File Allocation Table,* tabla de asignación de archivos extendida), está diseñada principalmente para su uso en memorias flash, y puede manejar discos con una capacidad máxima de 512 TB.
- **NTFS**: el *New Technology File System* (*NTFS*) es decir, sistema de archivos de nueva tecnología, almacena la organización del disco en un archivo de metadatos llamado MFT (*Master File Table,* o tabla maestra de archivos), e incluye características de seguridad y redundancia no disponibles en el sistema FAT, como los permisos de acceso o las copias de seguridad de su tabla de archivos. Es un sistema transaccional, ya que hace lo que en inglés se conoce como *journaling,* es decir, mantener un registro de todas las transacciones con el sistema de archivos, de manera que, si este pierde la coherencia debido a algún error, es posible ir revirtiendo las transacciones hasta llegar a un posible punto de recuperación. Otras características que diferencian al NTFS del FAT32 son: su capacidad para manejar volúmenes con un tamaño máximo de entre 16 TB (por defecto, usando clústeres de 4 kB) y 256 TB (con clústeres de 64 kB); que admite la creación de enlaces simbólicos; y que permite trabajar con clústeres de más de un sector, lo que lo hace algo más rápido que sus predecesores.
- **ReFS**: actualmente, Microsoft está desarrollando un nuevo sistema de archivos llamado *Resilient File System* (ReFS), es decir, sistema de archivos resiliente. Está diseñado para poder manejar un gran volumen de datos con una mayor eficiencia y fiabilidad que el NTFS,

siendo capaz de detectar y rectificar automáticamente errores en los datos almacenados, así como de manejar archivos de gran tamaño —hasta 16 exabytes—, en volúmenes de hasta un petabyte de capacidad.

Incluye también otras características avanzadas como la eliminación de datos [duplicados](http://duplicados) y la creación de volúmenes de almacenamiento virtual, capaces de crecer dinámicamente según lo requiera el sistema.

#### **Sistemas de archivos en Linux**

En la tabla a continuación se recogen los sistemas de archivos más utilizados en Linux:

| Nombre             | Tipo     | Descripción                                                               |
|--------------------|----------|---------------------------------------------------------------------------|
| extendido (Ext3)   | ext3     | Sistema compatible con la versión anterior (Ext2), pero con característi |
|                    |          | cas adicionales, como el journaling                                       |
| extendido (Ext4)   | ext4     | Versión más reciente y mejorada de Ext que ha reemplazado a Ext3.         |
| Reiser             | reiserfs | Sistema transaccional alternativo.                                        |
| JFS                | jfs      | Implementación por parte de IBM de un sistema transaccional para          |
| DOS-FAT            | msdos    | Permite acceder a un sistema FAT16.                                       |
| VFAT               | vfat     | Permite acceder a un sistema FAT32.                                       |
| NTFS               | ntfs     | Permite acceder a un sistema NTFS.                                        |
| ISO 9660           | iso9660  | Sistema de archivos utilizado tradicionalmente en CD-ROM.                 |
| UDF                | udf      | Sistema de archivos más reciente para CD-ROM.                             |
| System             | NFS      | Sistema de archivos de red.                                               |
| Samba (SMB)        | smbfs    | Protocolo de Microsoft para el acceso remoto de archivos.                 |
| File System (CIFS) | cifs     | Protocolo sucesor de Samba, aunque compatible con servidores SMB.         |

El sistema de archivos **Ext4** es el más utilizado en Linux. En comparación con sus predecesores, ofrece mejoras como el soporte de archivos de hasta 16 terabytes y la creación de volúmenes de hasta un exabyte de capacidad. Incluye también características avanzadas, como el *journaling* para la recuperación de datos, o la preasignación de espacio para archivos y la agrupación de bloques para la mejora del rendimiento.

Sin embargo, y a pesar de la gran fiabilidad y rendimiento del Ext4, han aparecido nuevos sistemas de archivos que ofrecen características incluso más avanzadas, como **Btrfs** (*B-tree File System*), que proporciona la posibilidad de crear imágenes (*snapshots*) y de trabajar con compresión y cifrado de datos, y **XFS** (*Extended File System*), dirigido al manejo de grandes volúmenes de archivos en entornos de alta escalabilidad.

De esta forma, el XFS sobrepasa, en rendimiento, al Ext4 en operaciones de lectura y escritura de archivos grandes, mientras que Btrfs está optimizado para la lectura de archivos pequeños y la administración de metadatos.

### **Sistemas de archivos virtuales**

Los protocolos de acceso a archivos en red, como **AFS, Samba** (SMB-CI-FS, propietario de Microsoft) o **NFS** (del inglés *Network File System,* es decir, sistema de archivos de red) implementan una capa de abstracción sobre el sistema de archivos subyacente, llamada **sistema de archivos virtual** (en inglés, *Virtual File System,* **VFS**), permitiendo de esta forma el acceso a los archivos a través de una red desde cualquier máquina que soporte el mismo protocolo.

![](_page_77_Picture_6.jpeg)

Un VFS se encarga de interactuar directamente con los dispositivos de almacenamiento para efectuar las operaciones de archivo, mientras que las aplicaciones se comunican con la interfaz unificada del VFS, por lo que no necesitan conocer la ubicación física de los datos ni las particularidades del sistema de archivos subyacente. Esto facilita no solo las operaciones de archivo en red, sino también la creación de sistemas de archivos virtuales que no tienen correspondencia con un medio de almacenamiento físico.

Otra posibilidad que ofrecen los VFS es la centralización de los mecanismos de control de acceso, el almacenamiento en caché y bloqueo de archivos de forma centralizada, lo que puede mejorar el rendimiento y la seguridad del sistema.

Linux integra un VFS como capa de abstracción entre el sistema de archivos y su núcleo, lo cual proporciona una interfaz uniforme para acceder tanto a los archivos de red como a los archivos locales y

Uno de los protocolos de red más utilizados es el NFS, ya que es un estándar abierto y relativamente fácil de implementar. Microsoft proporciona un componente servidor NFS para Windows Server, y cliente para Windows 10 y Windows 11, mientras que, en Linux, el servicio se implementa típicamente mediante el demonio nfsd, y se exportan los recursos compartidos, usando la orden *exportfs,* en el archivo de configuración */etc/exports.*

#### Para + info

a sistemas de archivos virtuales como *sysfs, tmpfs* o *procfs.* Este último, por ejemplo, se monta en el directorio */proc,* y proporciona información sobre los procesos en ejecución y el hardware del sistema en forma de archivos, aunque estos no estén almacenados físicamente en ningún volumen de disco.

Para realizar sus funciones, el VFS proporciona un conjunto de interfaces de programación (API) que los sistemas de archivos pueden utilizar para interactuar con el *kernel* de Linux, incluyendo llamadas al sistema como *open(), read(), write(), close()* e *ioctl()*. A su vez, contempla estructuras de datos para representar los objetos del sistema de archivos, como *inode,* que representa un archivo o directorio, y *dentry*, que representa una entrada de directorio, entre otras.
