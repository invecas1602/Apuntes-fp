# **8.1. Tipos de lenguaje de** *script*

Dentro de la gran familia de los lenguajes de *script,* podemos trazar una línea clara entre los que se utilizan principalmente para codificar aplicaciones (**de programación**), y los que se emplean para administrar sistemas (**de intérprete de órdenes**).

Los lenguajes de *script* orientados a aplicaciones se dividen, a su vez, en dos grandes grupos: los **lenguajes de cliente**, y los **lenguajes de servidor**. El lado del cliente es donde el usuario interactúa con la aplicación, normalmente mediante una navegador web, mientras que el lado del servidor es donde se procesan las peticiones del cliente y se le devuelven las respuestas correspondientes.

La ejecución de código en el lado del cliente reduce la carga de trabajo de los servidores, pero requiere que el código sea compatible con las aplicaciones cliente y expone los datos confidenciales a un riesgo mayor, ya que dependen de mecanismos de seguridad fuera del control del servidor. Por otro lado, si es el servidor el que ejecuta el código, este puede adaptarse de forma dinámica a las preferencias o acciones del usuario en un entorno más seguro, pero las características del servidor y de su carga de trabajo pueden acabar por afectar al rendimiento de la aplicación.

Algunos de los lenguajes de *script* más utilizados en el lado del cliente son HTML, CSS y JavaScript. En el lado del servidor, podemos situar, entre los más extendidos, a los lenguajes PHP, Python y Java.

Los lenguajes de *script* para la administración de sistemas normalmente van asociados a un determinado **intérprete de órdenes** (en inglés, *shell*), por lo cual también reciben el nombre de lenguajes de órdenes o lenguajes de *shell*. Es el caso de PowerShell, un programa de administración y automatización desarrollado por Microsoft, inicialmente, para su familia de sistemas Windows, pero portado posteriormente a Linux y macOS bajo licencia de código abierto.

También en Linux, los diferentes intérpretes de órdenes suelen llevar aparejado su propio lenguaje de *shell*. En este sistema operativo, el *shell* por defecto, en la mayor parte de las distribuciones, es Bash, y su lenguaje de *script* difiere, en algunos aspectos, del de otros intérpretes de órdenes, como Zsh o Fish.

Las divergencias entre cada lenguaje de órdenes no se limitan a ciertos matices —como que los índices en las matrices de Zsh empiecen en 1, mientras que en Bash lo hagan en 0—, sino que pueden afectar a las **estructuras de lenguaje** y funciones disponibles en cada uno.

Por ejemplo, Zsh incorpora características como soporte para notación científica en su sintaxis, aliases globales, carga de extensiones (*plugins*), permite operaciones de coma flotante, y muchas otras.
