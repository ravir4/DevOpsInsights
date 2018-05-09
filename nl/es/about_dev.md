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

# Acerca de Developer Insights
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Developer Insights proporciona una forma averiguar el riesgo en el desarrollo de un proyecto. Permite identificar los archivos más propensos a contener errores y obtener una vista de conformidad del proyecto con relación a los procedimientos de DevOps.
{:shortdesc}

Después de abrir {{site.data.keyword.DRA_short}} desde la cadena de herramientas, pulse **Developer Insights**. Desde allí, puede seleccionar una categoría analítica para profundizar en el codebase del proyecto. Lo que indica cada conjunto de datos puede variar de equipo a equipo. Podrá profundizar en cada visualización para obtener ayuda e información. Puede filtrar los datos por fecha y por muchos otros criterios.

## Categorías de datos
Los datos que utiliza {{site.data.keyword.DRA_short}} para llenar sus paneles de control se extraen automáticamente desde el repositorio de control de código fuente del equipo. Podrá obtener más información sobre lo que significan los datos y cómo se aplican a su proyecto pulsando **Información** o **Instrucciones** en los diagramas de prácticas recomendadas. Para obtener más información, también puede consultar los resultados y los detalles que forman parte de las demás visualizaciones.

### Prácticas recomendadas para los desarrolladores

Developer Insights proporciona una serie de diagramas que evalúan su proyecto con relación a las prácticas recomendadas para los desarrolladores y DevOps. Utilice esta categoría para obtener una visión de alto nivel de la madurez, salud y eficacia de su proyecto.

### Problemas

La categoría de Problemas visualiza todos los problemas de seguimiento de trabajo del equipo en un único lugar. Los problemas se agrupan automáticamente según el tipo, la prioridad y las etiquetas, y se pueden mostrar a lo largo del tiempo.

Estas agrupaciones de problemas pueden tener un significado diferente para cada equipo. Un equipo podría querer saber si se han cerrado la mayoría de los elementos etiquetados para un release concreto, mientras que otro equipo podría no querer etiquetar releases y, en su lugar, trabajar de acuerdo a la prioridad de los problemas abiertos.  

### Confirmaciones

En la categoría Confirmaciones se visualizan todas las confirmaciones del equipo en un único lugar. Las confirmaciones se agrupan automáticamente según el tipo, las etiquetas y los cambios de línea. Puede visualizarlas durante el periodo de tiempo que elija.

Las confirmaciones indican el trabajo que los miembros del equipo aportan al codebase. Examine los datos de las confirmaciones para entender dónde se ha realizado históricamente el esfuerzo y cómo equilibrar mejor las cargas de trabajo de los miembros del equipo.

### Archivos

La categoría de Archivos muestra cuáles de los archivos del proyecto son los más activos. Los cambios en el número de líneas, las confirmaciones o los defectos indican dónde es más activo el equipo.

Habitualmente, se debe intentar reducir el número de personas que trabajan en un archivo y la frecuencia de cambios en los archivos. Este objetivo puede ser imposible con determinados archivos, como por ejemplo los archivos de configuración comunes. Sin embargo, muchos desarrolladores realizando muchos cambios en el mismo archivo al mismo tiempo puede dar lugar a problemas.

### Solicitudes de extracción

La categoría Solicitudes de extracción muestra las solicitudes de extracción del equipo en un mismo lugar. Se evalúa la propensión a errores de las solicitudes de extracción mediante el aprendizaje de máquina. Puede comprobar rápidamente qué solicitudes de extracción suponen un riesgo para el codebase.

Las solicitudes de extracción muestran el trabajo que los miembros del equipo intentan incorporar al codebase.  Examine los datos de las solicitudes de extracción para conocer todos los riesgos asociados con ellas y saber cómo mitigarlos en el futuro.

## Filtrado de extensiones de archivo

DevOps Insights omite los archivos con estas extensiones:

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml
