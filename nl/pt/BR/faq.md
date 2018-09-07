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

# FAQ
{: #faqs}

Encontre as respostas para as perguntas mais frequentes sobre como usar o {{site.data.keyword.DRA_full}}.

## Como eu removo dados que o {{site.data.keyword.DRA_short}} extraiu de um repositório?

Mude o filtro de dados do repositório para que ele exclua os dados que você deseja remover. 

Para mudar o filtro de dados do {{site.data.keyword.DRA_short}}, clique em **Configurações** e, em seguida, em **Filtros**. 

## Alguns dos meus problemas desapareceram. Como eu os incluo?

Se o serviço de rastreamento de problemas não fizer parte da cadeia de ferramentas, inclua-o. O {{site.data.keyword.DRA_short}} apenas extrai serviços que façam parte da cadeia de ferramentas. 

Se o serviço de controle de problema faz parte da cadeia de ferramentas, verifique se as etiquetas do {{site.data.keyword.DRA_short}} estão mapeadas para as etiquetas que o seu o serviço usa. Clique em **Configurações**, clique em **Etiquetas** e, em seguida, verifique o mapeamento.

Como um último recurso, remova o serviço de controle de problema de sua cadeia de ferramentas. Em seguida, inclua-o de volta. O {{site.data.keyword.DRA_short}} extrairá o serviço desde o começo. A mineração pode levar algumas horas. 

## Como eu extraio novamente um repositório?

Para extrair novamente um repositório, exclua a integração do {{site.data.keyword.DRA_short}} de sua cadeia de ferramentas. Em seguida, inclua-a de volta.

## Como posso incluir um repositório a ser extraído?

Inclua uma cadeia de ferramentas clicando em **Incluir uma ferramenta** na página de visão geral da cadeia de ferramentas. Após o repositório fazer parte da cadeia de ferramentas, o Insights extrairá novamente os seus dados para incluir esse repositório.

Verifique a caixa **Ativar problemas do GitHub** enquanto inclui um repositório para ativar a mineração de problema. 

## Por que eu não vejo nenhuma compilação ou implementação?

O DevOps Insights minera automaticamente repositórios de código e problemas que são parte de uma cadeia de ferramentas, mas deve-se configurar o seu pipeline para que ele monitore compilações e implementações. 

Primeiro, confirme de você tem um pipeline de Entrega contínua ou Jenkins em sua cadeia de ferramentas. 

Em seguida, verifique se o seu pipeline está configurado para compilação e monitoramento de implementação. Para aprender como configurar o seu pipeline, veja a [Documentação de integração de Entrega contínua](risk_cd.html) ou a [Documentação de integração do Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
