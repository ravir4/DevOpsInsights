---

copyright:
  years: 2018
lastupdated: "2018-8-2"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Gerenciando dados pessoais no DevOps Insights
{: insights_personal_data}

É possível excluir dados pessoais que são coletados e armazenados no {{site.data.keyword.DRA_full}}.
{: shortdesc}

Os dados armazenados no {{site.data.keyword.DRA_short}} são indexados pelo ID da cadeia de ferramentas. Quando você excluir uma cadeia de ferramentas, todos os dados relacionados ao repositório que foi coletado como parte da cadeia de ferramentas serão excluídos.

A IBM não gerencia dados no serviço {{site.data.keyword.DRA_short}}. Antes de sair do serviço {{site.data.keyword.DRA_short}}, exclua seus próprios dados. Para excluir seus dados, exclua a integração de ferramenta do {{site.data.keyword.DRA_short}} de sua cadeia de ferramentas. Se a integração de ferramenta do {{site.data.keyword.DRA_short}} não for incluída novamente na cadeia de ferramentas dentro de sete dias, os dados serão excluídos.
{: tip}

## Excluindo dados do {{site.data.keyword.DRA_short}}
{: #insights_delete_data}

A tabela a seguir lista os cenários para excluir dados do {{site.data.keyword.DRA_short}} e descreve como eles impactam cada uma das categorias do {{site.data.keyword.DRA_short}}.

|  | Developer and Team Insights | Perigo De disposição | Insights de segurança |
|---------|-------------|-------------|-------------|
| [Excluindo um repositório ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	Todos os dados que estiverem relacionados ao repositório serão excluídos.  | N/A | N/A |
| [Excluindo uma integração de ferramenta do {{site.data.keyword.DRA_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	Todos os dados que estiverem relacionados ao repositório serão excluídos.  | Todos os dados que estiverem associados com a cadeia de ferramentas da qual a integração de ferramenta faz parte serão excluídos. | Todos os dados relacionados ao repositório que estiver associado à cadeia de ferramentas da qual a integração de ferramenta faz parte serão excluídos.  |
| [Excluindo uma cadeia de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | Todos os dados relacionados ao repositório que estiver associado à cadeia de ferramentas serão excluídos. | Todos os dados que estiverem associados com a cadeia de ferramentas serão excluídos.  | Todos os dados que estiverem associados com a cadeia de ferramentas serão excluídos. |
| [Excluindo um pipeline ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/A | N/A | N/A |
{:caption="Tabela 1. Cenários de exclusão de dados" caption-side="top"}

## Excluindo uma integração de ferramenta do {{site.data.keyword.DRA_short}}
{: #insights_delete_integration}

Se você excluir uma integração de ferramenta a partir de sua cadeia de ferramentas, a exclusão não poderá ser desfeita.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. No cartão para a integração de ferramenta do {{site.data.keyword.DRA_short}} que você deseja excluir, clique no menu para acessar as opções de configuração.
1. Para excluir a integração de ferramenta de sua cadeia de ferramentas, clique em **Excluir**.

  ![Menu de configuração](images/delete_insights_integration.png)

1. Confirme clicando em **Excluir**. 
