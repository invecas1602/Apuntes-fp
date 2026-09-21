# **7.2.1. Configuración de DNS**

En la unidad 6 vimos como, durante el proceso de promoción a controlador de dominio, quedó instalado el rol de Servidor DNS en nuestro servidor de pruebas, *Servidor01*. No obstante, es posible instalarlo y configurarlo, de manera independiente, en cualquier servidor basado en Windows Server. Para ello, seguiremos estos pasos:

- 1. Abrimos el Administrador del servidor y, en el menú *Administrar,*  seleccionamos *Agregar roles y características.* Como *Tipo de instalación,* seleccionamos *Instalación basada en características o en roles.*

- 2. Tras seleccionar el servidor local, en el apartado *Roles de servidor*, seleccionamos *Servidor DNS*. En el diálogo que aparece a continuación, pulsamos el botón *Agregar características* y, a continuación, en *Siguiente*. Saltamos el apartado *Características* y, en *Confirmación*, pulsamos el botón *Instalar.*

![](_page_191_Picture_7.jpeg)

- 3. Una vez instalados los servicios de DNS y las características asociadas a ellos, debemos configurarlos. Para ello, en el Administrador

del servidor, abrimos el menú *Herramientas* y seleccionamos *DNS*. Aparecerá la consola *Administrador de DNS*, donde veremos la entrada correspondiente a nuestro servidor (en este caso, *Servidor02*) en el árbol *DNS*.

Desplegamos el árbol del servidor y entramos en *Zonas de búsqueda directa.* En este lugar es donde tenemos que crear las correspondencias entre los nombres de nuestros sistemas anfitriones y sus respectivas direcciones IP. Si habíamos instalado previamente el servidor DNS durante la promoción de un servidor a controlador de dominio (procedimiento descrito en el apartado *6.3.1. Directorio Activo*), aquí ya se nos habrán creado automáticamente dos zonas: *\_msdcs.midominio.local* y *midominio.local.* Si estamos instalando el DNS desde cero, deberemos crear manualmente la entrada correspondiente a *midominio. local* (substituye *midominio.local* por el nombre de tu dominio). Para ello, hacemos clic derecho sobre *Zonas de búsqueda directa,*  escogemos la opción *Zona nueva* y seguiremos los pasos del 4 al 8; por el contrario, si ya disponemos de dicha zona, saltaremos directamente al paso 9.

![](_page_192_Picture_3.jpeg)

#### 4. En el *Asistente para nueva zona*, escogemos *Zona principal.*

- 5. Como nombre de la zona especificaremos el nombre del dominio, en este caso, *midominio.local.*

- 6. Indicamos el nombre del archivo donde se guardará la información de la zona, que quedará almacenado en la carpeta *%systemroot%\ system32\dns.*

- 7. En el siguiente paso, nos aseguramos de no admitir actualizaciones dinámicas y, en el diálogo siguiente, pulsamos el botón *Finalizar* para concluir el asistente.

- 8. Si entramos en la nueva zona, veremos que contiene los registros de inicio de autoridad (SOA) y de servidor de nombres (NS) que corresponden a nuestro nombre de anfitrión (*servidor02.midominio.local*).

- 9. Aunque la resolución inversa de nombres no es obligatoria (a partir de una IP se obtiene el nombre del anfitrión), es esencial si queremos que el servidor DNS sea plenamente funcional, por lo que haremos clic derecho en *Zonas de búsqueda inversa* y escogeremos la opción *Zona nueva.*

![](_page_194_Picture_5.jpeg)

- 10. En el *Asistente para nueva zona,* escogemos de nuevo *Zona principal.*

- 11. Por defecto, crearemos la zona de búsqueda inversa para direcciones IPv4.

![](_page_195_Picture_3.jpeg)

- 12. Para identificar la zona de búsqueda inversa se requiere el identificador de red (las primeras cifras fijas de cualquier IP del dominio). En nuestro caso, usaremos *10.0.1* como identificador de red, lo cual creará una zona de búsqueda inversa con el nombre *1.0.10. in-addr-arpa.*

- 13. Como en el caso de la zona de búsqueda directa, la información se guardará en un archivo con extensión *dns* en la carpeta de sistema *%systemroot%\system32\dns.* En el siguiente diálogo, dejaremos también la opción por defecto de no admitir actualizaciones dinámicas, y finalizaremos el asistente.

- 14. Una vez configuradas las zonas, podemos proceder a crear los registros que corresponden a cada uno de nuestros anfitriones. Empezaremos por el propio servidor, haciendo clic derecho en *Zonas de búsqueda directa* > *midominio.local* y escogiendo la opción *Host nuevo (A o AAAA)* (omitir este paso en caso de que ya se haya configurado el servidor DNS junto con el Directorio Activo). En el diálogo *Host nuevo*, especificamos el nombre del equipo y su dirección IP. También podemos crear automáticamente un puntero PTR marcando la casilla correspondiente pero, a efectos de este tutorial, lo haremos, a continuación, de forma manual.

![](_page_196_Picture_2.jpeg)

- 15. Seguidamente, hacemos clic derecho en *Zonas de búsqueda inversa > 1.0.10.in-addr-arpa* y escogemos la opción *Nuevo puntero PTR.* Como Nombre de *host*, especificamos S*ervidor02.midominio. local* (o bien lo buscamos mediante el botón *Examinar*). De esta forma, el servidor DNS ha quedado correctamente configurado y listo para que le añadamos más entradas.

![](_page_196_Picture_5.jpeg)

- 16. Si queremos añadir un anfitrión para la dirección *www.midominio. local,* debemos crear un nuevo registro de anfitrión para el servidor web (*www*) en su correspondiente dirección IP (por ejemplo, 10.0.1.135). En este caso, marcamos la casilla para crear el registro del puntero asociado.

- 17. Finalmente, para comprobar que el servidor DNS está funcionando correctamente, ejecutamos *nslookup* en una ventana de Símbolo del sistema o de PowerShell. Podemos hacerlo, sin salir del Administrador de DNS, haciendo clic derecho sobre la entrada correspondiente al servidor (*SERVIDOR02*) y seleccionando la opción *Ejecutar nslookup.*

![](_page_197_Picture_3.jpeg)

- 18. Si introducimos en *nslookup* el nombre de anfitrión *www.midomino. local*, veremos los nombres y direcciones IP del servidor DNS y del anfitrión web. Si especificamos la IP 10.0.1.135, debemos obtener de vuelta la misma información, lo que significa que las zonas de búsqueda directa e inversa están funcionando correctamente.
