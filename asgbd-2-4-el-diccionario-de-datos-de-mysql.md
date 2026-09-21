# **2.4. El diccionario de datos de MySQL**

![](_page_48_Picture_2.jpeg)

A partir de su versión 8.0, la información sobre los objetos de base de datos de MySQL se almacena en un **diccionario de datos transaccional global** —incompatible con las versiones anteriores, donde los datos se almacenaban parcialmente en archivos de metadatos y en tablas de sistema no transaccionales—. Este cambio conlleva los siguientes beneficios:

- **Mayor simplicidad**, derivada de un esquema de diccionario de datos centralizado y la eliminación de los archivos de metadatos.
- **Mayor estabilidad**, derivada de un sistema de almacenamiento de datos transaccional.
- **Caché de objetos de diccionario** centralizado y uniforme.
- **Simplificación y mejora** de algunas tablas del *INFORMATION\_SCHEMA*.
- **Soporte para sentencias DDL** que combinan en una única operación las actualizaciones del diccionario de datos, las operaciones del motor de almacenamiento y el registro binario asociado a una operación DDL (lo que se conoce por *DDL atómico*).

Obviamente, todo ello se traduce también en importantes diferencias en el uso del diccionario de datos, como, por ejemplo, las siguientes:

- Las tablas del diccionario de datos ya no son visibles para las sentencias DML y DDL, por lo que no se pueden consultar ni modificar directamente. En su lugar, podemos utilizar las tablas correspondientes en el *INFORMATION\_SCHEMA*, que no son más que vistas de las tablas del diccionario de datos subyacentes.
- Por su parte, las tablas del *INFORMATION\_SCHEMA* guardan ahora una estrecha relación con el diccionario de datos, por lo que existen también cambios en la forma en que se utilizan; entre los más importantes, se cuentan los siguientes:
  - Ahora las estadísticas no se obtienen siempre del motor de almacenamiento, sino que, por defecto, se utiliza la información almacenada en una caché de tablas; no obstante, es posible revertir este comportamiento estableciendo en cero el valor de la variable de sistema *information\_schema\_stats\_expiry*. –Gracias a las vistas del *INFORMATION\_SCHEMA*, el optimizador de MySQL puede ahora utilizar índices en las tablas subyacentes del diccionario de datos.
  - Las instrucciones *mysqldump* y *mysqlpump* ya no vuelcan la base de datos del *INFORMATION\_SCHEMA*, aunque se incluya explícitamente en la instrucción.

Recordemos que el *INFORMATION\_SCHEMA* es una base de datos presente en cada instancia de MySQL, cuya misión es almacenar información sobre el resto de las BD mantenidas en el servidor.

Como tal, proporciona información como el nombre de las bases de datos y las tablas, los tipos de datos de las columnas y los privilegios de acceso de los usuarios.

Las tablas contenidas en el *INFORMATION\_SCHE-MA* son de solo lectura, es decir, no se pueden realizar operaciones de inserción, actualización o eliminación sobre ellas; se trata, en realidad, de vistas, por lo que no tienen archivos asociados ni permiten el uso de disparadores.

### Para + info

Dado que MySQL ofrece acceso a la información almacenada en las tablas del diccionario de datos a través de las tablas del *INFORMA-TION\_SCHEMA*, podemos acceder a ellas utilizando las cláusulas *SHOW* o *SELECT*; por ejemplo, para obtener un listado resumen de dichas tablas, usaríamos la sentencia siguiente:

SHOW TABLES FROM INFORMATION\_SCHEMA;

Por otra parte, para obtener un listado más detallado, en el que, además de los nombres de las tablas (ordenados alfabéticamente), se nos muestre su tipo, usaríamos la siguiente sentencia:

SELECT table\_name, table\_type FROM information\_schema.tables ORDER BY table\_name;

El uso de *SELECT* permite filtrar, ordenar, concatenar y transformar los resultados de las consultas realizadas al *INFORMATION\_SCHEMA*, por lo que, por lo general, resulta preferible a la cláusula *SHOW*.

![](_page_49_Picture_6.jpeg)

#### Para + info

En el capítulo 26 del manual en línea de MySQL 8.0 encontrarás una referencia completa de todas las tablas contenidas en el *INFORMATION\_SCHEMA*:

[bit.ly/3TrlIM2](https://bit.ly/3TrlIM2)

![](_page_49_Picture_10.jpeg)
