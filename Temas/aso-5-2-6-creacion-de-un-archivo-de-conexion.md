# **5.2.6. Creación de un archivo de conexión**

A partir de cada uno de los programas incluidos en la lista RemoteApp, podemos crear un archivo RDP para distribuirlo entre los clientes a los que queramos proporcionar acceso a dicho programa.

Para ello, cargamos con Microsoft Edge la página de Acceso web de RD en el propio servidor (podemos usar la dirección *https://localhost/ RDweb*) y, haciendo clic sobre cada programa, podremos guardar el correspondiente archivo RDP. Por ejemplo, en el caso de WordPad, el archivo generado se llamaría *cpub-wordpad-colección-CmsRdsh.rdp*, donde "colección" es el nombre de la colección de sesiones en la cual está incluida la aplicación.

Seguidamente, y utilizando cualquier método de nuestra elección, podemos distribuir directamente el archivo entre los equipos clientes. De esta forma, para acceder a los programas publicados, los clientes únicamente tendrán que hacer doble clic sobre el archivo RDP para ejecutarlos, de forma remota, utilizando sus credenciales.

Conclusiones En esta unidad hemos entrado en el detalle de los Servicios de Escritorio remoto y de su configuración y uso en servidores de aplicaciones. También hemos visto cómo implementar la seguridad basada en un certificado SSL, y cómo añadir anfitriones de sesión para crear un clúster de servidores, en el que los roles clave se distribuyen entre varios equipos que trabajan de forma coordinada. Utilizando estos instrumentos, es posible proporcionar a los equipos clientes acceso seguro a aplicaciones que se ejecutan en el entorno seguro del servidor.

![](_page_154_Picture_9.jpeg)

### Para + info

Si todavía no tenemos instalado ninguno de los roles relativos a los Servicios de Escritorio remoto en nuestro dominio, podemos realizar su despliegue desde el servidor que actuará como Host de sesión de Escritorio seleccionando el tipo de implementación estándar. De esta forma podremos seleccionar, durante el asistente de instalación, los servidores en los que se implementarán los diferentes roles.

![](_page_155_Picture_0.jpeg)

![](_page_155_Picture_1.jpeg)

Otro aspecto presente en el día a día de un administrador de sistemas es la impresión de documentos.

En casa o dentro de una pequeña oficina, cada equipo suele contar con su propia impresora pero, en entornos empresariales, normalmente existen equipos multifuncionales encargados de las tareas de escaneo, copia, envío e impresión de documentos en papel que se ponen a disposición de todos los usuarios de la organización. Una vez agregados a la red local mediante su propio adaptador de red TCP/IP, estas impresoras pueden configurarse de forma independiente en cada equipo, o bien agregarse a un servidor de impresión para que los trabajos lanzados por los usuarios puedan gestionarse de forma centralizada.

En cualquiera de los casos, es fundamental que los administradores de sistemas conozcan bien cuáles son las diferentes opciones a su disposición para priorizar ciertos equipos o poder dirigir los trabajos a los dispositivos adecuados, y sepan aplicarlas de la mejor manera según la configuración del entorno de impresión.
