---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integración de análisis de Deployment Risk con entrega continua

{{site.data.keyword.DRA_short}} realiza un seguimiento de los riesgos de desarrollo en función de los datos que publica en él. Estos datos pueden incluir pruebas de unidad, cobertura de código, pruebas de verificación funcional, datos de SonarQube o datos de exploración de IBM Application Security on Cloud. Una vez publicados estos datos, puede añadir puertas a los conductos para poder detener compilaciones que no cumplan las políticas de riesgos.

Para ver una explicación de alto nivel del análisis de Deployment Risk de {{site.data.keyword.DRA_short}}, consulte [Acerca de Deployment Risk](./about_risk.html).

Para obtener más información sobre los conductos de entrega continua, consulte la [documentación oficial](../ContinuousDelivery/pipeline_working.html).

## Visión general
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} necesita esta información del conducto para analizar el riesgo de despliegue:

* Registros de compilación
* Registros de despliegue
* Resultados de pruebas

En los resultados de pruebas se deben proporcionar en uno de estos formatos soportados:

| Tipo de prueba               | Formatos soportados                                               |
|------------------------------|-----------------------------------------------------------------|
| Prueba de verificación funcional | Mocha, xUnit                                                    |
| Prueba de unidad                 | Mocha, xUnit, Karma/Mocha                                       |
| Cobertura de código              | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Exploración de app estática      | Exploraciones de app estáticas proporcionadas por IBM Application Security on Cloud  |
| Exploración de app dinámica      | Exploraciones de app dinámicas proporcionadas por IBM Application Security on Cloud |
| SonarQube                        | Datos de exploración proporcionados por exploraciones SonarQube                           |

Las variables de entorno que define en el conducto proporcionan contexto para la publicación de estos registros. Puede definirlas mediante el mandato `export` en los scripts de los trabajos. También puede definirlas en las etapas del conducto en el menú Propiedades de entorno.

Variables de entorno:

