# **6.4. Órdenes para la gestión de impresoras y trabajos**

Tanto en Windows como utilizando CUPS, podemos administrar el sistema de impresión desde el entorno gráfico. En el primer caso, empleamos para ello la consola de *Administración de impresión* y el monitor de cola de impresión de cada dispositivo, mientras que en CUPS utilizamos una interfaz web a la cual podemos acceder, desde cualquier navegador, mediante la dirección *http://localhost:631/admin.*

Ambas interfaces nos permiten realizar, de una forma cómoda e intuitiva, las tareas administrativas relativas a los trabajos y dispositivos de impresión como añadir, eliminar y agrupar impresoras, o pausar, cancelar o rechazar los trabajos.

#### **Gestión de impresoras y trabajos en Linux**

Para gestionar CUPS mediante el emulador de terminal, podemos utilizar las instrucciones *cupsctl* y *lpadmin.* La primera nos permite configurar los siguientes parámetros del servidor, que se almacenarán en el archivo de configuración *cupsd.conf*:

*Interfaz web de CUPS.*

Por ejemplo, para activar la administración remota y la compartición de impresoras en red, utilizaríamos la siguiente instrucción:

sudo cupsctl --remote-admin --remote-any --share-printers

Para mostrar la configuración actual, usamos la orden sin opciones.

En cuanto a *lpadmin,* nos permite configurar las impresoras y los grupos de impresoras o *clases.* Admite tres opciones básicas:

Por ejemplo, para hacer que la impresora *DCP-L3550CDW* sea la predeterminada, la instrucción quedaría como sigue:

sudo lpadmin -d DCP-L3550CDW

Opcionalmente, podemos utilizar opciones adicionales de la misma forma que en el caso de *cupsctl: -E* fuerza el uso del cifrado, *-U* especifica un usuario y *-h* apunta a la dirección del servidor. Por ejemplo:

sudo lpadmin -E -U jmartes -h 10.0.1.55:631 -x DCP-L3550CDW

Esta instrucción eliminará la impresora especificada, en el servidor ubicado en la IP 10.0.1.55, usando la cuenta *jmartes* y mediante una conexión cifrada.

Cuando utilizamos la opción *-p* para configurar una impresora o una clase, disponemos de un amplio conjunto de opciones adicionales. Entre las más importantes, se cuentan las siguientes:

| -E                     | Activa el cifrado en la conexión con el programador.                            |
|------------------------|---------------------------------------------------------------------------------|
| -U                     | Nombre de usuario para autenticarse en el programador.                          |
| -h                     | Servidor[:puerto]: especifica la dirección del servidor.                        |
| --[no-]debug-logging   | Activa/desactiva el registro de depuración en el archivo error_log              |
| --[no-]remote-admin    | Activa/desactiva la administración remota.                                      |
| --[no-]remote-any      | Activa/desactiva la impresión desde cualquier dirección, por ejemplo, Internet. |
| --[no-]share-printers  | Activa/desactiva el uso compartido de impresoras locales.                       |
| --[no-]user-cancel-any | Permite/impide a los usuarios cancelar trabajos propiedad de otros.             |

| -d impresora/clase | Especifica el nombre de la impresora o la clase predeterminadas. |
|--------------------|------------------------------------------------------------------|
| -p impresora/clase | Configura la impresora o la clase especificadas.                 |
| -x impresora/clase | Elimina la impresora o la clase especificada.                    |

De esta forma, para agregar una impresora usando *lpadmin*, ejecutaremos la siguiente secuencia:

- 1. Listamos los modelos disponibles para nuestra impresora (por ejemplo, los del fabricante Brother):

sudo lpinfo -m | grep -i 'Brother\*'

- 2. Listamos las URI y esquemas de URI soportados:

sudo lpinfo -v

- 3. Suponiendo que queramos llamar DCP-L3550CDW al nuevo destino o cola de impresión, la instrucción a utilizar podría ser parecida a la siguiente:

//10.0.1.125/ArchivosSMB /home/usuario/samba cifs username=usuario,password=contraseña,user 0 0 //10.0.1.125/ArchivosSMB /home/usuario/samba cifs username=usuario,password=contraseña,noauto,user 0 0

