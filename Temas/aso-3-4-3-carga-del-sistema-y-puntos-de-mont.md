# **3.4.3. Carga del sistema y puntos de montaje**

El componente de software administrador de arranque de los sistemas de Microsoft es Windows Boot Manager o BOOTMGR, un ejecutable que, en sistemas con BIOS, permanece oculto en la partición activa, y que en aquellos con UEFI encontraremos, dentro de la partición de sistema, bajo el nombre de *BOOTMGFW.EFI.*

#### **Arranque de Windows**

Para guardar su configuración, BOOTMGR utiliza una base de datos llamada BCD (del inglés *Boot Configuration Data*, es decir, datos de configuración de arranque). Si el sistema tiene BIOS, la BCD estará en la carpeta *C:\boot*, mientras que si incorpora UEFI lo encontraremos en la ruta *\EFI\Microsoft\Boot* de la partición de sistema EFI.

Los datos almacenados en la BCD se utilizan para cargar el sistema operativo y los programas que se deben ejecutar en tiempo de arranque. En sistemas anteriores a Windows Vista, esta información reside en un archivo denominado *boot.ini*, que encontraremos en el directorio raíz de la partición activa.

Si bien BOOTMGR es el administrador de arranque, el verdadero cargador del sistema operativo es Winload, un programa que encontraremos en la ruta *C:\WINDOWS\system32*. Se trata, pues, de un sistema de arranque en dos etapas en el que BOOTMGR carga la configuración de la BCD y se la transfiere a *winload.efi* (UEFI) o *winload.exe* (BIOS), que finalmente llevará a cabo la carga efectiva de los controladores y del núcleo (*ntoskrnl.exe*) del sistema operativo.

En versiones anteriores a Windows Vista, el administrador de arranque se denomina NTLDR, y habitualmente lo hallamos en el directorio raíz de la partición activa junto a *ntdetect. com*, un programa complementario que detecta la información básica del hardware necesaria para que pueda arrancar Windows.

#### Para + info

Si el sistema está hibernado, será el programa *winresume.efi*  (UEFI) o *winresume.exe* (BIOS), y no Winload, el que realizará la carga de la imagen de memoria desde la unidad de almacenamiento y reanudará la ejecución el sistema.

### Atención

Utilizando la instrucción en línea *bcdedit*, dentro de una ventana de MS-DOS o de PowerShell en modo administrador, podemos ver los datos de configuración almacenados en la BCD correspondientes a ambos cargadores. También podemos usar esta herramienta para agregar, eliminar, editar y anexar entradas en el almacén de datos de la configuración de arranque, aunque existen herramientas de terceros, como EasyBCD, que permiten hacerlo de forma más sencilla en el entorno gráfico.

#### **Arranque de Linux**

En Linux, el cargador de arranque GRUB utiliza también una estrategia de carga multietapa que, en sistemas con BIOS, podemos resumir en los siguientes pasos:

- 1. Tras la fase POST, el BIOS localiza el MBR del dispositivo de arranque y le cede el control del sistema.
- 2. Se ejecuta la primera etapa de GRUB, contenida en los primeros 446 bytes del MBR, en el sector cero del disco. Este espacio no es suficiente para albergar GRUB en su totalidad, pero sí bastaría para cargar la etapa 2, donde encontraremos el grueso del gestor de arranque.

- 3. Sin embargo, dado que la etapa 2 se ubica en un sistema de archivos, y que el código de la etapa 1 únicamente puede manejar bloques de disco, en su lugar carga una etapa intermedia, denominada 1.5, para que sea este código el encargado de localizar y ejecutar la etapa 2 dentro de su sistema de archivos. La etapa 1.5 no tiene un tamaño estándar definido, y normalmente reside en el espacio que hay entre el sector 1 y el 63 del disco, que es donde, por razones históricas, empieza la primera partición.
- 4. La etapa 2 de GRUB muestra al usuario su menú de inicio.

En un disco con GPT, la tabla de particiones y la etapa 1 del cargador de arranque están en el sector 1, y además no es necesario que exista separación alguna entre el final de este bloque, situado en el sector 34, y el inicio de la primera partición. En consecuencia, no habría espacio para la etapa 1.5.

Este problema se resuelve creando una nueva partición, normalmente entre los sectores 34 y 2048 (es decir, en el primer MB del disco), denominada BBP (del inglés *BIOS Boot Partition*, o partición de arranque del BIOS), que es donde residirá la etapa 1.5 y que viene a ejercer el papel de la ESP en los discos GPT bajo BIOS.

![](_page_80_Diagram_3.jpeg)

*En un disco GPT no existe espacio para la etapa 1.5 de GRUB.*

