# App Modernization Workshop (Copilot CLI)

## Overview

This workshop will walk you through the process of modernizing a Java application using **GitHub Copilot app modernization via the Copilot CLI**. You'll transform the `asset-manager` project from legacy technologies to a modern, cloud-ready solution — entirely from your terminal, with no IDE required.

**What the Modernization Process Will Do:**

The modernization will transform your application from outdated technologies to a modern solution. This includes:
- Upgrading from **Java 8 to Java 21**
- Migrating from **Spring Boot 2.x to 3.x**
- Review cloud findings and record what was migrated, deferred or left out of scope
- **Containerizing** the applications

## Time Estimates

Duration varies with the selected findings. The former health-endpoint timing no longer applies. Plan review, code changes and Azure integration testing are separate activities; no fixed total is promised for this revised workshop.

| Step | Duration |
|------|----------|
| Prerequisites & Setup | ~5 min |
| Start Copilot CLI & Add MCP Server | ~5 min |
| Upgrade Runtime & Frameworks | ~10 min |
| Cloud Migration Findings | Variable |
| Containerize Applications | ~5 min |

## Workshop Steps

| Step | Title | Description |
|------|-------|-------------|
| 01 | [Prerequisites & Setup](01-prerequisites.md) | Install tools and clone the repository |
| 02 | [Start Copilot CLI](02-assess.md) | Launch Copilot CLI and add the modernization MCP server |
| 03 | [Upgrade Runtime & Frameworks](03-upgrade.md) | Upgrade Java and Spring Boot versions |
| 04 | [Cloud Migration Findings](04-cloud-findings.md) | Plan focused migrations for storage, messaging, databases and identity |
| 05 | [Containerize Applications](05-containerize.md) | Prepare your app for cloud deployment |

## What You'll Learn

- How to use **GitHub Copilot CLI** to modernize legacy Java applications from the terminal
- How to configure the **GitHub Copilot modernization MCP server**
- How to upgrade Java versions and Spring Boot frameworks with AI assistance using natural language prompts
- How to containerize Java applications for cloud deployment
