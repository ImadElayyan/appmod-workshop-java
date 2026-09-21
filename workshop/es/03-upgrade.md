<!-- l10n-sync: source-file="03-upgrade.md" -->
# Paso 3: Actualizar Runtime y Frameworks

## 🎯 Objetivo

Actualizar la aplicación de Java 8 a Java 21 y de Spring Boot 2.x a 3.x utilizando las tareas de actualización automatizadas de GitHub Copilot app modernization.

## Iniciar la actualización desde QuickStart

> [!NOTE]
> La interfaz actual utiliza QuickStart. Las instrucciones antiguas muestran **Run Task** junto a los problemas de la evaluación; ese botón no es necesario y puede no aparecer en tu versión.

1. Abre en VS Code la raíz del repositorio que contiene el `pom.xml` principal.
2. Abre el panel **GitHub Copilot modernization** (o **GitHub Copilot app modernization**, según la versión).
3. En **QuickStart**, selecciona **Upgrade Java Runtime & Frameworks** para abrir Copilot Chat en modo Agent.
4. Selecciona **Java 21** y **Spring Boot 3.x**; puedes solicitar explícitamente **Spring Boot 3.5.x**. No aceptes Java 25 ni Spring Boot 4 para este taller.
5. Revisa el `plan.md` generado: versiones, rama de trabajo, módulos `web` y `worker`, y pasos de compilación y pruebas.
6. Confirma el plan para ejecutar la actualización. Revisa las solicitudes de permisos antes de aprobarlas.

**IntelliJ IDEA:** en el panel de modernización, selecciona **Upgrade Runtime & Frameworks** y revisa los mismos objetivos.

## Alternativa: Copilot Chat

Con la extensión de modernización habilitada, usa este prompt en modo **Agent**:

```text
Actualiza esta aplicación a Java 21 y Spring Boot 3.5.x.
Incluye los módulos web y worker.
Conserva las integraciones de almacenamiento y mensajería existentes.
No migres a Azure ni aprovisiones recursos en la nube.
Muéstrame el plan de actualización antes de realizar cambios.
```

> [!IMPORTANT]
> No selecciones todos los problemas de la evaluación con **Create Plan** para este ejercicio: eso puede incluir migraciones a la nube. Las configuraciones de región AWS, S3, autenticación y mensajería quedan fuera de este paso, salvo que bloqueen directamente la actualización acordada.

Si no ves QuickStart, vuelve a abrir el panel y comprueba la instalación de la extensión y el inicio de sesión. No busques **Run Task** en cada problema.

Referencia: [guía actual de Microsoft](https://learn.microsoft.com/en-us/azure/developer/github-copilot-app-modernization/quickstart-upgrade#launch-the-upgrade).

## Lo Que Hace la Actualización

La actualización automatizada:
- Actualizará la versión de Java en `pom.xml` de 8 a 21
- Actualizará las dependencias de Spring Boot de 2.x a 3.x
- Actualizará APIs incompatibles (por ejemplo, namespaces de Java EE `javax.*` → `jakarta.*` cuando corresponda; no renombres paquetes de Java SE como `javax.sql`)
- Corregirá llamadas a métodos y patrones obsoletos
- Actualizará las versiones de los plugins de Maven según sea necesario

> [!NOTE]
> Aunque la herramienta admite versiones más recientes, este taller mantiene Java 21 y Spring Boot 3.x.

## Revisar los Cambios

Después de que el agente complete su trabajo:
1. Revisa los cambios en la vista de diferencias
2. Verifica que `pom.xml` refleje las nuevas versiones de Java y Spring Boot
3. Comprueba los cambios necesarios de Java EE sin reemplazar paquetes de Java SE
4. Revisa y acepta los cambios (**Keep**, si tu versión muestra ese botón)
5. Con Maven usando JDK 21, ejecuta `mvn -version` y `mvn clean verify` desde la raíz. Revisa la compilación de ambos módulos y los resultados de las pruebas; resuelve los errores antes de continuar.

## ✅ Punto de Verificación

- [ ] Actualización iniciada desde QuickStart o Copilot Agent
- [ ] Plan revisado antes de ejecutarlo; migraciones a la nube excluidas
- [ ] Agente completó el proceso de actualización
- [ ] Cambios revisados en la vista de diferencias
- [ ] Versión de Java actualizada a 21 en `pom.xml`
- [ ] Spring Boot actualizado a 3.x
- [ ] Compilación y verificación Maven completadas con JDK 21
