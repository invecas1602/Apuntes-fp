# **1.4. Administración del directorio**

En OpenLDAP se emplean diferentes técnicas de configuración del directorio según la versión del protocolo que estemos utilizando. Antiguamente se utilizaban los archivos de configuración almacenados en */etc/openldap/*, principalmente *slapd.conf,* para configurar los parámetros del servidor como la ubicación de la base de datos y las reglas de control de accesos.

Sin embargo, a partir de su versión 2.3, la configuración del servidor OpenLDAP se gestiona dentro de un DIT especial que por defecto se halla enraizado en una entrada denominada *cn=config*. La principal ventaja de este método, conocido como *configuración en línea de OpenLDAP* u *OLC*, es que las modificaciones que realizamos se aplican de inmediato —a menudo, sin tan siquiera requerir que se reinicie el servicio—, mientras que el sistema previo depende de la lectura de los archivos de configuración en el inicio del servicio.

Utilizando la orden *ldapsearch* en un terminal podemos consultar la organización del servidor:

#### Para + info

La estructura que contiene todos los DIT que conoce el servidor OpenLDAP se denomina DSE raíz, por el inglés *DSA Specific Entry* o entrada específica DSA (siendo DSA las siglas de *Directory System Agent* o agente del sistema de directorio, que básicamente refiere al servidor de directorio basado en LDAP).

![](_page_25_Picture_1.jpeg)

Abrimos con privilegios de administrador nuestro editor de texto simple preferido (*sudo nano*, por ejemplo), y definimos dos nuevas unidades organizativas, contabilidad y *marketing*, guardándolas en */etc/ldap/slapd.d/ldapconfig.ldif*:

#Crea las OU contabilidad y marketing dn: ou=contabilidad,dc=asir,dc=local objectClass: organizationalUnit ou: contabilidad dn: ou=marketing,dc=asir,dc=local objectClass: organizationalUnit ou: marketing

Para cargar este archivo en el servidor OpenLDAP, utilizamos la siguiente orden (se nos solicitará la contraseña de administrador de LDAP):

sudo ldapadd -x -D "cn=admin,dc=asir,dc=local" -W -f /etc/ldap/slapd.d/ldapconfig.ldif

Como resultado, veremos los mensajes siguientes:

adding new entry "ou=contabilidad,dc=asir,dc=local" adding new entry "ou=marketing,dc=asir,dc=local"

Para añadir entradas al directorio, simplemente crearemos un nuevo archivo LDIF. Por ejemplo, podemos añadir dos nuevos usuarios al directorio, uno dentro de cada unidad organizativa:

#Crea un nuevo usuario en contabilidad dn: uid=juan,ou=contabilidad,dc=asir,dc=local objectClass: top objectClass: person objectClass: organizationalPerson objectClass: inetOrgPerson cn: Juan Barrachina givenName: Juan sn: Barrachina mail: jbarrachina@asir.local userPassword: {SSHA}ebHRdwJVXu3ND5PMvKaVtw8jE2BYpIrr title: Sr. initials: JB description: Contable homePhone: +349687564 mobile: +346456743 postalCode: 08929 postalAddress: Almendros 101

#Crea un nuevo usuario en marketing dn: uid=carlos,ou=marketing,dc=asir,dc=local objectClass: top objectClass: person objectClass: organizationalPerson objectClass: inetOrgPerson cn: Carlos Medina givenName: Carlos sn: Medina mail: cmedina@asir.local userPassword: {SSHA}MmFxEut3ZklKhwnzzwHGq8dzV14GJNw0 title: Sr. initials: CM description: Jefe de marketing homePhone: +34237456761 mobile: +34678456754 postalCode: 08923 postalAddress: Cerezos 103

Para generar las contraseñas (*userPassword*)**,** utilizaremos la orden *sudo slappasswd*.

Para modificar objetos del directorio, podemos usar la orden *ldapmodify.* Así pues, para editar el correo electrónico del usuario Carlos Medina, confeccionaríamos el siguiente archivo LDIF, guardándolo, por ejemplo, como */etc/ldap/slapd.d/nuevoemail.ldif*:

dn: uid=carlos,ou=marketing,dc=asir,dc=local ldapsearch -x -b "dc=asir,dc=local" uid=carlos cn mail changetype: Modify replace: mail mail: carlosmedina@asir.local

A continuación, ejecutaríamos la orden *ldapmodify*:

sudo ldapmodify -x -D "cn=admin,dc=asir,dc=local" -W -f /etc/ldap/slapd.d/nuevoemail.ldif

Para comprobar que la modificación se ha realizado correctamente, podemos utilizar la siguiente orden:

ldapsearch -x -b "dc=asir,dc=local" uid=carlos cn mail

![](_page_27_Picture_1.jpeg)

### ldapsearch -H ldap:// -x -s base -b "" -LLL "+"

Veremos los metadatos relevantes en las primeras líneas de la salida de la instrucción:

dn:

structuralObjectClass: OpenLDAProotDSE

#### Para + info

Para conocer todos los parámetros de *ldapsearch, ldapadd* y *ldapmodify*, así como una explicación detallada y con ejemplos acerca de la sintaxis y uso de cada uno de ellos, puedes recurrir a sus páginas de manual ejecutando las instrucciones *man ldapsearch*, *man ldapadd* y *man ldapmodify* en una ventana de terminal.

![](_page_27_Picture_4.jpeg)

En algunas implementaciones de LDAP se admite el uso del operador *~=* para localizar entradas aproximadamente iguales a la cadena de búsqueda; por ejemplo, el filtro "(*givenName~=María*)" podría mostrarnos todas las entradas de usuarios cuyo nombre de pila fuera María o Maria. Las reglas de coincidencia no están establecidas en el estándar LDAP, por lo que quedan a discreción de la configuración del servicio de directorio.

#### Para + info

|         |                   | Filtros      |
|---------|-------------------|--------------|
| Lógicos |                   | De igualdad  |
| &       | Y booleano (AND)  | = Igual a    |
|         | O booleano (OR)   | >= Mayor que |
| !       | No booleano (NOT) | <= Menor que |

configContext: cn=config

namingContexts: dc=asir,dc=local

En este caso, el DIT de configuración (*configContext*) es, efectivamente, *cn*=*config*, y el único DIT de no administración que podemos ver (*namingContexts*) tiene su raíz en el nombre distintivo *dc=asir,dc=local.*

Para realizar modificaciones en los DIT de OpenLDAP se utilizan archivos LDIF, que contienen una serie de entradas y atributos, y que podemos cargar en el servidor utilizando la instrucción *ldapadd.*
