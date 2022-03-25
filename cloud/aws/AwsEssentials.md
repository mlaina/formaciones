# Cloud computing

En vez de tener servidores físicos, se sirven servicios bajo demanda en red.
Una de las claves es poder reescalar los recursos según los necesitas.
Con AWS Cloud puedes levantar servidores y tirarlos en cuestión de minutos a placer.
Además tienes opción a probar desarrollos en nube y demás.

## Conceptos básicos de AWS

- Elasticidad es poder escalar recursos de servidores rápidamente. En AWS puedes autoprogramar reescalados según la demanda o según ciertos parámetros.
- Fiabilidad (Reliability) es la habilidad de recuperar un sistema por una caída o un fallo de infraestructura. Para que se dé la fiabilidad, la arquitectura tiene que estar preparada para cambios en caliente, detectar fallos y solventarlos automáticamente. Reliability es una de las claves de AWS cloud.
- Avaiability facilities significa tener los datos duplicados en varios servidores por si uno falla que los demás sean independientes a ese y estén "al toque" por si uno falla.
- La seguridad es una de las cosas más importantes para AWS, con AWS cloud puedes decidir en qué región alojas los datos, como tratas la encriptación y quién mantiene esa encriptación dependiendo de la región

### AWS Interfaces
Hay 3 posibilidades o interfaces distintas:

1. AWS Management Console (interfaz gráfica)
2. Command Line Interface (CLI, consola de comandos) 
3. Software Development Kits (SDKs, api-rests que te permiten controlar todo a través de código)

Se pueden usar las tres interfaces simultáneamente aunque CLI y SDKs te permite monitorizar y programar cambios y cualquier cosa que quieras a través de código o crons.
Se pueden taggear cosas en la propia cloud de AWS para buscarlo más fácilmente y modificar lo que necesitas.
Puedes crear tus propias herramientas a través de la CLI o del SDK.
Lenguajes disponibles de los SDKs (api's): JS, Java, C++, Ruby, .NET, Nodejs, Go, Python, PHP.
