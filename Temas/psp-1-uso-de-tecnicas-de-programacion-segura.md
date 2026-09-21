# 1. Uso de técnicas de programación segura

### 1.1. Prácticas de programación segura

A la hora de desarrollar programas, es necesario tener presente que un código limpio aportará seguridad a la aplicación.

#### Para ello es preciso:

- Estar siempre informado de los diferentes tipos de vulnerabilidades, con lo cual es necesario estar al día en ciberseguridad.
- Explorar software libre para conocer cómo se trabaja la seguridad en distintas aplicaciones.
Normalmente, toda aplicación recibirá información por parte del usuario, por lo que es importante el tratamiento de la misma. Los datos, al ser una parte muy sensible, es lo que más se suele atacar.

Es necesario verificar siempre que los datos introducidos son válidos, tanto los parámetros, como la información, como los ficheros que se utilizan.

Cuando se trabaja con URL páginas web, hay que tener presente la seguridad y, por ello, comprobar si la URL es fiable o no. Los datos de las webs pueden ser alterados por un usuario, tanto su contenido como la configuración.

En muchas ocasiones, los propios navegadores web avisan de que no se debe confiar en cookies de terceros, ya que estas también pueden ser modificadas.

Otro de los puntos clave en la programación segura es la reutilización de código, una práctica común y muy aconsejada, pero siempre teniendo en cuenta que ese código ha sido revisado y no cuenta con problemas de seguridad.

También se considera práctica de programación segura eliminar el código obsoleto para que no interceda con el código bueno, ya que, en las revisiones posteriores, podría llevar a confusión. Por último, se considera fundamental utilizar herramientas de software para detectar fallos en el código.

En resumen, durante el desarrollo de un producto software, se deben tener en cuenta los siguientes aspectos:

- Los usuarios son los mismos que intentarán vulnerar la aplicación.
- Los archivos que se utilicen en la aplicación deben ser de solo lectura, para evitar que un usuario los modifique.
- Toda información sensible guardada en la base de datos, o que se transmita por la red, debe ir siempre cifrada.
- Comprobar que todas las llamadas al sistema se han realizado con éxito y detener la aplicación si no ha sido así.
- Utilizar las rutas absolutas de los ficheros que se necesiten.
- No abrir nunca terminales desde una aplicación, ni otro software que no sea fiable.
### 1.2. Criptografía de clave pública y clave privada

La criptografía es el conjunto de técnicas que cifran información, con el objetivo de que un usuario no sea capaz de entender el contenido, y, por lo tanto, conseguir confidencialidad en el mensaje.

Para conseguir esta confidencialidad, es necesario transformar el mensaje mediante un algoritmo matemático. La criptología no solo se encarga de cifrar el mensaje, sino también de descifrarlo para que el receptor sea capaz de entenderlo.

Antes de conocer los distintos algoritmos que existen, es necesario conocer algunos conceptos importantes:

- Texto legible: es el mensaje original.
- Texto cifrado: es el resultado de aplicar uno de los siguientes algoritmos sobre un texto legible.
Existen diferentes tipos de algoritmos:

