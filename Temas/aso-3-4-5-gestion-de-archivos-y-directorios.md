# **3.4.5. Gestión de archivos y directorios**

Aunque la forma más cómoda de trabajar con el sistema de archivos es mediante una aplicación gráfica, como el Explorador de archivos de Windows o Krusader, GNOME Files y Nemo bajo Linux, los administradores muchas veces tienen que trabajar sin acceso al servidor gráfico del sistema o en circunstancias donde conviene más usar un emulador de terminal para manejar los archivos y directorios mediante órdenes.

En el contexto de un intérprete de órdenes, existen algunos símbolos especiales y convenciones para el trabajo con archivos que, en su mayor parte, son comunes para Windows y Linux. Es el caso de los comodines, que se utilizan para reemplazar un carácter o conjunto de caracteres:

- **Asterisco (\*)**: reemplaza cualquier secuencia de caracteres; por ejemplo, con la orden *ls a\** obtendremos en Linux un listado de todos los archivos del directorio actual que empiecen por la letra *a*.
- **Interrogante (?)**: reemplaza a un único carácter; por ejemplo, *del nombre?.txt* eliminará en Windows todos los archivos con un nombre de 7 caracteres que empiecen por nombre, como *nombre1.txt*  o *nombre9.txt*, pero no *nombre99.txt*.

- **Corchetes []**: en Linux se usan para reemplazar a un único carácter por varias alternativas; por ejemplo, *ls [12]-usuario[ABC].\** podría mostrarnos una lista de archivos como *1-usuarioA.txt, 2-usuarioC. png y 1-usuarioB.log,* pero no *3.usuarioB.txt*, porque el número 3 no se incluye entre los caracteres que figuran entre los dos primeros corchetes.

Podemos combinar los comodines ? y \* para crear todo tipo de patrones de búsqueda, como por ejemplo *juan??10\*.\**, que incluye a todos los archivos que comiencen por juan, seguido de dos caracteres cualesquiera, a continuación de *10,* cualquier otra combinación de caracteres para completar el nombre del archivo, y cualquier extensión de archivo; por ejemplo: *juanAA10contabilidad.txt, juan\_010-lista. xls,* etc.

Para desplazarnos a un directorio utilizamos la instrucción *cd,* como *cd /home/juan* en Linux o *cd d:\documentos\ juan* en Windows. En ambos casos estamos indicando la ruta completa desde la raíz, que en Linux es / y en Windows es, en este caso, *D:\.* Como podemos observar, Linux usa una barra para referirse a los directorios, mientras que Windows usa una contrabarra.

También es posible desplazarse por los directorios usando una ruta relativa al directorio actual. Sabemos en qué directorio estamos porque figura en el indicador de instrucciones; por ejemplo:

### /home/juan>

### D:\documentos\juan>

Así, estando en el directorio */home/juan,* podemos ir a */home/juan/ dibujos* indicando la ruta completa, o simplemente ejecutando *cd dibujos.* Y lo mismo sucede bajo Windows.

![](_page_87_Picture_8.jpeg)

#### Para + info

En Linux podemos sustituir la ruta a nuestro directorio personal por el carácter ~, por lo tanto, ejecutar simplemente *cd* ~ sin tener que especificar la ruta completa.

Para desplazarnos al directorio superior, usamos dos puntos (..), separando los dos puntos de la instrucción en Linux (*cd ..*), o sin importar la separación en Windows (*cd..*). En el caso del directorio raíz, la norma es la misma: separar la instrucción en Linux (*cd /*), y con o sin separaciones en Windows (*cd\*).

#### **Órdenes básicas**

Existen muchas instrucciones que podemos ejecutar en una consola de texto (en Windows, por ejemplo, existen unas 280). Algunas están integradas en el intérprete de órdenes, y otras se proporcionan como archivos ejecutables independientes (es posible que haya que instalar los paquetes en Linux, dependiendo de la distribución instalada).

En la siguiente tabla podemos ver un resumen de las más utilizadas para la manipulación del sistema de archivos:
