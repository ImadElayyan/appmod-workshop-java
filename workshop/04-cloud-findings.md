# Step 4: Resolve Cloud Migration Findings

## Goal and scope

Decide which cloud-readiness findings to resolve and create a focused migration plan. This is separate from Step 3's Java 21 / Spring Boot 3.x upgrade.

For a local-only workshop, it is valid to review the findings and document them as **out of scope**. Do not report them as resolved without implementing and validating the relevant changes.

## Select findings and create a plan

1. Save a working commit after the Java upgrade.
2. Open the assessment report. Select only the related findings you want to address, then select **Create Plan** if available in your installed interface. Start with one migration, such as AWS S3 to Azure Blob Storage, not all findings at once.
3. Review the plan's code, configuration, dependency, identity, data-transfer and test requirements. Exclude unrelated migrations and resource provisioning.
4. Approve code changes only after reviewing the plan. Review tool permissions before allowing commands.
5. Inspect the diff, build and test both modules, and validate the affected behavior. Commit a working checkpoint before starting another migration.
6. Rerun the assessment if supported. Record residual findings and integration tests still pending; a clean report alone is not proof that the application works.

**No Create Plan button?** Use Copilot Chat in Agent mode with the modernization extension enabled and the scoped prompt below. Labels vary by version; no per-issue Run Task button is required.

**CLI track:** enter the same scoped prompt in your configured Copilot CLI modernization session. The assessment report buttons above describe the IDE path, not terminal commands.

## What each finding requires

| Finding | Resolution | Validate |
|---------|------------|----------|
| AWS S3 to Azure Blob Storage | Replace S3 SDK/client code, dependencies and configuration in both web and worker modules. Plan bucket/container mapping and authentication. Existing object transfer is a separate step. | Upload, download and thumbnail processing; access to existing data if it must be migrated. |
| AWS region configuration | Remove the setting only after the AWS integration that uses it is replaced and no references remain. Do not substitute an Azure region name. | No active AWS client depends on the removed setting. |
| RabbitMQ to Azure Service Bus | Replace messaging code and configuration; map queues, routing and delivery behavior deliberately. | Sending, receiving, retries, failure handling and duplicate-message behavior. |
| PostgreSQL to Azure Database for PostgreSQL | Configure endpoint, TLS, networking and authentication for the target server. Schema/data transfer is separate from code changes. | Connectivity, queries and required data in the target database. |
| Credentials / managed identity | Use appropriate identity-based authentication; configure the Azure workload identity and service-specific permissions. Use a documented developer identity for local development. | Both modules can perform permitted operations without embedded secrets. Managed identity code alone does not configure roles or identities. |

## Prompt: plan storage migration only

```text
Create a plan to migrate this application's AWS S3 integration
to Azure Blob Storage across both web and worker modules.

Preserve upload, download and thumbnail-processing behavior.
Identify dependencies, configuration and authentication changes.
Identify any existing data that needs a separate transfer.
Remove AWS-specific settings only when no longer needed.

Keep Java 21 and Spring Boot 3.x.
Do not change RabbitMQ or PostgreSQL in this task.
Do not provision resources or deploy anything yet.
Show me the plan before making changes.
```

After reviewing the plan, explicitly authorize the chosen code changes. For other findings, create a similarly bounded plan rather than assuming the storage prompt resolves everything.

## Azure access, costs and validation

You can prepare plans and code changes **without an Azure subscription**. To validate against real Azure services you need access to provisioned services in a subscription, appropriate permissions and connectivity. Resources may incur charges; obtain approval before creating them and clean up temporary resources afterward.

From the repository root, with Maven using JDK 21, run `mvn -version` and `mvn clean verify`. Then exercise the changed integrations. Passing a build is not evidence that Azure authentication, messaging or storage works. Unit tests and local emulators can help where supported, but do not prove production Azure authorization.

## Checkpoint

- [ ] Findings selected deliberately, or documented as out of scope for local-only work.
- [ ] Plan reviewed before code changes or any provisioning.
- [ ] If code was changed, both modules build and relevant tests pass.
- [ ] If claiming a migration is complete, affected behavior is validated against the intended services.
- [ ] Pending data transfer, Azure permissions and untested integrations are recorded explicitly.

Reference: [Microsoft's predefined Java modernization tasks](https://learn.microsoft.com/en-us/azure/developer/java/migration/migrate-github-copilot-app-modernization-for-java-predefined-tasks).