- **Cifrado César**: cifrado en el que se realiza una sustitución de cada letra por otra. El desplazamiento será el mismo para todas las letras del mensaje. Es un cifrado muy simple, pero bastante vulnerable. Los atacantes pueden conocer el mensaje mediante estadísticas. Para más información: [https://es.wikipedia.org/wiki/Cifrado_César](https://es.wikipedia.org/wiki/Cifrado_C%C3%A9sar)

**Funciones Hash o funciones de una sola vía**

Una función hash es una función que, dada cualquier cadena de caracteres, los convierte en otra cadena de longitud fija.

Algoritmos de función Hash o funciones de una sola vía:

- MD5: genera resúmenes de 128 bits, es decir, de 32 símbolos hexadecimales. Se suele utilizar para proteger al usuario de troyanos o de cualquier otro software malicioso. Normalmente, cuando se descarga un software, se utiliza una aplicación externa que, mediante este algoritmo, genera un hash del instalador. Si coincide con el que ofrece el propio desarrollador, este no habrá sido alterado.

- SHA-1: genera resúmenes de 160 bits, es decir, de 40 símbolos hexadecimales. Desde hace algunos años no se considera un algoritmo seguro, aunque se ha actualizado a versiones posteriores, como es SHA-2, con diferentes longitudes en los resúmenes.

- Algoritmos de clave secreta o de criptografía simétrica

En este tipo de algoritmos, tanto el emisor como el receptor comparten una única clave. El mensaje se cifra y se descifra con esa única clave.

- DES: utiliza una clave de 56 bits, por lo que no se considera seguro. Cifra bloques de datos de 64 bits con la clave de 56, y después de varias iteraciones, muestra 64 bits de salida.

- **Triple DES**: el algoritmo es el mismo que DES, pero, debido a la necesidad de aumentar su seguridad, se aumentó la clave a 112 bits, aunque sigue cifrando bloques de 64 bits.

- **AES**: al igual que DES y Triple DES es un algoritmo cifrador de bloques. En este caso, bloques de 128 bits. La diferencia se encuentra en el tamaño de la clave, puede ser de 128, 192 y 256 bits.

- Algoritmos de clave pública o de criptografía asimétrica
En este tipo de algoritmos se generan dos claves, denominadas clave pública y clave privada. El receptor genera estas claves y muestra la clave pública al emisor. El emisor utiliza esta clave para cifrar el mensaje y, posteriormente, el receptor utilizará la clave privada para desencriptarlo.

- **RSA**: la seguridad de este algoritmo radica en el problema de la factorización de números enteros. Tanto la clave pública como la clave privada se componen de un par de números.

- Pública (n, e).
- Privada (n, d).

Estos números son hallados mediante operaciones a partir de dos números primos, escogidos de forma aleatoria. Hay que tener en cuenta que es imposible conocer d, aunque conozcamos n y e. Este algoritmo es la base de la firma digital.

### 1.3. Principales aplicaciones de la criptografía

- Seguridad en las comunicaciones: es la principal aplicación, puesto que se encarga de que los canales en Internet sean seguros.
- Identificación y autenticación en recursos y sistemas: mediante la criptografía es posible validar el acceso de los usuarios a la firma digital, tanto si se realiza a través de contraseña, o mediante una técnica más segura. La firma digital es el mecanismo mediante el cual el receptor es capaz de identificar al emisor. Asegura autenticación de origen y no repudio, además de integridad del mensaje.
La comprobación de la integración del mensaje, al igual que el de la autenticación del origen, se realiza comprobando la igualdad entre el resumen que se consigue al descifrar el mensaje y el resumen de la firma digital.

- **Certificación**: un certificado digital es un documento que asocia los datos de identificación a una persona física, empresa o a un organismo, de manera que pueda identificarse en Internet. Este certificado es generado por una Autoridad Certificadora (AC), que también es la encargada de realizar la autenticación al usuario.
- **Comercio electrónico**: mediante la criptografía es posible realizar operaciones sensibles por Internet, con la seguridad de que los datos no serán interceptados por terceros.

### 1.4. Política de seguridad

Una política de seguridad es un conjunto de normas que se utilizan para proteger un sistema. Para que un sistema sea seguro deben cumplirse todas estas características, teniendo en cuenta que tanto el no repudio como la confidencialidad dependen de la autenticidad para poder cumplirse.

- **Integridad de los datos**: se asegura de que no hayan sido modificados por terceros, es decir, que se recibe el mensaje tal y como se envió.
- **Disponibilidad**: característica por la cual los datos se encuentran a disposición de quienes deban acceder a ellos.
- **Confidencialidad**: los mensajes solo podrán ser leídos por aquellas personas que han sido autorizadas para ello. De esta forma se garantiza la privacidad de los datos.
- **Autenticidad**: característica mediante la cual el receptor conoce la identidad del emisor.
- **No repudio**: el emisor no puede negar que ha enviado el mensaje, por lo que se evita que se culpe al canal de información de que la información no ha llegado.

### 1.5. Programación de mecanismos de control de acceso

El control de acceso se encarga de comprobar si una persona u otra entidad tiene permisos necesarios para acceder al recurso que solicita.

#### Consta de tres fases:

- Identificación: es la parte del proceso en la que el usuario indica quién es. Por ejemplo, en el acceso al correo electrónico, el usuario indica su usuario.
- Autenticación: es la parte del proceso que realiza el sistema, en la cual se comprueba que el usuario es quien dice ser. En el mismo ejemplo anterior, el servidor de correo verifica que el usuario es quien ha indicado por la contraseña.
- Autorización: es la última parte del proceso. Si la autenticación ha resultado con éxito, el sistema ofrece la información requerida, o el acceso al recurso. Para acabar el ejemplo, sería el momento en el que el servidor muestra la bandeja de correo al usuario.
Se ha indicado anteriormente que en el proceso de autenticación el sistema debe verificar que el usuario es quien dice ser. Este proceso es necesario llevarlo a cabo mediante algún tipo de código con el cual únicamente pueda acceder este usuario.

#### Existen varias formas:

- Contraseña.
- Biometría: entre los que se engloban lectura de retina, huella dactilar, reconocimiento de voz, entre otros.
- Tarjetas de identificación: como puede ser el DNI electrónico.
Actualmente estos dispositivos están desbancando al sistema de seguridad por contraseña, ya que ofrecen una mayor seguridad y eliminan el factor humano para medir la seguridad.

A la hora de elegir una contraseña, el usuario suele escoger fechas claves, nombres o incluso su número de teléfono. Estos datos no son privados, por lo que la contraseña es vulnerable. Además, una contraseña poco segura puede ser hackeada mediante fuerza bruta en pocos segundos.

### 1.6. Encriptación de información utilizando protocolos criptográficos

Un protocolo criptográfico es un conjunto de reglas sobre la seguridad en la comunicación de los sistemas informáticos. Mediante estos protocolos se especifica cómo se debe utilizar este algoritmo.

Normalmente, los protocolos criptográficos tratan los siguientes aspectos:

- Establecimiento de las claves.
- Autenticación de entidades.
- Autenticación de los mensajes.
- Tipo de cifrado.
- Métodos de no repudio.
#### HTTPS (Hypertext Transfer Protocol Secure)

Es un protocolo de la capa de aplicación basado en el protocolo HTTP. Por así decirlo, añade seguridad a dicho protocolo. Utiliza un cifrado basado en SSL/TLS, que se estudiará en el siguiente apartado.

Mientras que el protocolo HTTP utiliza el puerto 80, HTTPS utiliza el 443. Otra diferencia fundamental se encuentra en la URL, que indica qué protocolo se está usando.

### 1.7. Protocolos seguros de comunicaciones

SSH. También denominado intérprete de órdenes seguro. Es un protocolo de seguridad implementado en la capa de aplicación del modelo OSI. Este protocolo utiliza el puerto 22 para la comunicación y la realiza de forma similar a SSL.

Un ejemplo de aplicación que utiliza este protocolo es Putty. Para realizar una conexión, el cliente envía una petición al servidor por el puerto 22. Una vez que el servidor la acepta, envía la clave pública al cliente, para que este pueda cifrar sus mensajes. Por último, una vez que el cliente ha recibido esta clave, puede enviar los mensajes cifrados al servidor.

SSH utiliza tanto cifrado asimétrico como simétrico. Mediante el primero, garantiza la autenticidad del cliente y del servidor, mientras que con el cifrado simétrico se garantiza la confidencialidad y la integridad de los mensajes.

SSL y TLS. El protocolo TLS (Transport Layer Security, seguridad de la capa de transporte) actúa en la capa de transporte, al mismo nivel que los sockets, y por debajo de HTTP. Suele utilizarse para la seguridad de otros protocolos de la capa de aplicación, como pueden ser FTP o SMTP. Es solo una versión actualizada y más segura de SLL.

Ambos protocolos utilizan tanto cifrado simétrico como asimétrico. Debido a que el cifrado asimétrico es demasiado costoso, se utiliza el cifrado simétrico para el intercambio de los mensajes. Como el cifrado asimétrico es más seguro y garantiza la autenticación, el mensaje inicial se realiza mediante este tipo de cifrado. Por último, garantiza la integridad de los mensajes mediante funciones hash.

Te resultará interesante la lectura del siguiente artículo (en inglés): [http://blogs.mdaemon.com/index.php/ssl-tls-best-practices/](http://blogs.mdaemon.com/index.php/ssl-tls-best-practices/)

### 1.8. Programación de aplicaciones con comunicaciones seguras

Existen diferentes clases que sirven para cifrar datos en Java. Entre ellas se encuentran:

- Clase Cipher
String getAlgorithm () Devuelve el algoritmo usado en ese objeto. static Cipher getInstance (String Crea un objeto de la clase Cipher con el algorithm) algoritmo recibido por parámetro. void init (int opmode, Key key) Inicializa el objeto para cifrar o descifrar con la clave recibida. El parámetro opmode puede ser Cipher.ENCRIPT_MODE y Chiper.DECRIPT_MODE Byte [] doFinal (byte [] input) Realiza la encriptación o desencriptación de los datos.

Para más información: [https://docs.oracle.com/javase/7/docs/api/javax/crypto/Cipher.html](https://docs.oracle.com/javase/7/docs/api/javax/crypto/Cipher.html)

- Clase MessageDigest para funciones hash

|static MessageDigest getInstance (String algorithm) byte[] digest () static boolean isEqual (byte[] digestA, byte[] digestB)|Asigna el algoritmo de cifrado para el objeto. Realiza el cálculo del resumen. Compara dos resúmenes para comprobar si son iguales.|
|---|---|
|void update (byte[] input)|Actualiza el contenido del objeto.|
|void reset ()|Elimina el contenido del objeto.|

Para más información: [https://docs.oracle.com/javase/7/docs/api/java/security/MessageDigest.html](https://docs.oracle.com/javase/7/docs/api/java/security/MessageDigest.html)

- Clase KeyGenerator para cifrado simétrico

|static KeyGenerator getInstance (String algorithm) SecretKey generateKey () String getAlgorithm ()|Asigna el algoritmo de cifrado para el objeto. Genera la clave secreta. Devuelve el algoritmo usado en ese objeto.|
|---|---|
|void init (int keysize)|Vuelve a generar la clave con el tamaño indicado.|

Para más información: [https://docs.oracle.com/javase/7/docs/api/javax/crypto/KeyGenerator.html](https://docs.oracle.com/javase/7/docs/api/javax/crypto/KeyGenerator.html)

- Clase KeyPair y KeyPairGenerator para cifrado asimétrico
Con la Clase KeyPair se crea un objeto que contiene una clave privada y una pública mediante el constructor KeyPair (PublicKey publicKey, PrivateKey privateKey). Es posible recoger estas claves con los siguientes métodos:

PrivateKey getPrivate () Genera la clave privada. PublicKey getPublic () Genera la clave pública.

Para más información: [https://docs.oracle.com/javase/7/docs/api/java/security/KeyPair.html](https://docs.oracle.com/javase/7/docs/api/java/security/KeyPair.html)

|KeyPair generateKeyPair () KeyPair genKeyPair () String getAlgorithm ()|Genera una pareja de claves. Genera una pareja de claves. Devuelve el algoritmo que se ha utilizado para la generación del par.|
|---|---|
|static KeyPairGenerator getInstance (String algorithm)|Genera un objeto KeyPairGenerator con un par de claves.|
|void initialize (int keysize)|Vuelve a generar las claves con el tamaño indicado.|

Para más información: [https://docs.oracle.com/javase/7/docs/api/java/security/KeyPairGenerator.html](https://docs.oracle.com/javase/7/docs/api/java/security/KeyPairGenerator.html)

### 1.9. Documentación de aplicaciones desarrolladas

En la documentación generada de cada aplicación desarrollada es necesario detallar la criptografía usada. En la mayor parte de las aplicaciones se trabaja con bases de datos, por lo que la información queda almacenada y podría ser vulnerada.

La primera parte de este proceso consiste en identificar aquella información considerada sensible. Se considera información sensible aquella información privada de un usuario.

Tipos de información sensible:

- Contraseñas.
- Datos personales: como puede ser el DNI o la cuenta bancaria de un usuario. También el número de tarjeta de crédito.
- Incluso, en algunos casos, también es considerada información sensible la dirección física.

Toda esta información no es posible guardarla en una base de datos sin cifrar, y hay que tener en cuenta que, si la información navega a través de Internet, debe ir cifrada y mediante un protocolo seguro. Todo esto es necesario reflejarlo en la documentación de la aplicación, centrándose en la información cifrada y en el tipo de cifrado que se ha realizado.