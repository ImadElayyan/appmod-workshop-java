<!-- l10n-sync: source-file="05-containerize.md" -->
# Etapa 5: Conteinerizar Aplicações

## 🎯 Objetivo

Preparar sua aplicação modernizada para implantação na nuvem, conteinerizando os módulos web e worker usando um prompt em linguagem natural no Copilot CLI.

## Executar a Tarefa de Conteinerização

1. Dentro da sessão do Copilot CLI em execução, digite o seguinte prompt:

   ```
   Containerize this application. Generate optimized Dockerfiles for each module with multi-stage builds, build the Docker images, and fix any build errors.
   ```

2. O Copilot analisará o workspace e gerará um plano de conteinerização. Permita que o Copilot prossiga em cada etapa, incluindo a execução de comandos para compilar imagens Docker.

3. Quando a tarefa for concluída, revise os arquivos `Dockerfile` gerados para os módulos `web` e `worker`.

## O que Isso Faz

O processo de conteinerização irá:
- Analisar a estrutura do projeto (módulo web + módulo worker)
- Gerar `Dockerfile` otimizado para cada módulo
- Configurar builds multi-estágio para imagens menores
- Definir configurações adequadas do runtime Java
- Compilar e testar as imagens Docker localmente

## ✅ Verificação

- [ ] Prompt de conteinerização executado no Copilot CLI
- [ ] Dockerfiles gerados para os módulos web e worker
- [ ] Imagens Docker compiladas com sucesso

## 🎉 Parabéns!

Você concluiu o workshop de Modernização de Aplicações usando o Copilot CLI! Aqui está o que você realizou:

- ✅ **Configurou** o Copilot CLI com o servidor MCP de modernização
- ✅ **Atualizou** do Java 8 → 21 e Spring Boot 2.x → 3.x
- Revisar as descobertas e registrar o que foi migrado, adiado ou deixado fora do escopo
- ✅ **Conteinerizou** a aplicação para implantação na nuvem

### Próximos Passos

- Implante sua aplicação conteinerizada no **Azure Container Apps** — experimente o prompt: `Deploy this application to Azure`
- Explore mais recursos do [GitHub Copilot app modernization via CLI](https://learn.microsoft.com/en-us/azure/developer/java/migration/github-copilot-app-modernization-for-java-copilot-cli)
- Confira o [Guia de Prompts do Copilot](../PROMPTS.md) para prompts adicionais usados durante o desenvolvimento
- Visite os outros [workshops do Copilot Dev Days](https://github.com/copilot-dev-days)
