---

copyright:
  years: 2017

lastupdated: "2017-07-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualización de datos de servidores IBM UrbanCode Deploy
{: #connect_ucd}

Para ver datos de un servidor IBM UrbanCode Deploy en Delivery Insights, es necesario instalar una instancia de DevOps Connect, instalar un parche en el servidor y, a continuación, conectar dicho servidor a DevOps Connect.
{:shortdesc}

## Requisitos previos
{: #prereqs}

Para ver información sobre los servidores IBM UrbanCode Deploy en {{site.data.keyword.DRA_short}}, debe alojar una instancia de DevOps Connect en un sistema que se pueda conectar a sus servidores IBM UrbanCode Deploy. Este sistema puede ser un sistema físico o una máquina virtual. 

El sistema que aloja DevOps Connect debe tener los siguientes requisitos previos:
- El sistema debe tener un JRE (Java Runtime Environment) versión 8 o posterior.
- La variable `PATH` del sistema debe incluir la ubicación del JRE.
- El sistema debe permitir que DevOps Connect cree conexiones salientes a IBM Bluemix.

Asimismo, el servidor IBM UrbanCode Deploy debe ser de la versión 6.2 o posterior.

## Configuración del servicio {{site.data.keyword.DRA_short}}
{: #configure_service}

Si no tiene el servicio {{site.data.keyword.DRA_short}}, añádalo:
1. Inicie sesión en {{site.data.keyword.Bluemix}} y pulse **Servicios > Panel de control**.
1. Pulse **Crear servicio**.
1. Pulse el servicio de {{site.data.keyword.DRA_short}}.
1. Seleccione un plan de precios y pulse **Crear**.
1. Pulse **Gestionar** y, a continuación, bajo "Profundizar en los despliegues de UrbanCode", pulse **Empezar aquí**.
1. En la ventana de plantilla de cadena de herramientas, pulse **Crear**.  
Delivery Insights creará una cadena de herramientas para su organización. Las cadenas de herramientas son conjuntos de integraciones de herramientas y, en este caso, IBM UrbanCode Deploy y {{site.data.keyword.DRA_short}} son parte de su cadena de herramientas. Para obtener más información sobre las cadenas de herramientas, consulte [Cómo trabajar con cadenas de herramientas](../ContinuousDelivery/toolchains_working.html).
1. En la cadena de herramientas, pulse la herramienta IBM UrbanCode Deploy.
1. Pulse el botón de valores y pulse **Instalación**.

En el futuro, puede acceder a {{site.data.keyword.DRA_short}} pulsando **Servicios > Panel de control** y pulsando la instancia del servicio {{site.data.keyword.DRA_short}}.

Si ya tiene una cadena de herramientas, puede añadirle las herramientas IBM UrbanCode Deploy y {{site.data.keyword.DRA_short}} y acceder a Delivery Insights a través de ellas. A continuación, pulse la herramienta IBM UrbanCode Deploy, pulse el botón de valores y pulse **Instalación**.

Ahora puede seguir las instrucciones de la página **Instrucciones de configuración** para instalar DevOps Connect y conectarlo a {{site.data.keyword.DRA_short}}, como se describe en la siguiente sección.

## Instalación de DevOps Connect y conexión con {{site.data.keyword.DRA_short}}
{: #install_connect}

1. En la página **Instrucciones de configuración**, siga los pasos para instalar DevOps Connect y conectar sus servidores IBM UrbanCode Deploy. Estos pasos incluyen:
{: #set_up_connect}
  1. Instale un sistema para ejecutar DevOps Connect, como se describe en [Requisitos previos](uc_insights_connect_ucd.html#prereqs).
  1. Descargue DevOps Connect, que se proporciona en un archivo JAR ejecutable.

  1. Si utiliza un proxy para conectarse a Internet, defina la variable del sistema `_JAVA_OPTIONS` en el valor siguiente:
    * Si el proxy utiliza HTTPS, defina `_JAVA_OPTIONS` en `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT`, donde `HOSTNAME` es el nombre de host del servidor proxy y `PORT` es el puerto HTTPS del servidor proxy.
    * Si el proxy utiliza HTTP, defina `_JAVA_OPTIONS` en `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT`, donde `HOSTNAME` es el nombre de host del servidor proxy y `PORT` es el puerto HTTP del servidor proxy.

  1. Copie el mandato de la página **Instrucciones de configuración**. Este mandato inicia DevOps Connect con una señal que le permite conectarse a su organización en {{site.data.keyword.Bluemix}}.
  1. De forma predeterminada, DevOps Connect se ejecuta en el puerto 8443, que es el mismo puerto en el que se ejecuta el servidor de IBM UrbanCode Deploy de forma predeterminada. Por lo tanto, si el servidor de IBM UrbanCode Deploy o cualquier otro servicio se ejecutan en el puerto 844s, modifique el puerto de DevOps Connect añadiendo el parámetro `-Dserver.port` al mandato. Por ejemplo, para definir que DevOps Connect utilice el puerto 8888, el mandato debe comenzar de la siguiente manera:  
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

El mandato completo contiene información sobre la cuenta de Bluemix, que configura DevOps Connect automáticamente, como en el ejemplo siguiente:

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. Ejecute el mandato y espere a que se inicie DevOps Connect.

  1. Conecte los servidores IBM UrbanCode Deploy a DevOps Connect, como se describe en la siguiente sección.

## Conexión de servidores IBM UrbanCode Deploy a DevOps Connect
{: #connect_ucd_to_connect}

1. Si el servidor de IBM UrbanCode Deploy es anterior a la versión 6.2.5, instale un parche en él. Para las versiones 6.2.5 y posteriores no es necesario un parche.
  1. Descargue el parche correcto para su versión de IBM UrbanCode Deploy desde la página siguiente. Por ejemplo, el archivo de parche para IBM UrbanCode Deploy 6.2.4.x se denomina [ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar).  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Detenga el servidor. Consulte [Inicio y detención del servidor](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Coloque los archivos de parche en la carpeta <code><em>datos_aplicación</em>/patches</code>, donde <code><em>datos_aplicación</em></code> es la carpeta de los datos de aplicación del servidor. La carpeta de datos de aplicación predeterminada es `/opt/ibm-ucd/server/appdata` en Linux y `C:\Program Files\ibm-ucd\server\appdata` en Windows. En sistemas de alta disponibilidad, la carpeta de datos de aplicación corresponde siempre a una unidad de red compartida a la que cada servidor puede acceder.

  1. Opcional: Mientras el servidor está detenido, para aumentar el rendimiento de la importación de datos desde este servidor, ejecute los siguientes mandatos SQL en la base de datos. Estos mandatos no son necesarios en la versión 6.2.5 y posteriores.  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Utilice el nombre de su base de datos en lugar de `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Inicie el servidor. 

    **Nota:** Es posible que tenga que esperar más que lo que suele hacer para que se inicie el servidor IBM UrbanCode Deploy. Si el servidor finalmente no se inicia, o si no está funcionando correctamente, suprima los archivos de parche y reinicie el servidor. Los archivos de parche no afectan de forma permanente al servidor.

1. Algunas versiones de IBM UrbanCode Deploy requieren un parche adicional en el servidor para conectarse a DevOps Connect. Si está utilizando IBM UrbanCode Deploy versión 6.2 a 6.2.1.2, debe instalar el siguiente parche adicional en el servidor:
  1. Descargue el parche: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Detenga el servidor.
  1. Coloque el archivo de parche en la carpeta <code><em>datos_aplicación</em>/patches</code>.
  1. Inicie el servidor.

1. Cree una integración entre DevOps Connect y el servidor IBM UrbanCode Deploy:  

  **Importante:** La primera vez que se ejecuta la integración, DevOps Connect recupera datos de los últimos 90 días. Si tiene una gran cantidad de datos de despliegue, este proceso puede tardar mucho tiempo. Para recuperar datos de menos de 90 días, consulte [Resolución de problemas](uc_insights_connect_ucd.html#troubleshooting).
  1. En IBM UrbanCode Deploy, cree una señal de autenticación. Consulte [Señales](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. En DevOps Connect, pulse **Integraciones**, y, a continuación, pulse **Añadir nueva**.
  1. Especifique un nombre y una descripción para la integración. La ubicación predeterminada de DevOps Connect es `https://hostname:8443/`, donde `hostname` es el nombre de host del sistema que aloja DevOps Connect.
  1. En la lista **Tipo de integración**, seleccione **IBM UrbanCode Deploy for Cloud Reporting**.
  1. En el campo **URI de servidor**, especifique el URL público del servidor IBM UrbanCode Deploy, por ejemplo, `https://my_UCD.example.com:8447`.
  1. En el campo **Señal de autenticación**, especifique o pegue la señal de autenticación que IBM UrbanCode Deploy haya generado.
  1. En el campo **Usuario de administración**, especifique una lista separada por campos de IBMid para otorgarles acceso a la interfaz DevOps Connect.
  1. Opcional: Pulse **Ejecutar integración** para ejecutar la integración de forma inmediata. De forma predeterminada, las integraciones se ejecutan cada minuto.
  1. Pulse **Guardar**.

  ![Configuración de la integración en DevOps Connect](images/uc_insights_dc_integration.gif)

Ahora sus datos están sincronizados con Delivery Insights. Podrá crear y ver informes que se basan en estos datos. A continuación, correlacione los entornos de los servidores IBM UrbanCode Deploy con entornos locales en Delivery Insights.

## Correlación de entornos para informes
{: #mapping}

### Entornos lógicos

Delivery Insights agrupa sus entornos IBM UrbanCode Deploy (también denominados *entornos físicos*) en uno o varios entornos lógicos. De este modo, puede recopilar entornos en grupos que tengan un significado para organización. Por ejemplo, si tiene varios entornos de producción de varias aplicaciones, puede agrupar todos esos entornos en un único entorno lógico y combinar las métricas de todos de esos entornos en un único panel de control del entorno de producción. La correlación se crea mediante una serie de búsqueda, que permite agrupar entornos de la forma que tenga sentido para sus servidores IBM UrbanCode Deploy.

### Entornos lógicos predeterminados

De forma predeterminada, los informes incluyen entornos lógicos que coinciden con series de texto de los entornos de IBM UrbanCode Deploy. Por ejemplo, todos los entornos con "dev" en el nombre se correlacionan con el entorno lógico DEV, y todos los entornos con "prod" en el nombre se correlacionan con el entorno lógico PROD.

![Los entornos lógicos predeterminados](images/uc_insights_mapping.gif)

### Correlación de entornos con entornos lógicos

Puede correlacionar de forma manual entornos físicos con entornos lógicos o puede utilizar patrones para asociar entornos físicos con entornos lógicos de forma dinámica.

Para correlacionar entornos físicos con entornos lógicos, siga estos pasos:

1. Abra Delivery Insights, pulse el botón de valores y pulse **Correlacionar entornos**.
1. En la página de correlación de entornos, pulse un entorno lógico existente o cree un entorno lógico pulsando **Añadir entorno lógico**.
1. Con un entorno lógico seleccionado, puede especificar patrones para correlacionar entornos con el entorno lógico. En **Patrones incluidos**, pulse **Añadir patrón** y especifique un patrón que desee utilizar. Todos los entornos con nombres que coincidan con el patrón, incluidos los entornos que cree después, se añadirán al entorno lógico. Puede utilizar el asterisco (*) como comodín. Por ejemplo, el patrón `env` coincide con los entornos `env1`, `env2` y `env`.
1. Para correlacionar entornos con entornos lógicos de forma manual, pulse **Añadir manualmente** y seleccione los entornos a añadir o eliminar.
1. Verifique que el entorno lógico contiene los entornos que desee.

![Configuración de la correlación de entorno lógico](images/uc_insights_mapping_manually.gif)

Ahora que ha correlacionado entornos con entornos lógicos, puede agregar la información de los informes por dichos entornos lógicos.

## Correlación de aplicaciones con líneas de negocio
{: #lines}

Las líneas de negocio son grupos de aplicaciones que sirven para un propósito comercial habitual. Puede correlacionar sus aplicaciones con líneas de negocio para facilitar el filtrado de aplicaciones en los gráficos. También puede crear gráficos basados en líneas de negocio.

Para configurar líneas de negocio (LOB), siga estos pasos:

1. En {{site.data.keyword.DRA_short}}, pulse **Delivery Insights**, pulse el botón de valores y pulse **Correlacionar líneas de negocio**.
1. En la página de correlación de líneas de negocio, pulse una LOB o cree una LOB escribiendo un nombre y pulsando **Crear**.
1. Con una LOB seleccionada, puede especificar patrones para correlacionar aplicaciones con la LOB. En **Patrones incluidos**, pulse **Añadir patrón** y especifique un patrón que desee utilizar. Todas las aplicaciones con nombres que coincidan con el patrón, incluidas las aplicaciones que cree después, se añadirán a la LOB. Puede utilizar el asterisco (*) como comodín. Por ejemplo, el patrón `env` coincide con los entornos `env1`, `env2` y `env`.
1. También puede correlacionar aplicaciones a la LOB de forma manual pulsando **Aplicaciones correlacionadas individualmente** y pulsando después **Añadir aplicaciones**.

Una vez que configure las LOB, puede filtrar los gráficos para que solo muestren las aplicaciones de determinadas LOB. Otros gráficos muestran métricas basadas en las LOB.

## Creación de informes

Para crear un informe, abra {{site.data.keyword.DRA_short}}, pulse **Delivery Insights** y, a continuación, pulse **Añadir informe**. Si no ve **Añadir informe**, los servidores de IBM UrbanCode Deploy no están conectados. Pulse el botón de valores y pulse **Instalación** para conectar los servidores.

Desde el informe, puede añadir tarjetas a la sección **Métricas**, filtrar la actividad en **Actividad de aplicación reciente** y añadir gráficas a la sección **Detalles de informe**. Cada gráfica en la sección **Detalles de informe** es personalizable y admite filtros. Para ver los datos sin formato de la gráfica, en la parte superior derecha del mismo, pulse en el botón Valores de la gráfica y, a continuación, pulse **Datos de informe**.

Para cambiar el orden de los diagramas, en la parte superior derecha de la página, pulse el botón Valores y, a continuación, pulse **Editar diseño de gráfica**. A continuación, arrastre y suelte los gráficos para establecer el orden en el informe.

## Compartición de informes
De forma predeterminada, sólo usted puede ver sus informes de Delivery Insights. Comparta los informes con otros usuarios en su organización de Bluemix. Para compartir un informe con otra persona en su organización de Bluemix, abra el informe, en la parte superior derecha del informe pulse el botón Valores y, a continuación, pulse **Compartir**.  

![Compartir un informe](images/uc_insights_sharing.gif).

## Creación de informes de auditoría

Los informes de auditoría muestran una lista completa de todas las actividades que satisfacen los filtros que establezca, por ejemplo, como un PDF. Para crear un informe de auditoría, pulse **Delivery Insights**, pulse el botón de valores y pulse **Crear informe de auditoría**. A continuación, especifique la información para el informe, incluido un nombre. Además, establezca el contexto para el informe, por ejemplo, para una aplicación, un entorno lógico o un entorno en un servidor IBM UrbanCode Deploy (un entorno físico). Desde aquí, seleccione los datos que se deben mostrar en el informe y pulse **Crear**. 

## Resolución de problemas
{: #troubleshooting}

Si muchas solicitudes de proceso de componentes y aplicaciones se almacenan en la base de datos del servidor IBM UrbanCode Deploy, se pueden producir errores durante el proceso de recuperación. Un mensaje similar al siguiente texto se registra en el registro de salida del servidor:

`ORA-01652: no es posible extender el segmento temp en 128 en el espacio de tablas TEMP`

Para solucionar este comportamiento, edite el archivo `plugin.properties` para que el plugin reduzca el número de días de datos útiles a recuperar. El archivo `plugin.properties` se encuentra en el directorio `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` en el sistema en donde se instaló DevOps Connect. Edite la línea siguiente para eliminar el signo de almohadilla (#) y reducir el número de días:

`#numDaysToRetrieve=90`

Por ejemplo, cambie la línea al texto siguiente para recuperar sólo los últimos 30 días de datos:

`numDaysToRetrieve=30`

Guarde el archivo, y, a continuación, ejecute la integración de nuevo. Consulte los registros del servidor para asegurarse de que ya no se produce el error.
