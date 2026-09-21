# **7.1. Copias de seguridad**

Existen muchos escenarios en los que la integridad de la información almacenada en una base de datos puede verse comprometida, ya sea de forma accidental o a causa de un fallo del software o del hardware del servidor. Por ello, es esencial diseñar e implementar una directiva de copias de seguridad periódicas que nos permita recuperar los datos en caso de necesidad.

### **Estrategias de copia de seguridad**

Para conseguir este objetivo, podemos recurrir a dos estrategias que, en conjunto, incrementan las posibilidades de recuperar por completo la información manejada por el SGBD.

La primera es almacenar una copia de seguridad del servidor mediante la realización de imágenes del sistema, de manera que sea posible restaurar el equipo a un estado de funcionamiento correcto tras un desastre, como por ejemplo una actualización del sistema fallida o un ataque informático. Esto puede conseguirse, bien utilizando las herramientas proporcionadas por el mismo sistema operativo, o bien software de terceros para la realización de copias de seguridad.

La segunda estrategia es realizar copias de los propios archivos de base de datos, empleando para ello las herramientas proporcionadas por el SGBD. En este caso, el procedimiento concreto dependerá de los programas incluidos para su uso a través del Símbolo del sistema de Windows o de un terminal de Linux, y de los métodos previstos en las distintas interfaces gráficas de cada SGBD, sin excluir herramientas de terceros que pueden facilitar, en mayor o menor medida, la realización de este tipo de operaciones.

### **Tipos de soporte para copias**

En cuanto a los soportes físicos de las copias, podemos optar por medios locales (llamados DAS, por las siglas del inglés *Direct Attached Storage*), como discos duros, SSD o cintas magnéticas, o bien por medios en línea, como los que podemos encontrar dentro de una red local o en un servidor en la nube, ya sea autogestionados o administrados por terceros.

Si optamos por una estrategia de almacenamiento en la nube, tenemos a nuestra disposición servicios como Microsoft OneDrive o Google Drive, que realizan la copia automática y sincronización de los archivos contenidos en un conjunto de carpetas determinado.

Llamamos *instantánea* o *imagen del sistema* a una copia exacta de las particiones en donde tenemos instalado el sistema operativo, ya sea la partición de arranque, la de intercambio o las reservadas para el sistema, incluyendo las que estuvieran ocultas.

### Para + info

Su principal ventaja es la disponibilidad, ya que podremos acceder a los archivos respaldados desde cualquier dispositivo en el que tengamos instalado el programa cliente. Además, algunos de ellos, como es el caso de Dropbox, también proporcionan control de versiones, con lo que podremos revertir los cambios realizados en los archivos a versiones anteriores de ellos.

En caso de utilizar una red local, podemos recurrir básicamente a dos sistemas de almacenamiento:

- **NAS** (*Network Attached Storage*): pequeños servidores de archivos con un sistema operativo muy ligero —normalmente embebido en el hardware— cuya única misión es servir de almacenamiento y servidor de archivos. Un NAS puede estar compuesto de uno o varios discos distribuidos, con o sin redundancia, y utilizar uno o varios protocolos de archivos en red para su transmisión mediante el protocolo TCP/IP: NFS, SMB, AFP, FTP o HTTP. Estos servidores son rápidos, muy fáciles de administrar, pueden ampliarse hasta un máximo de discos determinado y su uso es tan simple como montarlos en una carpeta o unidad de red. También son relativamente asequibles, ya que su coste viene determinado esencialmente por el número, velocidad y capacidad de los discos incluidos.
- **SAN** (*Storage Area Network*): sistema de almacenamiento distribuido donde los recursos globales de la red se consolidan y se dividen en bloques, cada uno de los cuales puede formatearse con su propio sistema de archivos. La principal diferencia con respecto a un NAS es que los clientes ven estos bloques como discos a los que acceder como cualquier otro dispositivo de bloques, y no como meros servidores de archivos. Las SAN, como los NAS en lo relativo a los sistemas de archivo, son multiprotocolo, porque además pueden emplear una variedad de protocolos de transporte; normalmente se utiliza el Canal de fibra (*Fibre Channel*) o el Canal de fibra sobre Ethernet (*Fibre Channel over Ethernet*, o FCoE), que es compatible con las redes Ethernet existentes, pero también pueden usarse el *Internet Small Computing System Interface* (iSCSI) en entornos pequeños y medianos, o el *InfiniBand* en entornos de alta exigencia y gran envergadura.

### **Integridad y documentación de las copias**

La responsabilidad del personal técnico encargado de las copias de seguridad no finaliza cuando la copia está realizada, sino que se extiende durante el tiempo mínimo que determinen las directivas de retención establecidas.

La protección de las copias tiene que realizarse a dos niveles:

- **Físico**: las copias de seguridad deberían conservarse, idealmente, en un lugar a prueba de desastres (inundaciones, incendios, etc.), de robos y, a ser posible, en una ubicación distinta a aquella donde se almacenen los datos originales.
- **Lógico**: es necesario establecer las medidas necesarias para impedir cualquier acceso no autorizado a las copias, para lo cual podemos usar contraseñas seguras (que además deberían cambiarse periódicamente) o técnicas de cifrado, además de los habituales sistemas de seguridad en red (cortafuegos, DMZ, etc.) si los conjuntos de copias se almacenan en un dispositivo conectado.

Para garantizar que los datos se están respaldando correctamente (y muy especialmente durante el periodo inicial), es necesario ejecutar una serie de rutinas de comprobación que impliquen la restauración y comparación de los datos en entornos de pruebas, para lo cual podemos usar técnicas de *hashing*, como las funciones SHA-1, SHA-2 o MD5.

Por otra parte, si documentamos de forma adecuada toda nuestra estrategia de copias de seguridad, en caso de surgir problemas nos será más sencillo identificar los posibles puntos de fallo, y por tanto aumentaremos nuestras posibilidades de preservar los datos.

El conjunto de medidas a adoptar depende en parte de las directivas establecidas por la organización con respecto a cuestiones como la seguridad y la privacidad de la información, pero podemos citar un conjunto de buenas prácticas de aplicación general, que incluyen las siguientes:

- Dónde se almacena cada copia.
- Quiénes pueden acceder a ellas, cuáles son sus responsabilidades y formas de contacto.
- Conjuntos de datos respaldados, con referencia tanto a los archivos y carpetas incluidos como a equipos de donde provienen.
- Tipo, frecuencia y directivas de retención de las copias.

### Para + info

Denominamos *hashing* al uso de un algoritmo criptográfico para generar una cadena de caracteres de longitud fija, que luego podemos utilizar con el fin de comparar la integridad de los datos en operaciones de copia de seguridad o de compresión y descompresión.

- Hardware y software utilizado en la realización de las copias.
- Técnicas de restablecimiento recomendadas.
- Comprobaciones realizadas sobre la integridad de las copias y el estado de funcionamiento del sistema.
- Historial de restauraciones realizadas y resultado de cada operación.
- Si se trasladan las copias a una ubicación segura, quién y cada cuándo lo realiza.

![](_page_169_Picture_2.jpeg)

