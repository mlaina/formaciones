# Map - Reduce

Modelo de programación de alto nivel e implementación para el procesamiento de datos paralelos a gran escala.

**Operaciones:** map, reduce.

**Data model:** key, value, pairs.

Los **Mappers** se ejecutan en el nodo que contiene los datos. Ejecuta los procesos en paralelo, por bloques. Formando pares clave/valor. La clave puede usarse o no dependiendo de la operación que se vaya a hacer, pero los datos de salida siempre son pares clave valor.


~~~
map(in_key, in_value) -> [(out-key, out-value) … ]
~~~


**Reducer**. 
Después del mapa, todos los valores intermedios para una clave de salida dada se combinan en una lista. El reductor puede producir pares clave/valor.

---

**Ejemplo Contador de palabras:**

~~~
map(String in-key, String in-text)
    foreach word w in in-text:
        emit(w,1)
~~~
~~~
reduce(String in-key, List<int> med-val)
    count = 0
    foreach val i in med-val:
        count += i
    emit(in-key, count)
~~~

### Maper

Input
~~~
(7456, ‘bigdata is not only big and data’)
(7489, ‘bigdata is also knowledge in data’)
~~~

Output
~~~
(‘bigdata’,1),(‘is’,1),(‘not’,1),(‘only’,1),
(‘big’,1),(‘and’,1),(‘data’,1),(‘bigdata’,1),
(‘is’,1),(‘also’,1),(‘knowledge’,1),(‘in’,1),
(‘data’,1)
~~~

### Reducer

Input
~~~
(‘bigdata’, [1,1]),(‘is’, [1,1]),(‘not’, [1]),
(‘only’,[1]),(‘big’,[1]),(‘and’,[1]),
(‘data’,[1,1]),(‘also’,[1]),
(‘knowledge’,[1]),(‘in’,[1])
~~~

Output
~~~
(‘bigdata’, 2),(‘is’, 2),(‘not’, 1),
(‘only’, 1),(‘big’, 1),(‘and’, 1),
(‘data’, 1),(‘also’, 1),
(‘knowledge’, 1),(‘in’, 1)
~~~