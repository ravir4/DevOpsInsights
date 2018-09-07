---

copyright:
  years: 2016, 2018
lastupdated: "2018-8-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Preguntas más frecuentes
{: #faqs}

Aquí encontrará respuestas a las preguntas más frecuentes sobre el uso de {{site.data.keyword.DRA_full}}.

## ¿Cómo puedo eliminar datos que {{site.data.keyword.DRA_short}} ha extraído de un repositorio?

Cambie el filtro de datos del repositorio para que excluya los datos que desea eliminar. 

Para cambiar el filtro de datos de {{site.data.keyword.DRA_short}}, pulse **Valores** y luego **Filtros**. 

## Faltan algunos de mis problemas. ¿Cómo los puedo añadir?

Si el servicio de seguimiento de problemas no forma parte de la cadena de herramientas, añádalo. {{site.data.keyword.DRA_short}} sólo extrae servicios que forman parte de la cadena de herramientas. 

Si el servicio de seguimiento de problemas forma parte de la cadena de herramientas, compruebe si las etiquetas de {{site.data.keyword.DRA_short}} están correlacionadas con las etiquetas que utiliza el servicio. Pulse **Valores**, pulse **Etiquetas** y luego verifique la correlación.

Como último recurso, elimine el servicio de seguimiento de problemas de la cadena de herramientas. A continuación, vuelva a añadirlo. {{site.data.keyword.DRA_short}} extraerá el servicio desde cero. La extracción puede durar varias horas. 

## ¿Cómo puedo volver a extraer un repositorio?

Para volver a extraer un repositorio, suprima la integración de {{site.data.keyword.DRA_short}} de la cadena de herramientas. A continuación, vuelva a añadirla.

## ¿Cómo puedo añadir un repositorio para que sea extraído?

Añádalo a una cadena de herramientas pulsando **Añadir una herramienta** en la página de visión general de la cadena de herramientas. Una vez que el repositorio forme parte de la cadena de herramientas, Insights volverá a extraer los datos para que incluir dicho repositorio.

Marque el recuadro **Habilitar GitHub Issues** al añadir un repositorio para habilitar la extracción de problemas. 

## ¿Por qué no veo ninguna compilación o despliegue?

DevOps Insights extrae automáticamente los repositorios de código que forman parte de una cadena de herramientas, pero debe configurar el conducto para que supervise las compilaciones y los despliegues. 

En primer lugar, compruebe que dispone de un conducto de entrega continua o Jenkins en la cadena de herramientas. 

Después, verifique que el conducto está configurado para la supervisión de compilaciones y despliegues. Para saber cómo configurar el conducto, consulte la [documentación de integración de entrega continua](risk_cd.html) o la [documentación de integración de Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