Si documentamos adecuadamente estos aspectos y cualquier otro que resulte relevante en nuestro entorno en particular, eso nos permitirá actuar con mayor eficacia y anticipar, en muchos casos, los posibles problemas que se puedan presentar.

### **7.1.1. Tipos y planes de copias de seguridad**

Con independencia del conjunto de datos que estemos salvaguardando, o del soporte escogido como medio de almacenamiento, existen tres tipos básicos copia de seguridad en función de la clase y del número de archivos respaldados:

- **Completa o total**: copia íntegra de todo el conjunto de archivos a respaldar. Este tipo de respaldo es muy lento y, con el paso del tiempo, requiere de mucho espacio, por lo que normalmente se establece un sistema de rotación de copias basado en el número de copias realizadas, en su antigüedad, o en ambos factores.
- **Diferencial o acumulativa**: se incluyen en la operación de respaldo tan solo aquellos archivos que hayan sido modificados desde la última copia de seguridad completa. Así, en cada copia diferencial encontraremos todos los archivos modificados hasta la fecha de dicha copia, por lo que el tamaño de las copias diferenciales se va incrementando con el tiempo hasta la realización de una nueva copia completa.
- **Incremental**: se copian solo aquellos archivos que se hayan modificado desde la última copia realizada, ya sea incremental o completa. El tamaño de estas copias de respaldo es, por lo tanto, variable, aunque típicamente mucho más pequeño que el de las copias diferenciales, y además se realizan de forma mucho más rápida.

Los programas especializados en la creación de copias de respaldo suelen contemplar la posibilidad de programar sus operaciones y automatizar la realización de copias totales, diferenciales o incrementales según un conjunto de reglas preestablecido; es lo que se conoce como un **plan de copias**.

Un aspecto importante a considerar es que, en aplicación del RGPD, es necesario crear un plan de copias de respaldo que garantice la seguridad de los datos sensibles, incluyendo su traslado un lugar a prueba de robo o de catástrofes, como inundaciones e incendios.

#### **3.3.** *Protección de datos y confidencialidad*

### **Planes de copia y esquemas de rotación**

De esta forma, es posible configurar el software para que vaya alternado entre los diferentes tipos de respaldo, de forma que siempre exista un número determinado de copias de cada tipo (por ejemplo, 2 copias totales, 4 diferenciales y 8 incrementales). Esto es especialmente importante cuando se utiliza un mismo soporte o conjunto de soportes —un sistema, por tanto, limitado en espacio—, para ir almacenando las sucesivas copias.

A la hora de crear un plan de copias de seguridad, y basándonos en todo lo que hemos ido viendo hasta el momento, deberemos evaluar los siguientes aspectos:

- **Selección de los datos**: determinar de qué conjuntos de datos vamos a realizar las copias de respaldo (tablas, bases de datos, archivos de usuario o de sistema, discos completos...), y qué criterios utilizaremos en su selección (fecha de creación o de modificación, tamaño, etc.).
- **Organización de las copias**: forma óptima de organizar las copias de manera física y lógica, con objeto de recuperar la información con la mayor eficacia. Por ejemplo, cuando se manejan grandes volúmenes de datos, resulta útil crear tablas de metadatos a modo de índice que faciliten la localización de datos concretos.
- **Selección del soporte**: qué medio o medios físicos, y sobre qué estructuras lógicas, se van a realizar las copias. El nivel de disponibilidad y accesibilidad del soporte escogido, así como su relación rendimiento/coste, son criterios clave a la hora de optar por un sistema local o en red, simple o distribuido, en la nube, basado en medios extraíbles, de lectura secuencial (discos duros, cintas) o aleatoria (memorias flash, SSD), etc.
- **Tolerancia a fallos**: implementación de medidas de redundancia que garanticen la integridad de las copias, como sistemas distribuidos reflejados, copias continuas sincronizadas en un servidor de archivos o mediante un servicio en la nube, implementación de un sistema de control de versiones, etc.

Los planes de copias de seguridad se basan principalmente en esquemas de rotación del soporte físico (por ejemplo, una cinta magnética), mediante los cuales un hardware especializado se encarga de ir seleccionando los soportes según se vayan necesitando. No obstante, podemos usar la misma fórmula para generar, dentro de uno o varios volúmenes, diferentes archivos con distintos conjuntos de datos, e ir alternándolos y reflejándolos para multiplicar la seguridad del sistema.

### **Reglas de retención**

En todos estos planes, es el software de copia de respaldo el que se encarga de crear el tipo de copia designado en los días que hayamos programado, y el que restituye los datos a recuperar a partir del conjunto de copias completas, incrementales y diferenciales que se conserven. En este sentido, resulta fundamental establecer unas reglas de retención adecuadas. Estas reglas son las que determinan la conservación durante un lapso de tiempo determinado de una cantidad concreta de copias según su tipo. Transcurrido este periodo, las copias que tengan una fecha anterior se eliminarán para hacer sitio a las más recientes. También es posible definir un umbral de espacio libre mínimo más allá del cual se producirá la eliminación de la copia más antigua.

En la siguiente tabla podemos ver las reglas de retención que podríamos establecer para algunos de los planes de copias de seguridad más habituales:

|                     | Abuelo-Padre-Hijo                                                                    |                  |
|---------------------|--------------------------------------------------------------------------------------|------------------|
| Tipo de copia       | Programación                                                                         | Retención        |
| Completa mensual    | Primer lunes de cada mes                                                             | 24 semanas       |
| Diferencial semanal | Todos los lunes del mes, excepto el primero                                          | 8 semanas        |
| Incremental diaria  | De martes a viernes Conjunto de copias diferenciales                                 | 14 días          |
| Tipo de copia       | Programación                                                                         | Retención        |
| Completa mensual    | Primer lunes de cada mes                                                             | 24 semanas       |
| Diferencial diaria  | De lunes a viernes, excepto el primer lunes del mes Conjunto de copias incrementales | 28 días          |
| Tipo de copia       | Programación                                                                         | Retención        |
| Completa mensual    | Primer lunes de cada mes                                                             | 24 semanas       |
| Incremental diaria  | De lunes a viernes, excepto el primer lunes del mes Copia incremental continua       | 28 días          |
| Tipo de copia       | Programación                                                                         | Retención        |
| Copia completa      | La primera vez que se ejecuta la pro gramación                                      | 28 incrementales |
| Incremental diaria  | De lunes a viernes                                                                   | 28 copias        |

### **Copias de BD: físicas y lógicas, en frío y en caliente**

Por otra parte, si nos centramos específicamente en la salvaguarda de bases de datos, podemos dividir los tipos de copia según su naturaleza: copias físicas y copias lógicas.

Una **copia física** de BD consiste en respaldar los directorios y los archivos donde se almacenan los datos (tablas, registros, ejecutables, etc.). Este tipo de copia puede realizarse **en caliente**, lo cual significa que se lleva a cabo mientras el servidor está en funcionamiento (y, por tanto, los datos pueden cambiar mientras se está realizando la operación de respaldo), o **en frío**, es decir, con el sistema detenido o fuera de línea (por ende, los datos no cambian durante el proceso), lo cual garantiza un mayor nivel de consistencia y fiabilidad en los datos resguardados. En la siguiente tabla podemos ver las principales características de ambos tipos de copia:

