<!-- l10n-sync: source-file="05-containerize.md" -->
# Paso 5: Containerizar Aplicaciones

## 🎯 Objetivo

Preparar tu aplicación modernizada para el despliegue en la nube containerizando tanto el módulo web como el worker usando un prompt en lenguaje natural en Copilot CLI.

## Ejecutar la Tarea de Containerización

1. Dentro de la sesión de Copilot CLI en ejecución, ingresa el siguiente prompt:

   ```
   Containerize this application. Generate optimized Dockerfiles for each module with multi-stage builds, build the Docker images, and fix any build errors.
   ```

2. Copilot analizará el workspace y generará un plan de containerización. Permite que Copilot proceda a través de cada paso, incluyendo la ejecución de comandos para construir las imágenes Docker.

3. Cuando la tarea se complete, revisa los archivos `Dockerfile` generados para los módulos `web` y `worker`.

## Lo Que Hace Esto

El proceso de containerización:
- Analizará la estructura del proyecto (módulo web + módulo worker)
- Generará `Dockerfile` optimizados para cada módulo
- Configurará compilaciones multi-stage para tamaños de imagen más pequeños
- Establecerá configuraciones apropiadas del runtime de Java
- Construirá y probará las imágenes Docker localmente

## ✅ Punto de Verificación

- [ ] Prompt de containerización ejecutado en Copilot CLI
- [ ] Dockerfiles generados para los módulos web y worker
- [ ] Imágenes Docker construidas exitosamente

## 🎉 ¡Felicitaciones!

¡Has completado el taller de Modernización de Aplicaciones usando Copilot CLI! Esto es lo que lograste:

- ✅ **Configuraste** Copilot CLI con el MCP server de modernización
- ✅ **Actualizaste** de Java 8 → 21 y Spring Boot 2.x → 3.x
- Revisar los hallazgos y registrar qué se migró, se pospuso o quedó fuera del alcance
- ✅ **Containerizaste** la aplicación para el despliegue en la nube

### ¿Qué Sigue?

- Despliega tu aplicación containerizada en **Azure Container Apps** — prueba el prompt: `Deploy this application to Azure`
- Explora más características de [GitHub Copilot app modernization via CLI](https://learn.microsoft.com/en-us/azure/developer/java/migration/github-copilot-app-modernization-for-java-copilot-cli)
- Consulta la [Guía de Prompts de Copilot](../PROMPTS.md) para prompts adicionales usados durante el desarrollo
- Visita los otros [talleres de Copilot Dev Days](https://github.com/copilot-dev-days)