| -c clase                        | Añade la impresora a una clase (si no existe, se crea automáticamente).                    |
|---------------------------------|--------------------------------------------------------------------------------------------|
| -m modelo                       | Establece un archivo PPD estándar para la impresora ( lpinfo -m proporciona la lista       |
| -o job-k-limit=valor            | Límite de KB a imprimir por usuario.                                                       |
| -o job-page-limit=valor         | Límite de páginas por usuario (las páginas a doble cara cuentan como dos                   |
| -o job-quota-period=valor       | Periodo contable en segundos (86 400 segundos corresponden a un día).                      |
| -o name=valor                   | Establece una opción PPD para la impresora ( lpoptions -l muestra la lista de opciones).   |
| -o printer-is-shared=true false | Establece la impresora o clase como compartida o no compartida (supeditada a la            |
|                                 | configuración en cupsd.conf ). El valor por defecto es true (verdadero).                   |
| -r clase                        | Elimina la impresora especificada de una clase (si la clase queda vacía, se elimina).      |
| -v "URI"                        | Establece el atributo URI de la cola de impresión ( lpinfo -v muestra la lista de URI      |
| -D "descripción"                | Establece una descripción para la impresora o la clase.                                    |
| -E                              | Fuerza el uso del cifrado TLS cuando se utiliza antes de las opciones - d , - p y - x . En |
| -L "ubicación"                  | Establece la ubicación de la impresora o clase.                                            |

Para imprimir documentos desde el emulador de terminal podemos usar la orden *lp*, que admite diferentes opciones para configurar parámetros como el número de copias (*-n*), la prioridad del trabajo (*-q*), el destino (*-d*), una lista de páginas (*-P*), el tamaño de la página (*-o media*), la calidad de la impresión (*-o print-quality*), etc. Además, soporta las opciones específicas del controlador, que podemos obtener mediante la orden *lpoptions -p destino.*

Por ejemplo, la siguiente instrucción imprimiría dos copias del documento *carta.pdf* en orientación vertical y a doble cara en *DCP-L3550CDW*:

lp -d DCP-L3550CDW -n 2 -o sides=two-sided-long-edge carta.pdf

Para ver el estado de la cola de impresión, podemos usar la orden *lpstat,* que muestra el estado de las colas de impresión; por ejemplo:

3550CDW-31 jmartes 32768 mar 09 may 2023 16:10:42

El identificativo de los trabajos se adjunta al nombre de la cola, en este caso (*3550CDW-31*) el identificativo sería 31.

Para cancelar este trabajo, utilizaríamos la orden *cancel,* seguida de este número:

cancel 31

Y para cancelar todos los trabajos del mismo destino, empleamos la opción *-a* (si no especificamos un destino, se cancelarán todos los trabajos en todas las colas de impresión):

cancel -a 3550CDW

#### **Gestión de impresoras y trabajos en Windows**

En Windows, podemos limpiar la cola de impresión desde una ventana elevada de línea de instrucciones utilizando las siguientes órdenes:

*Salida de la orden lpoptions.*

net stop spooler del %systemroot%\System32\spool\printers\\* /Q net start spooler

También es posible gestionar los trabajos de impresión, de manera individual, utilizando PowerShell y un conjunto específico de *cdmlets*:

#### 1. Obtenemos la lista de trabajos en curso:

Get-PrintJob -PrinterName "nombre\_impresora"

#### 2. Eliminamos el trabajo con el *Id 1*:

Remove-PrintJob -PrinterName "nombre\_impresora" -ID 1

#### 3. También podemos poner en pausa un trabajo:

Suspend-PrintJob -PrinterName "nombre\_impresora" -ID 2

#### 4. O continuarlo:

Resume-PrintJob -PrinterName "nombre\_impresora" -ID 2

#### 5. Y, de esta forma, reiniciaríamos el trabajo con *Id 3*:

Restart-PrintJob -PrinterName "nombre\_impresora" -ID 3

Para agregar una nueva impresora podemos utilizar los siguientes *cdmlets*:

![](_page_177_Picture_15.jpeg)

#### 1. Obtenemos la lista de puertos configurados:

Get-printerport | Format-Table -Property Name,Description -AutoSize

#### 2. Obtenemos la lista de controladores instalados:

Get-PrinterDriver | Format-Table -AutoSize

#### 3. Añadimos la impresora utilizando el puerto y controlador apropiados:

![](_page_177_Picture_24.jpeg)

Add-Printer -Name "Impresora Local 1" -DriverName "Brother DCP-L3550CDW" -PortName "USB001"

O bien, si se trata de un recurso compartido, podemos usar su nombre en la red:

Add-Printer -ConnectionName \\nombre\_servidor\ nombre\_impresora

#### Para + info

En PowerShell disponemos de un conjunto de *cdmlets* cuyas funciones son similares a las proporcionadas por CUPS, y que se listan en la siguiente web:

https://bit.ly/3pl27DX