Hablamos de **copia lógica** cuando únicamente salvaguardamos, en formato binario, el contenido de una base de datos (tablas, esquemas, procedimientos, etc.), utilizando para ello la herramienta de exportación e importación del SGBD. Esto permite tanto restaurar la BD a un estado previo, como copiarla o moverla a otra plataforma conservando todos los elementos interdependientes.

Cada tipo de copia tiene sus ventajas e inconvenientes, que resumimos, a continuación, en la siguiente tabla:

|                           | Copia en caliente | Copia en frío |
|---------------------------|-------------------|---------------|
| Sistema en línea          | Sí                | No            |
| Estado del sistema        | Dinámico          | Estático      |
| Velocidad de la copia     | Lenta             | Rápida        |
| Consistencia de los datos | Baja              | Alta          |
| Fiabilidad de la copia    | Menor             | Mayor         |

|                                | Copia física                             | Copia lógica                               |
|--------------------------------|------------------------------------------|--------------------------------------------|
| Velocidad de restauración      | Más rápida.                              | Más lenta.                                 |
| Complejidad de la restauración | Más sencilla.                            | Más compleja, al no incluir información    |
| Espacio necesario              | Incluye todos los archivos de la BD, por |                                            |
| Formato de datos               | Binario.                                 | Distintos formatos.                        |
| Portabilidad                   | Copia de naturaleza no portable.         |                                            |
| Contenido de la copia          | Todos los archivos físicos de la BD.     | Variable: usuarios, tablas, procedimientos |

### **7.1.2. Copias de sistema y respaldo de BD**

Una vez evaluados todos estos factores, es necesario seleccionar una herramienta de software capaz de satisfacer todas las necesidades derivadas de este estudio.

### **Herramientas de respaldo del sistema**

En GNU/Linux, como es habitual, disponemos de diferentes opciones de código abierto para realizar copias de seguridad. Una de las más utilizadas y potentes es Clonezilla, que permite realizar operaciones de respaldo de datos tanto locales como en red usando un servidor de copias de seguridad.

En cuanto a Windows, las versiones de escritorio de este sistema operativo incluyen varias utilidades para solventar problemas de muy leves a bastante graves. Dos de ellas son el Historial de archivos para respaldar archivos y carpetas individuales, y la herramienta de creación de puntos de restauración, que hace una foto fija de partes importantes de Windows como el registro, los controladores o los programas instalados.

*Clonezilla es una de las herramientas de copia de seguridad más populares para GNU/Linux.*

El uso más frecuente de esta última herramienta es recuperar la funcionalidad de Windows ante nuevos componentes de software incompatibles con otros componentes instalados, por lo que no podemos calificarla estrictamente como de copia de seguridad.

Por otra parte, la herramienta de copias de seguridad y restauración de Windows 7, presente en Windows 8 y 10, si bien permite respaldar los datos de las carpetas predeterminadas de Windows y crear una imagen del sistema que podríamos usar para restaurar el equipo si dejara de funcionar correctamente, incluye unas opciones de programación y recuperación bastante limitadas, por lo que no es recomendable utilizarla en entornos de organizaciones o empresas de tamaño medio a grande.

Finalmente, en Windows Server 2022 disponemos de diversas herramientas con las que podremos hacer copias de respaldo de nuestros datos, entre ellas la extensión *Instantáneas* del complemento *Carpetas compartidas de la Consola de administración de Microsoft* (MMC).

Sin embargo, la principal herramienta de respaldo, bajo este sistema operativo, se denomina **Copias de seguridad de Windows Server**, a la cual podemos acceder a través del complemento *wbadmin* de la MMC. Este complemento permite trabajar tanto con copias de seguridad en dispositivos locales o de red, como con copias en línea en Azure (el servicio de almacenamiento en la nube de Microsoft), en caso de tenerlo contratado y configurado en el equipo. En cuanto al contenido de las copias, estas pueden incluir conjuntos de archivos y directorios, aplicaciones instaladas o el contenido de todo el servidor.

Para realizar o programar copias de seguridad locales con *wbadmin*, es necesario instalar la característica *Copias de seguridad de Windows Server*. Podemos hacerlo mediante el *Asistente para agregar roles y características*, al que se accede desde el *Panel del Administrador del servidor* (o desde el menú *Administrar*), o bien utilizando la siguiente instrucción en una ventana de PowerShell:

### > Install-WindowsFeature Windows-Server-Backup

Una vez instalada la herramienta, podremos programar y gestionar copias de seguridad tanto en el servidor como en equipos remotos. Para ello tendremos que crear una primera copia de seguridad completa, de la siguiente manera:

- 1. Abrimos el menú *Herramientas* y, a continuación, seleccionamos *Copias de seguridad de Windows Server*. También podemos lanzar este complemento de la Consola de administración de Microsoft (MMC) desde el diálogo Ejecutar (*Windows + R*), usando la instrucción *wbadmin.msc*. En el panel izquierdo escogemos *Copia de seguridad*, y en el panel *Acciones* hacemos clic en *Hacer copia de seguridad una vez*.

- 2. Dado que todavía no existe ninguna copia, solo se nos permite escoger la segunda de las opciones del asistente.

- 3. En esta primera copia respaldaremos el servidor completo. Si en el futuro queremos realizar copias solo de ciertos archivos, directorios o volúmenes, disponemos de la opción *Personalizada*.

- 4. Podemos hacer la copia en una unidad local, ya sea un disco interno o externo, o en un disco óptico, y también usar una carpeta compartida remota, pero con esta herramienta no podremos usar *pendrives* o cintas magnéticas. En esta ocasión haremos una copia local en una unidad de disco externa conectada vía USB. Si el volumen estuviera incluido en el conjunto (como es el caso cuando hacemos una copia completa), deberemos eliminarlo de ella.

- 5. En el diálogo de confirmación veremos un resumen del trabajo. Al haber escogido la copia completa, se utilizará el servicio VSS (*Volume Shadow Copy*), en su modalidad compatible con otros servicios de copia de seguridad de terceros, para generar la imagen del sistema.

![](_page_178_Picture_3.jpeg)

- 6. Una vez finalizado el asistente, podemos cerrarlo, ya que la operación se seguirá ejecutando en segundo plano.

![](_page_178_Figure_5.jpeg)

Para hacer una copia de seguridad periódica, utilizaremos el *Asistente para programar copias de seguridad*, también disponible a través del panel *Acciones* de la herramienta *Copias de seguridad de Windows Server*. Los pasos son exactamente los mismos que los que acabamos de detallar para el asistente de copia de una vez, añadiendo un paso extra donde especificaremos las opciones de periodicidad deseadas; podemos realizar la copia una vez al día, a una hora específica, o más de una vez al día en diferentes horas.

Como destino de la copia, además de poder escoger entre un volumen local o una unidad de red, podemos usar un disco dedicado exclusivamente a almacenar las copias programadas, que no puede ser de sistema o pertenecientes a volúmenes compartidos, y que se formateará la primera vez que lo usemos.

