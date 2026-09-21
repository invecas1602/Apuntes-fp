# **4.3. Programación en bases de datos**

### **4.3.1. Funciones y procedimientos**

Los procedimientos y las funciones son objetos de base de datos que se almacenan en el servidor para poderse ejecutar cuando se precise, por lo que reciben el nombre de rutinas almacenadas.

![](_page_101_Picture_4.jpeg)

### **Funciones**

Las funciones se crean con la sentencia *CREATE FUNCTION*, y esta acción requiere, al menos, del privilegio *CREATE ROUTINE*. A no ser que se desactive la variable de sistema *automatic\_sp\_privileges*, los usuarios con el privilegio para crear rutinas lo tienen también para modificarlas (*ALTER ROUTINE*) y ejecutarlas (*EXECUTE*).

La forma en la que trabajan las funciones es la siguiente: toman el valor de un parámetro, realizan una operación, y devuelven un resultado. En la sentencia *CREATE FUNCTION* se definen, tanto el nombre de la función, como los parámetros que tomará en consideración. Por ejemplo, en una función que calcule el área de un rectángulo, necesitaríamos como parámetros los valores de alto y de ancho:

CREATE FUNCTION área (alto DOUBLE, ancho DOUBLE)

A continuación, es obligatorio definir el tipo valor que se devolverá utilizando la cláusula *RETURNS*:

RETURNS DOUBLE DETERMINISTIC

Las **funciones** son programas que se incluyen en una expresión, y que devuelven un determinado valor en el momento en que dicha expresión se evalúa. Los **procedimientos**, en cambio, se invocan usando la sentencia *CALL*, y aunque no tienen un valor de retorno, pueden generar conjuntos de resultados y ver modificados sus parámetros de ejecución. Junto con los disparadores y los eventos, las rutinas forman parte del conjunto de programas almacenados en MySQL.

RETURN alto\*ancho;

Para ejecutar la función, la invocamos con *SELECT* y le pasamos, entre paréntesis, los parámetros requeridos:

SELECT área(5,4);

El resultado será el siguiente:

+------------+

| área(5,4) |

+------------+

| 20 |

+------------+

Los nombres asignados a las funciones creadas no pueden coincidir con el nombre de una función integrada en MySQL.

Para modificar o eliminar funciones creadas, utilizaremos las sentencias *ALTER FUNCTION* y *DROP FUNCTION*, respectivamente.

Por último, si queremos obtener un listado de todas las funciones almacenadas en una DB (por ejemplo, *filmoteca*), usaremos la siguiente sentencia:

SHOW FUNCTION STATUS WHERE db='filmoteca' \G;

### Para + info

Las sentencias para la creación, modificación y eliminación de funciones, se discuten con detalle en el manual en línea de MySQL.

- 1. *CREATE FUNCTION* (sección 13.1.17).
- 2. *ALTER FUNCTION* (sección 13.1.4).
- 3. *DROP FUNCTION* (sección 13.1.29).

![](_page_102_Picture_17.jpeg)

**1** bit.ly/3VAkeRo **2** bit.ly/3Hcmry8 **3** bit.ly/3VNIDmc

![](_page_102_Picture_21.jpeg)

![](_page_102_Picture_22.jpeg)

![](_page_102_Picture_23.jpeg)

### **Procedimientos**

A la hora de escribir un procedimiento, en general seguiremos los pasos que se detallan a continuación:

- 1. Definimos un carácter delimitador para nuestra rutina, como, por ejemplo, la barra vertical (|), para distinguir el final de la rutina de los delimitadores regulares incluidos en ella (;):

### delimiter |

- 2. Seguidamente, creamos el procedimiento utilizando la sentencia *CREATE PROCEDURE* (como en el caso de las funciones, requiere del permiso *CREATE ROUTINE*). En ella debemos indicar el nombre del procedimiento (en nuestro ejemplo, *conteo\_género*) y sus parámetros de entrada y salida. Suponiendo que el propósito de esta rutina sea el de contar el número de veces que aparece un determinado género en la vista *pelis* de nuestra BD *filmoteca*, el parámetro de entrada será el género (*gen*), y el de salida, un número entero (*recuento*):

