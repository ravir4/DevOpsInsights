---

copyright:
  years: 2016, 2018
lastupdated: "2018-8-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Guía de aprendizaje de iniciación (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} aplica analíticas de despliegue, equipos y desarrolladores a los proyectos DevOps. Utilícelas para conocer en qué medida su equipo sigue los procedimientos de desarrollador y de DevOps, para gestionar el riesgo en su codebase y para imponer de forma automática estándares de calidad en proyectos de entrega continua. 
{:shortdesc}

{{site.data.keyword.DRA_short}} está disponible sólo en la región EE.UU. sur.
{: tip}

Para utilizar {{site.data.keyword.DRA_short}}, deberá añadirlo a una cadena de herramientas. Muchas cadenas de herramientas ya incluyen a {{site.data.keyword.DRA_short}}. Asegúrese también de [añadirlo a su grupo de recursos u organización de {{site.data.keyword.Bluemix_notm}} como servicio](/docs/services/reqnsi.html), de forma que pueda ver información sobre {{site.data.keyword.DRA_short}} y acceder desde su panel de control de {{site.data.keyword.Bluemix_notm}} a algunas de las plantillas de cadena de herramientas que lo incluyen.  

## Paso 1: Añadir DevOps Insights a una cadena de herramientas
{: #catalog}

{{site.data.keyword.DRA_short}} está disponible mediante la integración con cadenas de herramientas de {{site.data.keyword.contdelivery_full}}. {{site.data.keyword.DRA_short}} se puede añadir a cualquier cadena de herramientas seleccionándolo desde el catálogo de integración de herramientas.

{{site.data.keyword.DRA_short}} es parte de muchas plantillas de cadena de herramientas. Si crea una cadena de herramientas a partir de una plantilla que incluye {{site.data.keyword.DRA_short}}, asegúrese de que {{site.data.keyword.DRA_short}} se establece en **Avanzado**. A continuación, cree la cadena de herramientas y vaya al [Paso 2](/docs/services/DevOpsInsights/index.html#using).
{: tip}

1. Pulse **Añadir una herramienta**.

2. Pulse **{{site.data.keyword.DRA_short}}**.

3. Pulse **Crear integración**.

{{site.data.keyword.DRA_short}} está ahora disponible en la página Visión general de la cadena de herramientas. Automáticamente se exploran los datos de su repositorio y sistema de seguimiento de problemas. 

## Paso 2: Explorar los datos del proyecto
{: #using}

Si su cadena de herramientas incluye GitHub, GitLab, o JIRA, {{site.data.keyword.DRA_short}} proporciona de forma automática información sobre su codebase y del equipo después de una recopilación y análisis de los datos iniciales. Si su cadena de herramientas no incluye ninguna de estas integraciones, añada una de ellas.
{: tip}

1. Desde la página visión general de la cadena de herramientas, pulse **{{site.data.keyword.DRA_short}}**.

2. Pulse **Team** o **Developer Insights** y, a continuación, seleccione una categoría de datos. 

3. Explore los datos del proyecto mediante la visualización de los paneles de control en la categoría de datos. Si desea saber más sobre un gráfico o lo que puede hacer con su información, pulse **Information** o **Instrucciones**.

## Pasos siguientes
{: #next_steps}

Después de explorar Team y Developer Insights, configure [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) que le ayudará en el cumplimiento de calidad de código deseada. Deployment Risk es compatible con Delivery Pipeline for {{site.data.keyword.contdelivery_short}} y Jenkins.