![](_page_179_Figure_4.jpeg)

Tanto las copias realizadas como la programación de copias aparecen en el panel de *Estado* dentro de *Copia de seguridad local*.

![](_page_180_Picture_2.jpeg)

Desde aquí podemos consultar todos los detalles relativos a las tareas, pero no podremos editar las programaciones. Ello se realiza desde el mismo *Asistente para programar copias de seguridad*, en un diálogo inicial que nos permitirá modificar o detener las operaciones programadas.

![](_page_180_Picture_7.jpeg)

Para configurar un plan de almacenamiento que incluya copias completas e incrementales, *wbadmin* proporciona la acción *Configurar opciones de rendimiento*.

*Panel de estado de* Copia de seguridad local.

*Diálogo de modificación de una copia de seguridad programada.*

En el diálogo subsiguiente se nos proponen tres opciones:

- **Rendimiento de copia de seguridad normal**: opción por defecto, que hace que se copien siempre todos los datos incluidos en la copia original, hayan sufrido cambios o no.
- **Rendimiento de copia de seguridad más rápido**: opción que usaremos para crear copias incrementales continuas.
- **Personalizar**: permite decidir sobre qué elementos incluidos en la copia programada aplicaremos un esquema de copias incrementales o completas.

### **Herramientas para el respaldo de BD**

Para hacer una copia de respaldo de las BD contaremos con diferentes herramientas según el SGBD que estemos utilizando. Normalmente, se proporciona un programa ejecutable (en MySQL se denomina *mysqldump*) que puede realizar las copias de cualquier tipo de tabla, y posiblemente, en función de motor de almacenamiento utilizado, otros métodos integrados a través de determinadas sentencias.

Por ejemplo, para tablas MyISAM de MySQL, podemos respaldar directamente los archivos con extensión MYD, MYI y SDI, y utilizar los metadatos de estos últimos para importar las tablas usando la sentencia *IMPORT TABLE*.

*Diálogo para optimizar el rendimiento de la copia de seguridad.*

También resulta posible respaldar los datos de una tabla exportándolos en un archivo de texto delimitado por tabuladores. Para ello utilizaríamos la sentencia siguiente:

SELECT \* INTO OUTFILE 'películas.csv' FROM filmoteca.películas;

Esta sentencia almacena el contenido de la tabla *películas* de la *BD filmoteca*, en un archivo con extensión CSV, que podremos abrir con cualquier software compatible con este formato (por ejemplo, un programa de hoja de cálculo). Si preferimos que los campos queden delimitados por comas, utilizaremos el modificador *FIELDS TERMINATED BY*:

01 SELECT \* INTO OUTFILE 'películas.csv' 02 FIELDS TERMINATED BY ',' 03 FROM filmoteca.películas;

A continuación, ilustraremos el uso de *mysqldump* para realizar copias lógicas de las bases de datos en MySQL, aunque el funcionamiento básico de esta herramienta puede extrapolarse al de las que podríamos encontrar en cualquier otro SGBD.

*Mysqldump* puede volcar datos, tanto en formato SQL, como en archivos de texto delimitado cuando incluimos la opción *tab* en la instrucción. En este último caso, se crearán dos archivos: uno denominado *nombre\_de\_la\_tabla.txt*, y otro llamado *nombre\_de\_la\_tabla.sql*, que contendrá la sentencia *CREATE TABLE* necesaria para recrear la tabla salvaguardada.

Mediante la opción *tab* debemos especificar el directorio donde se almacenarán los archivos, el cual deberá estar configurado para escritura en MySQL. Por ejemplo, para almacenar la tabla películas de la base de datos *filmoteca*, en un archivo de texto delimitado, podríamos emplear la siguiente instrucción:

> mysqldump -h localhost -u root -p --tab="C:/ProgramData/MySQL/MySQL Server 8.0/Data/" filmoteca películas

Por defecto, MySQL delimita los campos utilizando un espacio de tabulación, no incluye delimitador de cadena, y delimita las líneas con un retorno de carro y una nueva línea (*\r\n*). No obstante, podemos configurar los caracteres delimitadores del archivo de datos generado por *mysqldump* añadiendo a la instrucción las opciones *fields-terminated-by* (delimitador de campo), *fields-enclosed-by*

(delimitador de cadena y *lines-terminated-by* (delimitador de línea). Por ejemplo, si queremos delimitar las cadenas con comillas dobles y los campos con comas, usaríamos la siguiente instrucción:

![](_page_183_Picture_2.jpeg)

> mysqldump -h localhost -u root -p --tab="C:/ProgramData/MySQL/MySQL Server 8.0/Data/" --fields-terminated-by=, --fields-enclosed-by=\" filmoteca películas

Si no se utiliza la opción *tab*, *mysqldump* generará un archivo SQL estándar, incluyendo todas las sentencias *CREATE* necesarias para recrear los objetos volcados, y las sentencias *INSERT* que cargarán los datos salvaguardados en las tablas recreadas. Por ejemplo, para respaldar todas las bases de datos en un archivo SQL llamado *copia\_de\_seguridad.sql*, utilizaríamos la siguiente instrucción:

> mysqldump -h localhost -u root -p --all-databases > copia\_de\_seguridad.sql

Si lo que deseamos es únicamente salvaguardar bases de datos específicas, lo haremos utilizando la opción *databases*:

> mysqldump -h localhost -u root -p --databases filmoteca > copia\_de\_seguridad.sql

De esta forma, la anterior instrucción respaldará todas las tablas pertenecientes a la base de datos *filmoteca*. Por último, con *mysqldump* podemos también respaldar eventos (opción *events*), procedimientos y funciones (opción *routines*), y disparadores (opción *triggers*); por ejemplo:

> mysqldump -h localhost -u root -p --events --routines --databases filmoteca > copia\_de\_seguridad.sql

![](_page_183_Picture_12.jpeg)

Ponte a prueba

**¿Qué tipos de copia podemos realizar utilizando las herramientas incluidas en Windows Server 2022?**

- a) Completas e incrementales.
- b) Completas y diferenciales.
- c) Únicamente completas.
- d) Completas y de sistema.

Dado que la opción *triggers* está activada por defecto en *mysqldump*, no es necesario incluirla en la instrucción, pero si lo que queremos es excluir los disparadores del volcado, podemos hacerlo mediante la opción *skip-triggers.*

### Para + info

![](_page_184_Picture_7.jpeg)

### **7.1.3. Recuperación del sistema y de los datos**

Cuando ocurre algún error en el sistema que impide su correcto funcionamiento, o se ha producido alguna circunstancia que ha derivado en la corrupción o destrucción de los datos almacenados en una BD, podemos recurrir al conjunto de copias de seguridad físicas y lógicas para recuperar la plena funcionalidad del sistema desde un punto lo más actualizado posible, con objeto de minimizar la pérdida de datos ocasionada por el fallo.