CREATE PROCEDURE conteo\_género (IN gen CHAR(50), OUT recuento INT)

- 3. En tercer lugar, escribimos el cuerpo de la rutina. Este bloque debe empezar con *BEGIN* y acabar con *END*, seguido del carácter delimitador. Entre estas dos cláusulas, escribiremos nuestra consulta:

BEGIN SELECT COUNT(\*) INTO recuento FROM filmoteca.pelis WHERE género = gen; END|

- 4. Finalmente, restituimos el delimitador a su valor por omisión:

delimiter ;

Para ejecutar el procedimiento, debemos invocarlo con una sentencia *CALL*, indicando entre paréntesis los parámetros de entrada y las variables donde se almacenarán los valores de salida:

CALL conteo\_género ('Comedia', @recuento);

Podemos obtener el valor de la variable *@recuento* con *SELECT*:

El resultado debe ser el siguiente:

+-----------+ | @recuento | +-----------+ | 1 | +-----------+

Para modificar o eliminar procedimientos almacenados, emplearemos las sentencias *ALTER PROCEDURE* y *DROP PROCEDURE*, respectivamente.

Al igual que con las funciones, si queremos obtener una lista de los procedimientos almacenadas en una DB en particular (en nuestro caso, *filmoteca*), utilizaremos la siguiente sentencia:

SHOW PROCEDURE STATUS WHERE db='filmoteca' \G;

![](_page_104_Picture_6.jpeg)

### **4.3.2. Estructuras de control de flujo**

MySQL soporta un conjunto de estructuras de control de flujo que se pueden incluir en los programas almacenados: *IF*, *CASE*, *ITERA-TE*, *LEAVE*, *LOOP*, *WHILE* y *REPEAT*, además de *RETURN* en funciones almacenadas. La mayor parte de estas sentencias pueden albergar otras sentencias dentro de ellas, lo que hace que puedan contener otras estructuras de control anidadas.

#### Para + info

Las sentencias para la creación, modificación y eliminación de procedimientos, se abordan de forma detallada en el manual en línea de MySQL.

- 1. *CREATE PROCEDURE* (sección 13.1.17).
- 2. *ALTER PROCEDURE* (sección 13.1.7).
- 3. *DROP PROCEDURE* (sección 13.1.29).

