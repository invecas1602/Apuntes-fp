# **1.4.1. Filtros de búsqueda**

![](_page_28_Picture_6.jpeg)

Para localizar la información que necesitamos dentro del directorio, tenemos a nuestra disposición una serie de filtros lógicos y de igualdad que podemos usar, en combinación con la orden *ldapsearch,* como criterios de búsqueda de entradas:

Los filtros de búsqueda tienen que ir entre paréntesis, y admiten el uso del carácter comodín \*. Por ejemplo, para listar todos los usuarios cuyo correo electrónico acabe en *@asir.local*, podríamos utilizar la siguiente instrucción:

ldapsearch -x -b "dc=asir,dc=local" "(mail=\*@asir.local)"

Para incluir dos condiciones en la misma búsqueda —por ejemplo que, además de acabar su correo en *@asir.local*, el nombre común del usuario empiece por Juan—, utilizaríamos la siguiente sintaxis:

ldapsearch -x -b "dc=asir,dc=local" "(&(mail=\*@asir.local) (cn=Juan\*))"

#### Para + info

En la siguiente web dedicada al LDAP se ofrece una explicación completa acerca de los diferentes filtros de búsqueda del protocolo:

http://bit.ly/3Zrm60b

![](_page_28_Picture_10.jpeg)

![](_page_29_Picture_1.jpeg)

Una vez familiarizados con los conceptos básicos del OpenLDAP y con su sistema de gestión mediante archivos LDIF, la administración de directorios utilizando herramientas gráficas, como las que proporciona nativamente el Directorio Activo, resulta relativamente sencilla.

La principal herramienta para administrar el AD es el Centro de Administración de Active Directory (CAAD) que, tras la instalación del servicio de directorio, encontraremos en *Inicio* > *Herramientas administrativas de Windows.*

Presente desde la versión Windows Server 2008 R2, el CAAD proporciona una interfaz fácil de utilizar para la gestión de algunos de los aspectos más importantes del AD. Alternativamente, podemos utilizar la tradicional herramienta *Usuarios y equipos de Active Directory*, que ofrece una funcionalidad parecida en un entorno más espartano aunque similar al resto de las consolas de administración clásicas de Windows Server, como la de directivas de grupo.

Algunas de las muchas tareas que el CAAD facilita a los administradores del AD incluyen las siguientes:

- Administrar equipos, grupos y cuentas de usuario.
- Gestionar unidades organizativas y contenedores.
- Administrar los permisos y el control de acceso del AD.
- Administrar las directivas de grupo.
- Gestionar las relaciones de confianza entre los dominios y los bos-

*El CAAD y la herramienta de Usuarios y equipos de Active Directory son las consolas de administración gráficas del Directorio Activo.*

ques del AD.

- Administrar de los servicios de federación del DA (ADFS).
- Gestión de los servicios de directorio ligero (LDS) del AD.

Adicionalmente, el CAAD permite utilizar secuencias de órdenes de PowerShell con el fin de automatizar tareas rutinarias o de realizar operaciones masivas con mayor grado de eficacia.

En el caso de Linux, los entornos gráficos de administración de directorio LDAP se limitan a unas pocas herramientas básicas, en su mayor parte desactualizadas, entre las que destaca phpLDAPadmin (PLA), que requiere de Apache y PHP para funcionar.

Sin embargo, si el servidor LDAP no es, a la vez, servidor web, puede resultar más conveniente el uso de Apache Directory Studio, un explorador LDAP de código abierto construido sobre la plataforma Eclipse Rich Client, disponible tanto para Linux como para Windows y macOS.

![](_page_30_Picture_6.jpeg)

Las características para la gestión de directorios LDAP que ofrece Apache Directory Studio son numerosas, incluyendo las siguientes:

- Navegación y búsqueda en directorios LDAP.
- Creación y edición de entradas y atributos de directorio.
- Gestión de elementos de esquema, incluyendo clases de objetos y atributos.

*Apache Directory Studio es una herramienta de gestión de directorios LDAP potente y versátil.*

- Exportación e importación de la información del directorio en varios formatos, incluyendo LDIF y CSV.
- Gestión de certificados y conexiones SSL.
- Soporte para múltiples servidores LDAP.
- Autenticación y autorización LDAP.
- Integración con Eclipse para el desarrollo de código Java compatible con LDAP.
