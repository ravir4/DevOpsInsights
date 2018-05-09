---

copyright:
  years: 2016, 2018
lastupdated: "2018-4-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a DevOps Insights (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} aplica analíticas de despliegue, equipos y desarrolladores a los proyectos DevOps. Utilícelas para conocer en qué medida su equipo sigue los procedimientos de desarrollador y de DevOps, para gestionar el riesgo en su codebase y para imponer de forma automática estándares de calidad en proyectos de entrega continua.
{:shortdesc}

**Nota**: {{site.data.keyword.DRA_short}} está disponible sólo en la región EE.UU. Sur.

{{site.data.keyword.DRA_short}} consta de varios grupos de funcionalidades:

   * Developer Insights proporciona una forma averiguar la madurez del desarrollo de un proyecto. Permite identificar los archivos más propensos a contener errores y obtener una vista de conformidad del proyecto con relación a los procedimientos de desarrollador.

   * Team utiliza análisis de codificación social para ayudarle a comprender cómo colabora entre sí el equipo y cómo puede hacerlo mejor.

   * Deployment Risk es como una red de seguridad para la entrega continua. Analiza los resultados de pruebas de unidad, pruebas funcionales, exploraciones de seguridad, exploraciones de aplicación y herramientas de cobertura de código en puertas concretas en su proceso de despliegue e impide que se liberen cambios peligrosos. Muestra gráficos de tendencias de la cobertura de código, las compilaciones y los despliegues.

{{site.data.keyword.DRA_short}} es una integración en el catálogo de cadenas de herramientas abiertas de Bluemix. Para obtener más información sobre las cadenas de herramientas, consulte [Cómo trabajar con cadenas de herramientas](/docs/services/ContinuousDelivery/toolchains_working.html).

Para utilizar {{site.data.keyword.DRA_short}}, deberá añadirlo a una cadena de herramientas. Muchas cadenas de herramientas ya incluyen a {{site.data.keyword.DRA_short}}. Asegúrese también de [añadirlo a su organización de {{site.data.keyword.Bluemix_notm}} como un servicio](/docs/services/reqnsi.html) de forma que pueda ver información sobre {{site.data.keyword.DRA_short}} y acceder desde su panel de control de {{site.data.keyword.Bluemix_notm}} a algunas de las plantillas de cadena de herramientas que lo incluyen.  

Además, IBM ejecuta Developer Insights y Team en la mayoría de los proyectos de código abierto de más éxito en GitHub. Vaya a [DevOpsInsights.io](http://devopsinsights.io/) para ver los datos de desarrollo y equipo.

## Adición de DevOps Insights a una cadena de herramientas
{: #catalog}

{{site.data.keyword.DRA_short}} está disponible mediante la integración con cadenas de herramientas de {{site.data.keyword.contdelivery_full}}. {{site.data.keyword.DRA_short}} se puede añadir a cualquier cadena de herramientas seleccionándolo desde el catálogo de integración de herramientas.

{{site.data.keyword.DRA_short}} también es parte de muchas plantillas de cadena de herramientas. Si crea una cadena de herramientas a partir de una plantilla que incluye {{site.data.keyword.DRA_short}}, asegúrese de que {{site.data.keyword.DRA_short}} se establece en **Avanzado**. A continuación, cree la cadena de herramientas y vaya a [Utilización de Insights](/docs/services/DevOpsInsights/index.html#using).

Para añadir {{site.data.keyword.DRA_short}} a una cadena de herramientas:

1. Pulse **Añadir una herramienta**.

2. Pulse **{{site.data.keyword.DRA_short}}**.

3. Pulse **Crear integración**.

{{site.data.keyword.DRA_short}} está ahora disponible en la página Visión general de la cadena de herramientas. Automáticamente se exploran los datos de su repositorio y sistema de seguimiento de problemas.

## Utilización de DevOps Insights
{: #using}

Si su cadena de herramientas incluye GitHub, GitLab, o JIRA, {{site.data.keyword.DRA_short}} proporciona de forma automática información sobre su codebase y del equipo después de una recopilación y análisis de los datos iniciales. Si su cadena de herramientas no incluye ninguna de estas integraciones, añada una de ellas y, a continuación, siga estos pasos:

1. Desde la página visión general de la cadena de herramientas, pulse **{{site.data.keyword.DRA_short}}**.

2. Pulse **Team** o **Developer Insights** y, a continuación, seleccione una categoría de datos.

3. Explore los datos del proyecto mediante la visualización de los paneles de control en la categoría de datos. Si desea saber más sobre un gráfico o lo que puede hacer con su información, pulse **Information** o **Instrucciones**.

Después de explorar Team y Developer Insights, configure [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) que le ayudará en el cumplimiento de calidad de código deseada. Deployment Risk es compatible con Delivery Pipeline for {{site.data.keyword.contdelivery_short}} y Jenkins.