**1** [bit.ly/3VAkeRo](https://bit.ly/3VAkeRo) **2** bit.ly/3VVYFLc **3** bit.ly/3VNIDmc

![](_page_104_Picture_11.jpeg)

![](_page_104_Picture_12.jpeg)

![](_page_104_Picture_13.jpeg)

En esta sección abordaremos las dos sentencias de control de flujo más utilizadas, *IF* y *CASE*. Se trata de estructuras condicionales en las que se evalúa si se cumple una determinada condición, y, en caso afirmativo, se ejecuta un bloque de sentencias.

### **La sentencia** *IF*

*IF* adopta la siguiente sintaxis:

IF condición THEN bloque\_de\_sentencias [ELSEIF condición THEN bloque\_de\_sentencias] ... [ELSE bloque\_de\_sentencias] END IF

Cuando la condición estipulada se cumple, se ejecuta la lista de sentencias a continuación del *THEN*. Si existe la cláusula *ELSEIF*, se evalúa a continuación de la misma forma. Si no se cumple ninguna de las condiciones, se ejecuta el bloque a continuación de la cláusula *ELSE*. Para ilustrar la aplicación de la sentencia *IF*, vamos a añadir una nueva columna, llamada puntuación, a nuestra tabla películas:

ALTER TABLE películas ADD COLUMN puntuación TEXT;

A continuación, actualizamos las puntuaciones de los títulos utilizando sentencias *UPDATE* como la siguiente:

1 UPDATE películas 2 SET puntuación = ('8') 3 WHERE título = 'Vértigo (De entre los muertos)';

Una vez actualizada la tabla, este podría ser el resultado:

SELECT idPelícula, título, puntuación FROM películas; +------------+----------------------------+-----------+ | idPelícula | título | puntuación | +------------+-----------------------------+-----------+ | 1 | Vértigo (De entre los muertos) | 8 | | 2 | Bullet Train | 6 | | 3 | Un pez llamado Wanda | 10 | | 4 | Lawrence de Arabia | 9 | | 5 | Horizonte Final | 9 | | 6 | Salvar al soldado Ryan | 8 | | 7 | El fantasma del Paraíso | 10 | +------------+-----------------------------+-----------+

Vamos a crear un procedimiento que, según la puntuación recibida, nos diga si la película es mediocre (menos de 7), notable (7 y 8) o sobresaliente (9 y 10):

 1 delimiter | 2 CREATE PROCEDURE calificación 3 (IN id INT, OUT calificación VARCHAR(15)) 4 BEGIN 5 DECLARE punt TEXT; 6 DECLARE punt\_dec DECIMAL; 7 SELECT puntuación INTO punt 8 FROM películas 9 WHERE idPelícula = id; 10 SET punt\_dec = CONVERT (punt, DECIMAL); 11 IF punt\_dec > 8 THEN 12 SET calificación = 'SOBRESALIENTE'; 13 ELSEIF punt\_dec <= 8 AND punt\_dec > 6 THEN 14 SET calificación = 'NOTABLE'; 15 ELSE 16 SET calificación = 'MEDIOCRE'; 17 END IF; 18 END| 19 delimiter ;

Podemos poner a prueba el procedimiento con las siguientes sentencias:

CALL calificación (1,@calificación);

SELECT @calificación;

+---------------+ | @calificación | +---------------+ | NOTABLE | +---------------+

Ponte a prueba

**¿Qué instrucción se usa, en SQL, para cambiar el carácter delimitador en una rutina?**

- a) character
- b) delimiter
- c) limiter
- d) create limiter

### **La sentencia** *CASE*

*CASE* admite dos sintaxis:

CASE valor\_case WHEN valor\_when THEN bloque\_de\_sentencias [WHEN valor\_when THEN bloque\_de\_sentencias] ... [ELSE bloque\_de\_sentencias] END CASE

CASE WHEN condición THEN bloque\_de\_sentencias [WHEN condición THEN bloque\_de\_sentencias] ... [ELSE bloque\_de\_sentencias] END CASE

En la primera sintaxis, se indica una expresión como valor de *CASE*, y se comprueba si dicho valor coincide con alguno de los especificados en las diferentes cláusulas *WHEN*, en cuyo caso se ejecutará el bloque de sentencias a continuación de *THEN*; en caso contrario, se ejecutan las sentencias a continuación de *ELSE*.

En la segunda sintaxis, se evalúan las expresiones indicadas en las diferentes cláusulas *WHEN*, y, si son verdaderas, se ejecuta el bloque de sentencias a continuación de *THEN*. Si ninguna de las condiciones se cumple, se ejecuta el bloque de sentencias a continuación de *ELSE*.

Podemos adaptar el procedimiento anteriormente creado para utilizar la sentencia *CASE* en lugar de *IF*. En este caso, emplearíamos la segunda sintaxis:

 1 delimiter | 2 CREATE PROCEDURE calificación\_case 3 (IN id INT, OUT calificación VARCHAR(15)) 4 BEGIN 5 DECLARE punt TEXT; 6 DECLARE punt\_dec DECIMAL; 7 SELECT puntuación INTO punt 8 FROM películas 9 WHERE idPelícula = id; 10 SET punt\_dec = CONVERT (punt, DECIMAL); 11 CASE 12 WHEN punt\_dec > 8 THEN 13 SET calificación = 'SOBRESALIENTE'; 14 WHEN punt\_dec <= 8 AND punt\_dec > 6 THEN 15 SET calificación = 'NOTABLE'; 16 ELSE 17 SET calificación = 'MEDIOCRE'; 18 END CASE; 19 END| 20 delimiter ;

Si probamos el procedimiento, obtendremos los mismos resultados que con el procedimiento basado en *IF*:

CALL calificación\_case (2,@calificación);

SELECT @calificación;

+---------------+

| @calificación |

+---------------+

| MEDIOCRE |

