# **3.2. Búsqueda de información del sistema. Comandos. Herramientas gráficas**

### Para + info

La búsqueda de información del sistema es un aspecto esencial en la administración de sistemas operativos. Todos los sistemas proporcionan una variedad de herramientas y comandos que permiten a los usuarios y administradores acceder a información crítica del sistema de manera eficiente.

Los sistemas operativos proporcionan varias formas de acceder a la información del sistema:

- **Comandos de línea de comandos**: estos son especialmente útiles para los administradores de sistemas y usuarios avanzados que requieren un acceso rápido y detallado a la información del sistema. Los comandos permiten extraer información específica y a menudo pueden combinarse con otros comandos para realizar tareas más complejas, como filtrar o redirigir la salida.
- **Herramientas gráficas**: son más accesibles para usuarios no técnicos y proporcionan una interfaz intuitiva para navegar y explorar la información del sistema. Las herramientas gráficas suelen ofrecer opciones de búsqueda, visualización de datos, y generación de informes de manera más visual y amigable.

#### **Comandos de línea de comandos en Windows 10**

- **Systeminfo**: este comando proporciona un resumen completo del sistema, incluyendo información sobre el sistema operativo, procesador, memoria RAM, tiempo de arranque, y más. Por ejemplo, abre una ventana de **PowerShell** o **símbolo del sistema** y escribe systeminfo. Obtendrás una lista detallada de la información del sistema.
- **Wmic**: el comando *Windows Management Instrumentation Command-line* (WMIC) permite acceder a una amplia gama de información del sistema, desde datos del BIOS hasta detalles de los discos duros. Por ejemplo, wmic cpu get name,NumberOfCores muestra el nombre del procesador y el número de núcleos. Y wmic bios get serialnumber muestra el número de serie del BIOS.

- **Get-WmiObject**: este comando de PowerShell es muy potente para obtener información detallada del sistema mediante consultas a WMI (Windows Management Instrumentation). Por ejemplo, Get-WmiObject -Class Win32\_OperatingSystem proporciona detalles sobre el sistema operativo.

#### **Herramientas gráficas en Windows 10**

- **Información del sistema** (msinfo32.exe): esta herramienta gráfica proporciona un resumen exhaustivo de la información del sistema, incluyendo el hardware, los componentes del sistema, y el software instalado.
  - **Cómo acceder**: escribe msinfo32 en la barra de búsqueda de Windows y selecciona *Información del sistema*. Aquí podrás navegar por las diferentes categorías de información.
- **Administrador de tareas**: proporciona información en tiempo real sobre el rendimiento del sistema, el uso de recursos, y los procesos en ejecución.
  - **Cómo acceder**: presiona Ctrl + Shift + Esc o haz clic derecho en la barra de tareas y selecciona *Administrador de tareas*. En la pestaña *Rendimiento*, puedes ver detalles del CPU, memoria, disco, red, y más.
- **Panel de control > sistema y seguridad > sistema**: proporciona información básica sobre el sistema, como la versión de Windows, el tipo de sistema (32 o 64 bits), la configuración de red, y la activación de Windows.
  - **Cómo acceder**: ve a *Panel de Control*, selecciona *Sistema y seguridad* y luego *Sistema*.

#### **Comandos de línea de comandos en Ubuntu**

- **uname**: este comando proporciona información básica sobre el sistema, como la versión del kernel y la arquitectura. Por ejemplo, uname -a muestra toda la información disponible, incluyendo el nombre del sistema, la versión del kernel, y la arquitectura de la CPU.
- **lshw**: List Hardware (lshw) es un comando poderoso para obtener información detallada sobre el hardware del sistema. Por ejemplo, sudo lshw -short proporciona un resumen de todo el hardware detectado en el sistema.

- **df**: este comando muestra el uso del disco para cada sistema de archivos montado. Por ejemplo, df -h muestra el uso del disco en un formato legible para humanos, con tamaños en GB o MB.
- **free**: muestra la cantidad de memoria libre y usada en el sistema. Por ejemplo, free -h proporciona un resumen del uso de la memoria en un formato más legible.
- **ifconfig o ip a**: estos comandos proporcionan información sobre la configuración de red del sistema. Por ejemplo: ifconfig muestra las interfaces de red activas y sus configuraciones. Y ip a también muestra las configuraciones de red y es el comando preferido en distribuciones modernas.

#### **Herramientas gráficas en Ubuntu**

- **Configuración del sistema**: proporciona una interfaz gráfica para ver y modificar la configuración del sistema, incluida la información sobre el hardware, la red, y las actualizaciones del sistema.
  - **Cómo acceder**: ve al menú de aplicaciones y selecciona *Configuración*. En la sección *Detalles* podrás ver información del dispositivo, como la cantidad de memoria, el tipo de procesador, y la versión de Ubuntu.
- **Monitor del sistema**: similar al **administrador de tareas** en Windows, esta herramienta gráfica muestra el uso de recursos en tiempo real, procesos en ejecución, y el rendimiento general del sistema.
  - **Cómo acceder**: ve al menú de aplicaciones y busca *Monitor del sistema*. Aquí puedes ver el uso de la CPU, memoria, disco, y red, así como gestionar los procesos.
- **Discos**: esta herramienta proporciona información detallada sobre los discos duros y las particiones.
  - **Cómo acceder**: busca *Discos* en el menú de aplicaciones. Desde aquí puedes ver detalles como el tamaño de las particiones, su tipo de sistema de archivos, y las opciones de configuración.

![](_page_64_Picture_4.jpeg)
