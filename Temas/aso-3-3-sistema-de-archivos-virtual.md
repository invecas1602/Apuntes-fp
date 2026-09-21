# **3.3. Sistema de archivos virtual**

Un **sistema de archivos virtual** (VFS, por sus siglas en inglés) es una capa de abstracción en el sistema operativo que permite que diferentes sistemas de archivos coexistan y se gestionen de manera uniforme. El VFS actúa como una interfaz que estandariza las operaciones de archivos y directorios, independientemente del sistema de archivos subyacente.

Esto significa que el sistema operativo y las aplicaciones pueden interactuar con archivos de diferentes sistemas de archivos (como NTFS, FAT32, ext4, etc.) de manera coherente, sin necesidad de conocer los detalles específicos de cada sistema de archivos.

![](_page_65_Picture_4.jpeg)

El **sistema de archivos virtual** es una tecnología crucial que permite a los sistemas operativos gestionar diferentes tipos de sistemas de archivos de manera coherente y uniforme. En todos los sistemas operativos, el VFS permite la coexistencia de múltiples sistemas de archivos, facilitando la interoperabilidad, la compatibilidad y la gestión eficiente de los recursos del sistema.

El VFS se encarga de traducir las llamadas al sistema relacionadas con el manejo de archivos (como abrir, leer, escribir, y cerrar archivos) a las operaciones específicas que cada sistema de archivos requiere. Esta capa es esencial para proporcionar un entorno unificado para la gestión de archivos en sistemas operativos que deben trabajar con múltiples sistemas de archivos simultáneamente.

En un mundo donde los entornos informáticos son cada vez más heterogéneos, el VFS juega un papel esencial en garantizar que las operaciones de archivos se realicen de manera consistente y sin problemas, independientemente del sistema de archivos subyacente.

El funcionamiento de un VFS puede entenderse en términos generales a través de los siguientes conceptos:

- **Abstracción de sistemas de archivos**: el VFS abstrae los detalles específicos de cada sistema de archivos y proporciona una interfaz común que el sistema operativo y las aplicaciones pueden utilizar. Por ejemplo, cuando un programa necesita abrir un archivo, realiza una llamada al sistema que el VFS traduce en una operación específica para el sistema de archivos subyacente.

- **Montaje de sistemas de archivos**: el VFS permite montar diferentes sistemas de archivos en diferentes puntos del árbol de directorios. Esto significa que un disco con un sistema de archivos NTFS puede montarse en un directorio, mientras que otro disco con un sistema de archivos ext4 puede montarse en otro directorio, y ambos serán accesibles desde un único espacio de nombres unificado.
- **Estructuras de datos uniformes**: el VFS utiliza estructuras de datos comunes, como inodos y dentries, para representar archivos y directorios, independientemente del sistema de archivos subyacente. Esto permite que las operaciones de archivos sean consistentes y coherentes.
- **Operaciones de archivos**: cuando una aplicación realiza una operación en un archivo, el VFS intercepta la solicitud y determina qué sistema de archivos está implicado, traduce la operación en términos específicos del sistema de archivos y luego la ejecuta.
- **Compatibilidad**: el VFS facilita la compatibilidad entre diferentes sistemas de archivos, lo que es particularmente útil en entornos heterogéneos donde es necesario trabajar con diferentes tipos de sistemas de archivos simultáneamente.

#### **Aplicación del sistema de archivos virtual en Windows 10**

En Windows 10, el concepto de VFS se aplica a través del **gestor de sistemas de archivos** integrado en el kernel de Windows. Este gestor permite que diferentes sistemas de archivos como NTFS, FAT32, exFAT, y ReFS coexistan y se gestionen de manera uniforme.

- **NTFS** (New Technology File System): es el sistema de archivos predeterminado en Windows 10. Soporta características avanzadas como permisos de archivo, compresión, cifrado, y journaling. NTFS es completamente compatible con el VFS de Windows, lo que permite que las aplicaciones accedan a archivos en volúmenes NTFS de manera coherente.
- **FAT32 y exFAT**: estos sistemas de archivos son compatibles principalmente para garantizar la interoperabilidad con dispositivos y sistemas más antiguos o con limitaciones, como unidades flash USB y tarjetas SD. El VFS en Windows traduce las operaciones de archivos para que estos sistemas de archivos más simples puedan ser utilizados sin problemas junto con NTFS.

