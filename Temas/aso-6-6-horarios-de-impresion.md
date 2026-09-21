# **6.6. Horarios de impresión**

Tanto bajo Windows como utilizando CUPS, podemos utilizar la agrupación de impresoras para diferir la impresión de ciertos documentos. De esta forma, podríamos dirigir los que excedan cierto número de páginas hacia un conjunto determinado de impresoras, o retenerlos durante la jornada e imprimirlos fuera del horario de oficina para no acaparar los dispositivos cuando la demanda es más elevada.

Para este fin, en CUPS podemos utilizar las órdenes *cupsenable* y *cupsdisable* en combinación con *cron*. Por ejemplo, para que todos los trabajos enviados a la clase *Contabilidad* queden retenidos a partir de las 9 de la mañana y empiecen a imprimirse a las 8 de la tarde, podríamos añadir a *crontab* (*crontab -e*) un trabajo similar a este:

# Retener los trabajos en Contabilidad a las 9 horas 0 09 \* \* \* /usr/sbin/cupsdisable --hold Contabilidad >/dev/null 2>&1 # Liberar los trabajos de Contabilidad a las 20 horas 0 20 \* \* \* /usr/sbin/cupsenable --release Contabilidad >/dev/null 2>&1

En Windows, mediante el uso de un *script* de PowerShell y el programador de tareas, podemos lograr el mismo resultado:

- 1. Programamos un *script* llamado *PausarImpresora.ps1* (donde *Impresora IPP* es el nombre de la impresora o grupo de impresoras cuya cola queremos pausar) y lo guardamos en una carpeta del equipo (por ejemplo, en *D:\Scripts*):

\$prn = gwmi win32\_printer | ? {\$\_.Name -eq 'Impresora IPP' } \$prn.pause()

- 2. Confeccionamos otro *script*, llamado esta vez *ReanudarImpresora. ps1*, y lo guardamos junto al anterior:

\$prn = gwmi win32\_printer | ? {\$\_.Name -eq 'Impresora IPP' } \$prn.resume()

- 3. Creamos una nueva tarea usando el Programador de tareas de Windows en la que, como acción, seleccionamos *Iniciar un programa*, indicando *powershell.exe* en *Programa* o *script* y -*file* "*D*:\ *Scripts*\*PausarImpresora.ps1*" como argumento del programa.