Si el error se ha producido a nivel de sistema operativo, o afecta a la estructura de archivos del SGBD, utilizaremos el conjunto de copias de sistema (completas, diferenciales e incrementales) para revertir el error, y, posiblemente, complementaremos la recuperación con una copia lógica más reciente para restaurar los datos de las BD. Si únicamente afecta a las BD, lo más efectivo será emplear, directamente, el conjunto de copias lógicas.

### **Recuperación del sistema**

Como vimos en el apartado anterior, la herramienta de copias de seguridad de Windows Server nos ofrece la posibilidad de realizar copias de servidor completas y e incrementales, a partir de las cuales podremos restaurar, íntegramente, la estructura de archivos del servidor desde el entorno de reparación del sistema (si el arranque fracasa dos veces seguidas, Windows entrará automáticamente en este modo). También podemos restaurar Windows desde una imagen de sistema mediante el Inicio avanzado, que encontraremos en la sección *Recuperación* de la configuración del sistema.

No obstante, y dado que no siempre es posible entrar en el entorno de reparación o utilizar el inicio avanzado, es muy recomendable crear una unidad de recuperación del sistema. En Windows Server 2022 esto se realiza mediante la opción Unidad de recuperación que encontraremos en el menú Herramientas del Administrador del servidor. Con ella será posible incluso reinstalar de cero el sistema operativo, en caso de no contar con una copia de seguridad viable.

Podemos crear la unidad de recuperación usando una unidad flash, o *pendrive*, o bien un disco externo (pero no un DVD-ROM), siempre que tengan una capacidad de almacenamiento de al menos 8 GB. Lógicamente, los datos que estuvieran guardados en el dispositivo se eliminarán en el proceso.

Cuando arranquemos desde el medio de instalación, y tras el diálogo de elección del idioma, se nos ofrecerá la posibilidad de instalar el sistema o de reparar el equipo, con lo cual entraremos en el modo de reparación. A partir de este punto, las opciones que debemos de escoger son *Solucionar problemas* > *Recuperación de imagen del sistema*, y seleccionar el perfil de administrador. De este modo, finalmente se abrirá el asistente *Recrear la imagen del equipo*, donde podemos usar la imagen más reciente disponible, o, si utilizamos medios extraíbles, podemos seleccionarla manualmente.

![](_page_185_Picture_5.jpeg)

*Asistente para crear una unidad de recuperación en Windows Server 2022.*

La operación formateará todos los discos conectados, formen o no parte del respaldo (excepto obviamente aquel donde tenemos la copia de seguridad), así que, si queremos conservar los datos de los dispositivos que no estuvieran presentes en el momento de realizar la copia, podremos excluirlos para conservar sus datos. Si solo existen los discos necesarios para la ejecución del sistema, esta opción estará desactivada. Además, si la copia está en algún dispositivo RAID por hardware que no haya sido reconocido automáticamente por el sistema de reparación de Windows, podremos también proporcionar los controladores necesarios para su detección y uso.

![](_page_186_Picture_2.jpeg)

Ya solo nos quedará revisar la información acerca de la copia que vamos a restaurar, pulsar el botón Finalizar, y aceptar el diálogo de advertencia acerca de la eliminación de los datos en los discos implicados para iniciar la recuperación del sistema.

![](_page_186_Picture_5.jpeg)

*Opciones de restauración adicionales.*

### **Recuperación de los datos a partir de una copia física**

Si el problema no está en la carga y funcionamiento del sistema operativo, sino en la integridad del propio SGBD, podemos utilizar una combinación de copias físicas y lógicas para repararlo.

En Windows Server 2022, para restaurar la estructura de archivos del SGBD a partir de una copia física del sistema, podemos usar la opción *Recuperar* de *wbadmin*, que iniciará el *Asistente para recuperación* de la herramienta Copias de seguridad de Windows Server. Este mecanismo nos permitirá seleccionar los elementos que deseamos restaurar dentro de cualquiera de las copias de seguridad realizadas con anterioridad. Para ello, seguiremos los pasos que se indican a continuación:

- 1. Escogemos la ubicación donde está almacenada la copia de seguridad cuyos archivos deseamos recuperar. Si optamos por una ubicación diferente al propio servidor, se añadirán dos pasos donde especificaremos el tipo de ubicación (unidad local o carpeta compartida), y la letra de unidad o la ruta UNC de la ubicación remota.

- 2. Windows analiza la ubicación especificada y detecta las copias disponibles, marcándolas en negrita sobre las fechas de un calendario. Para cada copia se nos indica la fecha y hora de realización, la ubicación, su disponibilidad y los elementos que se incluyeron en ella.

- 3. Una vez seleccionada la copia, podemos indicar qué tipo de elementos deseamos recuperar. En el caso de un SGBD, lo habitual será seleccionar la opción *Archivos y carpetas*.

- 4. A continuación, se nos mostrará el árbol de archivos que contiene la copia, que podemos navegar hasta llegar a los que contienen los archivos físicos del SGBD.

- 5. Seguidamente, se nos ofrecen diversas opciones de recuperación, como restaurar los archivos en una ubicación diferente a la original, conservar o sobrescribir los archivos restaurados, en caso de existir, y restaurar o no los permisos de los archivos recuperados.

![](_page_189_Picture_1.jpeg)

![](_page_189_Picture_5.jpeg)

- 6. El último paso del asistente nos ofrece un resumen de los archivos a recuperar y de las opciones seleccionadas; confirmaremos la operación pulsando el botón *Recuperar*.

![](_page_189_Picture_4.jpeg)

### **Recuperación de los datos a partir de una copia lógica**

Los métodos de recuperación de copias lógicas de las BD difieren según el SGBD utilizado, como ya vimos en el apartado anterior dedicado a los mecanismos de respaldo, así como del tipo de copia que se haya realizado.

Por ejemplo, y en el caso de MySQL, para volver a importar los datos previamente exportados a un archivo de texto utilizando una sentencia de tipo *SELECT INTO OUTFILE* (o desde cualquier otro archivo de texto delimitado por caracteres, como los que genera *mysqldump* con la opción *tab*), contamos con la sentencia *LOAD DATA*, cuya sintaxis básica es la siguiente:

LOAD DATA INFILE 'películas.csv' INTO TABLE filmoteca.películas;

Esta sentencia leerá los datos delimitados por tabuladores desde el archivo CSV especificado, y los almacenará en la tabla *películas*, perteneciente a la BD *filmoteca*. Si la tabla de destino no está vacía, podemos usar los modificadores *REPLACE* e *IGNORE* para reemplazar o ignorar, respectivamente, cualquier fila duplicada. También podemos especificar el carácter separador, el de escape y el delimitador de cadena para los campos, así como los caracteres de inicio y de terminación de la línea. De esta forma, para reemplazar los datos duplicados e importar datos delimitados por comas, utilizaríamos una sentencia como la siguiente:

1 LOAD DATA INFILE 'pelis.csv' REPLACE 2 INTO TABLE filmoteca.películas 3 FIELDS TERMINATED BY ',' ENCLOSED BY '"' 4 LINES TERMINATED BY '\r\n' 5 IGNORE 1 LINES;

