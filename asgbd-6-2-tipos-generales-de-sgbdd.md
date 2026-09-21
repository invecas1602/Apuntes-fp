# **6.2. Tipos generales de SGBDD**

Existen dos tipos generales de SGBDD: **homogéneos** y **heterogéneos**. Esta clasificación se basa en el grado de similitud del software utilizado, y en el nivel de autonomía de cada uno de los sistemas que integran el SGBDD.

### **SGBDD homogéneos**

En los sistemas homogéneos, el software utilizado es igual o muy similar (es decir, utilizan un SGBD idéntico o producido por la misma empresa), por lo que existe un alto nivel de compatibilidad e integración entre los diferentes sistemas que participan en el SGBDD. En este tipo de SGBDD, todos los sistemas tienen constancia del resto y cooperan para procesar las peticiones de los usuarios, que acceden a la BDD a través de una interfaz única como si se tratara de una BD simple.

Según el nivel de autonomía de cada SGBD, un sistema homogéneo puede catalogarse como **autónomo**, si cada sistema es independiente y se integra con el resto mediante una aplicación intermediaria, o **no autónomo**, lo que implica la presencia de nodos homogéneos entre los que se distribuyen los datos, y de un SGBD central que se encarga de coordinar el conjunto.

### **SGBDD heterogéneos**

En los sistemas distribuidos heterogéneos, los SGBD que lo integran pueden basarse en entornos de software totalmente diferentes, con sistemas operativos distintos, gestores de varias empresas y tecnologías diversas, y modelos de datos diferentes a los del resto. De esta forma, los SGBD que participan en un SGBDD heterogéneo pueden funcionar con una variedad de motores (jerárquicos, relacionales, orientados a objetos…), y puede que no tengan constancia del resto de los SGBD. Todas estas circunstancias hacen que los sistemas heterogéneos sean mucho más difíciles de gestionar, debido a que:

- Sus esquemas pueden ser muy diferentes, lo que dificulta el procesamiento de las consultas.
- El software puede ser muy distinto, lo que dificulta el procesamiento de las transacciones.
- Las posibilidades de cooperación entre los diferentes sistemas son, a menudo, muy limitadas.

Los SGBDD heterogéneos pueden clasificarse, a su vez, en **federados**, si se integran para funcionar como un único SGBD, o **no federados**, si utilizan algún tipo de módulo central que coordine el acceso a las diferentes BD.

![](_page_143_Diagram_2.jpeg)

Ponte a prueba

**Indica si es verdadera o falsa la afirmación siguiente: Para implementar un SGBDD, es necesario que los componentes de hardware y software de todos los sitios sean homogéneos.**

- a) Verdadero.
- b) Falso.

**Cuál de estas situaciones no es relevante a la hora de optar por un SGBDD:**

- a) Cuando los datos se distribuyen naturalmente entre diversos sitios.
- b) Cuando queremos ofrecer un alto nivel de disponibilidad de los datos.
- c) Cuando es necesario realizar copias de seguridad periódicas de los datos.
- d) Cuando queremos aumentar significativamente los tiempos de respuesta.

![](_page_143_Picture_8.jpeg)
