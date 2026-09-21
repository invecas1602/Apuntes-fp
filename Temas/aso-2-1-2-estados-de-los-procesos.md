# **2.1.2. Estados de los procesos**

Los estados por los que atraviesa un proceso pueden variar dependiendo del sistema operativo sobre el cual se estuvieran ejecutando, pero principalmente son cinco:

- **Preparado**: el proceso está en espera para ejecutarse en cuanto el procesador pueda asignarle los recursos necesarios.
- **En ejecución**: el procesador está ejecutando activamente el proceso.
- **Bloqueado**: el proceso no puede continuar con su ejecución hasta que un determinado recurso, como cierta cantidad de memoria o un bus de comunicaciones, esté disponible y le sea asignado.
- **Suspendido**: el proceso se ha retirado de la memoria, colocándose temporalmente en la memoria virtual en disco hasta que sea cargado de nuevo para continuar con su ejecución. Esto puede ser consecuencia, por ejemplo, de haber sido programado para suspenderse tras haber permanecido durante cierto tiempo inactivo.

En ocasiones podemos encontrar procesos huérfanos que, siendo hijos de otros procesos, han perdido la comunicación con su proceso padre y, por este motivo, no pueden finalizar, por lo que permanecen en ejecución. Esto puede suceder si el proceso padre termina de forma inesperada, ya que normalmente cuando un proceso padre finaliza, lo hacen también todos sus procesos hijos. En cualquier caso, los procesos huérfanos no solo continúan ocupando los recursos que se les hubiera asignado, sino que pueden ser fuente de inestabilidad del sistema, por lo que los sistemas operativos suelen contemplar mecanismos para lidiar con este problema. En los sistemas tipo Unix, por ejemplo, el proceso *init* adopta automáticamente a todos aquellos procesos que ya no estuvieran asociados a un padre.
