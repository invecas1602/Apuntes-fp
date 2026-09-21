# **6.5.2. Agrupación de impresoras en Windows**

En Windows podemos unir varias impresoras físicas en una sola impresora lógica. Para el cliente, esta aparecerá como una única impresora de red, aunque los trabajos se imprimirán en cualquier impresora libre dentro del grupo.

Para poder crear un grupo de impresoras, es necesario que todas funcionen utilizando un mismo controlador de impresión, lo que implica que sean idénticas o compatibles entre sí. Además, dado que no es posible saber de antemano en cuál de las impresoras se imprimirá cada trabajo, es muy recomendable que todas estén situadas en una misma ubicación física.

#### El procedimiento para agrupar impresoras es el siguiente:

- 1. Abrimos *Herramientas* > *Administración de impresión* en el Administrador del servidor. Desplegamos el árbol del servidor de impresión, seleccionamos *Impresoras* y hacemos clic derecho sobre la impresora a partir de la cual queremos crear el grupo. Aunque podemos seleccionar cualquier impresora previamente configurada, es recomendable crear una impresora nueva, en un nuevo puerto, que nos sirva como impresora virtual en la que agrupar todos los dispositivos físicos. A continuación, en el menú contextual de la impresora, escogemos *Propiedades*.
- 2. Nos situamos en la pestaña *Puertos*, marcamos la casilla *Habilitar agrupación de impresoras* y marcamos la casilla correspondiente al puerto de todas aquellas impresoras que deban formar parte de ese mismo grupo.

De esta forma, cuando la impresora virtual en la cual hayamos activado la agrupación de impresoras reciba un trabajo, se hará cargo de él la primera impresora física libre dentro del grupo. Hemos de tener en cuenta que, al igual que sucede en CUPS, los documentos se envían a los dispositivos en el mismo orden en que los hubiéramos agregado al grupo, por lo que añadiríamos primero las impresoras más eficientes.
