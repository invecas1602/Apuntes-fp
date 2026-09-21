# **1.4.3. Gestión de permisos y control de acceso**

La gestión de permisos y el control de acceso al directorio son dos aspectos fundamentales para mantener la seguridad de nuestro entorno. Así pues, y con independencia de las plataformas en las que estuviera basado, la integridad del directorio radica, en gran medida, en conseguir que los usuarios únicamente puedan acceder a aquellas funciones y recursos que necesiten para poder desarrollar sus actividades.

Tanto el AD como OpenLDAP u otras plataformas basadas en LDAP, contemplan mecanismos específicos de seguridad para la gestión de los permisos y del acceso a los recursos del dominio, como el cifrado de las conexiones, la gestión de cuotas, herramientas auditoría, etc. pero, en general, podemos destacar un conjunto de buenas prácticas aplicables en cualquier entorno:

- **Uso de los grupos para gestionar los permisos**: siempre que sea posible, resulta más conveniente asignar los permisos a grupos en lugar de a usuarios individuales, ya que esto simplifica la concesión o revocación del acceso a los recursos del directorio, sin perjuicio de que, además, se puedan configurar permisos individuales sobre usuarios específicos.
- **Principio del mínimo privilegio**: los usuarios únicamente deberían obtener los permisos que necesitan para realizar sus funciones, lo que ayuda a minimizar que se haga mal uso de los privilegios dentro del dominio.
- **Control de acceso basado en roles (RBAC)**: el RBAC (siglas de *Role-Based Access Control*) permite asignar permisos en función de las responsabilidades de los usuarios, lo cual nos ayuda a seguir el principio del menor privilegio.
- **Uso de listas de control de acceso (ACL)**: las ACL (por *Access Control List*) son instrumentos que nos permiten definir los permisos que los usuarios y grupos tienen sobre los objetos en el directorio,

controlando quién puede leer, escribir o modificar dichos objetos.

- **Auditoría de permisos**: es necesario revisar de forma periódica las asignaciones de permisos para asegurar que están debidamente actualizados. Para este fin podemos emplear diversas herramientas de auditoría que nos permiten realizar un seguimiento de cualquier cambio que se vaya produciendo en los permisos.
- **Uso de directivas y límites de contraseñas**: las directivas de contraseñas permiten forzar el uso de contraseñas seguras, lo cual contribuye a evitar los accesos no autorizados al directorio. Entre dichas directivas se incluyen los requisitos de complejidad de las contraseñas, establecer su plazo de caducidad y limitar el número de intentos fallidos de inicio de sesión.

Además de todo lo anterior, en el caso de las cuentas especialmente privilegiadas es recomendable implementar mecanismos de seguridad adicionales, como la autenticación multifactor, la restricción del acceso a recursos específicos y la supervisión de actividades.
