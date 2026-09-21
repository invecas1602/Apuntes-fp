# **1.2.4. Estructura lógica del dominio**

Los datos que se almacenan en un sistema LDAP se organizan en estructuras jerárquicas llamadas árboles de información de directorios o DIT (*Directory Information Trees*). La información acerca de un dominio que, normalmente, podemos encontrar en un DIT LDAP es la siguiente:

- **Nombre de dominio**: el nombre del dominio es una cadena de caracteres arbitraria que, según el LDAP, corresponde a un atributo componente de dominio (*dc*) —no confundir con un controlador de dominio o DC—, indicado como *dc=nombre\_de\_dominio.*
- **Extensión**: la extensión de un dominio corresponde también a un atributo componente de dominio, y se añade, separada por un punto, tras el nombre de dominio; por ejemplo, .es, .com o .net, entre otras muchas. Se indica como *dc=es, dc=com,* etc.
- **Unidad organizativa de grupos**: contiene todas la unidades organizativas (*ou*) hijas que son grupos de usuarios y que se identifican con un nombre común (*cn*), por ejemplo, *cn=contabilidad.* Tradicionalmente, en LDAP se identifica como *ou=Group.*
- **Unidad organizativa de usuarios**: conjunto formado por todos los usuarios individuales del dominio, que son hijos de esta unidad organizativa y que se identifican unívocamente mediante su UID. En LDAP se suele indicar como *ou=People.*

Una técnica muy útil a la hora de diseñar un dominio es plantearlo gráficamente mediante una estructura arborescente donde cada rama

![](_page_16_Diagram_6.jpeg)

represente un elemento dentro del dominio. El diseño más elemental que podemos crear es el formado por los elementos ya mencionados: nombre y extensión del dominio, unidades organizativas de usuarios y grupos, y un usuario administrador como elemento obligatorio adicional, definido mediante su nombre común (*cn=admin,* por ejemplo):

En el caso del Directorio Activo, su estructura lógica se basa en dos conceptos fundamentales:

- **Árboles**: un árbol está compuesto por un conjunto de dominios con un espacio de nombres contiguo. Los dominios son las unidades administrativas básicas del DA, y constan de un cierto número de equipos definido por un administrador que, conectados en red, comparten una misma base de datos de directorio. El primer dominio creado se considera el dominio raíz, y es el padre de todos los dominios que cuelgan directamente de él. Se pueden ir añadiendo directorios a los árboles, creando una estructura de relaciones padre-hijo en la que los nombres se asignan según el sistema DNS con objeto de reflejar sus relaciones de dependencia. Entre las funciones administrativas principales de un dominio se incluyen:
  - Proporcionar identidades válidas en todos los equipos unidos al mismo bosque, almacenándolas de forma segura en sus controladores de dominio.
  - Proporcionar, a través de los DC, los servicios de autenticación y gestión de grupos, que se pueden usar para controlar el acceso a los recursos de la red.
  - Extender los servicios de autenticación a los usuarios de dominios ajenos a su propio bosque mediante el uso de diferentes tipos de confianza.
  - Replicar los datos necesarios para poder proporcionar servicios de dominio entre los DC, permitiendo su administración como si constituyeran una misma unidad.

Al igual que sucede en un directorio LDAP, los objetos que contiene cada dominio del AD pueden agruparse en unidades organizativas (OU, *Organizational Units*). Los objetos dentro de una OU pueden ser de cualquier tipo: usuarios, grupos, dispositivos, equipos e incluso otras OU. Cada unidad organizativa utiliza listas de control de acceso (ACL) para gestionar el control sobre los objetos, y tiene un propietario que controla cómo se delega la administración, cómo se aplica la directiva de grupo a los objetos de la unidad, la creación de nuevos subárboles y la delegación de la administración de las OU

dentro de dichos subárboles.

- **Bosques**: grupos de dos o más árboles de dominio cuyos espacios de nombres no son contiguos, pero que establecen relaciones de confianza transitivas bidireccionales y que comparten una estructura lógica común, un esquema de directorio (definiciones de clase y atributo), la configuración de directorios (información de la replicación y del sitio) y el catálogo global (capacidades de búsqueda en todo el bosque).

Entre los principales conceptos que manejamos en un bosque del AD, cabe destacar los siguientes:

- **Relaciones de confianza**: cada nuevo dominio en un bosque establece automáticamente una relación de confianza bidireccional entre él y su dominio primario o padre. Gracias a la naturaleza transitiva de esta relación, los subdominios que vayamos creando en el mismo árbol del nuevo dominio gozarán de la misma relación de confianza bidireccional, que fluirá de abajo arriba a través de toda la jerarquía de dominios. Dado que las solicitudes de autenticación viajan a través de esta ruta de relaciones de confianza, las cuentas de cualquier dominio del bosque se pueden autenticar en cualquier otro dominio del mismo bosque.
- **Esquema de directorio**: contiene las definiciones formales de cada clase de objeto que se puede crear en un bosque, y las de cada atributo que puede existir en un objeto del directorio.
- **Catálogo global (GC)**: permite a los usuarios y las aplicaciones buscar objetos en un árbol de dominios, dados uno o más atributos del objeto de destino, sin saber qué dominio los contiene y sin necesidad de un espacio de nombres extendido contiguo. El GC se genera automáticamente mediante el sistema de replicación

![](_page_18_Diagram_6.jpeg)

del AD, y contiene una copia de todos los objetos del directorio, pero solo con un número pequeño de sus atributos. Entre ellos se cuentan los más utilizados en las búsquedas (como los nombres de inicio de sesión o el apellido de un usuario), y los necesarios para localizar una réplica completa del objeto.
