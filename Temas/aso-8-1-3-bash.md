# **8.1.3. Bash**

![](_page_237_Picture_2.jpeg)

En la mayor parte de las distribuciones de Linux, así como en macOS, se utiliza Bash como *shell* por omisión. Entre sus características más importantes, se cuentan las siguientes:

- **Ejecución de instrucciones**: permite ejecutar órdenes, *scripts*  o archivos ejecutables escribiendo su nombre en la interfaz de línea de órdenes (en inglés, *Command-Line Interface,* CLI), siempre que su ruta esté recogida en la variable de entorno *PATH*.
- **Scripting**: incluye un lenguaje de *shell* que no solo permite realizar tareas complejas, sino también automatizarlas.
- **Variables**: podemos definir variables mediante el operador =, y acceder a sus valores utilizando el prefijo \$; por ejemplo, *a=1*  asigna el valor 1 a la variable *a*, y *\$a* representa dicho valor. Por otra parte, mantiene un conjunto de variables de entorno que almacenan información acerca de la configuración del sistema y de la ubicación de archivos y carpetas clave, como los ejecutables, los directorios personales y el directorio de trabajo actual.
- **Estructuras de control**: en Bash podemos usar bucles y sentencias condicionales para controlar el flujo de ejecución de los scripts, a través de instrucciones presentes en muchos otros lenguajes de programación, como *if*-*else* y *case* (condicionales), o *for* y *while* (bucles).
- **Sustitución de órdenes**: permite asignar la salida de una instrucción a una variable, o utilizarla como parte de otra instrucción.
- **Tuberías**: las tuberías (|) permiten conectar la salida de una orden como entrada de otra, y se utilizan para procesar datos complejos encadenando varias instrucciones.

**Bash** es una forma abreviada para *Bourne Again Shell*, en referencia a uno de los intérpretes de órdenes Unix clásicos (*sh*), del cual es una versión ampliada. Tanto intérprete de órdenes como lenguaje de *shell*, Bash proporciona una interfaz de línea de instrucciones (CLI) que permite a los administradores interactuar con un sistema operativo Linux, integrando características no solo del *shell* Bourne original, sino también de los *shells* C (*csh*) y Korn (*ksh*).

- **Redirección de E/S**: es posible redirigir la salida de una orden a un archivo usando el operador >, o agregarla al mismo archivo usando >>. De igual modo, se puede dirigir la salida de un archivo a la entrada de una orden utilizando <.
- **Tareas en segundo plano**: permite ejecutar procesos en segundo plano mediante el uso del símbolo &.
- **Autocompletar**: mediante el uso del tabulador, Bash puede completar nombres de archivos, órdenes y otros elementos, lo cual ahorra tiempo y minimiza los errores de escritura.
