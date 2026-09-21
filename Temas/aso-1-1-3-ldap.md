# **1.1.3. LDAP**

![](_page_10_Picture_2.jpeg)

Desarrollado en la Universidad de Michigan hacia 1993 como sucesor de los protocolos DIXIE y DAS para el acceso a directorios X.500, el LDAP es un subconjunto de estándares contenidos en las especificaciones del propio estándar X.500 y diseñado específicamente para funcionar sobre la pila TCP/IP.

El principal foco de este protocolo es definir los métodos de acceso a los datos, y no la forma en la que estos se almacenan en el servidor. Proporciona para ello un conjunto de métodos de conexión y desconexión, de búsqueda y comparación de datos, y de edición de las entradas del directorio. También ofrece cifrado de las conexiones mediante el protocolo SSL, así como un sistema de autenticación segura basado en el uso de credenciales.

Los directorios se organizan en dos tipos de estructuras o topologías, lógica y física, siendo la una totalmente independiente de la otra:

- **Estructura física**: formada por las diferentes sedes donde pueden residir los controladores de dominio, lo cual es relevante en las búsquedas del directorio, las peticiones de servicio y las operaciones de autenticación en el inicio de sesión.
- **Estructura lógica**: para organizar y representar la información del directorio, el LDAP utiliza una estructura en forma de árbol, en la que los objetos se denominan *entradas*. Cada entrada tiene un nombre único basado en su posición en la jerarquía del directorio. Esta topología jerárquica recibe el nombre de DIT (del inglés *Directory Information Tree* o árbol de información de directorio). En ella, cada entrada de servicio de directorio o DSE (*Directory Service Entry*) es una rama del árbol que se relaciona con un objeto real (un usuario, un equipo) o lógico (parámetros). La entrada principal

El **LDAP** es un estándar diseñado para gestionar servicios de directorio con una larga tradición en el ámbito empresarial. Se trata de un protocolo ligero de tipo cliente-servidor para gestionar directorios usando una base de datos centralizada mediante el protocolo de red TCP/IP. Esta base de datos contiene la información de todos los recursos de la red, incluyendo usuarios, grupos, impresoras, directorios compartidos y cualquier otro nodo que interactúe con la red.

de la que cuelga el árbol es la *entrada raíz.*

Para distinguir la naturaleza de los objetos que forman el árbol se emplea un conjunto de atributos (formados por una clave y un valor) que pueden ser de tipo *normal* (los datos en sí) u *operacional* (permiten al servidor gestionar los datos). Las claves requeridas dependen de la norma bajo la cual se implemente el directorio; por ejemplo, según la norma X.509, entre los atributos más habituales encontraríamos los siguientes:

- *uid*: identificador de usuario.
- *cn*: nombre común.
- *o*: nombre de la organización.
- *ou*: nombre de la unidad organizativa.
- *dc*: componente de dominio.
- *street*: calle (primera línea de la dirección).
- **c**: país.
- **mail:** dirección de correo electrónico del usuario.
- **unstructuredname**: nombre de anfitrión.
- **unstructuredaddress**: dirección IP.

Como sabemos, todas las entradas del directorio están asociadas a un identificador único, denominado **nombre distintivo** o **dn** (*distinguished name*) y formado por una serie de atributos con formato de serie; por ejemplo *cn=Juan Redondo,ou=Contabilidad,o=Ilerna,c=España.* Normalmente el *dn* se normaliza eliminando los espacios después de las comas y los que rodean al signo igual y, aunque puede contener varios atributos *ou* y *dc*, solo se permite una instancia del resto.

El formato para el intercambio de datos que usa LDAP se denomina **LDIF**, por las siglas del inglés *Lightweight Data Interchange Format,* y permite la importación y exportación de datos mediante archivos de

![](_page_11_Picture_8.jpeg)

En el modelo cliente-servidor, los clientes envían peticiones al servidor y este les devuelve las respuestas. La naturaleza de estas peticiones puede ser diversa —acceso a almacenamiento en red, aplicaciones en línea, descargas, una impresora, etc.— pero, en cualquier caso, en este modelo el rol del servidor es siempre pasivo (espera la solicitud del cliente, la procesa y envía una respuesta de vuelta), mientras que el de los clientes es un papel activo (realizan las peticiones y procesan las respuestas).

#### Para + info

#### Para + info

El precursor del LDAP es el X.500, un protocolo de acceso a directorio desarrollado bajo la norma ISO/IEC 9594 que proporciona un método basado en el modelo OSI para implementar un directorio de usuarios en una organización, y que además permite su publicación a través de Internet.

texto simple.

#### **Funcionalidades y procedimientos**

![](_page_12_Picture_3.jpeg)

El LDAP proporciona una amplia gama de funcionalidades, entre las que se incluyen:

- **Autenticación**: el LDAP se utiliza normalmente para la autenticación de usuarios, pues las credenciales de inicio de sesión de un usuario se comparan con la entrada del usuario en el directorio.
- **Autorización**: el LDAP puede utilizarse para gestionar el acceso a los recursos de red, controlando qué usuarios y grupos tienen acceso a qué recursos.
- **Libreta de direcciones**: el LDAP también puede usarse para almacenar información de contacto y otros detalles sobre personas y organizaciones.
- **Aplicaciones habilitadas para directorios**: podemos emplear el LDAP para proporcionar una base de datos centralizada para aplicaciones habilitadas para directorios, como sistemas de correo electrónico y herramientas de colaboración.

| Operación | Traducción  | Descripción                                                                |
|-----------|-------------|----------------------------------------------------------------------------|
| Abandon   | Abandonar   | Cancela la última operación enviada al servidor.                           |
| Add       | Agregar     | Añade una entrada al directorio.                                           |
| Bind      | Enlazar     | Inicia una sesión nueva en el servidor.                                    |
| Compare   | Comparar    | Compara dos entradas del directorio según los criterios especificados.     |
| Delete    | Eliminar    | Borra una entrada del directorio.                                          |
| Extended  | Extendida   | Realiza una operación extendida.                                           |
| Rename    | Renombrar   | Cambia el nombre de una entrada del directorio.                            |
| Search    | Buscar      | Realiza una búsqueda en el directorio.                                     |
| Start TLS | Iniciar TLS | Utiliza la extensión de seguridad TLS para establecer una conexión segura. |
| Unbind    | Desenlazar  | Cerrar la sesión en el servidor.                                           |
