# **1.3. Componentes de un SGBD**

Aunque los componentes presentes en un SGBD pueden variar según el modelo de BD adoptado, los más utilizados son:

- **Lenguajes**: conjuntos de instrucciones cuya sintaxis nos permite definir y manipular los datos y los objetos presentes en la BD. Entre ellos, podemos distinguir:
  - **DDL**: el lenguaje de definición de datos (*Data Definition Language*) nos permite definir los objetos de la base de datos, así como sus estructura e interrelaciones.
  - **DCL**: el lenguaje de control de datos (*Data Control Language*) se encarga de la seguridad de los datos, incluyendo la gestión de los permisos de acceso y la concesión de privilegios sobre la BD.
  - **DML**: el lenguaje de manipulación de datos (*Data Manipulation Language*) es el que permite insertar, actualizar, eliminar y consultar los datos de la BD. El más extendido entre los SGBD relacionales es el SQL.
- **Diccionario de datos**: relación de todos los elementos presentes en la BD, que, en su forma más básica, consiste en una relación de tablas con sus correspondientes columnas, pero que normalmente incluye también metadatos como el tipo de columna, tamaño, procedencia, relaciones, condiciones y restricciones, utilización y una descripción de cada una de ellas.
- **Catálogo de sistema**: conjunto de tablas o vistas incluidos en el motor del SGBD, que permite el acceso a todos los metadatos de una BD, incluyendo información sobre tablas, guiones, registros de actividad y seguridad, y otros objetos presentes en la BD. El lenguaje SQL define un catálogo estándar llamado **information\_schema**, que contiene un conjunto predefinido de dichas tablas.
- **Objetos**: los diferentes objetos que podemos incluir en la BD (vistas, disparadores, secuencias, procedimientos almacenados, etc.).
- **Optimizador de consultas**: módulo dedicado a analizar las consultas y determinar la mejor estrategia para ejecutarlas, es decir, aquella que consuma una menor cantidad de tiempo y recursos del sistema.
- **Otras herramientas administrativas**: componentes de software que facilitan la realización de ciertas tareas administrativas, como la automatización de procesos, la gestión de diccionarios de datos y catálogos de sistema, la replicación, sincronización, migración o distribución de los datos, las copias de seguridad, el acceso compartido a la BD y la conexión con aplicaciones de terceros, entre otras.

![](_page_18_Picture_4.jpeg)
