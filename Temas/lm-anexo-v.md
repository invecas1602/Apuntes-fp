# Anexo V

### Introducción a Docker

Docker es una plataforma de virtualización ligera que permite desarrollar, empaquetar y ejecutar aplicaciones en contenedores. Los contenedores son entornos independientes y portátiles que incluyen todo lo necesario para que una aplicación funcione, como el código, las librerías, las configuraciones y las dependencias.

Docker simplifica el despliegue de aplicaciones, ya que garantiza que funcionen de manera consistente en cualquier sistema que tenga Docker instalado.

#### Conceptos básicos de Docker

- **Imagen (Image): es una plantilla inmutable que contiene todo lo necesario para ejecutar una** aplicación, incluyendo el sistema operativo, las dependencias y el código.
- **Contenedor (Container)**: es una instancia en ejecución de una imagen. Cada contenedor es independiente y aislado, pero puede comunicarse con otros contenedores si se configura.
- **Dockerfile: es un archivo de texto que contiene instrucciones para crear una imagen de Docker.**
- **Docker Hub: es un repositorio en línea donde se almacenan imágenes preconfiguradas que se** pueden descargar y usar.
- **Volúmenes: son áreas de almacenamiento persistente que los contenedores pueden usar para** guardar datos.
#### Ventajas de Docker

- **Portabilidad**: las aplicaciones en contenedores funcionan de manera idéntica en cualquier sistema que soporte Docker.
- **Aislamiento: cada contenedor está aislado del sistema anfitrión y de otros contenedores, lo que** evita conflictos entre aplicaciones.
- **Rapidez**: los contenedores se inician en segundos, ya que comparten el kernel del sistema operativo en lugar de virtualizarlo.
- **Escalabilidad: Docker permite escalar aplicaciones fácilmente mediante la creación de múltiples** contenedores.
- **Facilidad de despliegue**: con Docker, se puede replicar fácilmente un entorno de desarrollo, pruebas o producción.

#### Instalación básica de Docker

Docker se puede instalar en los sistemas operativos más comunes, como Linux, Windows y macOS. A continuación se describe el proceso básico:

**Linux**

1. Actualizar los paquetes del sistema: sudo apt update && sudo apt upgrade
2. Instalar Docker: sudo apt install docker.io
3. Verificar la instalación: docker --version
#### Windows y macOS

1. Descargar Docker Desktop desde Docker. [https://www.docker.com/](https://www.docker.com/)
2. Seguir al asistente de instalación.
#### Comandos básicos de Docker

- **Listar imágenes locales:** docker images
- **Descargar una imagen:** docker pull <nombre_imagen>
- **Ejecutar un contenedor:** docker run <nombre_imagen>
- **Listar contenedores en ejecución:** docker ps
- **Detener un contenedor:** docker stop <id_contenedor>

- **Eliminar un contenedor:** docker rm <id_contenedor>
- **Eliminar una imagen:** docker rmi <nombre_imagen>
#### ¿Por qué usar Docker para instalar Odoo?

Docker facilita la instalación y configuración de aplicaciones como Odoo, un ERP que requiere múltiples servicios (base de datos, backend, etc.). Con Docker puedes usar contenedores preconfigurados para desplegar Odoo rápidamente sin preocuparte por dependencias o configuraciones complejas. Además, permite

- Aislar la instalación de Odoo del sistema principal.
- Escalar la aplicación fácilmente.
- Realizar pruebas o actualizaciones sin riesgo de afectar el entorno de producción.