Esta sentencia importaría a nuestra tabla películas el archivo pelis.csv, cuyo contenido estaría delimitado por comas (delimitador de campo), comillas dobles (delimitador de cadena), y los caracteres de retorno de carro y nueva línea (delimitador de fila). Incluimos IGNORE para que no se tome en cuenta la primera línea, donde figuran los nombres de columna. Este es el formato de texto delimitado que utilizan, por defecto, muchas herramientas de exportación de tablas, y cuyo contenido podría tener, en nuestro caso, la siguiente codificación:

"idPelícula","título","año","país","director","idGénero" "1","Vértigo (De entre los muertos)","1958", "Estados Unidos","Alfred Hitchcock","7"

"2","Bullet Train","2022", "Estados Unidos","David Leitch","1" "3","Un pez llamado Wanda","1988", "Reino Unido","Charles Crichton","3" "4","Lawrence de Arabia","1962", "Reino Unido","David Lean","5" "5","Horizonte Final","1997", "Reino Unido","Paul W.S. Anderson","6" "6","Salvar al soldado Ryan","1998", "Estados Unidos","Steven Spielberg","2" "7","El fantasma del Paraíso","1974", "Estados Unidos","Brian De Palma","9" "8","The Whale","2022", "Estados Unidos","Darren Aronofsky","4"

Si no queremos recurrir a *mysql*, podemos realizar este mismo procedimiento utilizando la herramienta *mysqlimport*.

Por ejemplo, la siguiente instrucción importará los datos del archivo *películas.csv* con el mismo resultado que la sentencia *LOAD DATA* que acabamos de explicar:

> mysqlimport -h localhost -u root -p*contraseña* --replace --fields-terminated-by=, --fields-enclosed-by=\" --lines-terminated-by=\r\n --ignore-lines=1 filmoteca películas.csv

Nótese que, al final de la instrucción, especificamos el nombre de la BD (*filmoteca*) en primer lugar, y el nombre de la tabla, en última instancia, a través del propio nombre del archivo.

Si hemos realizado la copia mediante la herramienta *mysqldump*, podemos restaurar los datos utilizando *mysql* desde una ventana de Símbolo del sistema.

Por ejemplo, para restaurar los datos contenidos en el archivo *copia. sql* en la base de datos *filmoteca* (suponiendo que este estuviera almacenado en la carpeta *C:\copias*), podríamos utilizar la siguiente instrucción:

> mysql -h localhost -u root -p filmoteca < "C:/copias/copia.sql"

También es posible restaurar los datos desde el entorno de *mysql* con la instrucción *source*; por ejemplo:

### **7.2. Actualización del SGBD y migración de BD**

Entre las operaciones de mantenimiento del sistema, la actualización del SGBD es un procedimiento relativamente habitual, cuanto menos, entre versiones principales del software, ya que estas corrigen errores importantes, suelen añadir funciones y tienden a mejorar el rendimiento del sistema en general. No obstante, también puede ocasionar problemas imprevistos, especialmente cuando se actualiza desde una versión previa muy antigua, por lo que no debe realizarse nunca directamente en el servidor de producción.

El procedimiento de actualización recomendado sería, pues, clonar el servidor en una máquina para pruebas, y, una vez actualizada y verificado su correcto funcionamiento, acometer la actualización en producción, no sin antes realizar una copia de seguridad íntegra de todas las bases de datos. En el caso de MySQL, se debe incluir en la copia la DB de sistema, donde se ubican las tablas del diccionario de datos y las tablas de sistema.

### **Actualización de MySQL**

Un aspecto importante a tener en cuenta a la hora de actualizar el SGBD son las llamadas rutas de actualización. Así, normalmente no es posible actualizar desde cualquier versión hasta cualquier versión, sino que es necesario seguir un procedimiento distinto según la versión del SGBD que tengamos en producción. De esta forma, en MySQL solo podremos actualizar a la versión 8.0 desde la versión 5.7.9 o superior, por lo que, si nuestro sistema está basado en cualquier versión anterior (5.6, por ejemplo), primero deberemos actualizarlo a la versión 5.7 antes de poder llevarlo hasta la 8.0.

Para actualizar el SGBD, muchas veces es posible utilizar su instalador, que se ocupará de reemplazar todos los archivos antiguos por sus nuevas versiones y realizará los cambios necesarios en el sistema. No obstante, si la actualización es entre versiones principales (por ejemplo, de MySQL 5.7 a 8.0), casi siempre será necesario recurrir a una actualización manual. En Windows, esto implica descargar la distribución del SGBD en un formato de archivo comprimido (ZIP, por ejemplo), y realizar el siguiente procedimiento:

- 1. Detenemos el servidor con las instrucciones *sc stop* o *net stop*, en caso de ejecutarse como servicio, o bien *mysqladmin* si lo hace como programa.

Suponiendo que el nombre del servicio sea *MySQL80*, las posibilidades serían las siguientes:

> sc stop mysql80 > net stop mysql80 > mysqladmin -u root -p*contraseña* shutdown

Obviamente, también podemos utilizar el complemento *Servicios* de la MMC para detener los servicios, o bien, como último recurso, utilizar el Administrador de tareas para finalizar manualmente todos los procesos abiertos por *mysql.exe*. En cualquier caso, es importante reseñar que, si tenemos en funcionamiento varias instancias de MySQL, tendremos que asegurarnos de haberlas detenido todas antes de acometer la actualización del SGBD.

- 2. Extraemos los archivos del paquete de actualización en la ruta de instalación del SGBD, sobrescribiendo los archivos antiguos con los nuevos.
- 3. Reiniciamos el servidor utilizando las instrucciones *sc start*, *net start* o *mysqld*, según el caso.
- 4. En función de la nueva versión del SGBD que hayamos instalado, puede ser obligatorio comprobar la integridad de las tablas de sistema, repararlas en caso de necesidad, y actualizarlas para poder disfrutar de las posibles nuevas características introducidas en el gestor. En MySQL, a partir de la versión 8.0.16, de esto se ocupa automáticamente el propio SGBD, pero en versiones anteriores es necesario ejecutar la herramienta *mysql\_upgrade*; por ejemplo, para actualizar las tablas de la instancia por defecto, en el puerto 3306, utilizaríamos la siguiente instrucción:

### > mysql\_upgrade --protocol=tcp -P 3306

### **Migración de BD con MySQL Workbench**

El proceso de **migración de bases de datos** es, a menudo, considerablemente **complejo**, y realizarlo de forma manual **requiere invertir mucho tiempo**, lo que se traduce en varias horas, o incluso días, en los que el servidor tiene que estar detenido. Por este motivo, se han desarrollado herramientas que facilitan y aceleran este tipo de operaciones, que, casi siempre, implican el análisis de los datos que se van a migrar, mapear correctamente los objetos migrados en el nuevo servidor y mover los datos a una versión actualizada del mismo SGBD, o hasta un SGBD totalmente distinto.

Un ejemplo de este tipo de herramientas gráficas es el asistente de migración que se incluye MySQL Workbench, el cual permite importar bases de datos de otros SGBD, o copiarlas de una instancia de MySQL a otra, con mucha facilidad y rapidez.

