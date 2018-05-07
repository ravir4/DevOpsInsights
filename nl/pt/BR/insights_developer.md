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

# Developer Insights
{: #gettingstarted}

O {{site.data.keyword.DRA_full}} Developer Insights fornece uma maneira abrangente de explorar o risco de desenvolvimento de seu projeto. É possível identificar arquivos com alta tendência de erro e obter uma visão da conformidade do projeto com relação às práticas de DevOps.
{:shortdesc}

Depois de abrir o {{site.data.keyword.DRA_short}} por meio de sua cadeia de ferramentas, clique em **Developer Insights**. Daí, é possível selecionar uma categoria de analítica para pesquisar detalhadamente o código base de seu projeto. O que cada conjunto de dados indica pode variar de equipe para equipe e será possível realizar drill down em cada visualização para ajuda e orientação.

## Categorias de Dados
Os dados que o {{site.data.keyword.DRA_short}} usa para preencher seus painéis são extraídos automaticamente do repositório de controle de fonte de sua equipe. É possível obter mais informações sobre o que os dados significam e como podem ser aplicados a seu projeto clicando em **Informações** ou **Orientação** em qualquer gráfico.

### Melhores práticas do desenvolvedor

O Developer Insights fornece vários gráficos que medem seu projeto com relação às boas práticas do DevOps e do desenvolvedor. Use essa categoria para obter uma visualização de alto nível de maturidade, funcionamento e eficiência do seu projeto.

### Problemas

A categoria Problemas exibe todos os problemas de rastreamento de trabalho de sua equipe em um local. Os problemas são agrupados automaticamente por tipo, prioridade e identificação e podem ser mostrados ao longo do tempo.

O significado desses agrupamentos de problemas pode variar de equipe para equipe. Uma equipe pode querer saber se a maioria dos itens identificados para uma liberação específica está fechada, enquanto outra equipe pode não identificar liberações e, como alternativa, trabalhar de acordo com a prioridade de problema em aberto.  

### Compromissos

As confirmações indicam o trabalho com o qual os membros de sua equipe estão contribuindo com seu código base. Examine seus dados de confirmação para entender onde o esforço está sendo gasto historicamente e como balancear melhor as cargas de trabalho dos membros de sua equipe.

### Solicitações pull

As solicitações pull mostram o código que os seus membros da equipe estão mesclando em uma outra ramificação. Mergulhe em seus dados de solicitação pull para entender os riscos associados com a inclusão de um novo código em sua ramificação de código nova.

### Arquivos

A categoria Arquivos mostra quais dos arquivos de seu projeto são os mais ocupados. Seja pelo número de mudanças de linha, confirmações, autores ou defeitos, esses dados indicam onde sua equipe está mais ativa. Além disso, é possível ver qual é o risco em seus arquivos revisando a guia de propensão a erros de arquivos.

Geralmente, tente reduzir o número de mãos que tocam um arquivo e a frequência de mudança desse arquivo. Esse objetivo pode ser impossível com determinados arquivos, como arquivos de configuração comuns. No entanto, muitos desenvolvedores fazendo muitas mudanças no mesmo arquivo ao mesmo tempo é uma receita para problemas.

**Nota**: o DevOps Insights ignora arquivos com estas extensões:

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