En el caso de una UEFI, esta no necesita de programas externos para a) acceder a un sistema de archivos determinado, b) leer una tabla de particiones y c) ejecutar código. Así, la especificación UEFI contempla un gestor de arranque propio, llamado en inglés *UEFI Boot Manager.*  Se trata básicamente de un menú de arranque que se genera a partir de la información procedente de los discos conectados al sistema, y que se puede editar no solo desde el *firmware*, sino desde un sistema operativo en funcionamiento. En Linux, esto puede realizarse con una herramienta llamada Efibootmgr, pero bajo Windows existen también herramientas de terceros, como DiskGenius.

Cada entrada del menú de arranque UEFI almacena los siguientes datos:

- Nombre y tipo de dispositivo.
- Identificativo de disco, que incluye su fabricante, número de serie y tamaño.
- Partición activa.
- Ruta del gestor de arranque.

Como ya hemos visto, el administrador de arranque se instala en la partición de sistema o ESP. En el caso de Windows, lo encontramos en *\EFI\Microsoft\Boot\BOOTMGFW.EFI* y, de forma similar, en el caso de GRUB probablemente estará en *\EFI\sistema\grubx64.efi,* donde *sistema* es el nombre del sistema operativo que se tiene que cargar (por ejemplo, *opensuse* o *debian*).

![](_page_81_Diagram_1.jpeg)

*La BBP se ubica entre los sectores 34 y 2048 de un disco GPT bajo BIOS.* 

GRUB se configura ejecutando unos archivos y *scripts* ubicados en */etc/ grub.d,* y toma sus valores por defecto del archivo */etc/default/grub.*  La configuración generada de esta manera se almacena en */boot/grub/ grub.cfg,* y puede modificarse manualmente usando cualquier editor de textos. Aun así, el método recomendado para personalizar GRUB es editar los archivos arriba mencionados (por ejemplo, el archivo */ etc/grub.d/40\_custom* para añadir con la instrucción *menuentry* un nuevo sistema operativo como opción de arranque) y actualizar GRUB ejecutando la siguiente instrucción en un terminal:

#### sudo update-grub2

No obstante, el uso de una herramienta gráfica como GRUB Customizer nos puede facilitar mucho esta tarea.

Una vez hayamos seleccionado el sistema Linux que queremos cargar con GRUB, se carga en memoria el archivo *initramfs* (por *Initial RAM Filesystem*, es decir, sistema de archivos RAM inicial), que es el primer sistema de archivos raíz al que tiene acceso el sistema operativo.

*Initramfs* reside en el núcleo, y se utiliza principalmente para montar el auténtico sistema de archivos raíz donde residen los datos. Entre otras cosas, esto hace posible cargar módulos que no hayan sido compilados dentro del núcleo, lo cual a su vez permite utilizar ciertos dispositivos en tiempo de arranque.

Por ejemplo, en el núcleo rara vez encontraremos módulos que den soporte a volúmenes lógicos (LVM), RAID por software, dispositivos SCSI, particiones cifradas o sistemas de archivos de red como NFS, entre otros. Dado que los módulos requeridos para la carga de estos dispositivos están en el directorio */lib/modules* del sistema de archivos raíz, y este todavía no se ha montado, sería imposible su carga sin la asistencia de *initramfs*. Para montar dicha partición raíz se utiliza un disco RAM, *initrd.img,* que contiene los módulos requeridos para realizar esta operación.

En cuanto al archivo que contiene el núcleo, este recibe el nombre de *vmlinuz*, y es un ejecutable comprimido y *arrancable*. Como el resto de los archivos esenciales para el arranque de Linux, se halla en el directorio /*boot*, y normalmente su nombre incluye información acerca del número de versión (por ejemplo, *vmlinuz-5.10.0-21-amd*).

![](_page_83_Picture_1.jpeg)

#### **Montaje del sistema de archivos**

Si bien, bajo Windows, los volúmenes compatibles con el sistema se montan automáticamente cuando un dispositivo de almacenamiento se conecta al ordenador, en Linux es necesario hacerlo manualmente utilizando la orden *mount -t* seguida del tipo de sistema, del dispositivo físico donde reside el sistema de archivos, y del punto de montaje (directorio) bajo el que encontraremos todos los archivos; por ejemplo:

sudo mount -t ntfs /dev/hda2 /windows

Con esta orden montaremos un sistema de archivos ubicado en la partición *hda2* dentro de un directorio llamado *windows* (que debe existir previamente). Para desmontarla, utilizaremos la instrucción *umount:*

umount /windows

Además, podemos crear un sistema de archivos nuevo en cualquiera de nuestros dispositivos externos o particiones de disco, lo cual equivale a formatearlos. Para ello usaremos la instrucción *mkfs*:

mkfs -t reiserfs /dev/sda2

Esta orden crea un sistema de archivos Reiser en la partición *sda2.*
