# **3.4.4. Estructura de directorios del sistema**

![](_page_83_Picture_17.jpeg)

Los directorios no son únicamente un sistema que permite a los usuarios organizar sus archivos para que sean más fáciles de encontrar, sino que facilitan las tareas administrativas relativas al sistema operativo, ya que, tanto Windows como Linux, poseen una estructura de directorios predefinida donde encontrar los archivos del sistema según su tipo y cometido.

Los archivos almacenados en un volumen de disco pueden organizarse, al igual que sucede con los documentos de una oficina, dentro carpetas denominadas **directorios**. Así, un directorio es una estructura de datos jerárquica que puede contener archivos u otros directorios, denominados subdirectorios. El *camino* de directorio y subdirectorios que se debe seguir hasta llegar a un determinado archivo se denomina ruta (*path* en inglés), y cada ruta debe ser única, es decir, no puede haber dos subdirectorios con el mismo nombre dentro de un directorio.

#### **Estructura de directorios de Windows**

Windows asigna una letra de unidad a cada volumen que se conecte al sistema y que esté formateado con un sistema de archivos compatible. La unidad donde se instala el sistema se denomina C, y la raíz de su árbol de directorios es C:\.

En un sistema con lector óptico, este será normalmente la unidad D, por lo que el resto de las unidades (discos duros, SSD, etc.) irán recibiendo sus letras, en orden alfabético, a partir de la E. No obstante, mediante las herramientas de administración de discos podemos cambiar las letras de unidad según nuestras necesidades.

Dentro de C:\, Windows crea una serie de carpetas esenciales:

- **Program Files y Archivos de programa (x86)**: en estas carpetas se instala, por defecto, todo el software de aplicación y archivos relacionados.
- **Usuarios**: contiene las carpetas personales de los usuarios, en las que se almacenan documentos, configuraciones, o software solo accesible para algún usuario en particular.
- **ProgramData**: carpeta oculta en la que los programas pueden guardar información de todo tipo (cachés, preferencias, archivos de registro…), y que son de aplicación global.
- **Windows**: directorio donde se guardan todos los archivos y bibliotecas imprescindibles para el funcionamiento del sistema. En él tenemos, como directorios más destacados, los siguientes:
  - **System32**: directorio principal de Windows donde se ubican todas las bibliotecas y ejecutables esenciales del sistema. En sistemas x64, y a pesar de su nombre, esta carpeta contiene las bibliotecas de 64 bits.
  - **SysWOW64**: contrariamente a lo que parece indicar su nombre, es en esta carpeta donde, en sistemas de 64 bits, encontraremos todas las bibliotecas y ejecutables responsables de preservar la compatibilidad con el software de 32 bits.
  - **WinSxS**: contiene versiones alternativas de bibliotecas para incrementar la compatibilidad con el software antiguo.

#### **Estructura de directorios de Linux**

La estructura del sistema de archivos de Linux empieza en el directorio raíz, que se expresa, simplemente, mediante una barra (*/*). A partir de aquí, existen una serie de directorios que convencionalmente se utilizan para almacenar ciertos archivos de sistema, pero pueden diferir según la distribución en algunas rutas igualmente importantes.

Para intentar adoptar un punto de vista más neutral y todo lo estándar posible, utilizaremos la estructura propuesta por freedesktop.org para sistemas basados en el uso de systemd:

- **/boot**: contiene los archivos que se utilizan para realizar el arranque del sistema.
- **/etc**: contiene las configuraciones del sistema, los servicios y las aplicaciones para todas las cuentas de usuario.
- **/home**: contiene las carpetas personales de los usuarios, donde estos almacenan sus documentos y configuraciones específicas para cada programa. Cada carpeta personal contiene, a su vez, una estructura de subdirectorios, entre los que se cuentan:
  - **~/.cache**: memoria caché de cada usuario.
  - **~/.config**: configuraciones personales de las aplicaciones.
  - **~/.local/bin**: programas que solo puede lanzar ese usuario en particular.
  - **~/.local/share**: recursos compartidos por las diversas aplicaciones del usuario.
- **/root**: carpeta personal del usuario superadministrador.
- **/srv**: se nutre de todos los datos que el sistema comparte con el exterior, bien mediante servicios web como Apache, o mediante sistemas de archivos en red como NFS.
- **/tmp y /run**: ubicaciones donde se guardan los archivos temporales generados por diferentes procesos (datos de ejecución), y que el sistema purga en cada arranque. El directorio */var/run* es un enlace *a /run,* y tiene por finalidad preservar la compatibilidad con algunos programas antiguos.
- **/usr**: almacena el conjunto de paquetes proporcionado por la organización que hubiera creado la distribución:
  - **/usr/bin**: contiene los archivos ejecutables. Los directorios */bin, /sbin* y */usr/sbin* son meros enlaces simbólicos a este directorio.
  - **/usr/lib**: contiene un conjunto de bibliotecas y herramientas que utilizan otros programas. El directorio */lib* es también un enlace para compatibilidad.

- **/usr/share**: recursos compartidos para los programas a nivel de sistema (imágenes, documentos, plantillas, etc.).
- **/var**: almacena datos de ejecución persistentes, como pueden ser una base de datos:
  - **/var/cache**: alberga la memoria caché a nivel de sistema.
  - **/var/lib**: conjunto de bibliotecas que utiliza el sistema.
  - **/var/log**: almacena los archivos de registro del sistema.
  - **/var/spool**: en este directorio se ubican las colas de correo e impresión.
- **/dev**: contiene los dispositivos de hardware, de cuya gestión se encargan el demonio systemd-udevd y el propio núcleo del sistema.
- **/proc**: contiene información de los procesos administrados por el núcleo para facilitar su interacción con otros procesos.
- **/sys**: de naturaleza similar al anterior, este directorio contiene información sobre el núcleo que pueden utilizar otros procesos.
