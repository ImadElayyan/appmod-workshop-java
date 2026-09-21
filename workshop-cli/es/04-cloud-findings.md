# Paso 4: Resolver hallazgos de migración a la nube

## Objetivo y alcance

Decide qué hallazgos resolver y crea un plan de migración acotado. Esta actividad es distinta de la actualización a Java 21 / Spring Boot 3.x del Paso 3.

Para un taller local, puedes revisar los hallazgos y documentarlos como **fuera del alcance**. No los declares resueltos sin implementar y validar los cambios.

## Seleccionar hallazgos y crear un plan

1. Guarda un commit funcional después de la actualización de Java.
2. En el informe de evaluación, selecciona solo los hallazgos relacionados que quieras abordar y pulsa **Create Plan**, si tu interfaz lo ofrece. Empieza por una migración, por ejemplo S3 a Blob Storage, no por todos los hallazgos.
3. Revisa cambios de código, configuración, dependencias, identidad, transferencia de datos y pruebas. Excluye migraciones no relacionadas y aprovisionamiento.
4. Aprueba los cambios de código después de revisar el plan. Revisa los permisos antes de autorizar comandos.
5. Revisa el diff, compila y prueba ambos módulos y valida el comportamiento afectado. Guarda un commit antes de otra migración.
6. Repite la evaluación si está disponible. Registra hallazgos residuales y pruebas pendientes; un informe limpio no demuestra por sí solo que la aplicación funcione.

**¿No aparece Create Plan?** Usa Copilot Chat en modo Agent con la extensión de modernización y el prompt siguiente. No se necesita Run Task en cada problema.

**Ruta CLI:** usa el mismo prompt en tu sesión configurada de modernización de Copilot CLI. Los botones del informe describen la ruta IDE, no comandos de terminal.

## Cómo resolver cada hallazgo

| Hallazgo | Resolución | Validación |
|----------|------------|------------|
| AWS S3 a Azure Blob Storage | Sustituye el cliente/SDK, dependencias y configuración en web y worker. Planifica contenedores y autenticación. Transferir objetos existentes es otra actividad. | Carga, descarga, miniaturas y acceso a datos transferidos. |
| Configuración de región AWS | Elimínala solo después de sustituir la integración AWS y comprobar que no quedan referencias. No pongas un nombre de región Azure en su lugar. | Ningún cliente AWS activo depende de ella. |
| RabbitMQ a Azure Service Bus | Sustituye código y configuración; define colas, enrutamiento y semántica de entrega. | Envío, recepción, reintentos, errores y duplicados. |
| PostgreSQL a Azure Database for PostgreSQL | Configura endpoint, TLS, red y autenticación. Migrar esquema y datos es distinto de modificar código. | Conectividad, consultas y datos necesarios. |
| Credenciales / identidad administrada | Configura autenticación, identidad del servicio en Azure y permisos específicos. Usa una identidad de desarrollador documentada en local. | Ambos módulos acceden sin secretos incrustados; modificar código no asigna roles. |

## Prompt: planificar solo la migración de almacenamiento

```text
Crea un plan para migrar la integración AWS S3 a Azure Blob Storage
en los módulos web y worker.
Conserva carga, descarga y procesamiento de miniaturas.
Identifica dependencias, configuración y autenticación.
Identifica los datos existentes que necesitan una transferencia separada.
Elimina configuraciones AWS solo cuando ya no sean necesarias.
Mantén Java 21 y Spring Boot 3.x.
No cambies RabbitMQ ni PostgreSQL en esta tarea.
No aprovisiones recursos ni despliegues todavía.
Muéstrame el plan antes de hacer cambios.
```

Tras revisar el plan, autoriza explícitamente los cambios elegidos. Para otros hallazgos, crea planes separados y acotados.

## Azure, costes y validación

Puedes preparar planes y código **sin una suscripción Azure**. Las pruebas contra servicios Azure reales requieren acceso a recursos aprovisionados en una suscripción, permisos y conectividad. Pueden generar costes: solicita aprobación antes de crearlos y elimina los recursos temporales al terminar.

Con Maven usando JDK 21, ejecuta `mvn -version` y `mvn clean verify` desde la raíz, y prueba las integraciones modificadas. Compilar no demuestra que la autenticación, mensajería o almacenamiento Azure funcionen. Pruebas unitarias o emuladores no sustituyen la validación de autorización real.

## Verificación

- [ ] Hallazgos seleccionados o documentados como fuera del alcance local.
- [ ] Plan revisado antes de cambios o aprovisionamiento.
- [ ] Si se cambió código, ambos módulos compilan y las pruebas relevantes pasan.
- [ ] Si se declara una migración completa, su comportamiento se validó con los servicios previstos.
- [ ] Transferencias de datos, permisos y pruebas pendientes registrados.

Referencia: [tareas predefinidas de Microsoft](https://learn.microsoft.com/en-us/azure/developer/java/migration/migrate-github-copilot-app-modernization-for-java-predefined-tasks).
