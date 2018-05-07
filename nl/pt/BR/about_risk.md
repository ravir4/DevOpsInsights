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

# Sobre o Deployment Risk

O Risco de implementação do {{site.data.keyword.DRA_short}} fornece uma riqueza de informações sobre as suas implementações, especialmente o risco. É possível usá-lo para automatizar a proteção de qualidade em seu pipeline de entrega usando políticas e portas. Ele fornece dados sobre a frequência de construção e implementação, junto com as tendências de cobertura de código e de teste.
{:shortdesc}

Depois de abrir o {{site.data.keyword.DRA_short}} por meio de sua cadeia de ferramentas, clique em **Deployment Risk**. De lá, é possível selecionar uma categoria analítica para mergulhar mais fundo no que está acontecendo com as suas implementações.  

É possível usar o Deployment Risk para utilizar as normas de qualidade em sua cadeia de ferramentas por meio de políticas e portas. As políticas incluem conjuntos de regras; as portas utilizam políticas. Por exemplo, é possível criar uma política "Teste de unidade e Cobertura de teste" que requer que as construções atendam às normas de teste de unidade e de cobertura de teste. Em seguida, você inclui uma porta que se refere à política de seu processo de entrega contínua. As construções que não satisfizerem a política serão paradas nessa porta. 

## Análise de risco

Com a análise de risco, é possível obter uma visão geral dos riscos associados com os aplicativos em seus ambientes de preparação e produção. É possível realizar drill down para entender a cobertura de código, o desempenho de teste e os relatórios de segurança. Os painéis são preenchidos automaticamente com as informações mais recentes dos testes do {{site.data.keyword.DRA_short}} dos pipelines.

## Frequência de implementação

É possível visualizar as tendências de frequência de implementação para os seus ambientes de produção, preparação ou outros. Esta visualização também mostra o sucesso de implementação e as falhas. É possível clicar em uma implementação específica para ver detalhes sobre ela. Se você estiver em uma equipe ágil, deverá ver a tendência de frequência de implementação para cima ao longo do tempo. 

## Frequência de compilação

É possível visualizar as tendências de frequência de compilação para as suas ramificações de longa execução. Esta visualização também mostra sucessos de compilação e falhas. É possível clicar em um ponto de interesse e ver os detalhes da compilação. Se você estiver em uma equipe ágil, desejará ver muitas compilações diárias na ramificação de integração. Caso contrário, a sua equipe não estará mesclando o seu código frequentemente.

## Tendências de teste de unidade

É possível visualizar tendências para testes de unidade para as compilações que são de uma determinada ramificação ou são implementadas em um determinado ambiente. Por exemplo, é possível ver as tendências de teste para compilações da ramificação principal. Se alguns testes falharem para compilações que foram para produção, talvez você queira tomar alguma ação. Além disso, se o número de testes estiver diminuindo ao longo do tempo, isso pode ser um motivo de preocupação.

## Tendências de teste de verificação de função

É possível visualizar tendências para testes de verificação funcionais para as compilações que são de uma determinada ramificação ou são implementadas em um determinado ambiente. Por exemplo, é possível ver as tendências de teste para compilações da ramificação principal. Se alguns testes falharem para compilações que foram para produção, talvez você queira tomar alguma ação. Além disso, se o número de testes estiver diminuindo ao longo do tempo, isso pode ser um motivo de preocupação.

## Tendências de cobertura de código

É possível visualizar as tendências de cobertura de código para as compilações que são implementadas em um determinado ambiente. Por exemplo, é possível ver as tendências de cobertura de código para compilações que foram para produção. Idealmente, você deve ver que a cobertura de código melhora ao longo do tempo para compilações que vão para produção. Se a cobertura de código diminuir, talvez você queira tomar uma ação.

## Políticas

As políticas são conjuntos de regras que controlam as portas em seu pipeline de entrega. Se o seu código não atender nem exceder uma política executada em uma porta específica, a implementação será interrompida para evitar que as mudanças de risco sejam liberadas.


## Pré-Requisitos
{: #prerequisites}

O Deployment Risk requer alguma configuração além daquela descrita em [Introdução ao {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para usar o Deployment Risk, você precisa de duas coisas:

* Uma instância do {{site.data.keyword.deliverypipeline}} ou um projeto Jenkins
* Testes que você deseja usar para avaliar seu projeto

## Informações de integração

O Deployment Risk integra-se ao {{site.data.keyword.deliverypipeline}}, que faz parte do {{site.data.keyword.contdelivery_full}} e a projetos Jenkins. Em um alto nível, as instruções para usar um ou outro são semelhantes.  

Se você estiver usando o {{site.data.keyword.deliverypipeline}}, siga estas etapas:

1. [Crie políticas e regras](risk_policies.html) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Prepare os estágios de seu pipeline](risk_cd.html) para integração ao {{site.data.keyword.DRA_short}}.
3. [Crie ou edite tarefas de teste](risk_cd.html) no pipeline que façam upload de resultados no {{site.data.keyword.DRA_short}}.
4. [Inclua portas](risk_cd.html) no pipeline que tomem decisões de promoção com base nesses resultados e suas políticas.
5. Execute o pipeline e [visualize os resultados](results.html).

Se estiver usando o Jenkins, siga estas etapas:

1. [Crie políticas e regras](risk_policies.html) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Instale e configure o plug-in do Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Crie tarefas de teste e portas conforme descrito nas instruções do plug-in](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). Os testes fazem upload dos resultados no {{site.data.keyword.DRA_short}} para análise e as portas usam esses resultados para tomar decisões de promoção.
4. Execute o projeto e [visualize os resultados](results.html). 

Independentemente de como você construir e implementar seu código, os resultados serão os mesmos: as construções que atenderem às normas serão movidas depois das portas do Deployment Risk e as construções que não atenderem às normas serão paradas. 
