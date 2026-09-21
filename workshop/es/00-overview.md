<!-- l10n-sync: source-file="00-overview.md" -->
# Taller de Modernización de Aplicaciones

## Descripción General

Este taller te guiará a través del proceso de modernización de una aplicación Java utilizando **GitHub Copilot app modernization**. Transformarás el proyecto `asset-manager` de tecnologías heredadas a una solución moderna lista para la nube.

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
| Evaluar Tu Aplicación Java | ~5 min |
| Actualizar Runtime y Frameworks | ~10 min |
| Hallazgos de migración | Variable |
| Containerizar Aplicaciones | ~5 min |

## Pasos del Taller

| Paso | Título | Descripción |
|------|--------|-------------|
| 01 | [Prerrequisitos y Configuración](01-prerequisites.md) | Instalar herramientas y clonar el repositorio |
| 02 | [Evaluar Tu Aplicación](02-assess.md) | Ejecutar la evaluación para analizar tu aplicación |
| 03 | [Actualizar Runtime y Frameworks](03-upgrade.md) | Actualizar las versiones de Java y Spring Boot |
| 04 | [Hallazgos de migración](04-cloud-findings.md) | Planificar migraciones de almacenamiento, mensajería, bases de datos e identidad |
| 05 | [Containerizar Aplicaciones](05-containerize.md) | Preparar tu aplicación para el despliegue en la nube |

## Lo Que Aprenderás

- Cómo usar **GitHub Copilot app modernization** para evaluar aplicaciones Java heredadas
- Cómo actualizar versiones de Java y frameworks de Spring Boot con asistencia de IA
- Planificar migraciones de almacenamiento, mensajería, bases de datos e identidad
- Cómo containerizar aplicaciones Java para el despliegue en la nube