+---------------+

![](_page_108_Picture_8.jpeg)

#### Para + info

En la sección 13.6.5 del manual en línea de MySQL se abordan las sentencias de control de flujo:

[bit.ly/3VC3iKD](http://bit.ly/3VC3iKD)

![](_page_108_Picture_12.jpeg)

### **4.3.3. Disparadores**

![](_page_108_Picture_14.jpeg)

Los **disparadores** son objetos de la base de datos que están asociados a una tabla, y que se activan cuando dicha tabla experimenta un evento en particular. Los disparadores no pueden asociarse a tablas temporales o a vistas, y para crearlos se necesita, cuanto menos, del permiso *TRIGGER*.

La sentencia *CREATE TRIGGER* es la que se utiliza para crear disparadores, y requiere forzosamente de tres parámetros:

- **Nombre del disparador**: debe ser único dentro del esquema.
- **Momento de activación**: puede ser antes (*BEFORE*) o después (*AFTER*) del evento.

- **Evento de activación**: los disparadores pueden activarse cuando se inserte una fila en la tabla (*INSERT*), cuando se modifique una fila de la tabla (*UPDATE*) y cuando se elimine un registro de la tabla (*DELETE*).

Opcionalmente, es posible asociar un disparador con otro utilizando las cláusulas *FOLLOWS* o *PRECEDES*, seguido del nombre del disparador al que sigue o precede, según el caso.

Así pues, la sintaxis básica de la sentencia de creación de un disparador sería la siguiente:

CREATE TRIGGER nombre\_disparador [BEFORE | AFTER] [INSERT | UPDATE | DELETE] ON nombre\_tabla FOR EACH ROW [[FOLLOWS | PRECEDES] otro\_disparador] cuerpo\_disparador

Para probar los disparadores, añadimos una columna, llamada *favorita*, a nuestra tabla películas, cuyo valor podrá ser 0 o 1.

ALTER TABLE películas ADD COLUMN favorita BOOLEAN DEFAULT 0;

En primer lugar, crearemos un disparador para que nos muestre un mensaje de error si, cuando estemos insertando una nueva fila, el valor que queremos introducir como puntuación de la película está fuera del rango establecido:

 1 delimiter | 2 CREATE TRIGGER rango\_puntuación 3 BEFORE INSERT 4 ON películas FOR EACH ROW 5 BEGIN 6 IF (NEW.puntuación IS NOT NULL AND 7 NEW.puntuación NOT IN ('0','1','2','3','4','5', 8 '6','7','8','9','10')) THEN 9 SIGNAL SQLSTATE '50001' SET MESSAGE\_TEXT = 10 'La puntuación debe estar entre 0 y 10'; 11 END IF;12 END| 13 delimiter ;

Ahora vamos a crear un disparador para que, a continuación, se compruebe si el nuevo valor de puntuación es 9 o 10, y que, en caso afirmativo, se cambie el valor de la columna *favorita* a 1:

|    | 1 delimiter   2 CREATE TRIGGER favorita    |
|----|--------------------------------------------|
| 3  | BEFORE INSERT                              |
| 4  | ON películas FOR EACH ROW                  |
| 5  | FOLLOWS rango_puntuación                   |
| 6  | BEGIN                                      |
| 7  | IF (NEW.puntuación IN ( '9 ', '10 ')) THEN |
| 8  | SET NEW.favorita = '1 ';                   |
| 9  | END IF;                                    |
| 10 | END  11 delimiter ;                        |

Para comprobar el correcto funcionamiento de estos disparadores, ejecutamos las siguientes sentencias:

1 INSERT INTO películas(título,año,país,director, idGénero,puntuación) 2 VALUES 3 ('El sexto sentido','1999','Estados Unidos','M. Night Shyamalan','7','9'); 4 SELECT título, puntuación, favorita FROM películas;

Veremos cómo, automáticamente, se ha marcado como favorito el nuevo registro:

| título                             | puntuación   favorita |   |
|------------------------------------|-----------------------|---|
| Vértigo (De entre los muertos)   8 |                       | 0 |
| Bullet Train                       | 6                     | 0 |
| Un pez llamado Wanda               | 10                    | 0 |
| Lawrence de Arabia                 | 9                     | 0 |
| Horizonte Final                    | 9                     | 0 |
| Salvar al soldado Ryan             | 8                     | 0 |
| El fantasma del Paraíso            | 10                    | 0 |
| El sexto sentido                   | 9                     | 1 |

De igual forma, si intentamos introducir una puntuación no comprendida entre 0 y 10, se nos informará de que el valor está fuera de rango.

A partir de aquí, podemos crear, sin mucho esfuerzo, un nuevo disparador que actualice la columna favorita, de forma automática, cada vez que se actualice una puntuación:

 1 delimiter | 2 CREATE TRIGGER favorita\_update 3 BEFORE UPDATE 4 ON películas FOR EACH ROW 5 BEGIN 6 IF (NEW.puntuación IN ('9','10')) THEN 7 SET NEW.favorita = '1'; 8 ELSE 9 SET NEW.favorita = '0'; 10 END IF; 11 END| 12 delimiter ;

Para eliminar un disparador, utilizaremos la sentencia *DROP TRIGGER*.

![](_page_111_Picture_4.jpeg)

### Para + info

En el manual de MySQL encontraremos toda la información acerca de las sentencias para crear y eliminar disparadores.

- 1. Sintaxis y ejemplos de *CREATE TRIGGER* (25.3.1).
- 2. Sintaxis de *DROP TRIGGER* (13.1.34).

**1** [bit.ly/3uuJv3A](https://bit.ly/3uuJv3A) **2** [bit.ly/3UD2xQ1](https://bit.ly/3UD2xQ1)

![](_page_111_Picture_10.jpeg)

![](_page_111_Picture_11.jpeg)

Ponte a prueba

### **¿Qué función tiene la cláusula ELSE?**

- a) Precede a las sentencias que deben ejecutarse en caso de que se cumplan las condiciones de IF o de ELSEIF.
- b) Precede a las sentencias que deben ejecutarse en caso de que se cumplan las condiciones de IF o de CASE.
- c) Precede a las sentencias que deben ejecutarse en caso de que no se cumplan las condiciones especificadas dentro de un bloque condicional.

