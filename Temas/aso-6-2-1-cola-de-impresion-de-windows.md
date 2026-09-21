# **6.2.1. Cola de impresión de Windows**

El sistema de impresión integrado en Windows permite a los usuarios de la red compartir impresoras y gestionar sus trabajos de impresión. El servicio de impresión se denomina, simplemente, Spooler (*spoolsv. exe*), es decir, Cola de impresión, y es compatible con un amplio abanico de impresoras y con los protocolos SMB e IPP. También permite funciones de impresión avanzadas, como el enrutamiento y la priorización de los trabajos, así como la agrupación de impresoras.

Windows es capaz de gestionar cualquier impresora accesible por el servidor, tanto locales como de red, siempre que el controlador de impresora correspondiente esté instalado en el sistema.

Las **impresoras lógicas** son impresoras virtuales que representan una impresora física dentro del sistema de impresión. Suelen utilizarse para configurar colas de impresión compartidas por grupos de usuarios, así como para configurar los ajustes de los trabajos, o para dirigirlos a diferentes impresoras físicas en función de parámetros como la calidad de impresión, el formato del papel, etc. Esto permite satisfacer las necesidades de impresión de grupos de usuarios específicos, así como dirigir los trabajos a los dispositivos más adecuados según su naturaleza.

#### Para + info

Una vez configurada, el dispositivo de impresión es accesible mediante el panel *Impresoras y escáneres* de la *Configuración* del equipo, desde donde también es posible agregar nuevas impresoras mediante un asistente, utilizando varios métodos: en el Directorio Activo, por nombre de red, por su dirección IP, de forma inalámbrica o configurada de forma manual. La detección automática identifica impresoras WSD y TCP/IP, mientras que, para usar el protocolo IPP, tan solo es necesario agregar la dirección IP de una impresora compatible con este estándar.

El monitor de impresión permite gestionar los trabajos enviados por impresora, así como acceder a sus preferencias de impresión. En la cola de impresión veremos el nombre del documento y otros datos relacionados con el trabajo, como el número de páginas, el propietario y el estado de impresión.

Lógicamente, este sistema de impresión admite también el uso de directivas de grupo para gestionar las impresoras de forma centralizada, así como configurarlas para su utilización por parte de diferentes usuarios y máquinas dentro de una red local o de un dominio basado en Windows.