El asistente utiliza el controlador ODBC para conectar con la base de datos de origen, y requiere de los privilegios necesarios para poder leer la información de esquema y los datos de la BD de origen, así como los que se exigen para crear objetos e insertar datos en el servidor de destino. Además, deberemos asegurarnos de que la opción *max\_allowed\_packet* del servidor de destino es lo suficientemente grande como para albergar el valor de campo más largo de la BD de origen.

![](_page_194_Picture_3.jpeg)

Para ejemplificar el proceso de migración con el asistente de MySQL Workbench, trasladaremos la base de datos *filmoteca* a una segunda instancia local de MySQL, configurada como servicio, en el puerto 3308, bajo el nombre de *MySQL81*:

- 1. Abrimos el menú *Database* de MySQL Workbench y seleccionamos la opción *Migration Wizard*. En la pantalla de introducción, pulsamos el botón *Start Migration* para iniciar el asistente.

![](_page_194_Picture_9.jpeg)

- 2. Para realizar migraciones desde otros SGBD soportados, es necesario contar con la versión 2.1.8 o superior del módulo *pyodbc* de Python (aparecerá un mensaje advirtiéndonos de esta dependencia). En Windows podemos instalar este módulo, desde una ventana de Símbolo del sistema, mediante la siguiente instrucción:

Recuerda el procedimiento para instalar y configurar el conector ODBC de MySQL consultando el apartado:

**3.3.2.** *Configuración de acceso remoto*

Visita las páginas

![](_page_195_Picture_2.jpeg)

- 3. En primer lugar, seleccionaremos el SGBD o instancia de MySQL de origen. En el cuadro desplegable *Database System* veremos los SGBD compatibles con la herramienta. En nuestro caso, escogeremos *MySQL* y la conexión correspondiente a la instancia donde tenemos la base de datos que vamos a migrar (*MySQL80*, en el puerto 3306). Dado que los parámetros ya están almacenados para esta conexión, no necesitaremos rellenar ninguno de los campos subsiguientes. En caso contrario, tendremos que proporcionar los parámetros de la conexión (anfitrión, puerto, usuario y contraseña), y cualquier otro parámetro adicional. Podemos comprobar si esta configuración funciona pulsando el botón *Test Connection*.

![](_page_195_Picture_4.jpeg)

- 4. En segundo lugar, seleccionaremos la conexión al servidor de destino (en nuestro ejemplo, la segunda instancia, *MySQL81*, en el puerto 3308), cuyos parámetros de configuración deberemos proporcionar también. Al igual que en el paso anterior, podemos comprobar la validez de esta configuración mediante el botón *Test Connection*.

- 5. Si las conexiones se han configurado de la manera correcta, y los componentes ODBC requeridos están instalados en el sistema, el asistente conectará con el SGBD de origen y recuperará su lista de esquemas.

- 6. En el siguiente paso, podremos seleccionar cuáles de los esquemas listados deseamos migrar; en nuestro caso, seleccionamos únicamente la BD *filmoteca*.

- 7. El asistente se conectará de nuevo al SGBD de origen, y analizará los metadatos de los esquemas seleccionados para determinar su estructura.

![](_page_197_Picture_2.jpeg)

- 8. La siguiente fase del asistente consiste en la selección de los objetos que se van a migrar desde las BD seleccionadas. En nuestro caso, disponemos de dos tablas y de dos vistas; podemos seleccionarlas todas, o bien usar los botones *Show Selection* para seleccionar cuáles de los objetos se van a migrar.

![](_page_197_Picture_4.jpeg)

- 9. En el paso siguiente, los objetos de origen se convierten a objetos compatibles con MySQL, y se generan las correspondientes definiciones que se utilizarán en las sentencias *CREATE*. En cualquier momento del proceso, podemos obtener un listado pormenorizado de las operaciones que realiza el asistente pulsando el botón *Show Logs*.

![](_page_198_Picture_1.jpeg)

10.A continuación, se nos ofrecerá la oportunidad de editar manualmente la definición de los objetos migrados, antes de aplicarlos a la base de datos de destino. A través de la lista desplegable *View* podremos ver si se ha producido algún problema durante la migración (opción *Migration Problems*), una lista de los objetos de origen y de destino (*All Objects*), y el mapeo de las columnas (*Column Mapping*). En este último apartado podremos editar directamente el *script* SQL que se usará para recrear cada uno de los objetos seleccionados en el servidor de destino, renombrando de esta forma los esquemas y cambiando las definiciones de columna según nuestras necesidades.

![](_page_198_Picture_4.jpeg)

- 11. Seguidamente, tendremos la posibilidad de crear el esquema en el SGBD de destino, o de generar simplemente el *script* de migración (o ambas cosas), así como la de mantener los esquemas que ya existan en el destino. Esto significa que los objetos que ya existan no se recrearán ni se actualizarán con los datos migrados.

![](_page_199_Picture_1.jpeg)

- 12. En el siguiente paso, se ejecuta el guion SQL definido en el asistente, creándose de esta forma, en el destino, los esquemas y objetos migrados.

![](_page_199_Picture_3.jpeg)

13.No obstante, los datos almacenados en las tablas no se han migrado aún, lo que nos ofrece la posibilidad de editar los *scripts* de creación y pulsar el botón *Recreate Objets* para regenerarlos, o incluso de ir hacia atrás en el asistente para cambiar cualquier parámetro de la migración. Si no observamos ningún error, podemos avanzar hacia la fase siguiente, donde se realizará la migración de los datos en sí.

![](_page_199_Picture_5.jpeg)

- 14. El primer paso en la migración de datos es definir la forma en que esta se va a realizar. Podemos hacerla en línea, o bien crear sendos archivos de proceso por lotes que nos van a permitir, o ejecutar la migración en un momento posterior, o realizarla en el propio servidor de origen, generando así un paquete ZIP que contendrá el volcado de los datos y el script de carga. En este apartado también podemos definir: el número de tareas que se utilizarán, en paralelo, para transferir los datos; si se eliminarán los datos de las tablas de destino antes de copiar los nuevos; si el controlador enviará los datos ya codificados en UTF-8; y si se generará una salida de depuración.

![](_page_200_Picture_4.jpeg)

- 15. En el segundo paso, la herramienta procede a migrar los datos desde las tablas de origen hasta las de destino.

![](_page_200_Picture_7.jpeg)

16.Por último, el asistente nos muestra el correspondiente informe de migración.

### **7.3. Gestión de usuarios y perfiles de administración en un SGBD**

La gestión de usuarios y roles en un Sistema Gestor de Bases de Datos (SGBD) es fundamental para garantizar la seguridad, la administración eficiente y la integridad de los datos. A continuación, se describe cómo se manejan los usuarios, roles y niveles de administración en un SGBD, y cómo funciona esta gestión en herramientas como **phpMyAdmin**.

### **Usuarios en un SGBD**

Los usuarios en un SGBD representan entidades (personas, sistemas, o aplicaciones) que tienen acceso a la base de datos. Cada usuario tiene su propio conjunto de permisos y privilegios que determinan qué acciones puede realizar en la base de datos. Los tipos de usuarios pueden variar, pero se pueden clasificar en:

