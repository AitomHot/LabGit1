% Introducción a .NET Aspire
% [Tu Nombre/Organización]
% [Fecha]

# Introducción a .NET Aspire

---

# ¿Qué es .NET Aspire?

*   .NET Aspire es un **conjunto de bibliotecas y herramientas** diseñadas para facilitar la creación de **aplicaciones distribuidas, preparadas para la nube**, observables y listas para producción.
*   Se entrega a través de una **colección de paquetes NuGet** que manejan preocupaciones específicas de **cloud-native**.
*   Proporciona una **pila opinada** para la construcción de este tipo de aplicaciones.
*   No es un *framework* completo, sino que usa el concepto de la **filosofía Unix** para unir piezas del ecosistema cloud-native, añadiendo opiniones.

---

# ¿Por qué usar .NET Aspire?

*   Las aplicaciones cloud-native a menudo consisten en **piezas pequeñas e interconectadas o microservicios**, en lugar de una base de código monolítica.
*   Generalmente **consumen un gran número de servicios**, como bases de datos, mensajería y caching.
*   **Simplifica las conexiones y configuraciones** entre estos tipos de servicios.
*   **Mejora la experiencia de desarrollo local** al simplificar la gestión de la configuración y las interconexiones de tu aplicación cloud-native.
*   Es una **evolución del experimento Project Tye**.
*   Es **complementario a tecnologías como Dapr**; Dapr abstrae la plataforma cloud subyacente, mientras que .NET Aspire proporciona configuración opinada sobre tecnologías cloud subyacentes sin abstraerlas.

---

# Conceptos Clave de .NET Aspire

*   **Orquestación:** Un *host* de aplicación ligero, extensible y **multiplataforma** para aplicaciones .NET Aspire. Gestiona la **ejecución y conexión de aplicaciones de múltiples proyectos** y sus dependencias para entornos de desarrollo local.
*   **Componentes:** Paquetes NuGet curados para servicios comunes (como Redis, PostgreSQL) con interfaces estandarizadas que aseguran una conexión consistente. Facilitan la integración de aplicaciones cloud-native con servicios y plataformas prominentes.
*   **Descubrimiento de Servicios (Service Discovery):** Una técnica para localizar servicios dentro de una aplicación distribuida.
*   **Valores Predeterminados del Servicio (Service Defaults):** Un conjunto de configuraciones predeterminadas destinadas a ser compartidas entre los recursos dentro de las aplicaciones .NET Aspire, diseñadas para funcionar bien en la mayoría de los escenarios.
*   **Herramientas (Tooling):** Plantillas de proyecto y experiencias de herramientas para **Visual Studio** y el **dotnet CLI** para ayudar a crear e interactuar con aplicaciones .NET Aspire.

---

# Requisitos Previos

Para trabajar con .NET Aspire, necesitas lo siguiente instalado localmente:

*   **.NET 8.0**.
*   La **carga de trabajo de .NET Aspire** (instalable a través del instalador de Visual Studio o `dotnet workload install aspire`).
*   **Docker Desktop** o **Podman** para el soporte de *runtime* de contenedores. .NET Aspire está diseñado para ejecutarse en contenedores.
*   Un **Entorno de Desarrollo Integrado (IDE)** o editor de código, como **Visual Studio 2022 Preview** (v17.9+) o **Visual Studio Code**.

---

# Experiencia de Desarrollo Local

*   **Creación de Proyectos:** Puedes crear nuevas aplicaciones preconfiguradas con la estructura de proyecto y configuraciones predeterminadas de .NET Aspire utilizando plantillas de proyecto en **Visual Studio** o el **.NET CLI**.
*   **Proyecto AppHost:** Un proyecto de orquestación diseñado para **conectar y configurar** los diferentes proyectos y servicios de tu aplicación. Debe establecerse como el proyecto de inicio.
*   **Uso de Componentes:** Integra fácilmente servicios populares como **Redis**, **PostgreSQL**, **SQL Server**, **Azure Blob Storage**, **Azure Queue Storage**, **MongoDB**, **RabbitMQ**, etc.. La configuración de componentes puede hacerse a través de archivos JSON o código. Los componentes configuran automáticamente **health checks**, **logging**, **métricas**, reintentos y otras capacidades útiles.
*   **Dashboard:** Un dashboard sofisticado para **monitorización e inspección exhaustiva de la aplicación** durante el desarrollo local. Permite seguir varios aspectos de tu aplicación, incluyendo **logs**, **traces** y **configuraciones de entorno** en tiempo real. Se inicia automáticamente al ejecutar el proyecto .AppHost.

---

# Dashboard de .NET Aspire

