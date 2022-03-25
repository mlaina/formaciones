# IAM - AWS


- **IAM Users & Politicas**
- **CloudTrail**
- **IAM Groups**
  - **Crear IAM Groups**
  - **Asignación de usuarios a grupos & cambiar políticas**
  - **Cambiar de IAM Groups**
- **Escenarios de IAM Group**
- **Buenas prácticas**

---
## IAM Users & Politicas

- Acceso seguro
- Control minucioso
- Accesos temporales
- Identidad Contrastada
- Integración con otros servicios de AWS

Las pliticas de IAM se estructuran en un `.json`. 

~~~
{
    "Version" : "2012-10-17",
    "Statement" : [
        "Sid" : "VisualEditor0",
        "Effect" : "Allow",
        "Action" : "s3:CreateBucket",
        "Resource" : "*",
        "Condition" : {
            "IpAddress" : {
                "aws:SourceIp" : "210.75.12.75/16"
            }
        }
    ]
}

~~~

- **Action** - Service:Verbo

- **Resource** - Restricción. En este caso con * es totalmente permisivo.

- **Condition** - Condiciones de la política para que se aplique.

Sabemos **qué** es lo que puedes hacer, **dónde**, bajo **qué circunstancias**.

Estas políticas se aplican a **users**, **groups** o **roles**.

---

## **Cloud Trail**

Trackea toda la actividad que se hace mediante una cuenta de AWS.
- AWS console
- AWS CLI tools
- AWS SDKs
- Otros servicios de AWS

Analisis de seguridad y automatización. Analizador de problemas.


### **Management Events**

Operaciones de control.

Ejemplo: Eliminación de una instancia EC2.
- Cuenta AWS 
- IAM user role
- IP del usuario
- Tiempo de reacción
- Recursos afectados

### **Data Events**

Operaciones de datos.

Ejemplo: Acciones de un API sobre objetos S3.
- Cuenta AWS 
- IAM user role
- IP del que hace la llamada
- Tiempo de retardo de las llamadas a la API
- Y más.

Guarda los eventos de los últimos 90 días. Pero se pueden descargar los logs para que se guarden en 

--- 
## IAM Groups

Grupos de usuarios.

Una IAM Group no es una verdadera identificación.

Los nombres de grupos son únicos para cada cuenta.

Las políticas del grupo las heredan los usuarios.

Se pueden crear varios usuarios a la vez.

Se pueden tener multiples politicas 

---
## IAM Escenario

