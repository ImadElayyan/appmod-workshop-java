<!-- l10n-sync: source-file="05-containerize.md" -->
# Paso 5: Containerizar Aplicaciones

## 🎯 Objetivo

Preparar tu aplicación modernizada para el despliegue en la nube containerizando tanto el módulo web como el worker utilizando las tareas de containerización de GitHub Copilot app modernization.

## Ejecutar la Tarea de Containerización

1. En la barra lateral de Actividad, abre el panel de la extensión **GitHub Copilot app modernization**. En la sección **TASKS**, expande **Common Tasks** > **Containerize Tasks** y haz clic en el botón de ejecución de **Containerize Application**.

    ![Run Containerize Application task](../doc-media/containerization-run-task.png)

1. Se cargará un prompt predefinido en el panel de Copilot Chat con Agent Mode. Copilot Agent comenzará a analizar el workspace y a crear un archivo **containerization-plan.copilotmd** con el plan de containerización.

    ![Containerization prompt and plan](../doc-media/containerization-plan.png)

1. Revisa el plan y colabora con Copilot Agent mientras sigue los **Execution Steps** del plan haciendo clic en **Continue**/**Allow** en las notificaciones emergentes del chat para ejecutar comandos. Algunos de los pasos de ejecución aprovechan las herramientas agénticas de **Container Assist**.

1. Copilot Agent ayudará a generar Dockerfile, construir imágenes Docker y corregir errores de compilación si los hay. Haz clic en **Keep** para aplicar el código generado.

## Lo Que Hace Esto

El proceso de containerización:
- Analizará la estructura del proyecto (módulo web + módulo worker)
- Generará `Dockerfile` optimizados para cada módulo
- Configurará compilaciones multi-stage para tamaños de imagen más pequeños
- Establecerá configuraciones apropiadas del runtime de Java
- Construirá y probará las imágenes Docker localmente

## ✅ Punto de Verificación

- [ ] Tarea de containerización iniciada desde la vista de Tasks
- [ ] Plan de containerización generado (`containerization-plan.copiotmd`)
- [ ] Dockerfiles generados para los módulos web y worker
- [ ] Imágenes Docker construidas exitosamente

## 🎉 ¡Felicitaciones!

¡Has completado el taller de Modernización de Aplicaciones! Esto es lo que lograste:

- ✅ **Evaluaste** la aplicación Java heredada para comprender las necesidades de modernización
- ✅ **Actualizaste** de Java 8 → 21 y Spring Boot 2.x → 3.x
- Revisar los hallazgos y registrar qué se migró, se pospuso o quedó fuera del alcance
- ✅ **Containerizaste** la aplicación para el despliegue en la nube

### ¿Qué Sigue?

- Despliega tu aplicación containerizada en **Azure Container Apps**
- Explora más características de [GitHub Copilot app modernization](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure)
- Consulta la [Guía de Prompts de Copilot](../PROMPTS.md) para prompts adicionales usados durante el desarrollo
- Visita los otros [talleres de Copilot Dev Days](https://github.com/copilot-dev-days)
