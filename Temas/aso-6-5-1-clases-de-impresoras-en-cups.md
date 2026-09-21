# **6.5.1. Clases de impresoras en CUPS**

En CUPS, las impresoras se agrupan y priorizan utilizando un sistema de clases. No existe ninguna clase predefinida, y no es obligatorio incluir cada impresora existente dentro de una clase. Sin embargo, el uso de clases proporciona, como mecanismo de gestión centralizado, diversos beneficios, incluyendo los siguientes:

- Es posible configurar el sistema para que una impresora determinada rechace los trabajos mientras que los grupos los aceptan, lo que proporciona un mayor control sobre cómo se utilizan los recursos compartidos.
- Es posible reemplazar, añadir o eliminar impresoras dentro de cada clase de una forma rápida y sencilla.
- Es posible crear diferentes clases para que gestionen distintos trabajos: impresoras láser B/N para uso general, impresoras a color con restricciones según número de copias, etc.
- Permite dirigir el tráfico de impresión a un segmento aislado de la red para evitar que otros servicios consuman el ancho de banda disponible.
- Permite la redirección automática de los trabajos en caso de que alguna de las impresoras de la clase no pueda efectuar el trabajo por falta de tinta, papel u otra circunstancia.

Los criterios que se pueden utilizar para crear las clases son muy diversos, pero en la mayor parte de las ocasiones se crean por tipo de impresora, tipo de trabajo, ubicación física o departamento.

Existe también una clase implícita que se crea de forma automática cuando CUPS detecta dos o más impresoras con una configuración idéntica, de manera que los trabajos se envían a la primera impresora, que dentro de esta clase, queda disponible. Para determinar hacia cuál de las impresoras disponibles se dirigen los trabajos, se utiliza un sistema de prioridades determinado por el orden en que las impresoras se añadieron al grupo. De esta forma, a la hora de configurar una nueva clase, deberemos añadir en primer lugar aquellas impresoras que deban utilizarse de forma prioritaria según su tipo o prestaciones.

Las clases pueden pertenecer, a su vez, a otras clases, por lo que podemos crear clases de alta prioridad y clases de baja prioridad. A la hora de imprimir, una clase recibe el mismo tratamiento que una impresora individual.

Para añadir una impresora a una clase nueva o existente, utilizamos la instrucción *lpadmin -p nombre\_impresora -c nombre\_clase.* Para saber qué impresoras tenemos configuradas, podemos utilizar la orden *lpstat -v.* Por ejemplo, para crear una clase llamada *Contabilidad* e incluir en ella la impresora *DCP-L3550CDW*, utilizaríamos la siguiente instrucción:

sudo lpadmin -p DCP-L3550CDW -c Contabilidad

Para agregar una impresora llamada *EPSON-LaserBN* al mismo grupo, utilizaremos, por lo tanto, la orden siguiente:

sudo lpadmin -p EPSON-LaserBN -c Contabilidad

Podemos verificar qué impresoras están incluidas en una clase determinada (por ejemplo, *Contabilidad*) mediante la siguiente orden:

lpstat -c Contabilidad

Para eliminar una impresora dentro de una clase, utilizamos la opción *-r*:

sudo lpadmin -p EPSON-LaserBN -r Contabilidad

Podemos eliminar una clase mediante la opción *-x*:

sudo lpadmin -x Contabilidad

También podemos gestionar las clases utilizando la interfaz web de CUPS en la dirección *http://localhost:631/classes.*

Como hemos explicado, las clases se gestionan como si fueran impresoras físicas, por lo que disponemos de las mismas opciones de mantenimiento (pausar, rechazar, mover o cancelar los trabajos) y administración (modificar y borrar la clase, establecer sus opciones predeterminadas, establecer como clase predeterminada y establecer usuarios permitidos).
