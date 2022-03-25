# SQL

- [Sistemas SQL](#Sistemas_SQL)
- [Tipos de comandos](#Tipos_de_comandos)
- [DML](#DML)
- [DQL](#DQL)
- [DDL](#DDL)
- [JOINs](#JOINs)
- [DCL](#DCL)
- [Vista](#Vista)
- [Subqueries](#Subqueries)

---

## Sistemas SQL

- DB2
- Firebird
- HSQL
- Informix
- InterBase
- MariaDB
- Microsoft SQL Server
- MySQL
- Oracle
- PostgreSQL
- PervasiveSQL
- SQLite
- Sybase ASE

En particular, la sintaxis de fecha y tiempo, la concatenación de cadenas, nulas, y la comparación de textos en cuanto al tratamiento de mayúsculas y minúsculas varían de un proveedor a otro. Una excepción particular es PostgreSQL, que se esfuerza por lograr el cumplimiento del estándar.

- Oracle tiene el tipo `DATE` se comporta como `DATETIME`, y carece de un tipo `TIME`

**

---

## Tipos de comandos

- **DQL** : Lenguaje de consulta de datos.
- **DDL** : Lenguaje de definición de datos (contiene comandos para crear y modificar tareas).
- **DCL** : Lenguaje de control de datos (contiene comandos relacionados con el control de acceso).
- **DML** : Lenguaje de manipulación de datos (contiene comandos para operaciones de inserción, actualización y eliminación).

---

## DML

 “CRUD” (create, read, update y delete/ sus equivalentes son INSERT, SELECT, UPDATE y DELETE).

### INSERT

La necesidad de especificar las columnas o hacerlo en orden respectivo.

```sql
INSERT INTO person (person_id,person_first_name,person_last_name,person_contacted_number,person_date_last_contacted,person_date_added)
VALUES (5,'Foo','Bar',0,'2017-05-14 11:43:42','2017-05-14 11:43:42');
```

**BULK INSERT**

```sql
INSERT INTO person
(person_id,person_first_name,person_last_name,person_contacted_number,person_date_last_contacted,person_date_added)
VALUES
(6,'Foo6','Bar',0,'2017-05-14 11:43:42','2017-05-14 11:43:42'),
(7,'Foo7','Bar',0,'2017-05-14 11:43:42','2017-05-14 11:43:42'),
(42,'Foo8','Bar',0,'2017-05-14 11:43:42','2017-05-14 11:43:42');
```

**INSERT SELECT**:  puedes usar los valores de selección que te proporciona el SELECT de otra tabla previa, y utilizarlos directamente como la lista de columnas. Utilizas una tabla como base de la nueva para la actualización de los datos.

```sql
INSERT INTO 
person p
SELECT 
* FROM old_person op
Where op.person_id > 300;
```

### **UPDATE**: Modifica columna(s) en una sola tabla. El comando WHERE va a dictaminar qué filas van a verse afectadas, y el comando SET va a determinar las columnas y los valores que vamos a actualizar

```sql
UPDATE person p
SET
p.person_first_name = 'Bob',
p.person_last_name = 'Foo'
WHERE
p.person_id = 0;
```

### **DELETE**: cuidado! fijarse en utilizar WHERE en estos comandos

```sql
DELETE DELETE FROM person 
WHERE person_id > 4;
```

---

## DQL

- AND

```sql
SELECT p.person_last_name 
FROM 
person p
WHERE p.person_first_name = 'Jon'
AND
p.person_contacted_number > 5;
```

- OR

```sql
SELECT p.person_last_name 
FROM 
person p
WHERE p.person_first_name = 'Jon'
OR
p.person_contacted_number > 0;
```

- BETWEEN

```sql
SELECT p.person_last_name 
FROM 
person p
WHERE p.person_contacted_number 
BETWEEN 1 AND 20; 

```

- LIKE - %

```sql
SELECT p.person_last_name 
FROM 
person p
WHERE p.person_first_name 
LIKE 'J%';
```

- IN

```sql
SELECT  p.person_last_name
FROM person p
WHERE p.person_first_name
IN ('Jon','Fritz');
```

- IS

```sql
SELECT e.email_address_person_id, e.email_address
FROM
email_address e
WHERE
e.email_address_person_id IS NULL
```

- IS NOT

```sql
SELECT e.email_address_person_id, e.email_address
FROM
email_address e
WHERE
e.email_address_person_id IS NOT NULL
```

---

- DISTINCT: se utiliza para acotar, directamente dentro del comando select. Con ello podemos averiguar cuantos elementos distintos tenemos, utilizando por ejemplo "COUNT".

```sql
SELECT DISTINCT Country FROM Customers;

SELECT COUNT(DISTINCT Country) FROM Customers;
```

---

- ORDER

```sql
SELECT p.person_first_name,p.person_last_name
FROM person p
ORDER BY p.person_last_name;
```

- GROUP

```sql
SELECT  column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s);
```

---
SET FUNCTIONS:

- COUNT

```sql
SELECT COUNT(p.person_first_name)
FROM person p
WHERE p.person_last_name = 'Ahern';
```

- MAX

```sql
SELECT MAX(p.person_contacted_number)
FROM person p;
```

- MIN

```sql
SELECT MIN(p.person_contacted_number)
FROM person p;
```

- AVERAGE

```sql
SELECT AVG(p.person_contacted_number)
FROM person p;
```

- SUM

```sql
SELECT SUM(p.person_contacted_number)
FROM person p;
```

---

## JOINs

Si no se especifica el tipo de JOIN se realiza INNER JOIN.

![joins](sqljoin.jpeg)

- CROSS JOIN:
Consulta ineficiente, evitar. No utilizar. Cruza cada dato de las columnas utilizadas de la primera tabla con cada dato de las columnas utilizadas de la segunda tabla.

```sql
SELECT
```

- INNER JOIN: La más común. Hay que tener al menos un elemento que relacione las dos tablas.

Ejemplo:
¿Cuáles son las direcciones de email de mis contactos?

Relacionamos las tablas a través del elemento común, en este caso el identificador del contacto. p. person_id es primary key, mientras que e. email_address_person_id es la foreign key

Las INNER JOINs no tratan con valores “null” (ignoran , y las OUTER JOINs sí.

```sql
SELECT p. first_name, p.last_name, e.email_address
FROM person p
INNER JOIN email_address e
ON p. person_id= e. email_address_person_id;
```

- OUTER JOIN: Los OUTER JOINs darán valores “null” cuando no haya coincidencia en la presencia de datos de las tablas relacionadas, y lo reflejarán en el resultado. Nos sirve para tener en cuenta esos valores “null”.

```sql
SELECT p. first_name, p.last_name, e.email_address
FROM person p
OUTER JOIN email_address e
ON p. person_id= e. email_address_person_id;
```

- LEFT OUTER JOIN: Unión que puede dar valores “null”
todas las filas procedentes de la tabla “izquierda” se verán reflejadas en el resultado.
Las filas de la “derecha”, la de la foreign key, darán el resultado correspondiente, incluyendo los valores “null”
El esquema de construcción de la query es el mismo.

```sql
SELECT p. first_name, p.last_name, e.email_address
FROM person p
LEFT OUTER JOIN email_address e
ON p. person_id= e. email_address_person_id;
```

- RIGHT OUTER JOIN: Exactamente lo contrario al apartado anterior, se reflejan todas las filas de la tabla derecha, y los correspondientes de la tabla izquierda, incluyendo los valores “null”.

```sql
SELECT p. first_name, p.last_name, e.email_address
FROM person p
RIGHT OUTER JOIN email_address e
ON p. person_id= e. email_address_person_id;
```

- FULL OUTER JOIN: Combinación de las dos últimas uniones, obtenemos un resultado más completo que comprendería los matches de presencia de información de las tablas izquierda y derecha, además de los null presentes en cualquiera de las tablas. Todo esto matizando que siempre hablamos de las columnas especificadas en SELECT, no de las dos tablas en su totalidad.

MySQL no da soporte a este tipo de opción, a pesar de formar parte del estándar de SQL.
Sin embargo se puede hacer algo similar, que en general no se recomienda demasiado, pero es interesante saberlo.
Consiste en utilizar la keyword UNION junto con DISTINCT (para evitar la duplicación de filas) entre el código de la query LEFT OUTER JOIN y la query RIGHT OUTER JOIN. Se considera más avanzado pero aquí está.

```sql
SELECT p. first_name, p.last_name, e.email_address
FROM person p
FULL OUTER JOIN email_address e
ON p. person_id= e. email_address_person_id;
```

- SELF JOIN: El concepto detrás de esta JOIN es un poco particular, porque consiste en unir una tabla consigo misma. Suena raro pero puede resultar útil. No hay una KEYWORD asociada a esta JOIN, es algo conceptual que puede utilizarse en cualquiera de las JOINs anteriores, poniendo a la izquierda y a la derecha la misma tabla. Es útil para tablas que contienen información jerarquizada, como empleados y sus superiores, por ejemplo.

```sql
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```

- MERGE:
La instrucción MERGE básicamente une datos de un resultado de origen establecido en una tabla destino. Se envían los datos al MERGE, el los compara (por la llave primaria), si existe los actualiza y si no existe los ingresa, también podría ser que si no cumple con los requisitos los pueda borrar,  insert, update y delete en una sola instrucción.
MERGE también permite comparar dos tablas, una fuente y otra destino en ingresar o modificar los datos de la tabla en base a los datos de otra tabla, eso lo veremos en otro ejemplo que publicaremos en este sitio.

```sql
MERGE TargetProducts AS Target
USING SourceProducts AS Source
ON Source.ProductID = Target.ProductID
WHEN NOT MATCHED BY Target THEN
    INSERT (ProductID,ProductName, Price) 
    VALUES (Source.ProductID,Source.ProductName, Source.Price);
```

---

## DDL

- CREATE TABLE

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

- ALTER TABLE

```sql
ALTER TABLE Customers
ADD Email varchar(255);
```

- DROP TABLE

```sql
DROP TABLE Shippers;
```

### Data Types

![Data types](datatypes.png)

### CONSTRAINTS

Las restricciones de SQL se utilizan para especificar reglas para los datos de una tabla.

- PRIMARY KEY:
Las KEYS son una parte muy importante del diseño de una base de datos, porque son esenciales para el sistema relacional. La primera es la PRIMARY KEY, que tiene una serie de condiciones:

  - Debe ser único por fila.
  - No puede ser nulo.
  - Pueden ser varias columnas

```sql
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

- UNIQUE:
Asegura que todos los valores en una columna sean diferentes.

```sql
ALTER TABLE Persons
ADD UNIQUE (ID);
```

- FOREIGN KEY: La FOREIGN KEY restricción se utiliza para evitar acciones que destruirían enlaces entre tablas.
Una FOREIGN KEY un campo (o colección de campos) en una tabla, que se refiere a PRIMARY KEY en otra tabla.
La tabla con la clave externa se denomina tabla secundaria, y la tabla con la clave principal se denomina tabla principal o de referencia.

```sql
ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

- NOT NULL

El significado de NULL es que no hay valor real, que está “vacío”, lo cual no es lo mismo que un 0.
Si una columna es obligatoria o REQUIRED no puede tener valores NULL, en caso contrario sí que puede haber valores NULL.
Definir qué columnas van a ser REQUIRED y cuáles no es una cuestión de lógica.

```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

### Secuencia

Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según la especificación con la que se creó la secuencia.

CYCLE para permitir que la secuencia genere valor después de alcanzar el límite, el valor mínimo para una secuencia descendente y el valor máximo para una secuencia ascendente.
Cuando una secuencia ascendente alcanza su valor máximo, genera el valor mínimo.
Por otro lado, cuando una secuencia descendente alcanza su valor mínimo, genera el valor máximo.

CACHE Especifique la cantidad de valores de secuencia que Oracle preasignará y mantendrá en la memoria para un acceso más rápido.

```sql
CREATE SEQUENCE id_seq
    INCREMENT BY 10
    START WITH 10
    MINVALUE 10
    MAXVALUE 100
    CYCLE
    CACHE 2;
```

---

## DCL

### Schema

En SQL Server los esquemas representan un conjunto lógico dentro de una base de datos. Permiten organizar mejor de manera lógica las tablas, vistas, procedimientos y funciones. Por defecto, durante la creación de un objeto, éste se registra en el esquema del usuario actual.

### Sinónimo

Un sinónimo es un objeto de base de datos que sirve para los siguientes objetivos:
Proporciona un nombre alternativo para otro objeto de base de datos, denominado objeto base, que puede existir en un servidor local o remoto.
Proporciona una capa de abstracción que protege una aplicación cliente de cambios realizados en el nombre o la ubicación del objeto base.

### Grants

El comando GRANT permite asignar accesos por usuario sobre una o más tablas. Los derechos más utilizados son: SELECT: autoriza la selección de datos. UPDATE: autoriza la modificación de datos.

---

## Vista

En una base de datos, una vista es el conjunto de resultados de una consulta almacenada en los datos. Es una consulta que se presenta como una tabla (virtual) a partir de un conjunto de tablas en una base de datos relacional.

Las vistas tienen la misma estructura que una tabla: filas y columnas. La única diferencia es que sólo se almacena de ellas la definición, no los datos. Los datos que se recuperan mediante una consulta a una vista se presentarán igual que los de una tabla. De hecho, si no se sabe que se está trabajando con una vista, nada hace suponer que es así. Al igual que sucede con una tabla, se pueden insertar, actualizar, borrar y seleccionar datos en una vista. Aunque siempre es posible seleccionar datos de una vista, en algunas condiciones existen restricciones para realizar el resto de las operaciones sobre vistas.
Una vista se especifica a través de una expresión de consulta (una sentencia SELECT) que la calcula y que puede realizarse sobre una o más tablas. Sobre un conjunto de tablas relacionales se puede trabajar con un número cualquiera de vistas.

```sql
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';
```

---

## Subqueries

```sql
SELECT id, first_name 
FROM student_details 
WHERE first_name IN (SELECT first_name
FROM student_details 
WHERE subject= 'Science'); 
```

---

## Procedimiento Almacenado

Un procedimiento almacenado (stored procedure en inglés) es un programa (o procedimiento) almacenado físicamente en una base de datos. Su implementación varía de un gestor de bases de datos a otro. La ventaja de un procedimiento almacenado es que al ser ejecutado, en respuesta a una petición de usuario, es ejecutado directamente en el motor de bases de datos, el cual usualmente corre en un servidor separado. Como tal, posee acceso directo a los datos que necesita manipular y sólo necesita enviar sus resultados de regreso al usuario, deshaciéndose de la sobrecarga resultante de comunicar grandes cantidades de datos salientes y entrantes.
Los procedimientos pueden ser ventajosos: cuando una base de datos es manipulada desde muchos programas externos. Al incluir la lógica de la aplicación en la base de datos utilizando procedimientos almacenados, la necesidad de embeber la misma lógica en todos los programas que acceden a los datos es reducida. Esto puede simplificar la creación y, particularmente, el mantenimiento de los programas involucrados.
