<!-- l10n-sync: source-file="00-overview.md" -->
# Taller de Modernización de Aplicaciones (Copilot CLI)

## Descripción General

Este taller te guiará a través del proceso de modernización de una aplicación Java utilizando **GitHub Copilot app modernization a través de Copilot CLI**. Transformarás el proyecto `asset-manager` de tecnologías heredadas a una solución moderna lista para la nube — completamente desde tu terminal, sin necesidad de un IDE.

**Lo que hará el proceso de modernización:**

La modernización transformará tu aplicación de tecnologías obsoletas a una solución moderna. Esto incluye:
- Actualizar de **Java 8 a Java 21**
- Migrar de **Spring Boot 2.x a 3.x**
- Revisar los hallazgos y registrar qué se migró, se pospuso o quedó fuera del alcance
- **Containerizar** las aplicaciones

## Estimaciones de Tiempo

La duración depende de los hallazgos seleccionados. El tiempo anterior de endpoints de salud ya no aplica. La revisión del plan, los cambios de código y las pruebas con Azure son actividades distintas; no se promete una duración total fija.

| Paso | Duración |
|------|----------|
| Prerrequisitos y Configuración | ~5 min |
| Iniciar Copilot CLI y Agregar MCP Server | ~5 min |
| Actualizar Runtime y Frameworks | ~10 min |
| Hallazgos de migración | Variable |
| Containerizar Aplicaciones | ~5 min |

## Pasos del Taller

| Paso | Título | Descripción |
|------|--------|-------------|
| 01 | [Prerrequisitos y Configuración](01-prerequisites.md) | Instalar herramientas y clonar el repositorio |
| 02 | [Iniciar Copilot CLI](02-assess.md) | Iniciar Copilot CLI y agregar el MCP server de modernización |
| 03 | [Actualizar Runtime y Frameworks](03-upgrade.md) | Actualizar las versiones de Java y Spring Boot |
| 04 | [Hallazgos de migración](04-cloud-findings.md) | Planificar migraciones de almacenamiento, mensajería, bases de datos e identidad |
| 05 | [Containerizar Aplicaciones](05-containerize.md) | Preparar tu aplicación para el despliegue en la nube |

## Lo Que Aprenderás

- Cómo usar **GitHub Copilot CLI** para modernizar aplicaciones Java heredadas desde la terminal
- Cómo configurar el **GitHub Copilot modernization MCP server**
- Cómo actualizar versiones de Java y frameworks de Spring Boot con asistencia de IA usando prompts en lenguaje natural
- Cómo containerizar aplicaciones Java para el despliegue en la nube
