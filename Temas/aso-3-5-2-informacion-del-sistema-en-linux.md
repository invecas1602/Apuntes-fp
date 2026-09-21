# **3.5.2. Información del sistema en Linux**

En Linux existe una amplia variedad de métodos que nos permiten obtener información del sistema, y la mayor parte de ellos utiliza los archivos contenidos en */proc* para extraer la información requerida.

Una de las herramientas más prácticas para este cometido es *inxi,* capaz de generar informes completos acerca del hardware y el software del equipo. Una vez instalada, al ejecutar *inxi* desde un terminal, veremos la información más elemental correspondiente a la CPU, el núcleo y el almacenamiento de la máquina. No obstante, la verdadera potencia de *inxi* se desbloquea al utilizar sus numerosas opciones, de las que podremos obtener cumplida información ejecutando *inxi* -*h*. Por ejemplo, para obtener un listado de hardware más completo podemos ejecutar *inxi -b*.

*Información de particiones con Wmic.*

Otras combinaciones de opciones que resultan muy útiles son:

- **-d -m**: información sobre las unidades de almacenamiento y el uso de la memoria.
- **-n -I**: nos proporciona los datos del hardware de red y de las direcciones IP asignadas.

Por otra parte, la instrucción *uname* nos puede proporcionar también información mediante el uso de sus opciones. Por ejemplo, con *uname -r -v* obtendremos la versión del núcleo y la distribución a la que corresponde.

Particularmente útil si queremos conocer todos los detalles sobre el hardware del equipo es *lshw*, que deberemos ejecutar con *sudo* para obtener pleno acceso a los recursos en */proc*. Una vez instalada (*sudo apt install lshw*), podemos usarla para obtener una versión resumida y tabulada para impresión con la opción *-short*:

Dos variantes de esta instrucción son *lsusb*, que lista únicamente los dispositivos USB, y *lspci,* que muestra los dispositivos conectados al bus PCI. En estos casos, podemos obtener una información más detallada usando la opción *-v*:

sudo lsusb -v sudo lspci -v *Salida de lshw.*
