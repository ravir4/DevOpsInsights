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

# 管理 DevOps Insights 中的个人数据
{: insights_personal_data}

您可以删除在 {{site.data.keyword.DRA_full}} 中收集和存储的个人数据。
{: shortdesc}

{{site.data.keyword.DRA_short}} 中存储的数据通过工具链标识建立索引。删除工具链时，将删除与作为工具链一部分而收集的存储库的所有相关数据。

IBM 不会管理 {{site.data.keyword.DRA_short}} 服务中的数据。在离开 {{site.data.keyword.DRA_short}} 服务之前，必须先删除自己的数据。要删除数据，请从工具链中删除 {{site.data.keyword.DRA_short}} 工具集成。如果 {{site.data.keyword.DRA_short}} 工具集成未在七天之内再次添加到该工具链，那么数据会被删除。
{: tip}

## 删除 {{site.data.keyword.DRA_short}} 中的数据 
{: #insights_delete_data}

下表列出了删除 {{site.data.keyword.DRA_short}} 中数据的方案，并描述其如何影响每种 {{site.data.keyword.DRA_short}} 类别。

|  |Developer Insights 和 Team|Deployment Risk|Security Insights |
|---------|-------------|-------------|-------------|
|[删除存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window}|	删除与存储库相关的所有数据。|不适用|不适用|
|[删除 {{site.data.keyword.DRA_short}} 工具集成 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window}|	删除与存储库相关的所有数据。|删除与工具集成所属的工具链关联的所有数据。|删除与工具集成所属的工具链关联的存储库的所有相关所有数据。|
|[删除工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window}|删除与工具链关联的存储库的所有相关数据。|删除与工具链关联的所有数据。|删除与工具链关联的所有数据。|
|[删除管道 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window}|不适用|不适用|不适用|
{:caption="表 1. 数据删除方案" caption-side="top"}

## 删除 {{site.data.keyword.DRA_short}} 工具集成
{: #insights_delete_integration}

如果从工具链中删除工具集成，此删除操作将无法撤销。

1. 在 DevOps 仪表板的**工具链**页面上，单击工具链来打开其“概述”页面。或者，在应用程序“概述”页面的 Continuous Delivery 卡上，单击**查看工具链**，然后单击**概述**。
1. 在要删除的 {{site.data.keyword.DRA_short}} 工具集成的卡上，单击菜单以访问配置选项。
1. 要从工具链中删除工具集成，请单击**删除**。

  ![配置菜单](images/delete_insights_integration.png)

1. 单击**删除**以确认。 
