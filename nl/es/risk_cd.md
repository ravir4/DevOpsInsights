---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integración de análisis de Deployment Risk con entrega continua

Puede instrumentar conductos para {{site.data.keyword.contdelivery_full}} para utilizar las prestaciones de análisis de Deployment Risk de {{site.data.keyword.DRA_short}}. A continuación, puede publicar datos de estos trabajos y añadir puertas que apliquen políticas de riesgo.

Para ver una explicación de alto nivel del análisis de Deployment Risk de {{site.data.keyword.DRA_short}}, consulte [Acerca de Deployment Risk](./about_risk.html).

Para obtener más información sobre los conductos de entrega continua, consulte la [documentación oficial](../ContinuousDelivery/pipeline_working.html).

## Preparación de trabajos y etapas de conducto
{: #integrate_pipeline}

Para empezar, debe instrumentar el conducto para comunicarse con {{site.data.keyword.DRA_short}}. Para ello, defina variables de entorno específicas para todos los trabajos de conducto que compilen, prueben o desplieguen código. También debe añadir variables de entorno para probar trabajos que apliquen políticas de riesgo utilizando el tipo de probador Puerta de DevOps Insights.

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
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | El nombre de la app en el panel de control. | Todos los trabajos que compilan, prueban, despliegan y aplican políticas de riesgo de {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Texto que se añade como prefijo a las compilaciones de etapa. Este texto también aparece en el panel de control. | Todos los trabajos que compilan, prueban, despliegan y aplican políticas de riesgo de {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | El entorno en el que se ejecuta la aplicación. | Trabajos de prueba y despliegue. |

### Configuración de trabajos de compilación

Para el último trabajo de compilación de una etapa, defina las variables de entorno para un nombre de aplicación y un prefijo de compilación. Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Cuando se complete este trabajo de compilación, el conducto publicará un mensaje en {{site.data.keyword.DRA_short}} que indicará que ha finalizado una compilación SampleApp.

### Configuración de trabajos de despliegue

Para el último trabajo de despliegue de la etapa, defina un nombre de aplicación, un prefijo de compilación y un nombre de entorno. Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Cuando finalice el trabajo de despliegue, el conducto publicará un mensaje en {{site.data.keyword.DRA_short}} que indicará que se han desplegado en un entorno la app y la compilación especificadas.

### Configuración de trabajos de prueba

Para todos los trabajos que producen resultados, defina un nombre de aplicación y un prefijo de compilación.

Si el trabajo genera resultados de prueba de verificación funcional (FVT), debe definir también el nombre de entorno lógico en el que se ejecutan estas pruebas.

Estos son los mandatos que se incluirían en un script de ejemplo:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

Asegúrese de que los nombres de aplicación y los entornos coinciden donde corresponda. Por ejemplo, si desea que un trabajo de prueba de producción que se ejecuta en un despliegue de producción tenga valores `LOGICAL_ENV_NAME` idénticos.

## Publicación de datos de prueba en DevOps Insights
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utiliza los resultados de prueba de los trabajos para generar informes y aplicar políticas de riesgo. Puede publicar datos de prueba de todos los tipos de trabajo.

Hay dos opciones para publicar los resultados de prueba:

* Invocar una CLI (interfaz de línea de mandatos) simple en el script de un trabajo.

* Añadir un trabajo de prueba con el tipo Advanced Tester al conducto.

Cuando utiliza el método Advanced Tester, no publica resultados de prueba mediante la CLI. En su lugar, especifica la ubicación de los archivos resultantes en el trabajo del conducto, y el trabajo sube los resultados a medida que estén disponibles.

Sea cual sea el método de publicación que utilice, los resultados de prueba deben estar en uno de los formatos que soporta {{site.data.keyword.DRA_short}}:

<table><thead>
<tr>
<th>Tipo de prueba</th>
<th>Formatos soportados</th>
</tr>
</thead><tbody>
<tr>
<td>Prueba de verificación funcional</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Prueba de unidad</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura de código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

### Publicación de datos de prueba de cualquier tipo de trabajo

En un conducto, puede utilizar cualquier tipo de trabajo para ejecutar una prueba. Una vez que ejecuta dicha prueba, puede subir sus resultados a {{site.data.keyword.DRA_short}}. Para subir los resultados, invoque una CLI en el script de shell del trabajo. 

Puede subir estos tipos de resultados de prueba desde la CLI:

* Pruebas de unidad
* Cobertura de código
* Pruebas de verificación funcional
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

Para obtener más información acerca del mandato `idra`, consulte [la página del paquete grunt-idra3 en npm](https://www.npmjs.com/package/grunt-idra3). 

### Publicación de datos de prueba de trabajos Advanced Tester

Puede añadir trabajos de prueba con el tipo Advanced Tester a un conducto. Una vez que se ejecutan, suben sus resultados automáticamente a {{site.data.keyword.DRA_short}}. 

1. En la etapa en la que desea añadir el trabajo que sube los resultados, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png). Pulse **Configurar etapa**.
2. Cree un trabajo de prueba y escriba un nombre para el mismo. 
3. Seleccione **Advanced Tester** como tipo de trabajo.
4. Complete los campos **Mandato de prueba** y **Directorio de trabajo** tal como lo haría con un trabajo de prueba de conducto normal. 
5. Complete los campos restantes para subir los resultados de la prueba para un tipo de prueba concreto. 

 1. Elija el tipo de métrica que coincida con lo que definió en la política de {{site.data.keyword.DRA_short}} que desea utilizar.
 2. Escriba una ubicación para el archivo de resultados. Esta ubicación es relativa al directorio de trabajo. 

6. Si desea cargar resultados de un segundo tipo de prueba en el mismo trabajo, complete los campos que tienen el prefijo *Adicional*.
7. Pulse **Guardar** para volver al conducto.

La Figura 1 muestra un trabajo de prueba que está configurado para ejecutar pruebas de unidad, cargar los resultados en formato de Mocha y cargar los resultados de la cobertura de código en formato de Istanbul.

![Trabajo subido de DevOps Insights](images/insights_upload_job.png)
*Figura 1. Subir resultados para DevOps Insights*



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
