<!-- l10n-sync: source-file="05-containerize.md" -->
# Etapa 5: Conteinerizar Aplicações

## 🎯 Objetivo

Preparar sua aplicação modernizada para implantação na nuvem, conteinerizando os módulos web e worker usando as tarefas de conteinerização do GitHub Copilot app modernization.

## Executar a Tarefa de Conteinerização

1. Na barra lateral de Atividades, abra o painel da extensão **GitHub Copilot app modernization**. Na seção **TASKS**, expanda **Common Tasks** > **Containerize Tasks** e clique no botão de execução para **Containerize Application**.

    ![Executar tarefa Containerize Application](../doc-media/containerization-run-task.png)

1. Um prompt predefinido será preenchido no painel do Copilot Chat com o Agent Mode. O Copilot Agent começará a analisar o workspace e criará um arquivo **containerization-plan.copilotmd** com o plano de conteinerização.

    ![Prompt e plano de conteinerização](../doc-media/containerization-plan.png)

1. Visualize o plano e colabore com o Copilot Agent enquanto ele segue os **Execution Steps** do plano, clicando em **Continue**/**Allow** nas notificações pop-up do chat para executar comandos. Algumas das etapas de execução utilizam ferramentas agênticas do **Container Assist**.

1. O Copilot Agent ajudará a gerar o Dockerfile, compilar imagens Docker e corrigir erros de compilação, se houver. Clique em **Keep** para aplicar o código gerado.

## O que Isso Faz

O processo de conteinerização irá:
- Analisar a estrutura do projeto (módulo web + módulo worker)
- Gerar `Dockerfile` otimizado para cada módulo
- Configurar builds multi-estágio para imagens menores
- Definir configurações adequadas do runtime Java
- Compilar e testar as imagens Docker localmente

## ✅ Verificação

- [ ] Tarefa de conteinerização iniciada a partir da visualização de Tasks
- [ ] Plano de conteinerização gerado (`containerization-plan.copiotmd`)
- [ ] Dockerfiles gerados para os módulos web e worker
- [ ] Imagens Docker compiladas com sucesso

## 🎉 Parabéns!

Você concluiu o workshop de Modernização de Aplicações! Aqui está o que você realizou:

- ✅ **Avaliou** a aplicação Java legada para entender as necessidades de modernização
- ✅ **Atualizou** do Java 8 → 21 e Spring Boot 2.x → 3.x
- Revisar as descobertas e registrar o que foi migrado, adiado ou deixado fora do escopo
- ✅ **Conteinerizou** a aplicação para implantação na nuvem

### Próximos Passos

- Implante sua aplicação conteinerizada no **Azure Container Apps**
- Explore mais recursos do [GitHub Copilot app modernization](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure)
- Confira o [Guia de Prompts do Copilot](../PROMPTS.md) para prompts adicionais usados durante o desenvolvimento
- Visite os outros [workshops do Copilot Dev Days](https://github.com/copilot-dev-days)
