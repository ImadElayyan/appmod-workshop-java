# Step 3: Upgrade Runtime & Frameworks

## 🎯 Goal

Upgrade the application from Java 8 to Java 21 and from Spring Boot 2.x to 3.x using GitHub Copilot app modernization's automated upgrade tasks.

## Start the Upgrade from QuickStart

> [!NOTE]
> The current extension uses the QuickStart upgrade entry point. Older instructions and screenshots show a **Run Task** button beside assessment findings; that button is not required and may not appear in your version.

1. Open the repository root containing the parent `pom.xml` in VS Code.
2. In the Activity sidebar, open **GitHub Copilot modernization** (called **GitHub Copilot app modernization** in some versions).
3. In **QuickStart**, select **Upgrade Java Runtime & Frameworks**. This opens Copilot Chat in Agent mode.
4. Select **Java 21** and **Spring Boot 3.x** for this workshop; **Spring Boot 3.5.x** is an explicit target you can request. Do not accept Java 25 or Spring Boot 4 just because they are offered.
5. Review the generated `plan.md`: confirm the targets, the working branch, both `web` and `worker` modules, and build/test steps. Ask the agent to stop for review if needed.
6. Confirm the plan to execute the upgrade. Review tool and command permission requests before approving them.

**IntelliJ IDEA:** open the modernization panel and select **Upgrade Runtime & Frameworks**, then review the same targets and plan.

## Alternative: Start from Copilot Chat

With the modernization extension enabled, open Copilot Chat in **Agent** mode and enter:

```text
Upgrade this application to Java 21 and Spring Boot 3.5.x.
Include both the web and worker modules.
Keep the existing storage and messaging integrations.
Do not migrate to Azure or provision cloud resources.
Show me the upgrade plan before making changes.
```

> [!IMPORTANT]
> Do not select all assessment findings and use **Create Plan** for this exercise. That can include broader cloud migration work. AWS region, S3, authentication and messaging findings are not all Java upgrade tasks; leave them outside this step unless they directly block the agreed upgrade.

If QuickStart is not visible, reopen the modernization panel and check the extension installation and GitHub sign-in. Do not look for a **Run Task** button on every issue.

Reference: [Microsoft's current Java upgrade quickstart](https://learn.microsoft.com/en-us/azure/developer/github-copilot-app-modernization/quickstart-upgrade#launch-the-upgrade).

## What the Upgrade Does

The automated upgrade will:
- Update the Java version in `pom.xml` from 8 to 21
- Upgrade Spring Boot dependencies from 2.x to 3.x
- Update incompatible APIs (e.g., Java EE `javax.*` → `jakarta.*` changes where required; do not rename Java SE packages such as `javax.sql`)
- Fix deprecated method calls and patterns
- Update Maven plugin versions as needed

> [!NOTE]
> The tool supports newer targets too, but this workshop stays on Java 21 and Spring Boot 3.x so its instructions and checkpoints remain consistent.

## Review the Changes

After the agent completes its work:
1. Review the changes in the diff view
2. Verify that `pom.xml` reflects the new Java and Spring Boot versions
3. Check the required Java EE namespace changes without replacing unrelated Java SE packages
4. Review and accept the edits (**Keep**, if your installed version shows it)
5. With Maven using JDK 21, run `mvn -version` and `mvn clean verify` from the repository root. Confirm both modules build and review the test results. Stop and resolve any reported failures.

## ✅ Checkpoint

- [ ] Upgrade launched from QuickStart or Copilot Agent chat
- [ ] Plan reviewed before execution; unrelated cloud migration excluded
- [ ] Agent completed the upgrade process
- [ ] Changes reviewed in diff view
- [ ] Java version updated to 21 in `pom.xml`
- [ ] Spring Boot upgraded to 3.x
- [ ] Root Maven build/verification succeeds with JDK 21
