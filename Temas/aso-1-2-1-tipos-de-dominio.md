# **1.2.1. Tipos de dominio**

Existen dos tipos fundamentales de dominio según su alcance:

- **Locales**: constan de un conjunto de equipos conectados a una red local, en la que todos los recursos se gestionan de forma centralizada para permitir el acceso a los usuarios y grupos del dominio según los privilegios que se les hayan asignado.
- **De Internet**: estructura jerárquica en la que se utiliza un sistema de nombres separados por puntos para determinar la ubicación de red (IP) de los equipos conectados a Internet, gracias a una base

El Directorio Activo no solo usa el sistema DNS para resolver nombres, sino también para definir su propio espacio de nombres mediante la aplicación de la misma serie de convenciones a los nombres de dominio. Además, utiliza la base de datos DNS para almacenar los roles de cada equipo, lo cual permite dirigir de la forma adecuada las peticiones de los equipos dentro del dominio.

### Para + info

En un grupo de trabajo, cada ordenador conserva su propia configuración de cuentas y grupos de usuarios, por lo que es posible que algunos equipos de un mismo grupo no puedan acceder a los recursos compartidos por otros equipos debido a sus restricciones de seguridad en particular.

#### Para + info

Un **dominio** es también un sistema de agrupación lógica de dispositivos en red, pero con dos diferencias fundamentales con respecto a los grupos de trabajo de Windows: está administrado por uno o varios servidores, y aglutina dispositivos que pueden estar conectados a redes distintas.

de datos almacenada en los servidores de nombres de dominio (DNS).

Cabe destacar que, dentro de un mismo dominio, y con independencia de si es local o de Internet, pueden utilizarse diversos protocolos de comunicaciones en función del tipo de información que se desee transmitir. Por ejemplo, para enviar correo podemos usar los protocolos POP3 e IMAP, mientras que para la transmisión de archivos resulta más adecuado el protocolo FTP y, para acceder a páginas web, es preceptivo utilizar los protocolos HTTP/HTTPS.
