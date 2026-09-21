# **2.3. Planificación de procesos**

Cuando varios programas están en ejecución, el sistema operativo debe coordinar todos los procesos y subprocesos de forma que cada uno pueda ser debidamente atendido por el procesador. Para asignar estos *tiempos de CPU*, el sistema utiliza un **planificador de procesos** que se encarga de mantener una cola de procesos en espera y de seleccionar el que debe ejecutarse a continuación.

Para definir el momento en que cada proceso se ejecuta, los sistemas pueden emplear diferentes **algoritmos de planificación** con el fin de establecer un **orden de prioridades** dentro de la cola de procesos. Los más utilizados son los siguientes:

- **Por orden de llegada (***First-Come, First-Served,* **FCFS)**: este es el algoritmo más simple, ya que los procesos se programan según su orden de llegada: el primero en entrar en la cola es el primero en ejecutarse.
- **Primero el trabajo más corto (***Shortest Job First,* **SJF)**: este algoritmo prioriza los procesos según una estimación del tiempo que tardarán en ejecutarse: el proceso con un tiempo de ejecución estimado más corto será el primero en ejecutarse.
- **Programación por prioridades**: los procesos se programan en función del nivel de prioridad asignado: el proceso con la prioridad más alta es el que se ejecuta en primer lugar. La asignación de prioridades puede realizarse atendiendo a diversos factores, como el tiempo de CPU acumulado, la importancia del proceso según un baremo preestablecido, o la cantidad de recursos que el proceso estuviera utilizando en el momento de evaluarse.
- **Round Robin (RR)**: este algoritmo divide el tiempo total de CPU en varias porciones o *cuantos de tiempo*, y asigna a cada proceso una cantidad fija de ellos. Cuando el tiempo asignado expira, el proceso se coloca de nuevo en la cola de espera.

Dependiendo de la naturaleza de los procesos y de los recursos disponibles, una técnica de priorización de los procesos puede ofrecer una mayor eficiencia que otra, por lo que la correcta elección del algoritmo de planificación incide de forma significativa en el rendimiento general del sistema.

Los contadores de programa o *punteros de instrucción* son registros del procesador encargados de realizar el seguimiento de la secuencia de ejecución de un programa. Así, cuando se ejecuta un programa, la CPU lee la instrucción en la dirección de memoria indicada por el contador de programa y lo actualiza para que apunte a la dirección de memoria en donde se almacena la siguiente instrucción a ejecutar. Este proceso se repite hasta que se completa o se interrumpe el programa.

### Para + info