- **ReFS** (Resilient File System): es un sistema de archivos más reciente orientado a servidores y almacenamiento en Windows, diseñado para manejar grandes volúmenes de datos con mayor resiliencia y rendimiento. El VFS de Windows permite que ReFS coexista con NTFS y otros sistemas de archivos en el mismo entorno.
- **Redirección de archivos y carpetas**: a través de VFS, Windows 10 soporta la redirección de archivos y carpetas, lo que permite que las operaciones de archivos se redirijan a diferentes ubicaciones o sistemas de archivos sin que las aplicaciones sean conscientes de ello. Esto es útil para implementar políticas de red, como la redirección de carpetas en entornos empresariales.

#### **Aplicación del sistema de archivos virtual en Ubuntu**

En Ubuntu, como en otros sistemas operativos basados en Linux, el VFS es una parte integral del kernel que permite la coexistencia y la interoperabilidad de diferentes sistemas de archivos, como ext4, Btrfs, XFS, NTFS, y FAT.

- **ext4** (Fourth Extended Filesystem): es el sistema de archivos predeterminado en Ubuntu. El VFS en el kernel de Linux permite que ext4 funcione sin problemas junto con otros sistemas de archivos. Las operaciones de archivos realizadas en un volumen ext4 son manejadas a través del VFS de manera uniforme.
- **Btrfs** (B-tree File System): es un sistema de archivos avanzado con características como snapshots, compresión y gestión de volúmenes. El VFS en Ubuntu permite que Btrfs coexista con otros sistemas de archivos, y las operaciones de archivos se realizan de manera coherente a través de la capa de abstracción del VFS.

- **XFS**: es un sistema de archivos de alto rendimiento diseñado para manejar grandes volúmenes de datos. Ubuntu utiliza el VFS para integrar XFS en su estructura de archivos de manera uniforme, lo que permite que las aplicaciones accedan a archivos en volúmenes XFS sin necesidad de conocer los detalles de su implementación.
- **Montaje de sistemas de archivos de red**: Ubuntu permite montar sistemas de archivos de red como NFS (Network File System) o CIFS (Common Internet File System) a través del VFS, lo que facilita el acceso a recursos compartidos en red como si fueran locales. Esto es crucial en entornos de red, donde los archivos deben ser accesibles desde diferentes sistemas con diferentes tipos de sistemas de archivos.
- **Acceso a sistemas de archivos de windows**: gracias al VFS, Ubuntu puede montar y acceder a volúmenes NTFS de manera nativa, utilizando herramientas como ntfs-3g. Esto es esencial para la interoperabilidad entre sistemas operativos Windows y Linux.

#### **Aplicación del sistema de archivos virtual en macOS**

En macOS, al igual que en otros sistemas operativos modernos, el Sistema de Archivos Virtual (VFS) juega un papel esencial en la gestión de diferentes tipos de sistemas de archivos. El VFS en macOS permite a las aplicaciones y al propio sistema operativo interactuar de manera uniforme con varios sistemas de archivos, independientemente de las diferencias internas entre ellos.

macOS, al estar basado en Unix, utiliza un VFS que es muy similar en concepto al de otros sistemas operativos Unix-like. El VFS de macOS permite la interoperabilidad entre múltiples sistemas de archivos y proporciona una interfaz coherente para las operaciones de archivos, sin que las aplicaciones necesiten conocer los detalles específicos del sistema de archivos subyacente.

![](_page_68_Picture_5.jpeg)

- **Abstracción de sistemas de archivos**: el VFS de macOS abstracta las diferencias entre los sistemas de archivos, presentando una interfaz común para las operaciones como lectura, escritura, apertura, cierre y eliminación de archivos. Esto permite que diferentes sistemas de archivos puedan ser utilizados simultáneamente de manera coherente.