| Variable de entorno  | Finalidad | Necesaria en |
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`  | El nombre de la app en el panel de control. | Todos los trabajos que compilan, prueban, despliegan y aplican políticas de riesgo de {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Texto que se añade como prefijo a las compilaciones de etapa. Este texto también aparece en el panel de control. | Todos los trabajos que compilan, prueban, despliegan y aplican políticas de riesgo de {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | El entorno en el que se ejecuta la aplicación. | Trabajos de prueba y despliegue. |

Utilice estas variables de forma coherente:

* Para una aplicación determinada, utilice la misma variable `LOGICAL_APP_NAME` en todos los trabajos o etapas. 
* El valor `BUILD_PREFIX` debe ser el mismo para un tipo de compilación y una app determinada. Por ejemplo, para compilaciones de la rama maestra, el valor de `BUILD_PREFIX` podría ser `"master"`. 
* Utilice el mismo valor de `LOGICAL_ENVIRONMENT_NAME` en los trabajos de prueba y los trabajos de despliegue correspondientes. Si en `LOGICAL_ENVIRONMENT_NAME` utiliza el valor `"PRODUCTION"` en un trabajo de despliegue, utilice el mismo valor cuando publique los resultados de las pruebas que también se han ejecutado en dicho entorno.

## Variables de entorno de trabajos de compilación

Para el último trabajo de compilación de una etapa, defina las variables de entorno para un nombre de aplicación y un prefijo de compilación. Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Cuando se complete este trabajo de compilación, el conducto publicará un mensaje en {{site.data.keyword.DRA_short}} que indicará que ha finalizado una compilación SampleApp.

## Variables de entorno de trabajos de despliegue

Para el último trabajo de despliegue de la etapa, defina un nombre de aplicación, un prefijo de compilación y un nombre de entorno. Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Cuando finalice el trabajo de despliegue, el conducto publicará un mensaje en {{site.data.keyword.DRA_short}} que indicará que se han desplegado en un entorno la app y la compilación especificadas.

## Variables de entorno de trabajos de prueba

Para todos los trabajos que producen resultados, defina un nombre de aplicación y un prefijo de compilación.

Si el trabajo genera resultados de prueba de verificación funcional (FVT), debe definir también el nombre de entorno lógico en el que se ejecutan estas pruebas.

Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## Publicación de resultados de prueba
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utiliza los resultados de prueba de los trabajos para generar informes y aplicar políticas de riesgo. 

En un conducto, puede utilizar cualquier tipo de trabajo para ejecutar una prueba. Una vez que ejecuta dicha prueba, puede subir sus resultados a {{site.data.keyword.DRA_short}}. Para subir los resultados, invoque una CLI en el script de shell del trabajo. 

Puede subir estos tipos de resultados de prueba desde la CLI:

* Pruebas de unidad
* Cobertura de código
* Pruebas de verificación funcional
* Resultados de SonarQube
* Resultados de exploración de app estática y dinámica de IBM Application Security on Cloud. 

Este es un script de ejemplo que ejecuta pruebas y a continuación sube los resultados a {{site.data.keyword.DRA_short}}: 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

En este ejemplo, el mandato `idra` que se ejecuta con el distintivo `--publishtestresult` especifica que el script cargará los resultados. El distintivo `--filelocation` indica la ubicación del archivo de resultados de la prueba en relación con el directorio raíz del trabajo. El distintivo `--type` indica el tipo de pruebas que se ejecutan.

El mandato `idra` admite los valores siguientes de `type`: 

| Tipo | Descripción|
|------|-------------|
| `unittest` | Resultados de prueba de unidad | 
| `fvt` | Resultados de prueba de verificación funcional |
| `code` | Resultados de cobertura de código | 
| `sonarqube` | Resultados de exploración de SonarQube | 
| `staticsecurityscan` | Resultados de exploración de seguridad estática de IBM Application Security on Cloud |
| `dynamicsecurityscan` | Resultados de exploración de seguridad dinámica de IBM Application Security on Cloud |

Para obtener más información acerca del mandato `idra`, consulte [la página del paquete grunt-idra3 en npm](https://www.npmjs.com/package/grunt-idra3). 

## Definición de puertas
{: #configure_pipeline_gates}

Las puertas de {{site.data.keyword.DRA_short}} comprueban si los resultados de las pruebas cumplen con una política definida. Si no se cumple la política, de forma predeterminada la puerta de {{site.data.keyword.DRA_short}} falla. También puede configurar las puertas para que actúen en un rol de advertencia que permite el progreso en el conducto, incluso después de una anomalía.

El panel de control de Deployment Risk se basa en la presencia de una puerta después un trabajo de despliegue en el entorno de transferencia. Si desea utilizar el panel de control, asegúrese de que tiene una puerta después de realizar el despliegue en el entorno de transferencia y antes de realizar el despliegue en un entorno de producción.

Normalmente, las puertas se colocan en el conducto antes de la promoción de la compilación. Estas ubicaciones son ideales para comprobar la calidad de la compilación con las políticas para asegurarse de que es seguro promocionarla de un entorno a otro. Sin embargo, puede colocar puertas en cualquier sitio del conducto donde desee comprobar un criterio específico. Las puertas que se colocan antes del despliegue en un entorno de transferencia todavía impondrán las políticas, pero no aparecerán en el panel de control de Deployment Risk.

1. En una etapa, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png) y pulse **Configurar etapa**.
2. Pulse **Añadir trabajo**. Para el tipo de trabajo, seleccione **Prueba**.
3. Para el tipo de probador, **Puerta de {{site.data.keyword.DRA_short}}**.
4. Especifique el nombre del entorno. Asegúrese de que este valor coincida con el que ha definido en sus [propiedades de entorno](#toolchain_pipeline_props).
5. Especifique el nombre de la política a comprobar en esta puerta.

 Este nombre debe coincidir exactamente con uno de los nombres de política que ha definido. Puede especificar sólo políticas que están definidas en la misma organización de {{site.data.keyword.Bluemix_notm}} como su cadena de herramientas.

6. Opcional: Para hacer que una puerta funcione en modalidad de advertencia, desmarque el recuadro de selección **Dejar de ejecutar esta etapa si el trabajo falla**. En modalidad de advertencia, {{site.data.keyword.DRA_short}} completa el mismo análisis de política en la puerta y genera informes, pero si se produce un error, el conducto no se detiene.
7. Pulse **Guardar** para volver al conducto.
8. Configure puertas para todas sus políticas de {{site.data.keyword.DRA_short}} repitiendo estos pasos.

![Trabajo Mocha de Deployment Risk](images/insights_gate_job.png)
*Figura 2. Puerta de DevOps Insights*

Cuando haya terminado de configurar su conducto, empiece a utilizar use {{site.data.keyword.DRA_short}}. 