### **4.3.4. Eventos**

El Programador de eventos de MySQL permite ejecutar, a intervalos regulares, guiones compuestos por una serie de sentencias SQL. Lógicamente, esto nos permitirá programar también la ejecución de procedimientos almacenados, como veremos a continuación.

Supongamos que queremos ejecutar periódicamente la sentencia dinámica que elaboramos en la sección 4.2. Para ello, lo más práctico es crear un nuevo procedimiento:

 1 delimiter | 2 CREATE PROCEDURE registro\_leo() 3 BEGIN 4 SET @ruta\_archivo = 5 CONCAT('\'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/', 6 date\_format (NOW(),'%d-%m-%Y\_%H-%i-%s'),'\_actividad.log\''); 7 SET @consulta\_prep = CONCAT("SELECT \'ID\',\'USER\', 8 \'HOST\',\'DB\',\'COMMAND\',\'TIME\',\'STATE\' 9 UNION ALL 10 SELECT ID,USER,HOST,DB,COMMAND,TIME,STATE 11 FROM information\_schema.PROCESSLIST 12 WHERE USER=\'leonardo\' 13 INTO OUTFILE ",@ruta\_archivo, 14 " FIELDS TERMINATED BY \',\' 15 ENCLOSED BY \'\"\' 16 LINES TERMINATED BY \'\\n\' 17 "); 18 PREPARE sentencia\_prep FROM @consulta\_prep; 19 EXECUTE sentencia\_prep; 20 DEALLOCATE PREPARE sentencia\_prep; 21 END| 22 delimiter ;

De esta forma, podemos ejecutar manualmente la consulta mediante una sentencia *CALL*:

CALL registro\_leo();

Pero lo que nos interesa es que el procedimiento se ejecute automáticamente cada minuto, para lo cual vamos a crear un evento. Para definir un nuevo evento se utiliza la sentencia *CREATE EVENT*, y requiere del privilegio estático *EVENT*. En su forma más básica, la sentencia de creación de nuestro evento adoptaría la sintaxis siguiente:

