# **1.5. Uso del directorio como mecanismo de acreditación**

Una vez configurado el servicio de directorio, podemos utilizarlo como mecanismo de acreditación en todos los ordenadores que forman parte del dominio. A continuación vamos a ver cómo configurar Debian 11 para utilizar el servidor LDAP en los inicios de sesión:

![](_page_33_Picture_2.jpeg)

- 1. En primer lugar, utilizando un terminal como superadministradores (*su -l*), instalamos el paquete libnss-ldapd, que proporciona el servicio de seguridad de red (en inglés, *Network Security Service,* NSS) necesario para autenticar a los usuarios mediante el servicio de directorio:

apt -y install libnss-ldapd

- 2. Durante el proceso de configuración de paquetes, deberemos

![](_page_33_Picture_6.jpeg)

indicar la dirección IP del servidor LDAP.

- 3. También se nos solicitará el nombre distintivo de la base de búsquedas LDAP.

- 4. Por último, debemos escoger los servicios que habilitaremos para las búsquedas LDAP, que típicamente son *passwd, group* y *shadow.* Esta configuración quedará almacenada en el archivo */etc/ nsswitch.conf.*
- 5. Ahora debemos proceder a instalar los paquetes *libpam-ldap,*  que nos permitirán autenticarnos contra el LDAP, y el conjunto de herramientas *ldap-utils:*

#### apt -y install libpam-ldap ldap-utils

- 6. En la configuración de *libpam-ldap*, tendremos que especificar también nuestra configuración de LDAP. En primer lugar, la IP del servidor y, a continuación, de nuevo el nombre distinguido de la base de búsquedas.
- 7. Seguidamente, la versión del protocolo LDAP, que en nuestro caso será la 3.
- 8. Permitiremos al administrador de LDAP comportarse como administrador local, e indicaremos que no se requiere de un usuario para acceder a la base de datos LDAP.
- 9. Finalmente, debemos especificar el nombre de la cuenta del administrador del directorio, en nuestro caso, *cn=admin,dc=asir, dc=local.* Tendremos que introducir la contraseña de esta cuenta, que quedará almacenada en el archivo */etc/pam.ldap.secret.*
- 10. Una vez instalados los paquetes, tendremos que editar tres archivos de configuración. En primer lugar, abrimos */etc/nsswitch.conf* (usando *nano*, por ejemplo) y editamos las primeras líneas para que queden de la forma siguiente:

![](_page_34_Picture_4.jpeg)

passwd: files systemd compat ldap group: files systemd compat ldap shadow: files compat gshadow: files

- 11. A continuación, ejecutamos *nano /etc/pam.d/common-password* y añadimos la siguiente línea:

password [success=1 user\_unknown=ignore default=die] pam\_ldap.so try\_first\_pass

- 12. Y por último, ejecutamos *nano /etc/pam.d/common-session* e insertamos lo siguiente, lo cual permite la creación del directorio personal en el primer inicio de sesión:
