# ***Resumen de AWS Essentials***

## *Cloud computing*

En vez de tener servidores físicos, se sirven servicios bajo demanda en red.
Una de las claves es poder reescalar los recursos según los necesitas.
Con AWS Cloud puedes levantar servidores y tirarlos en cuestión de minutos a placer.
Además tienes opción a probar desarrollos en nube y demás.

## *Conceptos básicos de AWS*

- Elasticidad (*Elasticity*) es poder escalar recursos de servidores rápidamente. En AWS puedes autoprogramar reescalados según la demanda o según ciertos parámetros.
- Fiabilidad (*Reliability*) es la habilidad de recuperar un sistema por una caída o un fallo de infraestructura. Para que se dé la fiabilidad, la arquitectura tiene que estar preparada para cambios en caliente, detectar fallos y solventarlos automáticamente. Reliability es una de las claves de AWS cloud.
- *Avaiability* facilities significa tener los datos duplicados en varios servidores por si uno falla que los demás sean independientes a ese y estén "al toque" por si uno falla.
- La seguridad (*Security*) es una de las cosas más importantes para AWS, con AWS cloud puedes decidir en qué región alojas los datos, como tratas la encriptación y quién mantiene esa encriptación dependiendo de la región

## ***AWS Interfaces***
Hay 3 posibilidades o interfaces distintas:

1. *AWS Management Console* (interfaz gráfica)
2. *Command Line Interface* (CLI, consola de comandos) 
3. *Software Development Kits* (SDKs, api-rests que te permiten controlar todo a través de código)