CREATE EVENT registro\_leonardo ON SCHEDULE EVERY 1 MINUTE DO CALL registro\_leo();

Como vemos, la sentencia *CREATE EVENT* requiere de un nombre de evento (*registro\_leonardo*), una programación (*ON SCHEDULE*) —en nuestro caso, cada minuto (*EVERY 1 MINUTE*)— y las sentencias a ejecutar (a continuación de *DO*). Si queremos ejecutar un conjunto de sentencias, podemos también cambiar el delimitador con *delimiter* y encerrarlas en un bloque *BEGIN-END*, tal y como hemos visto en el apartado dedicado a los procedimientos.

Para modificar o eliminar eventos, se emplean las sentencias *ALTER EVENT* y *DROP EVENT*, respectivamente.

Por último, si queremos obtener un listado de todos los eventos programados en una DB (*filmoteca*), usaremos la siguiente sentencia:

SHOW EVENTS WHERE db='filmoteca' \G;

### **4.3.5. Manejo de excepciones**

Existen muchos escenarios en los que un programa almacenado puede experimentar un error o excepción, por lo que resulta importante la existencia de un mecanismo de manejo de excepciones que nos permita continuar con el programa o abortarlo, y ofrecer al usuario un mensaje de error que le oriente hacia la identificación del problema.

En MySQL, esto se consigue declarando en manejador de excepciones con la sentencia *DECLARE* ... *HANDLER*:

DECLARE acción HANDLER FOR condición [, condición] ... sentencia

Como acción, la sentencia acepta los siguientes valores:

- **CONTINUE**: continúa la ejecución del código del bloque *BEGIN-END*.
- **EXIT**: interrumpe la ejecución del bloque donde se declara el manejador.

### Para + info

Las sintaxis y parámetros de las sentencias para la creación, modificación y eliminación de eventos, se tratan en profundidad en el manual en línea de MySQL.

- 1. *CREATE EVENT* (sección 13.1.13).
- 2. *ALTER EVENT* (sección 13.1.3).
- 3. *DROP EVENT* (sección 13.1.25).

![](_page_113_Picture_7.jpeg)

**1** [bit.ly/3iFJwiH](https://bit.ly/3iFJwiH) **2** [bit.ly/3P4Pmq3](https://bit.ly/3P4Pmq3) **3** [bit.ly/3uspTNF](https://bit.ly/3uspTNF)

Como valor de la condición o condiciones que activarán el manejador, se aceptan los siguientes:

![](_page_114_Picture_2.jpeg)

- Un código de error de MySQL.
- Un valor *SQLSTATE* estándar.
- *SQLWARNING* , *NOTFOUND* o *SQLEXCEPTION*.

La sentencia puede ser única o un conjunto de ellas enmarcado en un bloque *BEGIN-END*.

### **4.3.6. Bibliotecas**

Las bibliotecas son colecciones de recursos orientados a los desarrolladores. En la mayor parte de las ocasiones, se trata de código reutilizable que ofrece soluciones a tareas comunes, y que evita al desarrollador el trabajo de programar estas funciones desde cero.

Los SGBD incluyen un conjunto de bibliotecas nativas, y también pueden implementar bibliotecas externas a través de extensiones o *plugins*. MySQL, por ejemplo, almacena sus bibliotecas en la carpeta *C:\Program Files\MySQL\MySQL Server 8.0\lib* en Windows, y en el directorio *lib* de Unix/Linux.

Un ejemplo de librería nativa para MySQL es la API C, llamada *libmysqlclient*, que proporciona acceso de bajo nivel al protocolo cliente/servidor y permite a los programas escritos en C acceder a las bases de datos.

![](_page_114_Picture_13.jpeg)

#### Para + info

La sentencia *DECLARE ... HANDLER* se aborda en la sección 13.6.7.2 del manual en línea de MySQL:

[bit.ly/3VCgSgJ](https://bit.ly/3VCgSgJ)

![](_page_114_Picture_8.jpeg)
