<!-- l10n-sync: source-file="README.md" -->
# Asset Manager

Este taller usa GitHub Copilot para evaluar y actualizar una aplicación Java, planificar migraciones acotadas y contenedorizar los módulos web y worker.

**Lo que hará el Proceso de Modernización:**
Actualice Java 8 a Java 21 y Spring Boot 2.x a 3.x. Revise por separado los hallazgos de almacenamiento, mensajería, base de datos e identidad; ejecute solo las migraciones elegidas y validadas.

## Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Arquitectura Actual](#arquitectura-actual)
- [Ejecutar Localmente](#ejecutar-localmente)
- [Taller de Modernización de Aplicaciones](#taller-de-modernización-de-aplicaciones)

## Descripción General

La rama [main](https://github.com/copilot-dev-days/appmod-workshop-java/tree/main) del proyecto asset-manager es el estado original antes de ser modernizado. Está organizado de la siguiente manera:
* AWS S3 para almacenamiento de imágenes, usando autenticación basada en contraseña (access key/secret key)
* RabbitMQ para colas de mensajes, usando autenticación basada en contraseña
* Base de datos PostgreSQL para almacenamiento de metadatos, usando autenticación basada en contraseña

En este taller, utilizará la extensión **GitHub Copilot app modernization** para evaluar, actualizar y contenedorizar el proyecto.

**Estimaciones de Tiempo:**
La duración depende de los hallazgos seleccionados. El tiempo anterior de endpoints de salud ya no aplica. La revisión del plan, los cambios de código y las pruebas con Azure son actividades distintas; no se promete una duración total fija.
- **Evaluar Su Aplicación Java**: ~5 minutos
- **Actualizar Runtime y Frameworks**: ~10 minutos
- **Hallazgos de migración**: Variable
- **Contenedorizar Aplicaciones**: ~5 minutos


## Arquitectura Actual
```mermaid
flowchart TD

%% Applications
WebApp[Web Application]
Worker[Worker Service]

%% Storage Components
S3[(AWS S3)]
LocalFS[("Local File System<br/>dev only")]

%% Message Broker
RabbitMQ(RabbitMQ)

%% Database
PostgreSQL[(PostgreSQL)]

%% Queues
Queue[image-processing queue]
RetryQueue[image-processing.retry queue]

%% User
User([User])

%% User Flow
User -->|Upload Image| WebApp
User -->|View Images| WebApp

%% Web App Flows
WebApp -->|Store Original Image| S3
WebApp -->|Store Original Image| LocalFS
WebApp -->|Send Processing Message| RabbitMQ
WebApp -->|Store Metadata| PostgreSQL
WebApp -->|Retrieve Images| S3
WebApp -->|Retrieve Images| LocalFS
WebApp -->|Retrieve Metadata| PostgreSQL

%% RabbitMQ Flow
RabbitMQ -->|Push Message| Queue
Queue -->|Processing Failed| RetryQueue
RetryQueue -->|After 1 min delay| Queue
Queue -->|Consume Message| Worker

%% Worker Flow
Worker -->|Download Original| S3
Worker -->|Download Original| LocalFS
Worker -->|Upload Thumbnail| S3
Worker -->|Upload Thumbnail| LocalFS
Worker -->|Store Metadata| PostgreSQL
Worker -->|Retrieve Metadata| PostgreSQL

%% Styling
classDef app fill:#90caf9,stroke:#0d47a1,color:#0d47a1
classDef storage fill:#a5d6a7,stroke:#1b5e20,color:#1b5e20
classDef broker fill:#ffcc80,stroke:#e65100,color:#e65100
classDef db fill:#ce93d8,stroke:#4a148c,color:#4a148c
classDef queue fill:#fff59d,stroke:#f57f17,color:#f57f17
classDef user fill:#ef9a9a,stroke:#b71c1c,color:#b71c1c

class WebApp,Worker app
class S3,LocalFS storage
class RabbitMQ broker
class PostgreSQL db
class Queue,RetryQueue queue
class User user
```
Autenticación basada en contraseña

## Ejecutar Localmente

Clone el repositorio y abra la carpeta asset-manager para ejecutar el proyecto actual localmente:

```bash
git clone https://github.com/copilot-dev-days/appmod-workshop-java.git
cd appmod-workshop-java
```

**Prerrequisitos**: 
- [JDK 8](https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-8): Requerido para ejecutar la aplicación inicial localmente.
- [Maven 3.6.0+](https://maven.apache.org/install.html): Requerido para compilar la aplicación localmente.
- [Docker](https://docs.docker.com/desktop/): Requerido para ejecutar la aplicación localmente.

Ejecute los siguientes comandos para iniciar las aplicaciones localmente. Esto:
* Usará el sistema de archivos local en lugar de S3 para almacenar imágenes
* Iniciará RabbitMQ y PostgreSQL usando Docker

Windows:

```batch
scripts\startapp.cmd
```

Linux:

```bash
scripts/startapp.sh
```

Para detener, ejecute `stopapp.cmd` o `stopapp.sh` en el directorio `scripts`.

## Taller de Modernización de Aplicaciones

¿Listo para modernizar esta aplicación? Siga la guía paso a paso del taller:

👉 **[Iniciar el Taller →](WORKSHOP.es.md)**

El taller cubre:
- Instalación de GitHub Copilot app modernization
- Evaluación de su aplicación Java
- Actualización de runtime y frameworks (Java 8 → 21, Spring Boot 2.x → 3.x)
- Planificar migraciones de almacenamiento, mensajería, bases de datos e identidad
- Contenedorización de aplicaciones
