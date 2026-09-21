# **8.1.4. Windows PowerShell**

![](_page_238_Picture_3.jpeg)

Algunas de las características clave de PowerShell son las siguientes:

- **Ejecución de órdenes**: permite ejecutar utilidades del sistema, *cmdlets* de PowerShell (complementos especializados) y programas externos desde su interfaz de línea de órdenes (CLI).
- *Scripting*: permite escribir secuencias de instrucciones para automatizar tareas complejas y repetitivas. Los guiones se guardan en forma de archivos de texto sin formato con extensión *.ps1.*
- **Variables**: puede utilizar variables para almacenar datos. Para asignar el valor a las variables se utiliza el operador =, y para representarlas, el símbolo \$. A diferencia de otros lenguajes de *shell,*  como Bash, a la hora de nombrar las variables no se distingue entre mayúsculas y minúsculas.
- **Estructuras de control**: proporciona estructuras condicionales (*if*-*else*) para la toma de decisiones, bucles (*for, while*) para la repetición de acciones, y sentencias *switch* para el manejo de casos.

**Windows PowerShell** es un potente y versátil *shell* de línea de órdenes y lenguaje de *scripting* desarrollado por Microsoft para la administración y automatización de Windows.

Uno de los aspectos diferenciadores de PowerShell es que está orientado a objetos, ya que tanto las variables como la salida de las instrucciones se representan como objetos .NET. Esta característica facilita la ejecución de tareas complejas, al simplificar, entre otras cosas, la manipulación y el filtrado de datos.

- • **Tuberías**: al igual que en Bash, la barra vertical (|) puede usarse en PowerShell para "entubar" la salida de una orden como entrada de otra.
- **Redirección de E/S**: PowerShell también soporta la redirección de entras y salidas; por ejemplo, podemos realizar la entrada a una orden desde un archivo utilizando el signo <, redirigir la salida de dicha orden a un nuevo archivo mediante el signo >, o anexarla a un archivo existente con >>. Además, soporta la redirección de errores mediante 2> y 2>>.
- *Cmdlets*: son órdenes de propósito único, es decir, especializadas en la ejecución de tareas concretas, y cuya nomenclatura sigue una convención basada en el uso de un verbo y un sustantivo, como *Set*-*Item* (definir ítem) o *Start-Service* (iniciar servicio).
- **Módulos**: son colecciones de *scripts*, *cmdlets* y otros recursos que permiten ampliar las funciones de PowerShell.
- **Administración remota**: permite gestionar servidores, el Directorio Activo, Exchange y otros sistemas mediante sus funciones integradas de administración remota.

#### **¿Qué es una tubería en Bash?**

- a) Un elemento que permite asignar la salida de una orden a una variable.
- b) Un elemento que permite redirigir la salida de una orden a un archivo.
- c) Conecta la salida de una orden con la entrada de otra.
- d) Bash no soporta el uso de tuberías.
