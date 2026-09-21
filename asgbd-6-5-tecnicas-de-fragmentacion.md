# **6.5. Técnicas de fragmentación**

Las tablas de una BD pueden fragmentarse en tres formas distintas:

- **Horizontalmente**: dividimos las tablas en fragmentos compuestos por tuplas o filas de acuerdo a los valores de uno o más campos. Cada partición se almacena en un nodo distinto, y contiene una serie de filas únicas que comparten los mismos atributos o columnas de la tabla original.

Por ejemplo, en nuestra BD *filmoteca*, si los detalles de las películas producidas en los Estados Unidos tuvieran que ubicarse en un nodo específico, podríamos fragmentarla de manera horizontal mediante la creación de una nueva tabla, a partir de la tabla *películas*, de la manera siguiente:

1 CREATE TABLE eeuu AS

2 SELECT \* FROM películas

3 WHERE país = 'Estados Unidos';

Como resultado, obtendríamos la siguiente tabla:

| idPelícula   título |                                                                               | año   país                               | director |
|---------------------|-------------------------------------------------------------------------------|------------------------------------------|----------|
|                     | 1   Vértigo (De entre los muertos)   1958   Estados Unidos   Alfred Hitchcock |                                          |          |
|                     | 2   Bullet Train                                                              | 2022   Estados Unidos   David Leitch     |          |
|                     | 6   Salvar al soldado Ryan                                                    | 1998   Estados Unidos   Steven Spielberg |          |
|                     | 7   El fantasma del Paraíso                                                   | 1974   Estados Unidos   Brian De Palma   |          |
|                     | 8   The Whale                                                                 | 2022   Estados Unidos   Darren Aronofsky |          |

- **Verticalmente**: dividimos las tablas en fragmentos compuestos por columnas. Cada partición se almacena en un nodo distinto, y contiene un conjunto único de columnas, exceptuando las columnas clave, que son comunes a todos los fragmentos. Este tipo de fragmentación refuerza la privacidad de los datos.

Un ejemplo de fragmentación horizontal sería crear una tabla para los países, en la BD *filmoteca*, como se muestra a continuación:

1 CREATE TABLE países AS 2 SELECT idPelícula, país 3 FROM películas;

El resultado sería la siguiente tabla:

+------------+----------------+

| idPelícula | país |

+------------+----------------+

| 1 | Estados Unidos |

| 2 | Estados Unidos |

| 3 | Reino Unido |

| 4 | Reino Unido |

| 5 | Reino Unido |

| 6 | Estados Unidos |

| 7 | Estados Unidos |

| 8 | Estados Unidos |

+------------+----------------+

- **Híbridamente**: mezcla de la fragmentación vertical y horizontal, puede implementarse de dos formas, bien generando un conjunto de fragmentos horizontales, para después fragmentar verticalmente uno o más de estos fragmentos, o bien generando un conjunto de fragmentos verticales a partir de los cuales generar los fragmentos horizontales.
