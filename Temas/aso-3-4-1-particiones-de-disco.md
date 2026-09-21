# **3.4.1. Particiones de disco**

La forma en que los ordenadores gestionan los dispositivos en donde se almacena la información viene determinada por su *firmware,* es decir, por el programa básico que les permite realizar sus funciones. Este software se almacena en una memoria no volátil de solo lectura o ROM, y se ejecuta cada vez que el dispositivo se pone en marcha, encargándose de detectar los componentes instalados (CPU, RAM, tarjetas de expansión, etc.), de comprobar que funcionen correctamente y de cargar el sistema operativo.

Existen dos tipos de *firmware* para PC: el ya obsoleto BIOS (*Basic Input/ Output System*, o sistema básico de entrada/salida), y el más reciente UEFI (*Unified Extensible Firmware Interface*, o interfaz de *firmware* extensible unificado).

#### **Master Boot Record (BIOS)**

Dado que todavía existen ordenadores en activo basados en BIOS, vamos a repasar brevemente el proceso de arranque basado en este tipo de *firmware.*

Cuando encendemos un ordenador con BIOS, este inicia los dispositivos conectados y realiza su comprobación (lo que se conoce como POST), tras lo cual examina el primer dispositivo de su lista de arranque en busca de un MBR (*Master Boot Record*, o registro maestro de arranque); si lo halla, le cede el control del equipo, y si no, pasa al siguiente dispositivo de la lista.

El MBR es un código de 512 bytes que reside en el primer sector de un disco de arranque y que tiene 3 partes: el código de arranque maestro o MBC (*Master Boot Code*), que ocupa 446 bytes; una tabla de particiones de disco de 64 bytes; y una firma de arranque, que marca el final del MBR y que consta de dos bytes cuyos valores deben ser 0 x 55 y 0 x AA, respectivamente.

En la tabla de particiones de un MBR pueden existir cuatro particiones primarias o tres primarias y una extendida. Como mínimo debe haber una partición primaria, pero si existen más, solo una de ellas puede ser la partición *activa* desde la que arrancará el sistema operativo. En cualquier caso, el tamaño máximo de cada partición no podrá superar nunca los 2,1 TB.

Es en el MBC donde se ubica el cargador de arranque (*o bootloader* en inglés), un programa que se encarga de realizar los pasos siguientes:

- 1. Busca en la tabla de particiones la partición marcada como activa.
- 2. Localiza el sector inicial de la partición activa, denominado *sector de arranque.*
- 3. Carga una copia del sector de arranque en la memoria.
- 4. Transfiere el control del sistema al código ejecutable del sector de arranque.

#### *GUID Partition Table* **(UEFI)**

En un sistema basado en UEFI se utiliza un nuevo esquema de particiones denominado GPT (del inglés *GUID Partition Table,* o tabla de particiones GUID), que nos permite crear hasta 128 particiones con una capacidad máxima de 18 exabytes (unos 18,8 millones de TB) por partición.

*Organización de un disco básico con tres particiones primarias, una extendida y dos volúmenes lógicos.*

Adicionalmente, y previo a la GPT, se crea un MBR de protección, cuya misión principal es la de evitar que ciertas herramientas de software para discos con MBR se confundan y puedan sobrescribir por accidente los datos de la GPT.

A cada una de las particiones de la GPT se asigna un identificador global único de 128 bytes llamado GUID (*Global Unique Identifier*). Además del nombre de la partición y otros atributos, como dónde empieza y dónde acaba, el GUID identifica a qué sistema operativo corresponde y cuál es su función.

A diferencia de lo que sucede en un sistema basado en un MBR, donde se localizan los datos mediante el sistema CHS (siglas en inglés de *cilindro*, *cabeza* y *sector*) heredado de los discos duros mecánicos, una partición GPT utiliza direcciones lógicas de bloque, o LBA (*Logical Block Address*), cada una con un tamaño de 512 bytes.

En Windows, por ejemplo, la GPT utiliza 32 bloques lógicos para almacenar la información de las 128 posibles particiones (4 por bloque).

| Entrada   | n           |
|-----------|-------------|
| Unidad E: | Particiones |
| Unidad    | n           |
| Entrada   | n           |
| MBR       | GPT         |

Muchas UEFI incorporan un modo de compatibilidad con BIOS, también llamado a veces CSM (*Compatibility Support Module*, módulo de soporte para compatibilidad), que permite al ordenador arrancar desde un disco con MBR.

Atención

El primero de los bloques (LBA 0) se usa para ubicar el código compatible con MBR, mientras que en el segundo (LBA 1) se sitúa la *cabecera GPT primaria*, que almacena el número total de particiones, sus GUID, y el tamaño y ubicación de la copia de seguridad de la tabla, o *cabecera GPT secundaria*, que se guarda justo al final del disco. Las 128 entradas de la tabla van inmediatamente después de la cabecera GPT primaria, y sus copias inmediatamente antes de la secundaria.

![](_page_74_Picture_2.jpeg)

En una unidad de almacenamiento con GPT, el cargador de arranque se ubica en una partición independiente denominada ESP (*EFI System Partition,* partición de sistema EFI), también llamada simplemente *partición del sistema.*

La ESP tiene un formato de archivos FAT32 y un tamaño mínimo de 100 MB; esto permite eludir el problema de espacio que plantea el MBR, ya que la mayor parte de los cargadores de arranque actuales no caben en el espacio asignado al MBC, por lo que se ven forzados a extender su código hacia una zona de tamaño indeterminado situada entre el MBR y el inicio de la primera partición.

Estamos, pues, ante un tipo de cargador de dos etapas en el que la primera etapa, ubicada en el MBR, tiene por única misión cargar una segunda etapa, almacenada en cualquier otro lugar.
