# **6.3.3. Agregar impresoras a los equipos cliente**

#### **En clientes Windows**

Para agregar una impresora configurada en un servidor de impresión basado en Windows Server a un equipo cliente con Windows 11, haremos lo siguiente:

- 1. Abrimos *Configuración* > *Bluetooth y dispositivos* > *Impresoras y escáneres* y pulsamos el botón *Agregar dispositivo*. Cuando aparezca el mensaje *La impresora que deseo no está en la lista,*  haremos clic en *Agregar manualmente.* Para agregar el dispositivo, utilizaremos su nombre de recurso de red (en nuestro ejemplo, \\*Servidor01*\Brother DCP-*L3550CDW*).

Es posible que, en función de la configuración de seguridad del servidor, sea necesario abrir el puerto 631 en el cortafuegos para permitir las conexiones IPP entrantes y salientes.

Atención

- 2. La impresora se instalará utilizando el controlador que hayamos configurado en el servidor de impresión, en este caso, el controlador IPP de Microsoft.

- 3. Una vez agregada la impresora, podemos imprimir una página de prueba para comprobar el correcto funcionamiento del servidor. Si consultamos la consola de *Administración de impresión* veremos, dentro del filtro *Impresoras con trabajos*, que la impresora tiene un trabajo en curso.

![](_page_169_Picture_4.jpeg)

- 4. Si hacemos clic derecho sobre la impresora y escogemos *Abrir cola de impresión*, podremos conocer detalles como el usuario al que pertenece el trabajo, el número de páginas o su tamaño.

Para agregar una impresora de red configurada en CUPS en un cliente Windows, realizaremos los siguientes pasos:

- 1. Cargamos en nuestro navegador la página relativa a las impresoras de la interfaz web de CUPS:

Debemos utilizar el protocolo HTTP (o HTTPS, si hemos configurado debidamente el cifrado SSL) y la dirección y puerto del servidor (en nuestro ejemplo, *10.0.1.55:631*). Hacemos clic en la impresora que queremos agregar y copiamos su URL (en nuestro ejemplo, *http://10.0.1.55:631/printers/DCP-L3550CDW*).

- 2. Abrimos *Configuración* > *Bluetooth* y *dispositivos* > *Impresoras y escáneres,* y pulsamos el botón *Agregar dispositivo.* Cuando aparezca el mensaje *La impresora que deseo no está en la lista*, haremos clic en *Agregar manualmente*. Para agregar el dispositivo, utilizaremos la URL que habremos copiado en el paso anterior mediante la opción *Seleccionar una impresora compartida por nombre.*

- 3. Escogemos el controlador de entre los ya instalados, pulsamos el botón *Windows Update* para actualizar la lista, o bien *Usar disco* si tenemos los controladores en cualquier ubicación de disco. En caso de no tener acceso a los controladores del fabricante, podemos utilizar uno genérico en su lugar, aunque en este caso las prestaciones del dispositivo pueden verse recortadas. Una vez instalado el controlador, podemos imprimir una página de prueba.

#### **En clientes Linux**

En este paso a paso, vamos a utilizar un cliente con Ubuntu 11.04.2 LTS conectado a un servidor de impresión con Debian 11:

- 1. Abrimos la *Configuración* del equipo y entramos en *Impresoras,*  donde pulsamos el botón *Configuración de impresora adicional* y, a continuación, el botón *Añadir.*

![](_page_171_Picture_6.jpeg)

- 2. En el apartado *Proporcione una URI*, escribimos la dirección del dispositivo (en nuestro caso, *http://10.0.1.55:631/printers/DCP-L3550CDW*).

Para agregar a un sistema Linux una impresora compartida en un dominio de Windows, es necesario agregar primero el equipo al Directorio Activo, instalando y configurando todos los paquetes y dependencias necesarios, incluyendo Samba. Dado que se trata de una operación relativamente compleja y, en muchas ocasiones, problemática, en estos casos se recomienda configurar la impresora directamente en un servidor Linux y compartirla mediante CUPS.

Atención

- 3. Escogemos el controlador de nuestra impresora.

- 4. Opcionalmente, editamos los detalles del dispositivo —nombre, descripción y ubicación—, tras lo cual pulsamos el botón *Aplicar*. Si lo deseamos, en este punto podremos imprimir una página de prueba.

- 5. La impresora ha quedado configurada, y podemos acceder a sus propiedades.
