# **5.2. Configuración y uso de RDS**

En la unidad 3 vimos el proceso de instalación de los Servicios de Escritorio remoto. En este punto, en nuestro dominio del Directorio Activo, además del rol de Controlador de dominio y otros posibles roles, como el de Servicios de archivos y de almacenamiento, deberemos tener ya instalados y configurados los roles de **Agente de conexión a Escritorio remoto**, **Acceso web a Escritorio remoto** y **Host de sesión de Escritorio remoto**. Podemos asignar estos roles a un mismo servidor o a diferentes servidores en función del tamaño y complejidad del dominio.

Para verificar que la configuración de partida es correcta, abre un navegador en cualquier equipo del dominio y carga la página de autenticación del acceso web de Escritorio remoto. Suponiendo que el FQDN del servidor sea *Servidor01.midominio.local*, la URL sería la siguiente:

#### https://Servidor01.midominio.local/RDWeb

Puedes reemplazar el nombre y dominio del servidor por su dirección IP, y utilizar como credenciales de acceso las de cualquier usuario del dominio. Una vez iniciada la sesión, verás las aplicaciones que, por defecto, se añadieron a la colección *QuickSessionCollection,* creada automáticamente durante la instalación de los Servicios de Escritorio remoto.

![](_page_137_Picture_6.jpeg)

Si no puedes acceder a esta página, repasa los apartados *1.3.1. Directorio Activo* y *4.3. Escritorio remoto,* y sigue las instrucciones que en ellos se dan para configurar tu entorno de la forma adecuada antes de continuar con el contenido de esta unidad.
