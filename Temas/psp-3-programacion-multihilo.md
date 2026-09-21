# 3. Programación multihilo

### 3.1. Elementos relacionados con la programación de hilos. Librerías y clases

- Clase Thread

|void start ()|Inicializa el hilo.|
|---|---|
|void run ()|Comienza la ejecución del hilo.|
|static Thread currentThread ()|Devuelve la referencia del hilo que se encuentra en ejecución.|
|long getId ()|Devuelve el identificador del hilo.|
|static void sleep (long milis)|El hilo se detiene durante el número de milisegundos especificado.|
|void interrupt ()|Interrumpe la ejecución del hilo.|

Para más información: [https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html](https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html)

### 3.2. Gestión de hilos

Un proceso es cualquier programa en ejecución y es totalmente independiente de otros procesos. Un proceso puede tener varios hilos de ejecución que realizarán subtareas del proceso principal que los ha creado.

Un hilo es un conjunto de tareas que se ejecutan por el Sistema Operativo. También se denominan hebras o subprocesos.

Los hilos contienen información propia, como, por ejemplo, su identificador y toda aquella información que sea necesaria para que la aplicación pueda comunicarse con el sistema, es decir, el contador del programa, la pila de ejecución y el estado de la CPU.

Mientras que los procesos se caracterizan por no compartir la memoria con la que trabajan y ser independientes entre ellos, lo hilos no son iguales. Estos últimos suelen compartir la memoria con la que trabajan, puesto que pertenecen al mismo proceso.

Un ejemplo que puede ayudar a entender este concepto es un navegador web. El navegador web es un proceso con un identificador. Dentro de ese navegador es posible crear diferentes pestañas que comparten la memoria.

Cuando un hilo modifica un dato en la memoria, el resto de hilos del proceso pueden obtener este valor modificado.

El uso de hilos en lugar de procesos tiene bastantes ventajas, entre las que se destacan dos:

- La creación de un hilo tiene un coste menor que la creación de un proceso, puesto que no es necesario reservar memoria para cada uno de ellos porque la comparten.
- Es más rápido cambiar de un hilo a otro que de un proceso a otro.
Estos hilos suelen ser utilizados la mayor parte de las ocasiones para llevar a cabo tareas en segundo plano, puesto que se reduce mucho el tiempo de realización de diversas tareas de forma simultánea.

Java es uno de los lenguajes de programación que permite trabajar con distintos hilos en el desarrollo de una aplicación.

### 3.3. Programación de aplicaciones multihilo

A la hora de desarrollar un software es necesario tener en cuenta qué tiempo de ejecución debe de tener como máximo una aplicación. Además, es importante medir el consumo de recursos que esta ha utilizado. Cuando existe solo un proceso, existe la posibilidad de que el consumo de memoria RAM y recursos del procesador por parte del proceso en ejecución, sobrecargue el sistema.

Como solución a esto se han creado los hilos de ejecución que permiten ser ejecutados dentro de una aplicación de forma paralela y haciendo uso de otra parte del código. De esta forma, es posible ejecutar un hilo en primer plano que permita la comunicación con el usuario, y, en segundo plano, hilos que vayan ejecutando las diferentes tareas de carga de una aplicación. Con esto se consigue que el rendimiento del equipo esté más optimizado.

Hoy en día la programación de aplicaciones con estas características es fundamental.

Además, permiten al usuario trabajar con diferentes aplicaciones al mismo tiempo sin penalizar el rendimiento del equipo. Esto posibilita una gran cantidad de opciones como, por ejemplo, el trabajo en múltiples escritorios con diversas aplicaciones de forma paralela.

### 3.4. Estados de un hilo. Cambios de estado

Al igual que los procesos, los hilos tienen un ciclo de vida en el que van pasando por diferentes estados.

Los estados que pueden tener un hilo son:

- Listo: se ha creado el hilo, pero aún no ha comenzado su ejecución.
- Ejecución: cuando un objeto llama al método start() comienza la ejecución del hilo, es decir, se empiezan a ejecutar las instrucciones que se encuentran en el método run().
- Bloqueado: el hilo se ha parado pero puede volver a ejecutarse. Normalmente, el hilo se bloquea por alguna de las siguientes acciones:
#### -Se invoca al método sleep().

- El hilo queda a la espera de que finalice una operación de entrada/salida.

- Se invoca el método wait(). Cuando un hilo queda bloqueado por este método, otro hilo debe invocar el método notify() o notifyAll(), dependiendo de si quiere despertar un único hilo, o todos aquellos que estén bloqueados, respectivamente.

- Otro hilo, externamente, invoca al método suspend(). Cuando un hilo llama al método suspend(), el hilo bloqueado debe recibir el mensaje resume() para poder volver a la ejecución.

- Muerto: el hilo muere, ya sea porque ha finalizado el método run() o porque externamente han decidido pararlo. Los cambios de estado de un hilo vienen dados por las siguientes situaciones:
- Creación: cuando se crea un proceso se crea un hilo para ese proceso. Después, este hilo puede crear otros hilos dentro del mismo proceso. El hilo pasará a la cola de los Listos.
- Bloqueo: cuando un hilo necesita esperar por un suceso, se bloquea (guardando sus registros de usuario, contador de programa y punteros de pila). Ahora el procesador podrá pasar a ejecutar otro hilo que esté al principio de la cola de Listos, mientras el anterior permanece bloqueado.
- Desbloqueo: cuando el evento por el que el hilo permanecía en estado de bloqueo finaliza, el hilo pasa a la cola de los Listos.
- Terminación: cuando un hilo finaliza, se liberan todos los recursos utilizados por él.
### 3.5. Compartición de información entre hilos y gestión de recursos compartidos por los hilos

Cuando varios hilos comparten el mismo espacio de memoria es posible que aparezcan algunos problemas, denominados problemas de sincronización:

- Condición de carrera: se denomina condición de carrera a la ejecución de un programa en la que su salida depende de la secuencia de eventos que se produzcan.
- Inconsistencia de memoria: es aquel problema en el que los hilos, que comparten un dato en memoria, ven diferentes valores para el mismo elemento.
- Inanición: es uno de los problemas más graves. Consiste en que se deniegue siempre el acceso a un recurso compartido al mismo hilo, de forma que quede bloqueado a la espera del mismo.
- Interbloqueo: es el otro de los problemas más graves. Es aquel en el que un hilo está esperando por un recurso compartido que está asociado a un hilo cuyo estado es bloqueado.

Para poder evitarlos en gran medida, es necesario implementar mecanismos de sincronización entre los hilos de un proceso. De esta forma se consigue que un hilo que quiere acceder al mismo recurso que otro, se quede en espera hasta que se liberan dichos recursos. Este tipo de mecanismos se denominan zona de exclusión mutua.

Estos hilos deben saber quiénes de ellos deben esperar y cuáles continuar con su ejecución. Para ello existen diferentes mecanismos de comunicación entre hilos:

- Operaciones atómicas: son aquellas operaciones que se realizan a la vez, es decir, que forman un pack. De esta forma se evita que los datos compartidos tengan distintos valores para el resto de hilos del proceso.
- Secciones críticas: se estructura el código de la aplicación de tal forma que se accede de forma ordenada a aquellos datos compartidos.
- Semáforos: este mecanismo solo puede tomar valores 0 o 1. El hilo que accede al recurso inicializa el semáforo a 1 y tras su finalización el valor se queda a 0.
- Tuberías: todos los hilos se añaden a una cola que se prioriza por medio de un algoritmo FIFO, es decir, el primero en solicitar el acceso será asignado al recurso.
- Monitores: garantizan que solo un hilo accederá al recurso con el estado de ejecución. Esto se consigue por medio del envío de señales.
#### devuelve este al monitor.