- **Montaje de sistemas de archivos**: en macOS, los sistemas de archivos se montan en el directorio raíz (/) o en subdirectorios específicos. El VFS gestiona el montaje de sistemas de archivos locales y de red, permitiendo que todos los archivos y volúmenes sean accesibles de forma unificada.
- **Compatibilidad y extensibilidad**: el VFS de macOS es extensible, lo que significa que puede soportar nuevos tipos de sistemas de archivos mediante la adición de módulos o drivers específicos. Esto permite que macOS pueda trabajar con una amplia variedad de sistemas de archivos, tanto nativos como de otros sistemas operativos.

#### **Sistemas de archivos soportados en macOS a través del VFS**

- **APFS** (Apple File System): es el sistema de archivos predeterminado en macOS desde la versión macOS High Sierra (10.13). APFS está optimizado para el almacenamiento en unidades de estado sólido (SSD) y ofrece características avanzadas como snapshots, clonación de archivos, cifrado de alto rendimiento, y la gestión eficiente de espacio. El VFS de macOS permite que APFS sea utilizado de manera nativa, gestionando las operaciones de archivos sin problemas.
- **HFS+** (Hierarchical File System Plus): HFS+ fue el sistema de archivos predeterminado en macOS antes de APFS. Aunque ha sido reemplazado por APFS en la mayoría de los casos, sigue siendo soportado a través del VFS de macOS, permitiendo que los volúmenes HFS+ sigan siendo accesibles y gestionables en sistemas más modernos.
- **FAT32 y exFAT**: estos sistemas de archivos son comúnmente utilizados en dispositivos de almacenamiento externos como memorias USB y discos duros portátiles. El VFS de macOS permite que los volúmenes FAT32 y exFAT sean montados y utilizados de manera transparente, facilitando la compatibilidad con otros sistemas operativos, como Windows.
- **NTFS** (New Technology File System): aunque macOS puede montar volúmenes NTFS de forma nativa, el soporte para operaciones de escritura en NTFS es limitado. A través del VFS, macOS permite montar volúmenes NTFS en modo de solo lectura de manera predeterminada. Sin embargo, existen soluciones de terceros que proporcionan soporte completo de lectura y escritura en volúmenes NTFS.

![](_page_70_Picture_0.jpeg)

- **Sistemas de archivos de red**: macOS soporta varios sistemas de archivos de red a través del VFS, como SMB (Server Message Block), AFP (Apple Filing Protocol) y NFS (Network File System). Esto permite que macOS acceda a recursos compartidos en red de manera eficiente y coherente, integrándolos en el sistema de archivos local como si fueran volúmenes nativos.

#### **Ejemplos de aplicación del VFS en macOS**

- **Montaje automático de volúmenes**: cuando un usuario conecta un disco duro externo o una unidad flash a un sistema macOS, el VFS se encarga de detectar el sistema de archivos en el volumen y montarlo automáticamente en el escritorio o en /Volumes. Esto permite que el usuario acceda inmediatamente a los archivos sin necesidad de realizar configuraciones adicionales.
- **Time Machine**: el sistema de copias de seguridad de macOS, Time Machine, utiliza el VFS para gestionar las operaciones de archivo en volúmenes dedicados de manera eficiente. Time Machine puede trabajar con APFS y HFS+ de manera transparente, aprovechando las capacidades de snapshot y clonación de APFS para optimizar las copias de seguridad.
- **Compatibilidad multiplataforma**: gracias al VFS, macOS puede interactuar con volúmenes formateados en FAT32 o exFAT, lo que es esencial para la interoperabilidad con dispositivos Windows. Esto permite que los usuarios de macOS puedan leer y escribir en dispositivos USB que se utilizan comúnmente entre diferentes sistemas operativos.
- **Acceso a servidores de archivos en red**: a través del VFS, macOS puede montar y acceder a recursos compartidos en red utilizando protocolos como SMB y AFP. Esto es particularmente útil en entornos empresariales donde los archivos y recursos deben ser accesibles desde múltiples plataformas y ubicaciones.
