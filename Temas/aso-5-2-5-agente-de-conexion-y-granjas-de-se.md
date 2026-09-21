# **5.2.5. Agente de conexión y granjas de servidores**

![](_page_152_Picture_2.jpeg)

El Agente de conexión es también el componente encargado de distribuir la carga en una granja de servidores, así como de garantizar la disponibilidad de las aplicaciones. En particular, estas son las funciones más importantes del Agente de conexión en un entorno clusterizado:

- **Gestión centralizada**: permite administrar desde un único punto las conexiones de los usuarios, las aplicaciones disponibles y los servidores del clúster.
- **Equilibrado de carga**: distribuye las conexiones de los usuarios entre los servidores del clúster para evitar que cualquiera de ellos se sobrecargue.
- **Alta disponibilidad**: redirige las conexiones a otros servidores de la granja si alguno de ellos falla o tiene que ponerse fuera de línea para su mantenimiento.
- **Seguridad**: el Agente de conexión aplica las directivas de seguridad establecidas para garantizar la integridad y confidencialidad de los datos.
- **Escalabilidad**: gracias al Agente de conexión, es posible añadir o quitar servidores del clúster con facilidad, por lo que la plataforma puede dimensionarse según las necesidades de cada momento.

El **Agente de conexión** (en inglés, *Connection Broker*) es un componente esencial de los Servicios de Escritorio remoto, ya que hace posible la conexión de múltiples usuarios con el servidor actuando como pasarela central y dirigiendo a los usuarios a un servidor disponible en el que poder abrir una sesión de escritorio remoto.

Para desplegar de forma eficiente una granja de servidores de aplicaciones, es necesario contar con un mínimo de 3 servidores, sin contar el controlador de dominio ni los posibles servidores de impresión o de archivos que existieran en el dominio. Estos equipos, y todos los que, en el futuro, vayan a formar parte de la granja, deberán pertenecer al mismo dominio de Directorio Activo.

A continuación se describen, de forma simplificada, los pasos a seguir para el despliegue de la granja:

- 1. Instalamos y configuramos los roles correspondientes a cada uno de los servidores.
- 2. Creamos una colección de sesiones para asignarla al anfitrión de sesión, incluyendo, en su caso, la publicación de aplicaciones remotas.
- 3. Para añadir nuevos Host de sesión de Escritorio remoto con los que hacer crecer la granja, hacemos lo siguiente en el servidor que detenta el rol de Agente de conexión a Escritorio remoto:
  - a. Desde el Administrador del servidor, añadimos el nuevo servidor a la lista de servidores administrados (*Administrar > Agregar servidor*).
  - b. Sin salir del Administrador del servidor, entramos en *Servicios de Escritorio remoto > Información general* y, en la lista *TAREAS*  del cuadro *SERVIDORES DE IMPLEMENTACIÓN*, seleccionamos *Agregar servidores host de sesión de Escritorio remoto.* Tras confirmar la selección del servidor, se instalará en él el rol de Host de sesión de Escritorio remoto.
  - c. Entramos en la colección que deseamos asignar al nuevo anfitrión y, en el cuadro *SERVIDORES HOST,* desplegamos *TAREAS* y seleccionamos *Agregar servidores host de sesión de Escritorio remoto.* Tan pronto como el nuevo servidor se haya asignado a la colección, el agente podrá empezar a dirigir usuarios hacia él.

| Nombre del servidor        | Roles                                    |
|----------------------------|------------------------------------------|
| RDS1.midominio.local       | Host de sesión de Escritorio remoto      |
| RDS-AG.midominio.local     | Agente de conexión a Escritorio remoto / |
| RDS-PT-WEB.midominio.local | Puerta de enlace / Acceso web de         |
