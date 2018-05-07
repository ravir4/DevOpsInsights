---

copyright:
  years: 2016, 2018
lastupdated: "2018-4-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao DevOps Insights (Beta)
{: #gettingstarted}

O {{site.data.keyword.DRA_full}} aplica análise de desenvolvedor, de equipe e de implementação a seus projetos DevOps mais ocupados. Use-o para saber quanto sua equipe é compatível com o DevOps e com as práticas do desenvolvedor, para gerenciar risco em seu código base e para aplicar normas de qualidade automaticamente em projetos de entrega contínua.
{:shortdesc}

**Nota**: o {{site.data.keyword.DRA_short}} está disponível apenas na região sul dos Estados Unidos.

O {{site.data.keyword.DRA_short}} inclui vários grupos de recursos:

   * O Developer Insights fornece uma maneira abrangente de explorar a maturidade de desenvolvimento de seu projeto. É possível identificar arquivos com alta propensão a erros e obter uma visualização de conformidade do projeto com relação às práticas do desenvolvedor.

   * A equipe usa a análise de código social para ajudá-lo a aprender como a sua equipe colabora e entender como ela pode funcionar melhor.

   * Risco de Implementação é como uma rede de segurança para entrega contínua. Ele analisa os resultados dos testes de unidade, testes funcionais, varreduras de segurança, varreduras de aplicativos e ferramentas de cobertura de código em portas especificadas em seu processo de implementação e impede que as mudanças de risco sejam liberadas. Ele mostra gráficos de tendências na cobertura de código, construções e implementações.

O {{site.data.keyword.DRA_short}} é uma integração no catálogo de cadeia de ferramentas aberta do Bluemix. Para obter mais informações sobre cadeias de ferramentas, veja [Trabalhando com cadeias de ferramentas](/docs/services/ContinuousDelivery/toolchains_working.html).

Para usar o {{site.data.keyword.DRA_short}}, deve-se incluí-lo em uma cadeia de ferramentas. Muitos modelos de cadeia de ferramentas já incluem o {{site.data.keyword.DRA_short}}. Certifique-se de também [incluí-lo em sua organização do {{site.data.keyword.Bluemix_notm}} como um serviço](/docs/services/reqnsi.html) para que você possa ver informações sobre o {{site.data.keyword.DRA_short}} e acessar alguns dos modelos de cadeia de ferramentas que o incluem por meio do painel do {{site.data.keyword.Bluemix_notm}}.  

Além disso, a IBM executa o Insights Developer and Team com relação a muitos dos projetos de software livre mais bem-sucedidos no GitHub. Acesse [DevOpsInsights.io](http://devopsinsights.io/) para ver os seus dados de desenvolvimento e da equipe.

## Incluindo o DevOps Insights em uma cadeia de ferramentas
{: #catalog}

O {{site.data.keyword.DRA_short}} está disponível por meio de integração com as cadeias de ferramentas do {{site.data.keyword.contdelivery_full}}. É possível incluir o {{site.data.keyword.DRA_short}} em qualquer cadeia de ferramentas, selecionando-o no catálogo de integração de ferramenta.

O {{site.data.keyword.DRA_short}} também faz parte de vários modelos da cadeia de ferramentas. Se você criar uma cadeia de ferramentas por meio de um modelo que inclui o {{site.data.keyword.DRA_short}}, certifique-se de que o {{site.data.keyword.DRA_short}} esteja configurado como **Avançado**. Em seguida, crie a cadeia de ferramentas e vá para [Usando o Insights](/docs/services/DevOpsInsights/index.html#using).

Para incluir o {{site.data.keyword.DRA_short}} em uma cadeia de ferramentas:

1. Clique em **Incluir uma ferramenta**.

2. Clique em **{{site.data.keyword.DRA_short}}**.

3. Clique em
**Criar integração**.

O {{site.data.keyword.DRA_short}} está agora disponível na página Visão geral de sua cadeia de ferramentas. Seu repositório e o sistema de rastreamento de problemas são varridos automaticamente para dados.

## Usando o DevOps Insights
{: #using}

Se a sua cadeia de ferramentas incluir GitHub, GitLab ou JIRA, o {{site.data.keyword.DRA_short}} fornecerá informações automaticamente sobre seu código base e equipe após alguma reunião e análise de dados iniciais. Se a sua cadeia de ferramentas não incluir nenhuma dessas integrações, inclua uma delas e, em seguida, siga estas etapas:

1. Na página Visão geral da cadeia de ferramentas, clique em **{{site.data.keyword.DRA_short}}**.

2. Clique em **Equipe ** ou **Developer Insights** e, em seguida, escolha uma categoria de dados.

3. Explore os dados de seu projeto visualizando os painéis na categoria de dados. Se desejar saber mais sobre um gráfico ou o que você poderia fazer com suas informações, clique em **Informações** ou **Orientação**.

Depois de explorar o Team and Developer Insights, configure [Risco de implementação](/docs/services/DevOpsInsights/about_risk.html) para ajudá-lo a cumprir a qualidade de código. O Deployment Risk é compatível com o Delivery Pipeline para {{site.data.keyword.contdelivery_short}} e Jenkins.
