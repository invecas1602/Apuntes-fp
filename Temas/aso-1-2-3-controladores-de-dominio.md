# **1.2.3. Controladores de dominio**

Los controladores de dominio o DC (por sus siglas en inglés, *Domain Controllers*), son servidores que forman parte de un dominio y que, entre otras funciones, se encargan de asignar los nombres de dominio y de proporcionar los servicios de autenticación.

Antiguamente, en un directorio basado en el protocolo LDAP solo podía existir un **controlador primario** por dominio, mientras que el resto de DC actuaban a modo de copias de respaldo. Sin embargo, implementaciones más modernas del protocolo permiten el uso de varios controladores primarios o **maestros**, cada uno con un rol diferente al del resto.

![](_page_15_Picture_1.jpeg)

Por ejemplo, los servicios de dominio del Directorio Activo o AD DS (*Active Directory Domain Services*) definen cinco posibles roles de maestro de operaciones, que pueden asignarse a DC distintos para que actúen como maestros en cada uno de dichos roles. Con ello se asegura la consistencia de ciertas operaciones que afectan a los DC. Estos roles son los siguientes:

- **Maestro de esquema**: responsable de actualizar el esquema de los servicios de dominio del AD (AD DS) y el único DC en todo el bosque que puede escribir directamente en el esquema.
- **Maestro de nombres de dominio**: este maestro lleva el registro de todos los dominios y particiones del directorio en la jerarquía del bosque, pudiéndolos añadir, eliminar, replicar en DC adicionales, agregar o borrar objetos de referencia cruzada hacia o desde directorios externos y preparar al directorio para un cambio de nombre de dominio.
- **Maestro de identificador relativo**: asigna bloques de identificadores relativos (RID) a cada controlador de dominio que exista en un dominio dado, y otorga a cada nuevo objeto del directorio su identificador de seguridad único (o SID, por el inglés *Security Identifier*), compuesto por el SID de dominio y un RID exclusivo.
- **Maestro de infraestructura**: se encarga de actualizar las referencias de objeto en su dominio que apuntan a un objeto en otro dominio, poniendo también al día todas las réplicas del dominio.
- **Maestro emulador del controlador de dominio primario**: el emulador de PDC tiene preferencia en la replicación de los cambios de contraseña realizados en el resto de los DC para un dominio determinado, y proporciona información actualizada relativa a las contraseñas cuando falla un intento de inicio de sesión por contraseña incorrecta. Es también el punto de administración preferente para servicios como la directiva de grupos y el sistema de archivos distribuido (DFS).

Este maestro procesa también las peticiones de replicación de los DC de respaldo (BDC) de Windows NT Server 4.0 y, en el caso del que se ubica en el dominio raíz, proporciona además el servicio horario de Windows (W32Time) para todo el bosque.

Los roles de maestro de operaciones se asignan automáticamente durante la creación del DA. El primer controlador de dominio dentro de un dominio dado adquiere los roles de maestro de identificador relativo, maestro de infraestructura y maestro emulador del controlador de dominio primario (estos roles existen, por lo tanto, en cada
