---

copyright:
  years: 2016, 2018
lastupdated: "2018-3-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk proporciona información diversa sobre los despliegues, especialmente su riesgo. Puede utilizarlo para automatizar la protección de la calidad en su conducto de entrega mediante el uso de políticas y puertas. Proporciona datos sobre la frecuencia de las compilaciones y los despliegues, además de cobertura de código y tendencias de prueba.
{:shortdesc}

Después de abrir {{site.data.keyword.DRA_short}} desde la cadena de herramientas, pulse **Deployment Risk**. Desde allí, puede seleccionar una categoría analítica para profundizar en lo que ocurre en los despliegues.  

Utilice Deployment Risk para imponer estándares de calidad en su cadena de herramientas mediante políticas y puertas. Las políticas comprenden conjuntos de reglas y las puertas que las imponen. Por ejemplo, podría crear una política denominada "Unit Testing and Test Coverage" que precisa que las compilaciones satisfagan estándares de realización de pruebas de unidad y estándares de cobertura de código. A continuación añadiría una puerta que haría referencia a la política de su proceso de entrega continua. Las compilaciones que no satisfagan la política se detendrán en la puerta. 

## Análisis de riesgos

El análisis de riesgos facilita una visión general de los riesgos asociados a las aplicaciones de los entornos de transferencia y producción. Puede profundizar para comprender la cobertura de código, el rendimiento de las pruebas y los informes de seguridad. Los paneles de control se rellenan automáticamente con la información más reciente sobre las pruebas de {{site.data.keyword.DRA_short}} de sus conductos.

## Frecuencia de despliegues

Puede ver las tendencias de frecuencia de despliegues de los entornos de producción y transferencia, entre otros. Esta vista también muestra los despliegues que se han realizado correctamente y los errores de despliegue. Puede pulsar un despliegue concreto para ver sus detalles. Si es miembro de un equipo Agile, debería ver que la tendencia de la frecuencia de despliegues aumenta con el tiempo. 

## Frecuencia de compilaciones

Puede ver las tendencias de frecuencia de compilaciones de las ramas de larga ejecución. Esta vista también muestra las compilaciones que se han realizado correctamente y los errores de compilación. Pulse un punto de interés para ver los detalles de compilación. Si es miembro de un equipo Agile, querrá ver muchas compilaciones diarias en la ramificación de integración. De lo contrario, significa que el equipo no incorpora el código con frecuencia.

## Tendencias de pruebas de unidad

Puede ver las tendencias de las pruebas de unidad de las compilaciones que son de una determinada rama o que se despliegan en un determinado entorno. Por ejemplo, puede ver las tendencias de prueba de las compilaciones de la rama maestra. Si falla alguna de las pruebas para compilaciones que han ido a producción, quizá quiera tomar medidas. Además, si el número de pruebas disminuye con el tiempo, puede ser motivo de preocupación.

## Tendencias de pruebas de verificación funcional

Puede ver las tendencias de las pruebas de verificación funcional de las compilaciones que son de una determinada rama o que se despliegan en un determinado entorno. Por ejemplo, puede ver las tendencias de prueba de las compilaciones de la rama maestra. Si falla alguna de las pruebas para compilaciones que han ido a producción, quizá quiera tomar medidas. Además, si el número de pruebas disminuye con el tiempo, puede ser motivo de preocupación.

## Tendencias de cobertura de código

Puede ver las tendencias de cobertura de código de las compilaciones que se despliegan en un determinado entorno. Por ejemplo, puede ver las tendencias de cobertura de código de las compilaciones que han ido a producción. En teoría, la cobertura de código debería mejorar con el tiempo en las compilaciones que van a producción. Si la cobertura de código disminuye, quizá quiera tomar medidas.

## Políticas

Las políticas son conjuntos de reglas que controlan las puertas en su conducto de entrega. Si su código no satisface o excede una política instaurada en una puerta concreta, se detiene el despliegue para evitar que se liberen cambios con un riesgo elevado.


## Requisitos previos
{: #prerequisites}

Deployment Risk precisa una configuración adicional más allá de lo que se describe en [Iniciación con {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para utilizar Deployment Risk, necesita dos cosas:

* Una instancia de {{site.data.keyword.deliverypipeline}} o un proyecto de Jenkins
* Pruebas que utilizará para evaluar su proyecto

## Información de integración

Deployment Risk se integra con {{site.data.keyword.deliverypipeline}}, que es parte de {{site.data.keyword.contdelivery_full}}, y con proyectos de Jenkins. En un alto nivel, las instrucciones para utilizarlos son similares.  

Si está utilizando {{site.data.keyword.deliverypipeline}}, siga estos pasos:

1. [Cree políticas y reglas](risk_policies.html) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Prepare las etapas de su conducto](risk_cd.html) para la integración con {{site.data.keyword.DRA_short}}.
3. [Cree o edite trabajos de pruebas](risk_cd.html) en el conducto para subir los resultados a {{site.data.keyword.DRA_short}}.
4. [Añada puertas](risk_cd.html) al conducto para que tomen decisiones de promoción en base a dichos resultados y a sus políticas.
5. Ejecute el conducto y [visualice los resultados](results.html).

Si utiliza Jenkins, siga estos pasos:

1. [Cree políticas y reglas](risk_policies.html) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Instale y configure el plugin Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Cree trabajos de pruebas y puertas tal como se describe en las instrucciones del plugin](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). Las pruebas suben resultados para que {{site.data.keyword.DRA_short}} los analice y las puertas utilizan dichos resultados para tomar decisiones de promoción.
4. Ejecute el proyecto y [visualice los resultados](results.html). 

Independientemente de cómo compila y despliega su código, los resultados serán los mismos: las compilaciones que satisfagan los estándares pasarán las puertas de Deployment Risk y las compilaciones que no lo hagan, serán detenidos. 
