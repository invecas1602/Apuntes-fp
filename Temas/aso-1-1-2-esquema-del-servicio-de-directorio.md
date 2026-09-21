# **1.1.2. Esquema del servicio de directorio**

El **esquema** de un servicio de directorio es lo que define las convenciones de nomenclatura, las clases de objetos y los atributos utilizados para identificar y gestionar los objetos del directorio.

En los servicios de directorio estructurados en forma de árbol, existe un directorio raíz en la parte superior de la jerarquía y ramas o subárboles por debajo. Los objetos del directorio se representan como nodos del árbol, y cada nodo tiene un nombre o identificador único basado en las convenciones de nomenclatura definidas en el propio esquema.

El esquema también contiene la definición de las clases de objetos que se usarán para representar los distintos tipos de recursos del directorio, así como los atributos asociados a cada una de dichas clases. De esta forma, las clases de objeto definen las propiedades y comportamientos de los objetos del directorio: atributos, relaciones con otros objetos, permisos de control de acceso, etc.

Cada tipo de servicio de directorio tiene una implementación particular de esquema. El esquema del servicio de Directorio Activo, por ejemplo, también se basa, como el LDAP, en una estructura arborescente, en la cual el directorio raíz se denomina *bosque* y cada rama representa un *dominio* dentro del bosque.

Por su parte, el también jerárquico eDirectory implementa un esquema de estructura plana basado en el espacio de nombres, en el que cada objeto tiene un DN único que incluye el nombre del objeto y su ubicación dentro de dicho espacio de nombres, siendo muchos de dichos objetos específicos del entorno NetWare de Novell.

#### Para + info

Originalmente desarrollado por Novell bajo el nombre de Novell Directory Services (NDS), el eDirectory es un servicio de directorio que cumple con las especificaciones de varios estándares abiertos, incluyendo la versión 3 del LDAP. Actualmente forma parte de la línea de productos NetIQ de CyberRes, una división de la multinacional de software británica Micro Focus.

http://bit.ly/3yV3LxN

![](_page_9_Picture_10.jpeg)
