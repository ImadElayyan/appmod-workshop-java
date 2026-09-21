# Etapa 4: Resolver descobertas de migração para a nuvem

## Objetivo e escopo

Decida quais descobertas resolver e crie um plano de migração delimitado. Isso é separado da atualização para Java 21 / Spring Boot 3.x da Etapa 3.

Em um workshop local, você pode revisar as descobertas e registrá-las como **fora do escopo**. Não as declare resolvidas sem implementar e validar as alterações.

## Selecionar descobertas e criar um plano

1. Salve um commit funcional após a atualização Java.
2. No relatório de avaliação, selecione apenas as descobertas relacionadas e clique em **Create Plan**, se disponível na sua interface. Comece com uma migração, como S3 para Blob Storage, não todas de uma vez.
3. Revise código, configuração, dependências, identidade, transferência de dados e testes. Exclua migrações não relacionadas e provisionamento.
4. Autorize alterações somente depois de revisar o plano. Leia os pedidos de permissão antes de aprovar comandos.
5. Revise o diff, compile e teste os dois módulos e valide o comportamento afetado. Salve um commit antes da próxima migração.
6. Execute novamente a avaliação, se disponível. Registre descobertas residuais e testes pendentes; um relatório limpo não prova que a aplicação funciona.

**Não há Create Plan?** Use Copilot Chat no modo Agent com a extensão de modernização e o prompt abaixo. Não é necessário Run Task em cada descoberta.

**Caminho CLI:** use o mesmo prompt na sessão configurada de modernização do Copilot CLI. Os botões do relatório descrevem o caminho IDE, não comandos de terminal.

## O que cada descoberta exige

| Descoberta | Resolução | Validação |
|------------|-----------|-----------|
| AWS S3 para Azure Blob Storage | Substitua cliente/SDK, dependências e configuração em web e worker. Planeje containers e autenticação. Transferir objetos existentes é uma atividade separada. | Upload, download, miniaturas e acesso aos dados transferidos. |
| Configuração de região AWS | Remova somente após substituir a integração AWS e confirmar que não há referências. Não substitua por um nome de região Azure. | Nenhum cliente AWS ativo depende dela. |
| RabbitMQ para Azure Service Bus | Substitua código e configuração; defina filas, roteamento e semântica de entrega. | Envio, recebimento, tentativas, falhas e duplicatas. |
| PostgreSQL para Azure Database for PostgreSQL | Configure endpoint, TLS, rede e autenticação. Migração de esquema/dados é separada das alterações de código. | Conectividade, consultas e dados necessários. |
| Credenciais / identidade gerenciada | Configure autenticação, identidade da aplicação Azure e permissões específicas. Use uma identidade de desenvolvedor documentada localmente. | Ambos os módulos acessam sem segredos embutidos; código não atribui funções de acesso. |

## Prompt: planejar somente a migração de armazenamento

```text
Crie um plano para migrar a integração AWS S3 para Azure Blob Storage
nos módulos web e worker.
Preserve upload, download e processamento de miniaturas.
Identifique dependências, configuração e autenticação.
Identifique dados existentes que exigem transferência separada.
Remova configurações AWS somente quando não forem mais necessárias.
Mantenha Java 21 e Spring Boot 3.x.
Não altere RabbitMQ nem PostgreSQL nesta tarefa.
Não provisione recursos nem faça deploy ainda.
Mostre o plano antes de fazer alterações.
```

Após revisar o plano, autorize explicitamente as alterações escolhidas. Para outras descobertas, crie planos separados e delimitados.

## Azure, custos e validação

Você pode preparar planos e código **sem assinatura Azure**. Testar contra serviços Azure reais exige acesso a recursos provisionados em uma assinatura, permissões e conectividade. Pode haver custos: obtenha aprovação antes de criar recursos e remova os temporários ao terminar.

Com Maven usando JDK 21, execute `mvn -version` e `mvn clean verify` na raiz e teste as integrações alteradas. Um build aprovado não prova que autenticação, mensageria ou armazenamento Azure funcionam. Testes unitários e emuladores não comprovam autorização real.

## Verificação

- [ ] Descobertas selecionadas ou registradas como fora do escopo local.
- [ ] Plano revisado antes de alterações ou provisionamento.
- [ ] Se houve alterações, ambos os módulos compilam e os testes relevantes passam.
- [ ] Se uma migração é declarada completa, seu comportamento foi validado nos serviços previstos.
- [ ] Transferências de dados, permissões e testes pendentes registrados.

Referência: [tarefas predefinidas da Microsoft](https://learn.microsoft.com/en-us/azure/developer/java/migration/migrate-github-copilot-app-modernization-for-java-predefined-tasks).