*   Integrado en el AppHost para desarrollo local.
*   También se distribuye como una **imagen Docker** y puede usarse de forma **independiente** con cualquier aplicación habilitada para OpenTelemetry.
*   Recibe datos de OpenTelemetry (OTLP) en un puerto específico (por defecto 4317).
*   Muestra recursos, logs estructurados, traces y métricas.
*   Por defecto, el dashboard independiente está protegido con autenticación basada en tokens.

---

# Implementación (Deployment)

*   Las aplicaciones .NET Aspire se construyen con **principios cloud-agnostic**.
*   **Manifiesto de Implementación:** El proyecto AppHost puede generar un archivo JSON que describe todos los recursos y propiedades de la aplicación para herramientas de implementación.
*   **Objetivos de Implementación:**
    *   **Azure Container Apps (ACA):** Un entorno completamente gestionado para ejecutar microservicios y aplicaciones contenerizadas. Es un gran escenario de hosting para aplicaciones .NET Aspire.
    *   **Kubernetes:** Una plataforma popular de orquestación de contenedores. Kubernetes es un **objetivo de implementación** para aplicaciones .NET Aspire, no un reemplazo.

---

# Implementación con Herramientas Microsoft

*   **Azure Developer CLI (azd):** Tiene soporte extendido para implementar aplicaciones .NET Aspire.
    *   El flujo `azd init` tiene soporte personalizado para proyectos .NET Aspire.
    *   `azd` interroga el manifiesto de .NET Aspire para generar los recursos de Azure necesarios (por defecto Bicep en memoria) y desplegar las aplicaciones.
    *   Puede **aprovisionar y desplegar** recursos en Azure (por ejemplo, ACA) con un solo comando (`azd up`).
    *   Puede **generar archivos Bicep** a partir del modelo de aplicación .NET Aspire para revisión y control de versiones (`azd generate bicep`).
*   **Visual Studio:** Permite publicar proyectos .NET Aspire directamente a Azure Container Apps.
*   **CI/CD:** `azd` permite la implementación de aplicaciones .NET Aspire utilizando **GitHub Actions**.

---

# Observabilidad

*   Las aplicaciones .NET Aspire están diseñadas para usar **OpenTelemetry** para la telemetría de la aplicación.
*   Por defecto, se utiliza la **exportación OTLP** (OpenTelemetry Protocol).
*   El Dashboard de .NET Aspire es un servidor OTLP estándar que visualiza logs, traces y métricas.
*   Puede integrar con **Azure Application Insights** (requiere configurar el exporter de Azure Monitor).
*   Soporte para **Seq** a través de un componente para enviar logs y traces persistentes.
*   Soporte para métricas con **Prometheus y Grafana** (ejemplo disponible).

---

# Componentes Populares (Ejemplos)

Los paquetes de hosting de .NET Aspire proporcionan extensiones para añadir recursos comunes.

*   **Bases de Datos:**
    *   PostgreSQL.
    *   SQL Server.
    *   Azure Cosmos DB.
    *   MySQL.
    *   MongoDB.
    *   Oracle Entity Framework.

---

# Componentes Populares (Ejemplos - Continuación)

*   **Caching:**
    *   Redis.
*   **Almacenamiento (Storage):**
    *   Azure Blob Storage.
    *   Azure Queue Storage.
    *   Azure Table Storage.
*   **Mensajería (Messaging):**
    *   RabbitMQ.
    *   Azure Event Hubs.
    *   Azure Service Bus.
    *   Apache Kafka.
    *   NATS.

---

# Componentes Populares (Ejemplos - Continuación)

*   **Otros:**
    *   Seq.
    *   Azure Key Vault.
    *   Azure SignalR Service.
    *   Node.js y npm.

---

# Extensibilidad

*   Puedes crear **tipos de recursos personalizados** para .NET Aspire.
*   Los recursos personalizados son clases y métodos dentro de una biblioteca de clases que referencia la biblioteca `Aspire.Hosting`.
*   Esto permite compartir y **reutilizar definiciones de recursos** entre diferentes aplicaciones .NET Aspire.

---

# Conclusión

*   .NET Aspire es un **conjunto de herramientas y bibliotecas** para simplificar el desarrollo y la implementación de **aplicaciones .NET distribuidas y cloud-native**.
*   Se centra en mejorar la **experiencia de desarrollo local** a través de la orquestación, los componentes y el dashboard.
*   Simplifica la integración con **servicios comunes de datos y mensajería**.
*   Proporciona soporte para la **observabilidad** mediante OpenTelemetry.
*   Facilita la **implementación** a **Azure Container Apps** y **Kubernetes** mediante herramientas como `azd` y manifiestos de implementación.
*   Es un **proyecto open source**.

--------------------------------------------------------------------------------