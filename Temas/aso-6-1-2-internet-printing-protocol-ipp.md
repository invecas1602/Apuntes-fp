# **6.1.2. Internet Printing Protocol (IPP)**

Uno de los protocolos de impresión más utilizados por los servidores de impresión es el Internet Printing Protocol (IPP), es decir, el Protocolo de impresión de Internet.

El IPP es un estándar abierto que utiliza el protocolo TCP como protocolo de transporte, normalmente a través del **puerto 631**. Está basado en el modelo cliente-servidor, en el que el cliente envía los trabajos de impresión a un servidor, que es el encargado de gestionarlos y de comunicarse directamente con la impresora. El formato de las instrucciones de este protocolo es muy similar al de las solicitudes HTTP y, como en el caso del LPD, admite una amplia variedad de atributos de impresión: número de copias, tamaño, calidad y orientación del papel, calidad de la impresión, etc. En cuanto a la naturaleza de los trabajos, pueden ser de impresión, escaneo, copia y envío de fax.

Utilizando el IPP, los clientes pueden recibir información actualizada, no solo acerca de si la impresora los ha recibido o si se han completado, sino también del progreso, en tiempo real, de la impresión en sí.

Aún más importante es su compatibilidad con el cifrado TLS, por lo que puede utilizarse para enviar los trabajos de forma segura a través de una red local o de Internet, evitando de esta forma el acceso no autorizado a datos confidenciales.
