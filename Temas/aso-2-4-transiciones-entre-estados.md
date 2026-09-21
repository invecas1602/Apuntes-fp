# **2.4. Transiciones entre estados**

Como ya hemos visto, un proceso atraviesa, a lo largo de su vida, una serie de estados, y en los compases de espera entre uno y otro estado permanece en diversas colas gestionadas por el planificador de procesos del sistema: **la cola de trabajos** —que recoge los procesos nuevos—, **la cola de procesos preparados** para ejecutarse, y la **cola de espera**.

En este esquema podemos observar cómo las transiciones entre estados pueden ser unidireccionales —es decir, el proceso puede cambiar de un estado a otro, pero no regresar al estado previo—, como las que se dan entre los estados Preparado, En ejecución y En espera, o bidireccionales —el proceso puede transitar entre un estado y otro de manera indistinta—, como es el caso de los estados En espera y Bloqueado, o Suspendido y Preparado.

Otro concepto presente en el esquema es el de **interrupción**, que es una señal que se envía al procesador para requerir su atención inmediata. Esto permite detener la ejecución de un programa de forma temporal para pasar a tareas identificadas como de mayor prioridad, como las operaciones de entrada y salida de datos (E/S), la entrada de un usuario o la gestión de errores.

Las interrupciones pueden ser de naturaleza diversa: **de hardware** (por ejemplo, las generadas por dispositivos externos como teclados y ratones), **de software** (lanzadas por programas que demandan servicios del sistema operativo) y **excepciones** (provocadas por errores o condiciones inusuales, como un error de división por cero o el fallo de una página de memoria).
