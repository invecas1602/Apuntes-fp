# **3.5.1. Información del sistema en Windows**

En Windows 11, podemos obtener los datos básicos del sistema a través de *Configuración > Sistema > Información* (o *Configuración > Sistema > Acerca de* en Windows 10 y Windows Server 2022). La información queda repartida en dos secciones: Especificaciones del dispositivo, donde veremos datos relativos al procesador, la memoria y el nombre e identificador del equipo, entre otros; y Especificaciones de Windows, donde figuran la edición, versión y compilación de Windows, así como su fecha de instalación.

Desde esta pantalla podemos acceder, a través de sus botones y enlaces, a los diálogos que nos permitirán ver y editar ciertos parámetros, como por ejemplo cambiar la clave del producto o comprobar su estado de activación. De entre estas posibilidades, hay una de especial importancia: la *Configuración avanzada* del sistema, desde donde podremos acceder a la lista de variables pulsando el botón *Variables de entorno.*

![](_page_90_Picture_3.jpeg)

El diálogo *Variables de entorno* muestra las variables que afectan al usuario activo y las variables de sistema, que son de aplicación global para todos los usuarios. En cada sección contamos con la posibilidad de crear, editar o eliminar variables.

*Propiedades del sistema de Windows.*

Es posible incluir distintos valores en una variable (como sucede, por ejemplo, con las variables *Path* y *PATHEXT*) separándolos sin espacios mediante un punto y coma.

Para + info

![](_page_90_Picture_7.jpeg)

En lo relativo al intérprete de órdenes, podemos usar Systeminfo en una ventana de Símbolo del sistema o de PowerShell para obtener información variada acerca del procesador, el uso de los recursos de memoria, los adaptadores de red, la instalación del sistema y las revisiones aplicadas. Si únicamente deseamos conocer la versión del sistema, podemos utilizar, en su lugar, Winver.

Por otra parte, con Path podemos ver las rutas de búsqueda añadidas en esta variable, o utilizarla para añadir una nueva ruta agregando *;%path%*:

### path d:\documentos;%path%

Por último, con la orden Wmic (del inglés *Windows Management Interface Command,* u orden de la interfaz de administración de Windows) podemos obtener numerosos datos acerca del sistema utilizando diversos parámetros. Por ejemplo, la orden *wmic bios* nos devolverá toda la información relacionada con el BIOS. Es posible filtrar ciertos atributos con la opción *get*; por ejemplo, *wmic bios get version* obtendremos el número de versión del BIOS.

Otros parámetros interesantes que podemos utilizar, de la misma forma, con Wmic son:

- **cpu**: muestra todos los datos relativos al procesador. Como en el caso de *bios*, podemos filtrar atributos con la opción *get*; por ejemplo, *wmic cpu get name, numberofcores, maxclockspeed* nos informará acerca del nombre, velocidad y número de núcleos de la CPU.

*Salida de Systemninfo en PowerShell.*

- **partition**: nos ofrece los datos en bruto acerca de las particiones detectadas en la unidad del sistema. Podemos una vez más filtrar ciertos atributos con *get;* por ejemplo, con *wmic partition get name, size, type* obtendremos un listado filtrado por nombre, tamaño (en bits) y tipo de partición.
