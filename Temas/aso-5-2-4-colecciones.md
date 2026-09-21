# **5.2.4. Colecciones**

Las *colecciones de sesiones* son el elemento que permite a los usuarios abrir sesiones de Escritorio remoto y utilizar aplicaciones mediante el acceso web. Cada sesión se asigna a uno o varios servidores de Host de sesión de Escritorio remoto, aunque cada anfitrión solo puede tener asignada una única colección.

Para configurar una nueva colección, sigue los pasos a continuación:

- 1. Inicia el asistente *Crear colección*, desde el Administrador del servidor, yendo a *Servicios de Escritorio remoto* > *Colecciones,*  desplegando *TAREAS* y seleccionando *Crear colección de sesiones.* En el apartado *Nombre de colección* da un nombre y, opcionalmente, una descripción a la nueva colección.

- 2. Escoge uno o varios servidores de entre los que aparecen en el listado; recuerda que únicamente aparecerán aquellos que tengan asignado el rol de Host de sesión de Escritorio remoto y a los que no hayamos asignado aún ninguna colección.

Para + info

Aunque podemos utilizar certificados autofirmados para realizar la configuración de la puerta de enlace de Escritorio remoto, es recomendable emplear siempre certificados que provengan de una autoridad de certificación reconocida. En caso contrario, el certificado se mostrará como no confiable.

- 3. Escoge los grupos de usuarios que tendrán acceso a la colección.

- 4. Escoge la ubicación de red de los discos de perfil, donde se almacenarán las configuraciones y los datos de los usuarios. Por defecto se guarda todo el perfil, incluyendo los datos de aplicaciones, documentos, etc., por lo que es importante que el lugar donde ubiquemos estos discos esté convenientemente dimensionado. Pulsamos el botón *Crear* para finalizar el asistente.

- 5. Una vez creada la colección, podemos agregarle programas accesibles mediante navegador. Para ello, entramos en la colección y hacemos clic sobre el enlace *Publicar programas RemoteApp.*

![](_page_150_Picture_6.jpeg)

- 6. Seleccionamos los programas de la lista o agregamos algunos de forma manual. Los programas seleccionados deben estar instalados en todos los servidores de Host de sesión de Escritorio remoto a los que hayamos asignado la colección.

#### 7. Pulsamos el botón *Publicar* para confirmar la selección.

#### 8. Las aplicaciones seleccionadas aparecen en el cuadro *PROGRAMAS REMOTEAPP.*

![](_page_151_Picture_4.jpeg)

- 9. Para configurar en detalle las propiedades de la colección, desplegamos *TAREAS* en el cuadro *PROPIEDADES* y seleccionamos *Editar propiedades.* Podremos configurar opciones como los tiempos de espera y las condiciones de desconexión y finalización de la conexión, el nivel de seguridad, el equilibrio de carga, el acceso a los recursos del dispositivo cliente y la ubicación y tamaño máximo de los discos de perfil de usuario.

![](_page_152_Picture_0.jpeg)
