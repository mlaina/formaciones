# REGEX

Reconocimiento de patrones.
 
- '*'  -> utilizado de comodín
- g/ -> Global search
- /p -> Print result

Ejemplo para una entrada RGB #AF1234

**Busca coincidencias**

Rango entre [A F] y [0 9] con un # al principio.

[] Los corchetes se utilizan para agrupar un rango de caracteres.

/ Las barras se utilizan para delimitar el principio y el final de la expresión regular.

? coincida 0 ó 1 veces

* coincida con 0 ó más veces

+ con 1 ó más veces

{n} especificamos el numero de caracteres que queremos utilizar

| significa Ó

() para caracteres concretos

/i -> insensitivo a mayusculas o minusculas

^ -> Al principio obligará a que coincida con un ancla al comienzo

$ -> Al final obligará a que coincida con un ancla al final.


/^\s*#?([A-F0-9]{6}|[A-F0-9]{3})$\s*/i

#333333

#aa1122

#222222

#111

Modificadores