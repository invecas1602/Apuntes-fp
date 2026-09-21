# **7.2.2. Configuración de DHCP**

Para ilustrar el proceso de configuración de un servidor DHCP vamos a utilizar nuestro controlador de dominio de pruebas, *Server01.midominio. local*, en el cual vamos a instalar los servicios necesarios para la asignación automática de direcciones IP dentro de un rango de la intranet.

Dado que los equipos conectados a este servidor DHCP lo van a utilizar como puerta de enlace, es necesario que este les proporcione salida a Internet, para lo cual, previamente, habremos de instalar los servicios de enrutamiento:

- 1. Abrimos el Administrador del servidor; en el menú *Administrar,*  seleccionamos *Agregar roles y características* y escogemos la *Instalación basada en características o en roles* en la sección *Tipo de instalación.*

- 2. Tras seleccionar el servidor local, en el apartado *Roles de servidor*  seleccionamos *Acceso remoto.*

![](_page_198_Diagram_7.jpeg)

- 3. Saltamos el apartado *Características* y, en *Acceso remoto* > *Servicios de rol*, activamos la opción *Enrutamiento*. Esto agregará una serie de características y servicios, las cuales aceptamos pulsando el botón *Agregar características*, con lo cual se marcará también la

casilla *DirectAccess* y *VPN (RAS)*. Con esto podemos ya finalizar el asistente e instalar todos los componentes seleccionados.

- 4. De vuelta al Administrador del servidor, abrimos la consola *Enrutamiento* y *acceso remoto* desde el menú *Herramientas*. Hacemos clic derecho sobre la entrada correspondiente a nuestro servidor y escogemos la primera de las opciones, *Configurar y habilitar Enrutamiento y acceso remoto.*

![](_page_199_Picture_4.jpeg)

- 5. En el diálogo *Configuración* del asistente, activamos *Traducción de direcciones de red (NAT)* y pulsamos *Siguiente*.

- 6. En este punto no podremos continuar con el asistente, ya que, en el apartado *Utilizar esta interfaz pública para conectarse a Internet*, no nos aparecerán las dos interfaces de red que tenemos en el equipo. Se trata de un error en Windows Server 2022 que podemos solventar cancelando el asistente e iniciándolo de nuevo. En esta ocasión sí aparecerán los dos adaptadores con los que está equipado nuestro servidor.

El primer adaptador tiene la IP fija 10.0.1.120 y está conectado a Internet a través del rúter. El segundo tiene 192.168.0.1 como IP fija y tiene acceso a otros clientes mediante una intranet sin salida a Internet en la que todos los clientes tienen asignadas sus respectivas IP fijas. Lo que pretendemos es que, mediante DHCP, estos clientes puedan recibir del servidor una IP libre en el rango de direcciones de 192.168.0.100 a 192.168.0.200 y que, a su vez, puedan tener salida a Internet a través de esta misma máquina.

Para concluir con el asistente, seleccionamos la interfaz con salida a Internet, denominada aquí *WAN.*

- 7. Una vez configurado el enrutamiento en el servidor, vamos a los clientes y configuramos la IP de la puerta de enlace como la de nuestro servidor (192.168.0.1). Si tenemos instalado el servicio DNS (ver apartado *7.2.1. Configuración de DNS*), podemos poner esta misma IP como servidor DNS preferido. En caso contrario, podemos utilizar cualquier servidor DNS público (por ejemplo, 208.67.222.222 y 208.67.220.220 para utilizar el de OpenDNS).

Los equipos cliente ya pueden tener salida a Internet a través del servidor utilizando su IP como puerta de enlace. El siguiente paso es configurar el servicio DHCP:

- 1. Una vez más, abrimos el Administrador del servidor y, en el menú *Administrar*, seleccionamos *Agregar roles y características*. En la sección *Tipo de instalación*, de nuevo escogemos la *Instalación basada en características o en roles* y, tras seleccionar el servidor local, en el apartado *Roles de servidor*, seleccionamos *Servidor DHCP*, agregando las características sugeridas por el asistente. Con esto ya podemos avanzar hasta finalizar el asistente.

Una vez realizada la instalación veremos, en el Administrador del servidor, un aviso de configuración posterior a la implementación, donde haremos clic en *Completar configuración de DHCP.*

- 2. En el apartado *Autorización del asistente,* simplemente tendremos que confirmar las credenciales del usuario administrador del servicio DHCP.

![](_page_202_Picture_2.jpeg)

- 3. Abrimos el menú *Herramientas* del Administrador del servidor y hacemos clic sobre *DHCP*, con lo que abriremos la consola de administración del servicio. Desplegamos el árbol del servidor y hacemos clic derecho sobre *IPv4*, escogiendo la opción *Ámbito nuevo* en el menú contextual.

![](_page_202_Picture_5.jpeg)

- 4. En el primer paso del asistente, indicamos el nombre del ámbito y, opcionalmente, una descripción.

- 5. Indicamos las direcciones inicial y final del ámbito. La información correspondiente a la longitud y máscara de subred se establecerán automáticamente.

- 6. Si queremos agregar alguna exclusión dentro del intervalo especificado, lo haremos en el siguiente diálogo del asistente.

- 7. A continuación estableceremos la duración de las concesiones de las direcciones IP (por defecto serán 8 días).

- 8. Avanzamos hasta el diálogo *Enrutador,* donde especificamos la puerta de enlace predeterminada para el ámbito que estamos configurando. Aquí especificaremos la IP del propio servidor que, en nuestro caso, y gracias al servicio de enrutamiento que le hemos instalado, es la máquina que ofrece a la intranet salida a internet.

![](_page_204_Picture_2.jpeg)

- 9. Como dirección del servidor DNS, para este ámbito dejaremos únicamente la misma que hemos utilizado como puerta de enlace (en nuestro caso, 192.168.0.1), eliminando cualquier otra que nos aparezca en la lista de IP. A continuación, podemos avanzar en el asistente hasta finalizarlo.

- 10. Para poner a prueba el servidor, vamos a un cliente y configuramos el protocolo IPv4 del adaptador de red para que obtenga su dirección IP y la dirección del servidor DNS automáticamente. Si, en la consola *DHCP*, entramos en *Servidor01.midominio.local > IPv4 > Concesiones de direcciones*, veremos la lista de clientes a los que nuestro servidor DHCP ha cedido una dirección IP, así como su fecha de expiración.
