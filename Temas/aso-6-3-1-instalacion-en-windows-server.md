# **6.3.1. Instalación en Windows Server**

Para configurar un servidor de impresión basado en Windows Server 2022, seguiremos los pasos que se detallan a continuación:

- 1. Abrimos el Administrador del servidor, desplegamos el menú *Administrar* y escogemos *Agregar roles* y *características*. En el *Asistente para agregar roles y características*, escogemos, como tipo de instalación, la primera de las opciones, *Instalación basada en características o en roles*.

![](_page_162_Picture_6.jpeg)

- 2. Seleccionamos el servidor del dominio en donde queremos instalar el nuevo rol.

![](_page_162_Picture_9.jpeg)

- 3. En el apartado *Roles de servidor,* seleccionamos *Servicios de impresión y documentos*, y, en la ventana de dependencias, pulsamos el botón *Agregar características* para incluir en la instalación las herramientas relacionadas con este rol.

- 4. Avanzamos en el asistente hasta el apartado *Servicios de rol y* marcaremos los servicios que deseamos implementar. Si el servidor se halla en un entorno heterogéneo, podemos marcar el servicio LPD para dar soporte a este protocolo. En este caso, deberemos regresar al apartado *Características* para marcar la casilla *Monitor de puerto LPR.* No obstante, esta característica está en proceso de ser declarada obsoleta por Microsoft, por lo que, en este caso, se recomienda instalar un servidor de impresión de terceros como PaperCut. Para concluir con el asistente, iniciamos la instalación del rol pulsando el botón *Instalar.*

![](_page_163_Picture_3.jpeg)

- 5. Una vez instalados los Servicios de impresión, abriremos el menú *Herramientas* del Administrador del servidor y haremos clic en *Administración de impresión.* Este complemento nos dará acceso a la configuración de los servidores de impresión que hayamos

agregado (es posible añadir servidores de impresión haciendo clic derecho sobre el árbol de servidores y escogiendo *Agregar o quitar servidore*s).

![](_page_164_Picture_3.jpeg)

- 6. Dentro de cada servidor veremos los controladores, formularios, puertos e impresoras ya configurados en ellos. Para agregar una nueva impresora de red TCP/IP, el primer paso es añadir un puerto de red. Para ello, hacemos clic derecho sobre *Puertos* y escogemos *Agregar puerto* en el menú contextual. En el diálogo *Puertos de impresora*, escogemos el puerto TCP/IP estándar y pulsamos el botón *Puerto nuevo*.

- 7. El *Asistente para agregar puerto de impresora estándar TCP/IP* nos solicita un nombre de impresora o dirección IP, y el nombre que le vamos a asignar al puerto. Esto configurará un nuevo puerto para el dispositivo de impresión.

- 8. Es posible añadir puertos de red aunque el dispositivo de impresión esté fuera de línea. En tal caso, una vez finalizado el intento de detección, normalmente configuraremos el tipo de dispositivo como *Estándar* para un adaptador de red genérico, lo que añadirá un nuevo puerto con protocolo RAW (sin especificar).

![](_page_165_Picture_3.jpeg)

- 9. Para que cuando el dispositivo configurado ingrese en la red podamos administrarlo, es necesario instalar también los controladores. Para ello, hacemos clic derecho sobre *Controladores* y escogemos *Agregar controlador*. Pulsando el botón *Usar disco*, el asistente nos permite usar los controladores que tengamos almacenados en el equipo local.

- 10. A continuación, añadiremos manualmente la impresora (clic derecho sobre *Impresoras*, opción *Agregar impresora*). En el primer diálogo del asistente, escogemos el puerto que habíamos creado previamente.

- 11. Seguidamente, seleccionamos el controlador que también habíamos instalado de antemano.

- 12. Escogemos el nombre de la impresora y el nombre y detalles de recurso compartido, y avanzamos en el asistente hasta finalizarlo.

- 13. Para compartir una impresora en red y agregarla al directorio, hacemos doble clic sobre ella, vamos a la pestaña *Compartir* y activamos las casillas *Compartir esta impresora* y *Mostrar lista en el directorio.*
