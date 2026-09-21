# **6.1. Puertos y protocolos de impresión**

Los equipos que pertenecen a una red tienen a su disposición dos tipos de puertos para comunicarse con un dispositivo de impresión: **local** y **de red**. Cuando la impresora está conectada directamente al equipo, habitualmente se utiliza un puerto local USB, estándar que ha reemplazado a los antiguos puertos serie (COM) y paralelo (LPT). Cuando el dispositivo de impresión está físicamente separado del equipo, de manera que no es posible la conexión directa, se utiliza un puerto de red TCP/IP estándar.

Si bien el puerto es el canal de comunicación entre los dispositivos que envían y reciben los trabajos de impresión, el protocolo es el conjunto de reglas específicas que se utilizan para transmitir los documentos de manera que la impresora pueda entenderlos y procesarlos adecuadamente.

Aunque existe una variedad de protocolos de impresión, en esta unidad nos centraremos en los tres que, actualmente, suelen utilizarse en la mayor parte de entornos de red: el Line Printer Daemon (LPD), el Internet Printing Protocol (IPP) y Samba (SMB).
