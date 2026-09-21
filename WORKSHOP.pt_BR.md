<!-- l10n-sync: source-file="WORKSHOP.md" -->
# Workshop de Modernização de Aplicações

As seções a seguir orientam você no processo de modernização da aplicação Java de exemplo `asset-manager` para o Azure usando o GitHub Copilot app modernization.

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Instalar o GitHub Copilot app modernization](#instalar-o-github-copilot-app-modernization)
- [Avaliar Sua Aplicação Java](#avaliar-sua-aplicação-java)
- [Atualizar Runtime e Frameworks](#atualizar-runtime-e-frameworks)
- [Resolver descobertas de migração para a nuvem](workshop/pt_BR/04-cloud-findings.md)
- [Conteinerizar Aplicações](#conteinerizar-aplicações)

## Pré-requisitos

- Uma conta GitHub com o [GitHub Copilot](https://github.com/features/copilot) habilitado. É necessário um plano Pro, Pro+, Business ou Enterprise.
- Um dos seguintes IDEs:
  - A versão mais recente do [Visual Studio Code](https://code.visualstudio.com/). Deve ser a versão 1.101 ou posterior.
    - [GitHub Copilot no Visual Studio Code](https://code.visualstudio.com/docs/copilot/overview). Para instruções de configuração, consulte [Configurar o GitHub Copilot no Visual Studio Code](https://code.visualstudio.com/docs/copilot/setup). Certifique-se de entrar na sua conta GitHub dentro do Visual Studio Code.
    - [GitHub Copilot app modernization](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure). Reinicie o Visual Studio Code após a instalação.
  - A versão mais recente do [IntelliJ IDEA](https://www.jetbrains.com/idea/download). Deve ser a versão 2023.3 ou posterior.
    - [GitHub Copilot](https://plugins.jetbrains.com/plugin/17718-github-copilot). Deve ser a versão 1.5.59 ou posterior. Para mais instruções, consulte [Configurar o GitHub Copilot no IntelliJ IDEA](https://docs.github.com/en/copilot/get-started/quickstart). Certifique-se de entrar na sua conta GitHub dentro do IntelliJ IDEA.
    - [GitHub Copilot app modernization](https://plugins.jetbrains.com/plugin/28791-github-copilot-app-modernization). Reinicie o IntelliJ IDEA após a instalação. Se você não tiver o GitHub Copilot instalado, pode instalar o GitHub Copilot app modernization diretamente.
    - Para uso mais eficiente do Copilot na modernização de aplicações: nas configurações do IntelliJ IDEA, selecione a janela de configuração **Tools** > **GitHub Copilot** e então selecione **Auto-approve** e **Trust MCP Tool Annotations**. Para mais informações, consulte [Configurar ajustes do GitHub Copilot app modernization para otimizar a experiência no IntelliJ](configure-settings-intellij.md).
- [Java JDK](/java/openjdk/download) para as versões de JDK de origem e destino.
- [Maven](https://maven.apache.org/download.cgi) ou [Gradle](https://gradle.org/install/) para compilar projetos Java.
- Um projeto Java gerenciado por Git usando Maven ou Gradle.
- Para projetos baseados em Maven: acesso ao repositório público Maven Central.
- Nas configurações do Visual Studio Code, certifique-se de que `chat.extensionTools.enabled` esteja definido como `true`. Esta configuração pode ser controlada pela sua organização.

> Nota: Se você estiver usando Gradle, apenas o Gradle wrapper versão 5+ é suportado. O Kotlin Domain Specific Language (DSL) não é suportado.
>
> A funcionalidade `My Tasks` ainda não é suportada para o IntelliJ IDEA.

## Clonar o Repositório

```bash
git clone https://github.com/copilot-dev-days/appmod-workshop-java.git
cd appmod-workshop-java
```

## Instalar o GitHub Copilot app modernization

No VSCode, abra a visualização de Extensões na Barra de Atividades, pesquise pela extensão `GitHub Copilot app modernization` no marketplace. Clique no botão Instalar para a extensão. Após a conclusão da instalação, você deverá ver uma notificação no canto inferior direito do VSCode confirmando o sucesso.

**Alternativa: IntelliJ IDEA**
Alternativamente, você pode usar o IntelliJ IDEA. Abra **File** > **Settings** (ou **IntelliJ IDEA** > **Preferences** no macOS), navegue até **Plugins** > **Marketplace**, pesquise por `GitHub Copilot app modernization` e clique em **Install**. Reinicie o IntelliJ IDEA se solicitado.

## Avaliar Sua Aplicação Java

O primeiro passo é avaliar a aplicação Java de exemplo `asset-manager`. A avaliação fornece insights sobre a prontidão da aplicação para migração ao Azure.

1. Abra o VS Code com todos os pré-requisitos instalados para o asset manager, mudando o diretório para o diretório `asset-manager` e executando `code .` nesse diretório.
1. Na barra lateral de Atividades, abra o painel da extensão **GitHub Copilot app modernization**.
1. Na seção **QUICKSTART**, clique em **Start Assessment** para iniciar a avaliação da aplicação.

   ![Trigger Assessment](doc-media/trigger-assessment.png)

1. Aguarde a conclusão da avaliação. Esta etapa pode levar vários minutos.
1. Após a conclusão, uma aba **Assessment Report** será aberta. Este relatório fornece uma visão categorizada de problemas de prontidão para a nuvem e soluções recomendadas. Selecione a aba **Issues** para visualizar as soluções propostas e prosseguir com as etapas de migração.

## Atualizar Runtime e Frameworks

1. No **QuickStart** do painel de modernização, selecione **Upgrade Java Runtime & Frameworks** no VS Code, ou **Upgrade Runtime & Frameworks** no IntelliJ IDEA.
2. Selecione **Java 21** e **Spring Boot 3.x** (por exemplo, 3.5.x). Revise o plano gerado antes de confirmar a execução.
3. Mantenha as integrações de armazenamento e mensageria; não inclua problemas de migração para a nuvem com **Create Plan**.
4. Revise as alterações e verifique os dois módulos com Maven e JDK 21.

A interface atual não exige **Run Task** em cada problema. Consulte a [Etapa 3](workshop/pt_BR/03-upgrade.md) para o fluxo atualizado, o prompt alternativo e os pontos de verificação.

## Resolver descobertas de migração para a nuvem

Planejar migrações de armazenamento, mensageria, bancos de dados e identidade. [Resolver descobertas de migração para a nuvem](workshop/pt_BR/04-cloud-findings.md).

## Conteinerizar Aplicações

Após revisar as descobertas selecionadas, conteinerize a aplicação. Um plano revisado não comprova uma migração concluída; registre separadamente o trabalho de integração pendente.

1. Na barra lateral de Atividades, abra o painel da extensão **GitHub Copilot app modernization**. Na seção **TASKS**, expanda **Common Tasks** > **Containerize Tasks** e clique no botão de execução para **Containerize Application**.
  
    ![Run Containerize Application task](doc-media/containerization-run-task.png)

1. Um prompt predefinido será preenchido no painel do Copilot Chat com o Agent Mode. O Copilot Agent começará a analisar o workspace e criará um **containerization-plan.copiotmd** com o plano de conteinerização.

    ![Containerization prompt and plan](doc-media/containerization-plan.png)
1. Visualize o plano e colabore com o Copilot Agent enquanto ele segue as **Execution Steps** do plano, clicando em **Continue**/**Allow** nas notificações pop-up do chat para executar comandos. Algumas das etapas de execução utilizam ferramentas agênticas do **Container Assist**.

    <!-- ![Containerization execution steps](doc-media/containerization-execution-steps.png) -->
1. O Copilot Agent ajudará a gerar Dockerfile, construir imagens Docker e corrigir erros de build, se houver. Clique em **Keep** para aplicar o código gerado.
