# App Modernization Workshop

The following sections guide you through the process of modernizing the sample Java application `asset-manager` to Azure using GitHub Copilot app modernization.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Install GitHub Copilot app modernization](#install-github-copilot-app-modernization)
- [Assess Your Java Application](#assess-your-java-application)
- [Upgrade Runtime & Frameworks](#upgrade-runtime--frameworks)
- [Expose health endpoints using Custom Skills](#expose-health-endpoints-using-custom-skills)
- [Containerize Applications](#containerize-applications)

## Prerequisites

- A GitHub account with [GitHub Copilot](https://github.com/features/copilot) enabled. A Pro, Pro+, Business, or Enterprise plan is required.
- One of the following IDEs:
  - The latest version of [Visual Studio Code](https://code.visualstudio.com/). Must be version 1.101 or later.
    - [GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/overview). For setup instructions, see [Set up GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/setup). Be sure to sign in to your GitHub account within Visual Studio Code.
    - [GitHub Copilot app modernization](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure). Restart Visual Studio Code after installation.
  - The latest version of [IntelliJ IDEA](https://www.jetbrains.com/idea/download). Must be version 2023.3 or later.
    - [GitHub Copilot](https://plugins.jetbrains.com/plugin/17718-github-copilot). Must be version 1.5.59 or later. For more instructions, see [Set up GitHub Copilot in IntelliJ IDEA](https://docs.github.com/en/copilot/get-started/quickstart). Be sure to sign in to your GitHub account within IntelliJ IDEA.
    - [GitHub Copilot app modernization](https://plugins.jetbrains.com/plugin/28791-github-copilot-app-modernization). Restart IntelliJ IDEA after installation. If you don't have GitHub Copilot installed, you can install GitHub Copilot app modernization directly.
    - For more efficient use of Copilot in app modernization: in the IntelliJ IDEA settings, select the **Tools** > **GitHub Copilot** configuration window, and then select **Auto-approve** and **Trust MCP Tool Annotations**. For more information, see [Configure settings for GitHub Copilot app modernization to optimize the experience for IntelliJ](configure-settings-intellij.md).
- [Java JDK](/java/openjdk/download) for both the source and target JDK versions.
- [Maven](https://maven.apache.org/download.cgi) or [Gradle](https://gradle.org/install/) to build Java projects.
- A Git-managed Java project using Maven or Gradle.
- For Maven-based projects: access to the public Maven Central repository.
- In the Visual Studio Code settings, make sure `chat.extensionTools.enabled` is set to `true`. This setting might be controlled by your organization.

> Note: If you're using Gradle, only the Gradle wrapper version 5+ is supported. The Kotlin Domain Specific Language (DSL) isn't supported.
>
> The function `My Tasks` isn't supported yet for IntelliJ IDEA.

## Clone the Repository

```bash
git clone https://github.com/copilot-dev-days/appmod-workshop-java.git
cd appmod-workshop-java
```

## Install GitHub Copilot app modernization

In VSCode, open the Extensions view from the Activity Bar, search for the `GitHub Copilot app modernization` extension in the marketplace. Click the Install button for the extension. After installation completes, you should see a notification in the bottom-right corner of VSCode confirming success.

**Alternative: IntelliJ IDEA**
Alternatively, you can use IntelliJ IDEA. Open **File** > **Settings** (or **IntelliJ IDEA** > **Preferences** on macOS), navigate to **Plugins** > **Marketplace**, search for `GitHub Copilot app modernization`, and click **Install**. Restart IntelliJ IDEA if prompted.

## Assess Your Java Application

The first step is to assess the sample Java application `asset-manager`. The assessment provides insights into the application's readiness for migration to Azure.

1. Open VS Code with all the prerequisites installed for the asset manager by changing the directory to the `asset-manager` directory and running `code .` in that directory.
1. In the Activity sidebar, open the **GitHub Copilot app modernization** extension pane.
1. In the **QUICKSTART** section, click **Start Assessment** to trigger the app assessment.

   ![Trigger Assessment](doc-media/trigger-assessment.png)

1. Wait for the assessment to be completed. This step could take several minutes.
1. Upon completion, an **Assessment Report** tab opens. This report provides a categorized view of cloud readiness issues and recommended solutions. Select the **Issues** tab to view proposed solutions and proceed with migration steps.

## Upgrade Runtime & Frameworks

1. In the modernization panel's **QuickStart**, select **Upgrade Java Runtime & Frameworks** in VS Code, or **Upgrade Runtime & Frameworks** in IntelliJ IDEA.
2. Select **Java 21** and **Spring Boot 3.x** (for example, 3.5.x). Review the generated plan before confirming execution.
3. Keep existing storage and messaging integrations; do not include unrelated cloud findings through **Create Plan**.
4. Review edits and verify both modules with Maven using JDK 21.

The current UI does not require a **Run Task** button on each assessment issue. See [Step 3: Upgrade Runtime & Frameworks](workshop/03-upgrade.md) for the current workflow, Agent-mode prompt alternative, and checkpoints.

## Expose health endpoints using Custom Skills

In this section, you will use custom skills to expose health endpoints for your applications instead of writing code yourself. The following steps demonstrate how to create a custom skill with references and proper prompts.

> Note: Custom skills (My Skills) are not supported for the IntelliJ IDEA plugin. If you are using IntelliJ IDEA, you can skip this section.

1. In the Activity sidebar, open the **GitHub Copilot app modernization** extension pane. Hover over the **TASKS** section, and then select **Create a Custom Skill**.

   ![Create Custom Skill](doc-media/create-formula-from-source-control.png)
1. A **Create a Skill** form opens with the following fields. Fill them in as shown below:
   - **Skill Name**: `expose-health-endpoint`
   - **Skill Description**: `This skill helps add Spring Boot Actuator health endpoints for Azure Container Apps deployment readiness.`
   - **Skill Content**: `You are a Spring Boot developer assistant, follow the Spring Boot Actuator documentation to add basic health endpoints for Azure Container Apps deployment.`

1. Click **Add Resources** to add the Spring Boot Actuator official documentation as a resource. Paste the following link: `https://docs.spring.io/spring-boot/reference/actuator/endpoints.html`.

   ![Create a Skill form](doc-media/health-endpoint-task.png)
1. Click **Save** to create the skill. Your custom skill now appears in the **TASKS** > **My Skills** section.
1. Click **Run** to execute it.
1. The Copilot chat window opens in Agent Mode and automatically generates the migration plan, checks out a new branch, performs code changes, and runs the validation and fix iteration loop. Click **Allow** for any tool call requests from the agent.
1. Review the proposed code changes and click **Keep** to apply them.

## Containerize Applications

Now that you have completed the upgrade and health endpoint steps, the next step is to prepare your application for cloud deployment by containerizing both the web and worker modules. In this section, you will use **Containerization Tasks** to containerize your applications.

1. In the Activity sidebar, open the **GitHub Copilot app modernization** extension pane. In the **TASKS** section, expand **Common Tasks** > **Containerize Tasks** and click the run button for **Containerize Application**.
  
    ![Run Containerize Application task](doc-media/containerization-run-task.png)

1. A predefined prompt will be populated in the Copilot Chat panel with Agent Mode. Copilot Agent will start to analyze the workspace and to create a **containerization-plan.copiotmd** with the containerization plan.

    ![Containerization prompt and plan](doc-media/containerization-plan.png)
1. View the plan and collaborate with Copilot Agent as it follows the **Execution Steps** in the plan by clicking **Continue**/**Allow** in pop-up chat notifications to run commands. Some of the execution steps leverage agentic tools of **Container Assist**.

    <!-- ![Containerization execution steps](doc-media/containerization-execution-steps.png) -->
1. Copilot Agent will help generate Dockerfile, build Docker images and fix build errors if there are any. Click **Keep** to apply the generated code.
