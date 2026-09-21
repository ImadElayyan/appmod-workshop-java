🌐 [Português (Brasil)](README.pt_BR.md) | [Español](README.es.md)

# Asset Manager

This workshop uses GitHub Copilot to assess and upgrade a Java application, plan focused cloud migrations, and containerize its web and worker modules.

**What the modernization Process Will Do:**
Upgrade Java 8 to Java 21 and Spring Boot 2.x to 3.x. Review storage, messaging, database and identity findings separately; execute only the migrations you choose and validate.

## Table of Contents

- [Overview](#overview)
- [Current Architecture](#current-architecture)
- [Run Locally](#run-locally)
- [App Modernization Workshop](#app-modernization-workshop)

## Overview

The [main](https://github.com/copilot-dev-days/appmod-workshop-java/tree/main) branch of the asset-manager project is the original state before being modernized. It is organized as follows:
* AWS S3 for image storage, using password-based authentication (access key/secret key)
* RabbitMQ for message queuing, using password-based authentication
* PostgreSQL database for metadata storage, using password-based authentication

In this workshop, you will use the **GitHub Copilot app modernization** extension to assess, upgrade, and containerize the project.

**Time Estimates:**
Duration varies with the selected findings. The former health-endpoint timing no longer applies. Plan review, code changes and Azure integration testing are separate activities; no fixed total is promised for this revised workshop.
- **Assess Your Java Application**: ~5 minutes
- **Upgrade Runtime & Frameworks**: ~10 minutes
- **Cloud Migration Findings**: Variable
- **Containerize Applications**: ~5 minutes


## Current Architecture
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
Password-based authentication

## Run Locally

Clone the repository and open the asset-manager folder to run the current project locally:

```bash
git clone https://github.com/copilot-dev-days/appmod-workshop-java.git
cd appmod-workshop-java
```

**Prerequisites**: 
- [JDK 8](https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-8): Required for running the initial application locally.
- [Maven 3.6.0+](https://maven.apache.org/install.html): Required to build the application locally.
- [Docker](https://docs.docker.com/desktop/): Required for running the application locally.

Run the following commands to start the apps locally. This will:
* Use the local file system instead of S3 to store images
* Launch RabbitMQ and PostgreSQL using Docker

Windows:

```batch
scripts\startapp.cmd
```

Linux:

```bash
scripts/startapp.sh
```

To stop, run `stopapp.cmd` or `stopapp.sh` in the `scripts` directory.

## App Modernization Workshop

Ready to modernize this application? Follow the step-by-step workshop guide:

👉 **[Start the Workshop →](WORKSHOP.md)**

The workshop covers:
- Installing GitHub Copilot app modernization
- Assessing your Java application
- Upgrading runtime & frameworks (Java 8 → 21, Spring Boot 2.x → 3.x)
- Plan focused migrations for storage, messaging, databases and identity
- Containerizing applications