Se pueden usar las tres interfaces simultáneamente aunque CLI y SDKs te permite monitorizar y programar cambios y cualquier cosa que quieras a través de código o crons.
Se pueden taggear cosas en la propia cloud de AWS para buscarlo más fácilmente y modificar lo que necesitas.
Puedes crear tus propias herramientas a través de la CLI o del SDK.
Lenguajes disponibles de los SDKs (api's): JS, Java, C++, Ruby, .NET, Nodejs, Go, Python, PHP.


### ***Core Services***

#### 1. Amazon EC2
*EC2* (Elastic Compute Cloud) son servidores en la nube configurables y elásticos (relacionado con el concepto de elasticity). Son "pay as you go" (pagas por lo que levantas y está activo). Puedes elegir hardware y software de las instancias que levantas y dónde se van a alojar. Cuando levantas una instancia eliges el servidor (Linux-Windows servers), el tipo de instancia (vCPUs, RAM, etc), redes (networks, ips...), almacenamiento (GBs de almacenamiento, discos...), etiquetas (tags para facilitar la gestión) y grupos de seguridad (reglas de firewall, protocolos, etc). Cuando vas a configurar una instancia, al final te pide una clave pública y una privada así que para entrar a una instancia tendrás que añadir una y para conectarte deberás vincularla. 

#### 2. Amazon EBS
*EBS* son volúmenes para las instancias EC2. Puedes escoger entre HDD y SDD, bloques persistentes de almacenamiento y configurables. Se replican en la misma zona de viabilidad (Avaiability Zone) para evitar la pérdida de datos en caso de fallo o caída. Se pueden configurar backups en forma de SNAPSHOTS con los EBS. Se pueden crear EBS encriptados sin coste adicional. Se pueden realizar on the fly (en caliente). Para poder vincular un volumen a una instancia EC2 necesitan estar en la misma zona de viabilidad (Avaiability Zone). Para utilizar un volumen tendrás que vincularlo a la instancia y posteriormente montarlo. Si quieres desvincularlo de una instancia tendrás que desmontarlo y luego desvincularlo de la misma. 

----------
Ventajas de **EC2 vs Servidores físicos**
- La capacidad de tener diferentes requerimientos de capacidad
- Pagar sólo por la capacidad que estés usando
----------

#### 3. Amazon S3
S3 (Amazon Simple Storage Service) es una nube de almacenamiento de servicios gestionable, la cual provee de una API sencilla para enviar y recibir datos. Puedes guardar una cantidad ilimitada de objetos, de cualquier tipo, en S3. Puedes incluso guardar snapshots de bbdds como objeto en S3. S3 provee de la capacidad de almacenar cualquier objeto desde donde sea y cuando sea. Tiene un sistema fuerte de control de seguridad, ya sea gestionando grupos de acceso que puedan acceder, creando buckets de seguridad o incluso gestionando la seguridad objeto a objeto. Puedes encriptar los datos en tránsito y, por defecto, la visibilidad de los objetos es privada. Cuando creas un bucket en S3, tienes que definir la región en la que se va a almacenar y éste se replicará en distintos servidores de la misma región para evitar pérdida de datos. La gestión de la capacidad de los buckets es reescalable en caliente al igual que la gestión de los grupos de acceso. Puedes acceder a S3 a través de las 3 interfaces de AWS. Casos básicos de uso: Storing Application Assets, Static Web Hosting, Backup & Disaster Storage, Staging area for Big Data...

#### 4. AWS Global Infrastructure
La infraestructura de AWS puede resumirse en 3 puntos: AWS Regions, Avaiability Zones y Edge Locations. 
- *AWS Regions*: Son regiones geográficas que sustentan dos o más "Avaiability Zones" y son las que se encargan de organizar los servicios de AWS. Para elegir una región hay que tener en cuenta cuánta latencia generará con el mínimo coste posible mientras que se ajuste a los requerimientos regulatorios de la zona. Los recursos que tengas desplegados en una región no se replicarán en otra automáticamente y no todos los servicios están disponibles en todas las regiones. 
- *Avaiability Zones*: Son una colección de data centers en una región concreta. Cada zona es independiente pero las de una misma región están conectadas por una red de baja latencia. Cada una es distinta y cada una tiene sus propias fuentes de alimentación y de recuperación de datos. Al tener esta infraestructura se garantiza la high avaiability y la redundancia de datos sin riesgo de pérdida.
- *Edge Locations*: Estas localizaciones albergan una Content Delivery Network (CDN) llamada Amazon CloudFront. CloudFront está dirigido para enviar el contenido a los consumidores de las aplicaciones en AWS. Cuando un cliente hace una petición se envía al Edge location enrutado más cercano para garantizar una rápida respuesta de los servidores. Estas localizaciones están situadas en zonas de alta densidad de población para responder a las peticiones más rápidamente. 

#### 5. Amazon Virtual Private Cloud (VPC)
Es la red de servicios de AWS que provee de los requerimientos de protocolos de seguridad y regionales necesarios para la actividad de las aplicaciones en AWS. Es una red privada y virtual en AWS Cloud (con las mismas premisas de una red normal) que te provee de control total para tus redes y te ofrece una variedad de protocolos de seguridad para el tráfico de la red además de poder desplegar otros servicios de AWS en VPC. Puedes definir redes, grupos de redes, subredes y un montón de cosicas de cosiquear de redes dentro de ellas.

#### 6. Security Groups
Los grupos de seguridad actuan como firewalls para los servidores virtuales que tengas desplegados y proporcionan, según estén gestionados, acceso a unas u otras instancias dependiendo del grupo de seguridad al que pertenezca el usuario a través de reglas. Puedes definir el tráfico que puede permitir un servidor dependiendo del grupo de usuarios al que pertenezca el que esté accediendo. Por ejemplo, un grupo que accede a través de internet (como los clientes) puede tener acceso sólo al Web tier (página web y asociados), sólo ésta es la que se encarga de llamar a servicios del Application tier (a través de una API por ejemplo) y, a su vez, ésta es la que accede a servicios del Database tier. Se pueden crear y gestionar los grupos de seguridad a través de la interfaz gráfica y de ésta manera gestionar y crear las reglas necesarias para acceder a tus servidores y servicios desplegados en AWS. 
