# **5.1.1. Servidores de aplicaciones web**

#### **Apache Tomcat**

Uno de los servidores de aplicaciones más populares es Apache Tomcat. Se trata de un servidor de aplicaciones ligero y de código abierto que, usualmente, se utiliza para generar páginas web dinámicas basadas en el uso del lenguaje Java.

Estas son algunas de las características más destacadas de Apache Tomcat:

- **Soporte de clústeres**: proporciona las funciones necesarias para poder replicar sesiones y gestionar el despliegue de granjas de servidores.
- **Soporte para Servlets**: proporciona un contenedor para Servlets Java, que son aplicaciones que se ejecutan en el servidor y gestionan las peticiones HTTP, generando contenidos dinámicos, es decir, que cambian según el contexto de ejecución.
- **Soporte para JSP**: las Java Server Pages (JSP) son páginas web que contienen código Java. Como en el caso de los Servlets, se ejecutan en el lado del servidor para generar contenidos dinámicos.
- **Servidor HTTP**: Tomcat puede funcionar como servidor web independiente y, por lo tanto, gestionar las peticiones HTTP y contenidos web, tanto estáticos como dinámicos.
- **Control de acceso basado en roles**: permite gestionar los procesos de autenticación y autorización de forma segura.

#### Para + info

Los conjuntos de servidores de aplicaciones que gestionan grandes volúmenes de peticiones reciben el nombre de *granjas de servidores*. En esta configuración, los servidores de aplicaciones se agrupan en clústeres y se configuran de forma idéntica, de manera que pueda distribuirse la carga de trabajo entre todos ellos. Además, este diseño garantiza una alta disponibilidad de la plataforma, ya que el equilibrador de carga redirige las peticiones a otros equipos cuando cualquiera de los servidores falla o se sobrecarga. Esta disposición permite, a su vez, el crecimiento en horizontal de la plataforma, ya que basta con añadir nuevos servidores cuando se produce un aumento en el tráfico.

- **Cifrado de datos**: ofrece soporte para SSL/TLS, que garantiza la seguridad de las comunicaciones.
- **Extensibilidad**: Tomcat admite el uso de complementos personalizados con los cuales ampliar su funcionalidad y satisfacer las necesidades específicas de cada entorno.

#### **Oracle WebLogic**

En el ámbito empresarial, una de las plataformas más utilizadas para alojar aplicaciones Java es Oracle WebLogic, una familia de productos que incluye software para servidor (WebLogic Server), la creación y gestión de portales corporativos (WebLogic Portal) y la integración de soluciones empresariales (WebLogic Integration). Algunas de sus características principales incluyen:

- **Compatibilidad con Jakarta EE**: admite el uso de Servlets, JSP, EJB, JMS y JTA.
- **Alta disponibilidad**: permite crear y gestionar clústeres con mecanismos de equilibrado de carga y conmutación por error,

### Para + info

Otro de los servidores de aplicaciones más utilizados para el alojamiento de aplicaciones web basadas en Java es Red Hat JBoss Enterprise Application Platform (JBoss EAP), cuyas principales características son muy similares a las de Tomcat, aunque añade soporte para la edición empresarial de Java, Jakarta EE. Para quienes estén familiarizados con Tomcat, existe una alternativa llamada TomEE, que es plenamente compatible con Jakarta EE 9.1 Web Profile y MicroProfile 5. Para más información acerca de estas soluciones, visita sus páginas web mediante los siguientes enlaces:

Apache Tomcat: https:// bit.ly/422yy89

![](_page_135_Picture_7.jpeg)

![](_page_135_Picture_8.jpeg)

![](_page_135_Picture_9.jpeg)

Apache TomEE: https:// bit.ly/41GaYhZ

JBoss EAP: https://bit.ly/3n8Sqb4 lo que garantiza la disponibilidad de las aplicaciones en caso de fallo del servidor.

![](_page_136_Picture_2.jpeg)

- **Integración**: se integra fácilmente con aplicaciones basadas en portales y otras aplicaciones empresariales.
- **Herramientas de gestión y monitorización**: incorpora potentes herramientas para gestionar la plataforma de manera integral y monitorizarla mediante todo tipo de registros y métricas.
- **Seguridad**: incorpora técnicas de cifrado de datos, como el uso SSL/TSL, de control de acceso y de autorización, con el fin de garantizar la seguridad y la integridad del entorno, las conexiones y los datos transmitidos.
- **Extensibilidad**: admite el uso de complementos personalizados para adaptar las prestaciones del servidor al entorno.
