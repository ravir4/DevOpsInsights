---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Sobre o Delivery Insights
{: #about_delivery}

O Delivery Insights, uma parte do {{site.data.keyword.DRA_short}}, mostra estatísticas de implementação, métricas e outras informações sobre a instalação do IBM UrbanCode Deploy. Por exemplo, ele pode mostrar gráficos de duração da implementação, sucessos e falhas, todos classificados por ambientes agrupados logicamente.
{:shortdesc}

O Delivery Insights requer uma instalação do DevOps Connect. Para obter informações de configuração, consulte [Mostrando dados de servidores IBM UrbanCode Deploy](uc_insights_connect_ucd.html).

![Dois gráficos dos dados demo do UrbanCode Insights](images/uc_insights_demo_data.gif)

Algumas das informações que podem ser vistas no Delivery Insights incluem:

- Estatísticas sobre implementação, incluindo a duração da implementação e o volume de implementação ao longo do tempo.
- Estatísticas sobre a taxa de falha da implementação por aplicativo e ambiente.
- Estatísticas sobre a implementação do componente, incluindo taxa de falha, tempo de implementação e duração.

## Visão geral dos sistemas
{: #systems_overview}

A topologia para o Delivery Insights inclui uma ou mais instalações locais do IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> e o utilitário DevOps Connect.

O diagrama a seguir mostra uma instalação típica desses sistemas.

![Visão geral da topologia para o UrbanCode Insights, incluindo sistemas locais do cliente e o IBM Cloud Services](images/uc_insights_overview_topology_multi_ucd.png)

- Uma instalação do **IBM UrbanCode Deploy** fornece as informações sobre implementações bem-sucedidas e com falha das métricas. O IBM UrbanCode Deploy requer uma correção para se comunicar com o IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, anteriormente o IBM UrbanCode Sync Utility, coordena a comunicação entre as instalações locais do IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> e os serviços hospedados pela IBM, como o UrbanCode Insights. O DevOps Connect usa a comunicação HTTPS segura para os servidores locais e a autenticação do token para fornecer dados para o UrbanCode Insights.

  O DevOps Connect requer plug-ins para se conectar aos outros sistemas na topologia.

- O **Delivery Insights**, parte do {{site.data.keyword.DRA_short}}, fornece métricas sobre a atividade de implementação no IBM UrbanCode Deploy, incluindo os tempos de implementação e as taxas de falha, de acordo com grupos de ambientes. A autorização é controlada pelas contas do {{site.data.keyword.Bluemix}}.
