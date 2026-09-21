# **8.2.1. Expresiones regulares**

Las expresiones regulares, o *regex*, permiten manipular textos con base en patrones, por lo que a menudo resultan de utilidad en la confección de *scripts* y en el procesamiento de los datos. Aunque el significado y sintaxis de estas expresiones puede diferir en función del lenguaje o herramienta de programación utilizados, en general podemos identificar ciertas características y patrones comunes:

- **Caracteres literales**: podemos buscar coincidencias con caracteres específicos, como letras ("a","b",...), números y otros símbolos.
- **Metacaracteres**: algunos caracteres, como ".", "\*", "+", o los distintos tipos de paréntesis, pueden tener un significado especial en las expresiones regulares.
- **Clases de caracteres**: los corchetes "[ ]" se emplean para definir una clase de caracteres, como "[aeiou]" (coincidir con cualquier vocal) y "[0-9]" (coincidir con cualquier dígito).
- **Cuantificadores**: definen las veces que se debe encontrar un determinado patrón, por ejemplo, "\*" para ninguna o más, "+" para una o más, y "?" para ninguna o una.
- **Anclas**: los símbolos "^" y "\$" coinciden con el inicio y final de una línea o cadena, respectivamente.
- **Patrones**:
  - **Comodín**: el punto (".") coincide con cualquier carácter excepto el de nueva línea.
  - **Alternancia**: la barra vertical ("|") permite la coincidencia de cualquier patrón especificado; por ejemplo, "pera|manzana" coincide con *pera* y con *manzana.*
  - **Repetición**: los cuantificadores "\*", "+" y "?" pueden utilizarse para denotar repeticiones.
  - **Conjuntos de caracteres**: los corchetes "[ ]" permiten coincidir con grupos concretos de caracteres.
  - **Secuencias de escape**: la contrabarra (\) se utiliza para "escapar" metacaracteres, de forma que se interpreten de forma literal; por ejemplo, "\\*" coincide con el símbolo literal del asterisco. No obstante, también se puede usar para indicar cualquier dígito (\d), cualquier no dígito (\D), espacio (\s), no espacio (\S), carácter alfanumérico (\w) y carácter no alfanumérico (\W).

- **Agrupación**: los paréntesis "( )" se usan para agrupar patrones y aplicarles cuantificadores; por ejemplo, "(ab)+" coincide tanto con "ab" como con "abab", "ababab", etc. También pueden servir para capturar coincidencias para uso posterior.
- **Referencias anteriores**: permiten hacer referencia a grupos previamente capturados; por ejemplo, "\1" hace referencia al primer grupo.
- **Búsquedas adelante y atrás**: permiten la coincidencia si van seguidos o precedidos de otro patrón.

![](_page_241_Picture_2.jpeg)
