# **5.1. Concepto, técnicas y productos**

![](_page_133_Picture_1.jpeg)

Las principales características de un servidor de aplicaciones son:

- **Equilibrio de carga**: son capaces de distribuir las peticiones de los clientes entre varios servidores dispuestos en clúster para evitar que cualquiera de ellos se sobrecargue.
- **Caché de datos**: almacenan en una memoria caché los datos a los que los clientes acceden de forma más frecuente con objeto de reducir el número de peticiones a las bases de datos y a otros sistemas externos, lo que, a su vez, reduce la carga del servidor y contribuye a mejorar los tiempos de respuesta.
- **Agrupación de recursos**: pueden asignar una cantidad de recursos del sistema determinada (memoria, procesador, etc.) por aplicación y usuario.
- **Agrupación de conexiones**: las conexiones a las bases de datos de una aplicación pueden compartirse entre diferentes instancias de esta, evitando la necesidad de establecer una conexión por instancia.
- **Seguridad**: proporcionan los mecanismos necesarios de autenticación, autorización y cifrado para garantizar la seguridad e integridad de los datos transmitidos.

Un **servidor de aplicaciones** es un equipo de red diseñado para ejecutar múltiples instancias de aplicaciones personalizadas por usuario, y que está dotado de los recursos necesarios para atender un gran volumen de peticiones por parte de los clientes. De esta forma, los usuarios autorizados normalmente se conectan al servidor mediante el protocolo HTTP/HTTPS, y disponen de un conjunto propio de aplicaciones que pueden ejecutar, de forma remota, utilizando un simple navegador web.
