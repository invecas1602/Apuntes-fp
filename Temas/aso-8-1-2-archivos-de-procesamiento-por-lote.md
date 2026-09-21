# **8.1.2. Archivos de procesamiento por lotes**

Los archivos de procesamiento por lotes (o archivos *batch*) son una forma elemental de guion que permite almacenar y ejecutar conjuntos de instrucciones en el intérprete del sistema.

En Windows, por ejemplo, podemos utilizar uno de estos archivos, escritos en texto simple e identificados mediante la extensión BAT, para ejecutar una secuencia de órdenes en una ventana de Símbolo del sistema (*cmd.exe*).

Pese a que los archivos de procesamiento por lotes no cuentan con las características más avanzadas presentes, por lo general, en los lenguajes de *script*, sí incluyen algunas estructuras básicas, como variables, bucles, sentencias condicionales y de control de flujo, así como llamadas a otros archivos *batch*, a través de un conjunto limitado de instrucciones. Estas son algunas de las más utilizadas:

- **ECHO:** imprime un mensaje en la consola.

ECHO Hola, mundo.

- **REM:** añade un comentario en el archivo, que será ignorado por el intérprete de instrucciones (puede reemplazarse por ::).

REM Esto es un comentario. :: Esto es otro comentario.

- **SET:** crea o modifica una variable de entorno.

SET nombre\_variable=valor

- **IF:** ejecuta un bloque de instrucciones si se cumple determinada condición.

IF condición ( instrucción 1 instrucción 2 ... instrucción n

)

- **GOTO:** salta a una etiqueta (palabra precedida de :) dentro del archivo.

GOTO ETIQUETA

...

:ETIQUETA

- **FOR:** ejecuta una instrucción para cada elemento dentro de un conjunto.

FOR %%variable IN (conjunto) DO (

instrucción

)

- **CALL**: llama a otro archivo *batch* o a una etiqueta dentro del propio archivo.

CALL otro\_archivo.bat

- **PAUSE:** pausa la ejecución del archivo, a la espera de que se pulse una tecla.
- **CLS:** borra la pantalla.
- **EXIT:** finaliza la ejecución del archivo por lotes.
