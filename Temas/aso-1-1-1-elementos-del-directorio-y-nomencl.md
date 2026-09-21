# **1.1.1. Elementos del directorio y nomenclatura**

Un servicio de directorio suele constar de los siguientes tres elementos básicos:

- **Directorio**: repositorio central donde se deposita toda la información sobre los usuarios, ordenadores y el resto de los recursos de la red. Está estructurado de forma jerárquica para que la información quede organizada de manera lógica, a la par que significativa.

Podemos definir el **servicio de directorio** como una clase de software que nos permite almacenar y administrar toda la información referente a la estructura, los ordenadores, los usuarios y el resto de los recursos de una red, denominados *objetos*. Gracias al directorio, los administradores de red pueden gestionar, de forma centralizada, las comunicaciones y el acceso a dichos objetos entre los distintos elementos que forman parte de la red.

- **Agente**: elemento que responde a las solicitudes de los clientes y que se encarga de actualizar el directorio cuando se producen cambios. En definitiva, es el responsable de proporcionar acceso al directorio y de gestionar la información almacenada en él.
- **Clientes**: aplicaciones y servicios que ingresan al directorio, ya sea para recuperar información o con el fin de realizar cambios en él. Los usuarios utilizan aplicaciones cliente para acceder al directorio, pero también pueden hacerlo los equipos conectados a la red y una variedad de servicios de directorio.

Para identificar y poder localizar los diferentes objetos que pertenecen al directorio, es necesario asignarles un nombre único dentro del servicio. Para ello se emplea una nomenclatura estandarizada, es decir, un conjunto de convenciones que nos permiten localizar y administrar los recursos de la red de una forma más sencilla con independencia de la implementación específica del directorio que se haya realizado.

Por otra parte, la nomenclatura del directorio normalmente obedece a su estructura, de manera que cada nivel dentro de su jerarquía representa un aspecto o cualidad distinta del objeto nombrado, lo cual nos permite identificarlo con mayor facilidad, si cabe.

![](_page_8_Picture_4.jpeg)

En el caso de un servicio de directorio LDAP, un ejemplo de objeto del directorio podría ser: *cn=Pablo Barbero,ou=Ventas,dc=midominio,dc=es.*

Esta convención de nomenclatura obedece a la asignación al objeto de un conjunto de atributos o claves estándar, en el que *cn* significa *nombre común* (*common name* en inglés), *ou* es *unidad organizativa* (*organizational unit*) y *dc* significa *componente de dominio* (*domain component*).

De esta forma, a través de este nombre sabemos que el objeto corresponde a un usuario llamado Pablo Barbero, y que este pertenece al departamento de ventas de una organización cuyo dominio es *midominio.es.*
