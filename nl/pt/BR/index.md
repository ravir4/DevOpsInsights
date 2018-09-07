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

# Tutorial de introdução (Beta)
{: #gettingstarted}

O {{site.data.keyword.DRA_full}} aplica análise de desenvolvedor, de equipe e de implementação a seus projetos DevOps mais ocupados. Use-o para saber quanto sua equipe é compatível com o DevOps e com as práticas do desenvolvedor, para gerenciar risco em seu código base e para aplicar normas de qualidade automaticamente em projetos de entrega contínua. 
{:shortdesc}

O {{site.data.keyword.DRA_short}} está disponível somente na região Sul dos EUA.
{: tip}

Para usar o {{site.data.keyword.DRA_short}}, deve-se incluí-lo em uma cadeia de ferramentas. Muitos modelos de cadeia de ferramentas já incluem o {{site.data.keyword.DRA_short}}. Certifique-se de também [incluí-lo em seu grupo de recursos ou organização do {{site.data.keyword.Bluemix_notm}} como um serviço](/docs/services/reqnsi.html), para que seja possível ver informações sobre o {{site.data.keyword.DRA_short}} e acessar alguns dos modelos de cadeia de ferramentas que o incluem no seu painel do {{site.data.keyword.Bluemix_notm}}.  

## Etapa 1: incluir o DevOps Insights em uma cadeia de ferramentas
{: #catalog}

O {{site.data.keyword.DRA_short}} está disponível por meio de integração com as cadeias de ferramentas do {{site.data.keyword.contdelivery_full}}. É possível incluir o {{site.data.keyword.DRA_short}} em qualquer cadeia de ferramentas, selecionando-o no catálogo de integração de ferramenta.

O {{site.data.keyword.DRA_short}} faz parte de vários modelos de cadeia de ferramentas. Se você criar uma cadeia de ferramentas por meio de um modelo que inclui o {{site.data.keyword.DRA_short}}, certifique-se de que o {{site.data.keyword.DRA_short}} esteja configurado como **Avançado**. Em seguida, crie a cadeia de ferramentas e vá para a [Etapa 2](/docs/services/DevOpsInsights/index.html#using).
{: tip}

1. Clique em **Incluir uma ferramenta**.

2. Clique em **{{site.data.keyword.DRA_short}}**.

3. Clique em
**Criar integração**.

O {{site.data.keyword.DRA_short}} está agora disponível na página Visão geral de sua cadeia de ferramentas. Seu repositório e o sistema de rastreamento de problemas são varridos automaticamente para dados. 

## Etapa 2: explore os dados do seu projeto
{: #using}

Se a sua cadeia de ferramentas incluir GitHub, GitLab ou JIRA, o {{site.data.keyword.DRA_short}} fornecerá informações automaticamente sobre seu código base e equipe após alguma reunião e análise de dados iniciais. Se a sua cadeia de ferramentas não incluir nenhuma dessas integrações, inclua uma delas.
{: tip}

1. Na página Visão geral da cadeia de ferramentas, clique em **{{site.data.keyword.DRA_short}}**.

2. Clique em **Equipe ** ou **Developer Insights** e, em seguida, escolha uma categoria de dados. 

3. Explore os dados de seu projeto visualizando os painéis na categoria de dados. Se desejar saber mais sobre um gráfico ou o que você poderia fazer com suas informações, clique em **Informações** ou **Orientação**.

## Próximos passos
{: #next_steps}

Depois de explorar o Team and Developer Insights, configure [Risco de implementação](/docs/services/DevOpsInsights/about_risk.html) para ajudá-lo a cumprir a qualidade de código. O Deployment Risk é compatível com o Delivery Pipeline para {{site.data.keyword.contdelivery_short}} e Jenkins.
