# **3.7. Gestión del software instalado**

Tanto en Windows como en Linux podemos obtener información acerca de los programas instalados desde un emulador de terminal o desde el entorno gráfico.

#### **Gestión del software mediante órdenes**

En Windows disponemos de la ya conocida Wmic, que mediante la opción *product* nos presentará una lista de los programas instalados por Microsoft o por ciertos desarrolladores reconocidos. Para obtener una información más útil, es recomendable filtrar la lista por los atributos de nombre y versión:

### wmic product get name, version

Por otra parte, Microsoft está desarrollando una nueva herramienta para la gestión de paquetes de software llamada Windows Package Manager CLI, también conocida como Winget. Presentada oficialmente en mayo de 2020, Winget es un software que permite a los usuarios no solo comprobar qué programas tienen instalados desde la línea de órdenes, sino también instalar nuevos paquetes de programa, desinstalarlos y comprobar si existen nuevas versiones de los ya existentes, en cuyo caso es posible actualizarlos en una misma operación. Como *apt*  en Linux, admite la resolución de dependencias, por lo que resulta una opción muy práctica para gestionar el software en Windows.

![](_page_99_Picture_8.jpeg)

Podemos instalar Winget fácilmente, desde una ventana de PowerShell, mediante la siguiente instrucción:

Set-PSRepository -Name 'PSGallery' - InstallationPolicy Trusted Install-Script -Name winget-install -Force winget-install.ps1

En Linux podemos usar la opción *list* de *apt* para obtener un listado de los paquetes de software que tenemos instalados. Para que la salida de pantalla sea más manejable, podemos entubarla a la entrada de *less*, revisar el listado con el ratón, y regresar al emulador de terminal pulsando *q*:

sudo apt list --installed | less

#### Para + info

Winget está disponible para su descarga desde el repositorio GitHub de Microsoft, en el enlace siguiente:

http://bit.ly/3MwInqm

![](_page_99_Picture_15.jpeg)

Si tenemos instalados paquetes de Snap, para listarlos deberemos usar la orden *snap list.* Snap es un mecanismo de distribución de paquetes de software que incluye en el contenedor de la instalación el programa y todas sus dependencias. El sistema permite a los desarrolladores distribuir sus *snaps* mediante la web Snap Store, o directamente desde sus propios sitios web. De la gestión de este sistema se encarga el demonio snapd (*sudo apt install snapd*).

A continuación se incluye una tabla con las órdenes más comunes para todos estos gestores de paquetes:

|                     | Winget                    | Apt                          | Snap                         |
|---------------------|---------------------------|------------------------------|------------------------------|
| Instalar paquete    | install nombre_paquete    | install nombre_paquete       | install nombre_paquete       |
| Desinstalar paquete | uninstall nombre_paquete  | remove nombre_paquete        | remove nombre_paquete        |
| Actualizar fuentes  |                           | update                       |                              |
| Actualizar paquete  | upgrade nombre_paquete    | install --only-upgrade       |                              |
|                     |                           | nombre_paquete               | refresh nombre_paquete       |
| Actualizar todo     | -r, --all                 | upgrade                      | refresh                      |
| Buscar paquete      | search nombre_paquete     | search nombre_paquete        | find nombre_paquete          |
| Listar paquetes     | list                      | list                         | list                         |
| Exportar lista      | export lista_paquetes.txt | list > lista_paquetes.txt    | list > lista_paquetes.txt    |
| Importar lista      | import lista_paquetes.txt | install < lista_paquetes.txt | install < lista_paquetes.txt |
| Versión             | -v, --version             | -v, --version                | version                      |
| Ayuda               | -?, --help                | -h, --help                   | help --all                   |

![](_page_100_Figure_4.jpeg)

![](_page_100_Picture_5.jpeg)

#### **Gestión del software mediante herramientas gráficas**

La forma más sencilla de administrar el software instalado es, sin duda, utilizar el entono gráfico del sistema. Una vez más, en Linux se nos presenta una variedad de posibilidades relacionadas con cada distribución en particular. Por ejemplo, en Debian disponemos de una herramienta llamada simplemente *Software* que nos permite obtener información general acerca del propósito, versión, fuente y tamaño de los programas instalados, así como lanzarlos, actualizarlos o eliminarlos.

En Windows, podemos ir a *Configuración > Aplicaciones > Aplicaciones instaladas* para gestionar desde ahí el software del equipo, en concreto modificar los componentes del programa, si el instalador lo permite, o desinstalarlo. También podemos recurrir a la lista clásica de *Programas y características del* Panel de control*,* que cumple exactamente con las mismas funciones.

*Herramienta gráfica para la gestión del software en Debian.*

![](_page_102_Picture_1.jpeg)

#### **¿Qué función tiene la instrucción** *logman create counter perf\_log***?**

- a) Inicia el sistema de recopilación de datos de Windows.
- b) Crea un nuevo conjunto de recopiladores de datos llamado *perf\_log.*
- c) Crea un recopilador de datos de rendimiento llamado *counter*.
- d) Crea un contador de rendimiento basado en la plantilla *perf\_log.*
