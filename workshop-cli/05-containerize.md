# Step 5: Containerize Applications

## 🎯 Goal

Prepare your modernized application for cloud deployment by containerizing both the web and worker modules using a natural language prompt in Copilot CLI.

## Run the Containerization Task

1. Inside the running Copilot CLI session, enter the following prompt:

   ```
   Containerize this application. Generate optimized Dockerfiles for each module with multi-stage builds, build the Docker images, and fix any build errors.
   ```

2. Copilot will analyze the workspace and generate a containerization plan. Allow Copilot to proceed through each step, including running commands to build Docker images.

3. When the task completes, review the generated `Dockerfile` files for both the `web` and `worker` modules.

## What This Does

The containerization process will:
- Analyze the project structure (web module + worker module)
- Generate optimized `Dockerfile` for each module
- Configure multi-stage builds for smaller image sizes
- Set up proper Java runtime configurations
- Build and test the Docker images locally

## ✅ Checkpoint

- [ ] Containerization prompt executed in Copilot CLI
- [ ] Dockerfiles generated for both web and worker modules
- [ ] Docker images built successfully

## 🎉 Congratulations!

You've completed the App Modernization workshop using the Copilot CLI! Here's what you accomplished:

- ✅ **Set up** Copilot CLI with the modernization MCP server
- ✅ **Upgraded** from Java 8 → 21 and Spring Boot 2.x → 3.x
- Review cloud findings and record what was migrated, deferred or left out of scope
- ✅ **Containerized** the application for cloud deployment

### What's Next?

- Deploy your containerized app to **Azure Container Apps** — try the prompt: `Deploy this application to Azure`
- Explore more [GitHub Copilot app modernization via CLI](https://learn.microsoft.com/en-us/azure/developer/java/migration/github-copilot-app-modernization-for-java-copilot-cli) features
- Check out the [Copilot Prompts Guide](../PROMPTS.md) for additional prompts used during development
- Visit the other [Copilot Dev Days workshops](https://github.com/copilot-dev-days)
