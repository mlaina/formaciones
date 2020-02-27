## **HDFS**

**Hadoop Distributed File System**

In Sandbox:
`hdfs dfs -ls /user/hue`

Sistema de archivos distribuido con alta disponibilidad.

Tiene un **Namenode** y muchos **Datanodes**

**Fault Tolerance**, tolerante a fallos de hardware. por lo que se mantienen mínimo tres copias del mismo archivo, por si un **DataNode**.

**Yarn** es un framework que funciona como programador y cluster.

**MapReduce**, basado en YARN para paralelizar procesos de conjuntos muy grandes.

---

## **Creating, Manipulating and Retrievign HDFS files**

### **Basics**

`hdfs dfs -ls`

`hdfs dfs -ls /user/`

`hdfs dfs -help`

`hdfs dfs -usage <utility_name>`

`hdfs namenode`

`hdfs datanode`

- `ls` -> muestra todos los ficheros y carpetas.
- `touchz` -> crea un fichero en ese directorio.
- `cat` -> display el contenido del fichero.
- `mkdir` -> crea un directorio.
- `cp` -> copia archivos.
- `mv` -> mueve ficheros.
- `rm` -> borra ficheros.

### **Permisions**

Estos son los permisos que hay, read, write or execution.

- POSIX. `chmod` -> modo
- Groups. `chgrp` -> frupo
- Owner. `chown` -> propietario

### **Comandos Data**

- `hdfs dfs -put file /user/hdfs/file` -> copia archivos de local a hdfs.
- `hdfs dfs -get /user/hdfs/file file` -> copia archivos de hdfs a local.
- `hdfs dfs -moveFromLocal file /user/hdfs/file` -> copia archivos de local a hdfs y borra el archivo local.

`hdfs dfs -expunge` vacía la papelera.

---
## **Sqoop**

Herramienta para trasferir data entre bases de datos relacionales y hadoop.
Escrito en Java. Admite *MySQL, Oracle, SQL Server, PostgreSQL*.

También tiene la opcioón de utilizar bases de datos NoSQL. Permite la automatización.
Sirve tanto para introducir datos en bases de datos, como para introducirlos en HDFS.

`DESCRIBE TABLE;` -> Información de tabla SQL.

Comandos **Sqoop**:

- `sqoop list-tables --connect jdbc:mysql://(MySQL Address)/dbname`-> Muestra las tablas de la base de datos.
- `sqoop import --connect jdbc:mysql://host/dbname --table tableName -m 1` -> Importa una tabla de la base de datos a HDFS.
- `sqoop import --connect jdbc:mysql://host/dbname --query 'select * from ...'` -> Importa datos de una query concreta, de la base de datos a HDFS.

`--target-dir /user/dir` directorio destino.

---
## **Pig and Hive**

### **Hive**

Schema bound | HiveQL | Extendable

`hive`  -> Se abrirá una sesión de Hive, después se puede proceder a escribir las queries en HiveQL (muy parecido al SQL).

Dentro de la consola se pueden ejecutar los siguientes comandos.

- `!ls`
- `dfs -ls /user`

`LOAD DATA INPATH 'user/file.csv' OVERWRITE INTO TABLE ...;`

### **Apache Pig**

No tiene schema bound | utiliza Pig Latin | Desestructurado o semiestructurado.

~~~
A = LOAD 'somefile' USING PigStorage(',')
AS (field1, field2, field3);
results = FOREACH a GENERATE field1;
DUMP results;


STORE combined INTO /user/var' USING PigStorage(,);
~~~

`pig -x local` -> abre la consola de local.

---
## **HBase**

Base de datos NoSQL distribuida y escalable.

- `hbase shell`
- `list`
- `create 'tableName', 'columnName'`
- `put 'tableName', 'rowNumber', 'columnName', 'value'`
- `get 'tableName', 'rowNumber'`
- `scan 'tableName'`
- `disable 'tableName'`
- `drop tableName`

Enable **Ambari** -> gestión de ecosistema HDFS.

~~~
a = LOAD 'file.csv' USING PigStorage(',') as (open:chararray);

STORE a INTO 'hbase://app_stock' USING org.apache.pig.backend.hadoop.hbase.HBaseStorage('info:open')
~~~

`nano hbase_pig.pig`

`pig -f hbase_pigloader.pig`

---
