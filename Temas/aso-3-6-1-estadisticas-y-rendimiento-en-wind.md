# **3.6.1. Estadísticas y rendimiento en Windows**

En Windows contamos con dos herramientas gráficas que nos permiten monitorizar el sistema: el **Monitor de rendimiento** y el **Monitor de recursos**.

El Monitor de rendimiento (*perfmon.exe*) no solo cuenta con un visor gráfico que nos ofrece la información en tiempo real de multitud de contadores —que podemos incluir en el gráfico y activar o desactivar cuando nos interese—, sino que además puede generar informes de rendimiento mediante un recopilador de datos llamado *System Performance* (*Rendimiento del sistema*), que podemos encontrar en la carpeta *Conjuntos de recopiladores de datos > Sistema.*

El recopilador de rendimiento del sistema incluye un seguimiento de las trazas del núcleo de Windows, y un contador de rendimiento llamado *Performance Counter*, ambos configurables abriendo su diálogo de propiedades. Para generar un informe de rendimiento, haremos clic derecho sobre el recopilador y seleccionaremos *Iniciar* en el menú contextual. En los siguientes 60 segundos se registrarán los datos de rendimiento y seguimiento incluidos en el recopilador, y se mostrarán en *Informes* > *Sistema* > *System Performance*. Además, los resultados se almacenarán en *C:\PerfLogs*\*System*\*Performance*, generándose un informe llamado *report*.*html,* que se puede abrir con cualquier navegador web, y otro con el mismo nombre en formato XML.

![](_page_95_Picture_0.jpeg)

Con esta herramienta gráfica podemos crear conjuntos de recopiladores de datos personalizados en la carpeta *Conjuntos de recopiladores* de *datos > Definido por el usuario*, haciendo clic derecho sobre ella y escogiendo la opción *Nuevo* > *Conjunto de recopiladores de datos* del menú contextual. Se trata de un proceso guiado por un asistente en el que podemos utilizar una plantilla o bien crear un conjunto de forma manual. No obstante, existe también la posibilidad de crear contadores de rendimiento desde una ventana de Símbolo del sistema mediante la herramienta *logman*.*exe*.

Por ejemplo, podemos crear un conjunto de recopiladores de datos llamado *Rendimiento*-*Log* que monitorice la actividad de los discos físicos y lógicos, la memoria, las interfaces de red, el archivo de paginación y los procesos en intervalos de 5 minutos mediante la siguiente instrucción:

logman create counter Rendimiento-Log -f bincirc -v mmddhhmm -max 250 -c "\LogicalDisk(\*)\\*" "\Memory\\*" "\Network Interface(\*)\\*" "\Paging File(\*)\\*" "\PhysicalDisk(\*)\\*" "\Process(\*)\\*" "\Redirector\\*" "\Server\\*" "\System\\*" -si 00:05:00

Para mostrar la lista de los recolectores de datos configurados, así como su estado de ejecución, utilizamos la orden *logman query,* mientras que para iniciar la recopilación de datos, utilizaríamos la siguiente orden:

logman start Rendimiento-Log

Por último, si queremos eliminar un conjunto en particular, primero debemos detener la recolección de la siguiente forma:

logman stop Rendimiento-Log logman delete Rendimiento-Log

Por su parte, el Monitor de recursos (*resmon.exe*) nos ofrece, también en tiempo real, un conjunto predeterminado de información acerca del rendimiento general del sistema y de cuatro de sus indicadores de rendimiento más importantes: la CPU, la memoria, las operaciones de lectura y escritura de archivos y las comunicaciones de red.
