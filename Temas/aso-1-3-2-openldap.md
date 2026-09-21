# **1.3.2. OpenLDAP**

A continuación se expone el proceso de instalación del servicio OpenL-DAP para Linux. Hemos tomado como sistema de base la última versión oficial de Debian disponible al momento de redactar estas líneas (11.6.0), aunque el proceso debería ser aplicable a cualquier variante basada en esta distribución de Linux, como Ubuntu, Linux Mint, MX Linux o Knoppix.

En primer lugar, abrimos una ventana de terminal y actualizamos la lista de paquetes mediante la siguiente orden:

sudo apt update

A continuación, instalamos el paquete del servidor OpenLDAP ejecutando la siguiente instrucción:

sudo apt install slapd ldap-utils

Durante el proceso de instalación se nos solicitará una contraseña de administrador de LDAP. Una vez finalizado, podemos comprobar si el servidor OpenLDAP se está ejecutando mediante la siguiente instrucción:

sudo systemctl status slapd

Tras instalar el servidor, lo primero que debemos hacer es configurarlo. Para ello ejecutaremos las siguientes instrucciones:

su -

dpkg-reconfigure slapd

Esto permite definir el nombre distintivo base del directorio LDAP (en nuestro caso, usaremos el dominio *asir.local*), el nombre de la organización a la cual corresponde el directorio (emplearemos *asirldap*) y la contraseña del administrador del directorio (utilizaremos la misma que se nos solicitó al instalar el paquete *slapd*).

Para verificar el correcto funcionamiento del servicio, podemos utilizar la orden *ldapsearch* para obtener el *dn* del directorio (en nuestro caso, *dc=asir,dc=local*):

ldapsearch -H ldap:// -x -s base -b "" -LLL "namingContexts"

![](_page_24_Picture_6.jpeg)
