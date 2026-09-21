# **4.1.1. Secure Shell (SSH)**

El Secure Shell (SSH) es un protocolo de red criptográfico, lo que significa que, a diferencia de Telnet y otros protocolos inseguros, no envía los datos en texto plano, sino que los cifra. Además, hace uso de criptografía de clave pública y certificados digitales para la autenticación, garantizando que so lo los usuarios autorizados tengan acceso remoto a los equipos. Por ello, el SSH se utiliza de forma habitual para acceder y gestionar de forma segura un dispositivo remoto a través de una red no segura.

Por defecto, el SSH utiliza el puerto 22, pero admite el reenvío de puertos, lo que permite a los usuarios reenviar el tráfico de red de un puerto local a otro puerto remoto. Asimismo, puede emplearse para la transferencia de archivos, por lo que es un mecanismo útil para el envío y la recepción segura de archivos entre dos equipos.

Otra característica esencial del SSH es la posibilidad de ejecutar órdenes, a través de la interfaz de línea de órdenes del ordenador remoto, desde la propia interfaz de línea de órdenes del equipo local.

Aunque tanto Windows como Linux instalan, de forma predeterminada, un cliente SSH, para conectarnos con un ordenador remoto este debe tener instalado y funcionando un servidor SSH. La sesión se inicia introduciendo la dirección IP o nombre de anfitrión del equipo remoto, y proporcionando unas credenciales de acceso autorizadas.
