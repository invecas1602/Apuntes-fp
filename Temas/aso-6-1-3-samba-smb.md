# **6.1.3. Samba (SMB)**

Samba no es solo un protocolo para compartir archivos, sino que también puede actuar como cola de impresión (en inglés, *spooler*) de un sistema CUPS. Esto significa que la comunicación entre el cliente y la impresora se gestiona mediante Samba, incluyendo el envío, supervisión de estado y gestión de los errores relativos al trabajo de impresión.

Samba puede utilizar tres puertos TCP, dependiendo del protocolo de nuestra elección: el **139**, el **445** y el **631**. El puerto 139 se utiliza para compartir archivos e impresoras sobre TCP/IP mediante NetBIOS, un protocolo utilizado para proporcionar compatibilidad con sistemas operativos antiguos, como Windows XP. Sin embargo, NetBIOS es poco seguro, por lo que no es recomendable utilizarlo a no ser que se requiera de forma forzosa. En cualquier otra circunstancia, se utiliza el puerto 445 mediante el protocolo Server Message Block (SMB), más seguro y eficiente que NetBIOS. Además, Samba también soporta el IPP a través del puerto 631, por lo que puede utilizarse en red sin necesidad de instalar controladores adicionales.

Por otra parte, este protocolo admite el uso de funciones avanzadas que permiten filtrar y personalizar los trabajos de impresión. También proporciona la posibilidad de agrupar impresoras y llevar una contabilidad de las impresiones realizadas.

Aunque Samba no es el protocolo de impresión más popular, todas las características mencionadas lo convierten en un sistema muy potente y adaptable a una amplia variedad de entornos de impresión. De hecho, gracias a su gran versatilidad, es una opción a tomar muy en cuenta en redes heterogéneas participadas por equipos basados en Windows, Linux y macOS.

![](_page_159_Picture_4.jpeg)

#### Para + info

Además de facilitar la compartición de archivos e impresoras, Samba incluye características que lo convierten en un protocolo extremadamente versátil, especialmente en dominios basados en el Directorio Activo, con el cual se integra de forma nativa. Esto permite que los sistemas basados en Unix puedan unirse a un dominio AD, autenticándose con sus credenciales del directorio para acceder a los recursos compartidos. Además, Samba puede funcionar también como controlador de dominio, tanto primario (PDC) como de respaldo (BDC), soportando sólidos protocolos de autenticación, como Kerberos y NTLM, y sistemas de cifrado como TLS y la firma SMB.

![](_page_159_Picture_7.jpeg)

![](_page_160_Picture_9.jpeg)
