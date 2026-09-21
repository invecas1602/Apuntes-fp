# **4.1.5. Métodos de cifrado**

Una característica común a la mayoría de los protocolos de red para el acceso remoto es el cifrado de los datos transmitidos en las comunicaciones, así como también el de las credenciales de acceso a los equipos. Para ello se emplean diferentes métodos, entre los que se cuentan, de manera destacada, los siguientes:

- **Transport Layer Security (TLS)/Secure Sockets Layer (SSL)**: el protocolo TLS/SSL se emplea, principalmente, en los navegadores web para cifrar los datos entre el ordenador de los usuarios y los servidores web con los que se conectan.

El TLS es, técnicamente, el protocolo sucesor del SSL y, de entre sus diferentes versiones, las más utilizadas son las 1.2 y 1.3. Algunas características clave del TLS son:

- **Cifrado**: el TLS emplea la criptografía para cifrar los datos en la capa de aplicación de la pila de red, lo cual garantiza que no puedan ser interceptados ni modificados durante su transmisión.

Entre los algoritmos de cifrado que se pueden utilizar se cuentan el AES y el 3DES —ambos algoritmos de cifrado simétrico por bloques—, el RSA —de cifrado asimétrico y utilizado para el intercambio de claves y en las firmas digitales— y el ECC asimétrico también, aunque más rápido y seguro que el RSA.

- **Autenticación**: este protocolo emplea certificados digitales para verificar la identidad de los equipos conectados.
- **Protocolo de negociación**: se emplea para establecer una conexión segura, negociando los métodos de autenticación, algoritmos de cifrado y cualquier otro parámetro que se utilice en el proceso.

- **Compatibilidad**: se trata de un protocolo ampliamente soportado y se utiliza, de manera universal, en navegadores web, clientes de correo electrónico y otras muchas aplicaciones de red.
- **IPSec**: protocolo que cifra y autentica los paquetes IP, y que se emplea habitualmente en las redes privadas virtuales (en inglés, *Virtual Private Networks,* VPN) como mecanismo de protección de los datos que se transmiten entre los usuarios remotos y las redes corporativas a las que se conectan.

Trabaja en la capa de red de la pila TCP/IP, y está a disposición de cualquier aplicación de red que utilice el protocolo IP, tanto en redes IPv4 como IPv6.

Para verificar la identidad de los terminales de red, IPSec utiliza certificados digitales y algoritmos criptográficos basados en un protocolo de intercambio de claves, proporcionando dos modos de trabajo: modo de transporte —en el que el paquete IP se cifra solo parcialmente— y modo de túnel, que es el que utilizan normalmente las VPN al encriptar el paquete IP completo y transmitirlo, encapsulado, en otro paquete IP.

- **WPA2**: el Wi-Fi Protected Access II, o WPA2, es un protocolo de seguridad utilizado en las redes Wi-Fi para proteger los datos transmitidos e impedir los accesos no autorizados. Utiliza el algoritmo Advanced Encryption Standard (AES) para cifrar los datos transmitidos por la red inalámbrica, así como un protocolo de negociación de cuatro vías para autenticar los dispositivos que se conectan a la red inalámbrica, durante el cual el punto de acceso Wi-Fi y el dispositivo intercambian una clave compartida o un certificado único para autenticarse mutuamente.

#### Para + info

La principal característica diferenciadora entre un algoritmo de cifrado simétrico y uno asimétrico es su relación entre eficiencia y seguridad: el sistema simétrico es más eficiente pero menos seguro, ya que emplea la misma clave para cifrar y descifrar los datos, mientras que, en el cifrado asimétrico, las claves son distintas, ya que existe una clave pública para el cifrado, compartida por ambos dispositivos, y una clave secreta, privada de cada uno, para el descifrado.
