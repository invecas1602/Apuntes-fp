# **6.1.1. Line Printer Daemon (LPD)**

Cuando el principal criterio es la facilidad de implementación y uso del protocolo, en los servidores de impresión basados en Unix podemos utilizar el Line Printer Daemon, también llamado Line Printer Remote o LPR, un protocolo cliente-servidor que utiliza el TCP como protocolo de transporte a través del **puerto 515**.

El LPD es un protocolo basado en texto, es decir, utiliza una serie de instrucciones de texto que la impresora es capaz de interpretar para imprimir los documentos, y soporta una variedad de atributos de impresión relativos a la naturaleza y tamaño del papel, la calidad de la impresión o el número de copias, por ejemplo, así como instrucciones específicas para cada impresora que ofrecen acceso a la configuración del dispositivo o a ciertas funciones especiales.

Sin embargo, si bien el LPD es un protocolo muy fiable, eficiente y con un amplio soporte en cuanto a sistemas y dispositivos compatibles, su propia simplicidad limita sus prestaciones. Por ejemplo, no ofrece ningún tipo de retroalimentación de estado en tiempo real, por lo que los clientes de impresión no reciben información puntual acerca del progreso de los trabajos enviados al dispositivo de impresión.