- Paso de mensajes: todos los hilos deben tener implementados los métodos para entender los mensajes. Esto supone un mayor coste, aunque si existe seguridad en el envío y recepción de un mensaje, se garantiza que solo un proceso accederá en el mismo momento a un recurso.
### 3.6. Programas multihilo, que permitan la sincronización entre ellos

Cuando en un programa tenemos varios hilos ejecutándose a la vez es posible que varios hilos intenten acceder a la vez al mismo sitio (fichero, conexión, otro). Para solucionar estos problemas, hay que sincronizar los hilos.

La finalidad es que el Hilo A escriba en el fichero esto:

```java
fichero.println("Hola");
```

Mientras el Hilo B hará esto:

```java
fichero.println("Adiós");
```

Si los dos hilos lo hacen a la vez, sin ningún tipo de sincronización, el fichero final puede tener las letras entremezcladas.

Así que cuando un hilo escriba en el fichero, debe marcar de alguna manera que el fichero está ocupado y el otro hilo deberá esperar a que esté libre. La forma de comunicarse consiste en compartir un objeto. Imaginemos que escribimos en un fichero usando una variable `fichero` de tipo `PrintWriter`.

Para evitar este problema debemos sincronizar los hilos. En Java el código sería así:

```java
synchronized (fichero) {
    fichero.println("Hola");
}
```

Y el otro hilo:

```java
synchronized (fichero) {
    fichero.println("Adiós");
}
```

Al poner `synchronized(fichero)` marcamos `fichero` como ocupado desde que se abren las llaves hasta que se cierran. Cuando el Hilo B intenta también su `synchronized(fichero)`, se queda ahí bloqueado, en espera de que el Hilo A termine con el fichero.

### 3.7. Gestión de hilos por parte del sistema operativo. Planificación y acceso a su prioridad

Los sistemas operativos tienen dos formas de implementar hilos:

- Multihilo apropiativo: permite al sistema operativo determinar cuándo debe haber un cambio de contexto. Pero esto tiene una desventaja, y es que el sistema puede hacer un cambio de contexto en un momento inoportuno, causando una confusión de prioridades, creando una serie de problemas.
- Multihilo cooperativo: depende del mismo hilo abandonar el control el control cuando llega a un punto de detección, lo cual puede traer problemas cuando el hilo espera la disponibilidad de un recurso.
En cuanto a la gestión de las prioridades, en el lenguaje Java, cada tiene una preferencia. Predeterminadamente, un hilo hereda la prioridad del hilo padre que lo crea, aunque puede aumentar o disminuir mediante el método setPriority(). Para obtener la prioridad del hilo se utiliza el método getPriority().

La prioridad se mide mediante un rango de valores enteros entre 1 y 10, siendo 1 la mínima prioridad (MIN_PRIORITY) y 10 el valor de máxima (MAX_PRIORITY). Si varios hilos tienen la misma prioridad, la máquina virtual va cediendo control de forma cíclica.

### 3.8. Depuración y documentación de aplicaciones

Durante todo el proceso de desarrollo de una aplicación es necesario hacer depuraciones constantes y comprobaciones del comportamiento y resultados obtenidos.

La mejor forma de realizarlas es a través del uso de puntos de interrupción. Estos puntos indican al depurador del software que ejecuta la aplicación qué debe parar o pausar su ejecución en un punto determinado.

Estos puntos suelen usarse para mostrar los valores obtenidos y mensajes necesarios para comprobar que los datos son los correctos y la ejecución hasta ese punto es correcta. Además, este tipo de puntos se utilizan como herramienta de trazabilidad de la aplicación.

Con esto se consiguen focalizar los errores y poder resolver las incidencias más rápidamente.

Toda la documentación debe detallar cuál es la funcionalidad de dicha aplicación. En ella deben de aparecer de forma esquemática todos los puntos relevantes, que son necesarios para comprender y conocer el correcto funcionamiento de la misma.