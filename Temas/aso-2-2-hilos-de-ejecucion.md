# **2.2. Hilos de ejecución**

![](_page_40_Picture_5.jpeg)

Podemos ver los hilos como procesos ligeros que el sistema puede gestionar de manera independiente, pero que, a pesar de tener un identificador, un contador de programa y una pila propios, comparten el PCB de un mismo programa en ejecución. De este modo, los hilos comparten el mismo espacio de memoria que el proceso padre, teniendo acceso a las mismas estructuras de datos, variables y recursos que otros hilos dentro del mismo proceso, de tal forma que, cuando un hilo modifica alguno de estos recursos, el cambio afecta al resto de los hilos que forman parte de dicho proceso.

El empleo de múltiples hilos *o multithreading* es una técnica que, en general, tiende a mejorar el rendimiento de las aplicaciones, ya que permite ejecutar diferentes tareas en paralelo.

Un **hilo** (*thread* en inglés) es la unidad básica que utiliza el sistema operativo para asignar el uso del procesador. Consiste en una secuencia de instrucciones que puede ejecutarse independientemente de otras secuencias de instrucciones dentro de un mismo proceso. Si el proceso consta de un único hilo de ejecución —lo cual significa que nunca se ejecutan dos partes de un programa al mismo tiempo—, estamos ante un proceso monohilo; en el caso de que se ejecuten diferentes tareas en paralelo, se trata de un proceso de múltiples hilos, o multihilo.

![](_page_41_Picture_0.jpeg)
