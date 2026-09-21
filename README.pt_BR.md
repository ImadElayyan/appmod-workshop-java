<!-- l10n-sync: source-file="README.md" -->
# Asset Manager

Este workshop usa GitHub Copilot para avaliar e atualizar uma aplicação Java, planejar migrações delimitadas e conteinerizar os módulos web e worker.

**O que o Processo de Modernização Fará:**
Atualize Java 8 para Java 21 e Spring Boot 2.x para 3.x. Revise separadamente as descobertas de armazenamento, mensageria, banco de dados e identidade; execute apenas as migrações escolhidas e validadas.

## Índice

- [Visão Geral](#visão-geral)
- [Arquitetura Atual](#arquitetura-atual)
- [Executar Localmente](#executar-localmente)
- [Workshop de Modernização de Aplicações](#workshop-de-modernização-de-aplicações)

## Visão Geral

O branch [main](https://github.com/copilot-dev-days/appmod-workshop-java/tree/main) do projeto asset-manager é o estado original antes de ser modernizado. Ele está organizado da seguinte forma:
* AWS S3 para armazenamento de imagens, usando autenticação baseada em senha (access key/secret key)
* RabbitMQ para filas de mensagens, usando autenticação baseada em senha
* Banco de dados PostgreSQL para armazenamento de metadados, usando autenticação baseada em senha

Neste workshop, você usará a extensão **GitHub Copilot app modernization** para avaliar, atualizar e conteinerizar o projeto.

**Estimativas de Tempo:**
A duração depende das descobertas selecionadas. O tempo anterior de endpoints de saúde não se aplica mais. Revisão do plano, alterações de código e testes com Azure são atividades distintas; não há duração total fixa prometida.
- **Avaliar Sua Aplicação Java**: ~5 minutos
- **Atualizar Runtime e Frameworks**: ~10 minutos
- **Descobertas de migração**: Variável
- **Conteinerizar Aplicações**: ~5 minutos


## Arquitetura Atual
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
Autenticação baseada em senha

## Executar Localmente

Clone o repositório e abra a pasta asset-manager para executar o projeto atual localmente:

```bash
git clone https://github.com/copilot-dev-days/appmod-workshop-java.git
cd appmod-workshop-java
```

**Pré-requisitos**: 
- [JDK 8](https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-8): Necessário para executar a aplicação inicial localmente.
- [Maven 3.6.0+](https://maven.apache.org/install.html): Necessário para compilar a aplicação localmente.
- [Docker](https://docs.docker.com/desktop/): Necessário para executar a aplicação localmente.

Execute os seguintes comandos para iniciar as aplicações localmente. Isso irá:
* Usar o sistema de arquivos local em vez do S3 para armazenar imagens
* Iniciar o RabbitMQ e o PostgreSQL usando Docker

Windows:

```batch
scripts\startapp.cmd
```

Linux:

```bash
scripts/startapp.sh
```

Para parar, execute `stopapp.cmd` ou `stopapp.sh` no diretório `scripts`.

## Workshop de Modernização de Aplicações

Pronto para modernizar esta aplicação? Siga o guia passo a passo do workshop:

👉 **[Iniciar o Workshop →](WORKSHOP.pt_BR.md)**

O workshop abrange:
- Instalação do GitHub Copilot app modernization
- Avaliação da sua aplicação Java
- Atualização de runtime e frameworks (Java 8 → 21, Spring Boot 2.x → 3.x)
- Planejar migrações de armazenamento, mensageria, bancos de dados e identidade
- Conteinerização de aplicações
