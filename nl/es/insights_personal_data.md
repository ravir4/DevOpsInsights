---

copyright:
  years: 2018
lastupdated: "2018-8-2"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Gestión de datos personales en DevOps Insights
{: insights_personal_data}

Puede suprimir datos personales que se recopilan y almacenan en {{site.data.keyword.DRA_full}}.
{: shortdesc}

Los datos que se almacenan en {{site.data.keyword.DRA_short}} están indexados por ID de cadena de herramientas. Cuando suprime una cadena de herramientas, se suprimen todos los datos relacionados con los repositorios que se han recopilado como parte de la cadena de herramientas.

IBM no gestiona datos en el servicio {{site.data.keyword.DRA_short}}. Antes de abandonar el servicio {{site.data.keyword.DRA_short}}, debe suprimir sus propios datos. Para suprimir los datos, suprima la integración de herramientas de {{site.data.keyword.DRA_short}} de la cadena de herramientas. Si la integración de herramientas de {{site.data.keyword.DRA_short}} no se vuelve a añadir a la cadena de herramientas en el plazo de siete días, los datos se suprimen.
{: tip}

## Supresión de datos de {{site.data.keyword.DRA_short}}
{: #insights_delete_data}

En la tabla siguiente se listan los casos de ejemplo para suprimir los datos de {{site.data.keyword.DRA_short}} y se describe cómo afectan a cada una de las categorías de {{site.data.keyword.DRA_short}}.

|  | Developer y Team Insights | Deployment Risk | Security Insights |
|---------|-------------|-------------|-------------|
| [Supresión de un repositorio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	Se suprimen todos los datos relacionados con el repositorio.  | N/A | N/A |
| [Supresión de una integración de herramientas de {{site.data.keyword.DRA_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	Se suprimen todos los datos relacionados con el repositorio.  | Se suprimen todos los datos asociados con la cadena de herramientas de la que forma parte la integración de herramientas. | Se suprimen todos los datos relacionados con los repositorios asociados con la cadena de herramientas de la que forma parte la integración de herramientas.  |
| [Supresión de una cadena de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | Se suprimen todos los datos relacionados con los repositorios asociados con la cadena de herramientas. | Se suprimen todos los datos asociados con la cadena de herramientas.  | Se suprimen todos los datos asociados con la cadena de herramientas. |
| [Supresión de un conducto ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/A | N/A | N/A |
{:caption="Tabla 1. Casos de ejemplo de supresión de datos" caption-side="top"}

## Supresión de una integración de herramientas de {{site.data.keyword.DRA_short}}
{: #insights_delete_integration}

Si suprime una integración de herramientas de la cadena de herramientas, la supresión no se puede deshacer.

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, tarjeta Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
1. En la tarjeta de la integración de herramientas de {{site.data.keyword.DRA_short}} que desea suprimir, pulse el menú para acceder a las opciones de configuración.
1. Para suprimir la integración de herramientas de la cadena de herramientas, pulse **Suprimir**.

  ![Menú de configuración](images/delete_insights_integration.png)

1. Confirme la acción pulsando **Suprimir**. 