- **Usuarios administradores**: son aquellos con privilegios avanzados que les permiten realizar tareas de configuración y mantenimiento del SGBD. Pueden crear bases de datos, gestionar usuarios, realizar copias de seguridad, restaurar datos y supervisar el rendimiento.
- **Usuarios de aplicación**: son usuarios que representan a aplicaciones que acceden a la base de datos. Generalmente tienen permisos limitados para realizar operaciones específicas, como insertar, actualizar o consultar datos, pero no pueden alterar la estructura de las bases de datos.
- **Usuarios finales**: son usuarios que acceden a los datos de la base de datos mediante aplicaciones. Generalmente tienen permisos muy restringidos y pueden únicamente consultar o interactuar con la información según su perfil.
- **Usuarios invitados o de lectura**: son usuarios que solo tienen acceso de lectura a la base de datos y no pueden realizar modificaciones en los datos.

### **Roles de los usuarios en un SGBD**

En un SGBD, los **roles** definen conjuntos de permisos y privilegios que pueden ser asignados a uno o más usuarios. Los roles permiten agrupar permisos para simplificar la gestión de acceso. Los roles más comunes incluyen:

- **Administrador del sistema** (DBA): el rol más alto en el SGBD. El DBA tiene todos los privilegios y puede realizar cualquier operación en el sistema, como la creación de bases de datos, usuarios y la configuración del sistema.
- **Desarrollador de bases de datos**: este rol incluye permisos para crear, modificar y eliminar objetos dentro de una base de datos (tablas, índices, vistas, etc.), pero no tiene privilegios para gestionar el sistema en su totalidad.
- **Analista o consultor de datos**: tiene permisos para ejecutar consultas y analizar los datos, pero no puede realizar modificaciones en la estructura de la base de datos ni administrar usuarios.
- **Usuario de aplicación**: tiene permisos para realizar operaciones de lectura y escritura en las tablas a las que su aplicación necesita acceder.
- **Usuario de solo lectura**: tiene permisos únicamente para consultar los datos y no puede realizar modificaciones ni añadir datos.

### **Perfiles con rol de administración**

Dentro de un SGBD, los perfiles de administración suelen estar vinculados a usuarios con responsabilidades avanzadas. Algunos perfiles que deberían tener el rol de administración son:

- **Administrador del sistema** (DBA): este perfil es responsable del mantenimiento y la gestión global del SGBD. Debe tener control total sobre el sistema.
- **Administrador de seguridad**: responsable de la configuración de permisos, autenticación, y auditoría de accesos. A menudo tiene acceso avanzado para gestionar quién puede acceder a qué partes de la base de datos.
- **Administrador de copias de seguridad y recuperación**: se encarga de gestionar las políticas de respaldo y restauración de datos para asegurar que la base de datos esté protegida contra fallos.

Estos perfiles deben tener permisos para modificar la estructura del sistema, asignar roles a otros usuarios y realizar tareas críticas, como la optimización y respaldo de datos.

### **Niveles de administración en un SGBD**

En un SGBD, la administración se puede segmentar en diferentes niveles de control:

- **Nivel 1**, **administrador global o DBA**: tiene control completo sobre todas las bases de datos y usuarios. Puede crear, modificar, eliminar bases de datos, asignar roles y gestionar la configuración del sistema.
- **Nivel 2**, **administrador de bases de datos específicas**: tiene privilegios sobre una o más bases de datos en particular. Puede gestionar usuarios, crear y modificar estructuras de datos dentro de esas bases de datos específicas, pero no puede realizar cambios a nivel global del SGBD.
- **Nivel 3**, **administrador de mantenimiento y operaciones**: tiene permisos para realizar tareas de mantenimiento como respaldos, restauraciones y monitoreo del rendimiento, pero no puede realizar cambios estructurales importantes en las bases de datos.
- **Nivel 4**, **usuario avanzado o usuario con permisos de gestión parcial**: tiene permisos específicos, como ejecutar ciertas operaciones críticas, modificar tablas o ejecutar scripts, pero sin acceso completo a todas las funcionalidades del sistema.

### **Gestión de roles y usuarios en phpMyAdmin**

phpMyAdmin es una herramienta gráfica que permite la gestión de bases de datos MySQL. En esta herramienta, la gestión de usuarios y roles se puede realizar de manera sencilla desde la interfaz gráfica. A continuación, se describe cómo manejar los roles y permisos en phpMyAdmin:

### **Creación de usuarios en phpMyAdmin**

- 1. Inicia sesión en phpMyAdmin.
- 2. Dirígete a la pestaña *Usuarios*.
- 3. Haz clic en *Añadir usuario*.
- 4. Rellena los datos del usuario, como el nombre de usuario, el host (normalmente % para permitir acceso desde cualquier lugar), y la contraseña.
- 5. En la sección *Global privileges*, puedes seleccionar qué privilegios asignar al nuevo usuario. Las opciones incluyen:
  - ALL PRIVILEGES: da todos los permisos al usuario (equivalente al rol de administrador).

- SELECT, INSERT, UPDATE, DELETE: permisos para manipular los datos (lectura/escritura).
- CREATE, ALTER, DROP: permisos para crear, modificar y eliminar tablas y bases de datos.

### **Asignación de roles en phpMyAdmin**

- 1. En phpMyAdmin, los roles pueden configurarse manualmente asignando privilegios específicos a cada usuario.
- 2. Para hacerlo, ve a la pestaña *Usuarios*, selecciona el usuario que deseas modificar, y haz clic en *Editar privilegios*.
- 3. Podrás asignar permisos específicos a nivel de base de datos, tabla o incluso campo. Algunos ejemplos son:
  - **Permisos a nivel de tabla**: puedes otorgar a un usuario acceso a una tabla específica dentro de una base de datos, permitiendo solo las operaciones que sean necesarias.
  - **Permisos a nivel de base de datos**: otorga a un usuario acceso total o parcial sobre una base de datos completa.

### **Niveles de administración en phpMyAdmin**

En phpMyAdmin, puedes aplicar niveles de administración ajustando los privilegios de los usuarios de la siguiente manera:

- **Administrador global**: selecciona todos los privilegios a nivel global al crear o modificar un usuario. Este usuario tendrá acceso total a todas las bases de datos y podrá realizar cualquier operación.
- **Administrador de una base de datos específica**: durante la edición de los privilegios, selecciona una base de datos específica y asigna permisos solo sobre esa base.
- **Usuarios con privilegios limitados**: otorga permisos solo a nivel de tabla o campos específicos. Este tipo de usuario puede ser útil para situaciones donde necesitas un control granular de las operaciones permitidas.

Con esta funcionalidad en phpMyAdmin, puedes gestionar con precisión los roles y niveles de acceso, asegurando que solo los usuarios autorizados puedan realizar tareas críticas dentro del sistema. Este enfoque garantiza un equilibrio entre la seguridad y la eficiencia en la gestión de bases de datos, al proporcionar diferentes niveles de acceso según las necesidades de los usuarios y los perfiles de administración.
