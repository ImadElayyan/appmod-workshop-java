<!-- l10n-sync: source-file="03-upgrade.md" -->
# Etapa 3: Atualizar Runtime e Frameworks

## 🎯 Objetivo

Atualizar a aplicação do Java 8 para o Java 21 e do Spring Boot 2.x para o 3.x usando as tarefas automatizadas de atualização do GitHub Copilot app modernization.

## Iniciar a atualização pelo QuickStart

> [!NOTE]
> A interface atual usa o QuickStart. As instruções antigas mostram **Run Task** ao lado dos problemas da avaliação; esse botão não é necessário e pode não aparecer na sua versão.

1. Abra no VS Code a raiz do repositório que contém o `pom.xml` principal.
2. Abra o painel **GitHub Copilot modernization** (ou **GitHub Copilot app modernization**, dependendo da versão).
3. No **QuickStart**, selecione **Upgrade Java Runtime & Frameworks** para abrir o Copilot Chat no modo Agent.
4. Selecione **Java 21** e **Spring Boot 3.x**; você pode solicitar explicitamente **Spring Boot 3.5.x**. Não aceite Java 25 ou Spring Boot 4 para este workshop.
5. Revise o `plan.md` gerado: versões, branch de trabalho, módulos `web` e `worker`, e etapas de build e testes.
6. Confirme o plano para executar a atualização. Revise as solicitações de permissão antes de aprová-las.

**IntelliJ IDEA:** no painel de modernização, selecione **Upgrade Runtime & Frameworks** e revise os mesmos objetivos.

## Alternativa: Copilot Chat

Com a extensão de modernização habilitada, use este prompt no modo **Agent**:

```text
Atualize esta aplicação para Java 21 e Spring Boot 3.5.x.
Inclua os módulos web e worker.
Mantenha as integrações de armazenamento e mensageria existentes.
Não migre para o Azure nem provisione recursos na nuvem.
Mostre o plano de atualização antes de fazer alterações.
```

> [!IMPORTANT]
> Não selecione todos os problemas da avaliação com **Create Plan** neste exercício: isso pode incluir migrações para a nuvem. Configurações de região AWS, S3, autenticação e mensageria ficam fora desta etapa, salvo se bloquearem diretamente a atualização acordada.

Se o QuickStart não aparecer, reabra o painel e verifique a instalação da extensão e o login. Não procure **Run Task** em cada problema.

Referência: [guia atual da Microsoft](https://learn.microsoft.com/en-us/azure/developer/github-copilot-app-modernization/quickstart-upgrade#launch-the-upgrade).

## O que a Atualização Faz

A atualização automatizada irá:
- Atualizar a versão do Java no `pom.xml` de 8 para 21
- Atualizar as dependências do Spring Boot de 2.x para 3.x
- Atualizar APIs incompatíveis (ex.: namespaces de Java EE `javax.*` → `jakarta.*` quando necessário; não renomeie pacotes Java SE como `javax.sql`)
- Corrigir chamadas de métodos e padrões obsoletos
- Atualizar versões dos plugins do Maven conforme necessário

> [!NOTE]
> A ferramenta aceita versões mais recentes, mas este workshop mantém Java 21 e Spring Boot 3.x.

## Revisar as Alterações

Após o agente concluir seu trabalho:
1. Revise as alterações na visualização de diff
2. Verifique se o `pom.xml` reflete as novas versões do Java e Spring Boot
3. Confirme as alterações necessárias de Java EE sem substituir pacotes Java SE
4. Revise e aceite as alterações (**Keep**, se sua versão mostrar esse botão)
5. Com o Maven usando JDK 21, execute `mvn -version` e `mvn clean verify` na raiz. Confira o build dos dois módulos e os resultados dos testes; resolva os erros antes de continuar.

## ✅ Verificação

- [ ] Atualização iniciada pelo QuickStart ou Copilot Agent
- [ ] Plano revisado antes da execução; migrações para a nuvem excluídas
- [ ] Agente concluiu o processo de atualização
- [ ] Alterações revisadas na visualização de diff
- [ ] Versão do Java atualizada para 21 no `pom.xml`
- [ ] Spring Boot atualizado para 3.x
- [ ] Build e verificação Maven concluídos com JDK 21
