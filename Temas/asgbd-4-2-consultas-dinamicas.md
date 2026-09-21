# **4.2. Consultas dinámicas**

![](_page_98_Picture_2.jpeg)

Las **consultas dinámicas** son una técnica de programación que permite crear consultas capaces de cambiar de una ejecución a otra sin intervención manual.

De esta forma, y mediante el uso de variables, las consultas se confeccionan en tiempo de ejecución basándose en los requerimientos de cada momento.

El lenguaje SQL soporta la ejecución de consultas dinámicas mediante las sentencias *PREPARE* y *EXECUTE*, mientras que, para definir las variables que utilizaran estas sentencias, empleamos *SET*.

![](_page_98_Picture_6.jpeg)

### Para + info

La sintaxis de la sentencia *SET* y todas sus opciones se detallan en la sección 13.7.6.1 del manual en línea de MySQL:

Los detalles acerca de las sentencias preparadas, así como las sentencias admitidas dentro de su sintaxis, se discuten con detalle en el apartado 13.5 de la guía:

[bit.ly/3H56aLj](http://bit.ly/3H56aLj)

![](_page_98_Picture_10.jpeg)

[bit.ly/3UtKlIo](http://bit.ly/3UtKlIo)

![](_page_98_Picture_13.jpeg)

Vamos a ver, a continuación, como se puede escribir una consulta dinámica que, al crear los archivos de registro, les añada la fecha y hora actuales, para evitar de esta forma el error que se produciría al intentar sobrescribir un registro existente.

![](_page_99_Picture_1.jpeg)

En primer lugar, definiremos las variables que se van a utilizar en la consulta dinámica. Es posible usar *CONCAT* para unir varias variables, o el resultado de funciones, en una sola cadena.

En nuestro caso, y para mayor claridad en el código, crearemos una variable que concatene la ruta y el nombre del archivo de registro a escribir (*@ruta\_archivo*), y la concatenaremos, a su vez, con la cadena de la consulta a ejecutar (*@consulta\_prep*):

 1 SET @ruta\_archivo = CONCAT('\'C:/ProgramData/MySQL/ MySQL Server 8.0/Uploads/', 2 date\_format (NOW(),'%d-%m-%Y\_%H-%i-%s'), 3 '\_actividad.log\''); 4 SET @consulta\_prep = CONCAT("SELECT \'ID\',\'USER\', 5 \'HOST\',\'DB\',\'COMMAND\',\'TIME\',\'STATE\' 6 UNION ALL 7 SELECT ID,USER,HOST,DB,COMMAND,TIME,STATE 8 FROM information\_schema.PROCESSLIST 9 WHERE USER=\'leonardo\' 10 INTO OUTFILE ",@ruta\_archivo, 11 " FIELDS TERMINATED BY \',\' 12 ENCLOSED BY \'\"\' 13 LINES TERMINATED BY \'\\n\' 14 ");

Para evitar errores de sintaxis, en la confección de las cadenas es necesario utilizar caracteres de escape (precedidos por \) para representar la contrabarra y las comillas simples y dobles. Podemos comprobar el contenido de cada variable mediante las sentencias siguientes:

SELECT @ruta\_archivo AS ruta\_archivo;

SELECT @consulta\_prep AS consulta\_prep;

Si la variable *@archivo* no se hubiera declarado, el valor de la variable *@consulta\_prep* será nulo.

Una vez declaradas las variables, lo único que nos queda es preparar la sentencia y ejecutarla:

PREPARE sentencia\_prep FROM @consulta\_prep;

Para ilustrar el uso de las sentencias SET, retomaremos el ejemplo de la sección 3.3.1, donde creábamos un archivo con formato CSV para monitorizar la actividad de un usuario.

**3.3.1.** *Monitorización de usuarios*

Es posible ejecutar sentencias preparadas mediante API clientes y conectores de MySQL, como el de Java (MySQL Connector/J) o el de .NET (MySQL Connector/NET). Las sentencias preparadas son de ámbito global —es decir, pueden ejecutarse desde diferentes rutinas almacenadas— y específicas de la sesión en la que se hubieran creado, por lo que, si esta se cierra, el servidor las desasigna automáticamente. No obstante, pueden desasignarse de forma manual; en nuestro ejemplo:

### DEALLOCATE PREPARE sentencia\_prep;

Para evitar que el rendimiento del servidor se vea afectado por demasiadas sentencias preparadas, podemos configurar un límite utilizando la variable del sistema *max\_prepared\_stmt\_count*. En consecuencia, si el valor de esta variable se establece en cero, no será posible preparar ninguna sentencia.

Ponte a prueba

**¿Cuál o cuáles de las siguientes sentencias dan soporte a la ejecución de consultas dinámicas en el lenguaje SQL?**

- a) PREPARE
- b) EXECUTE
- c) EXECUTE y SET
- d) PREPARE y EXECUTE

**¿Cuál de las siguientes opciones no es el nombre un intérprete de órdenes?**

- a) sh
- b) bash
- c) gawk
- d) fish
