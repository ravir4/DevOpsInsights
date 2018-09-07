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

# 入门教程 (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} 将开发者、团队和部署分析应用于您最繁忙的 DevOps 项目。使用 DevOps Insights 可了解团队在多大程度上遵循 DevOps 和开发者实践，也可管理代码库中的风险，以及在 Continuous Delivery 项目中自动强制实施质量标准。
{:shortdesc}

{{site.data.keyword.DRA_short}} 仅在美国南部区域可用。
{: tip}

要使用 {{site.data.keyword.DRA_short}}，必须将其添加到工具链。许多工具链模板已经包含 {{site.data.keyword.DRA_short}}。另外，确保[将其作为服务添加到 {{site.data.keyword.Bluemix_notm}} 资源组或组织](/docs/services/reqnsi.html)，这样才能在 {{site.data.keyword.Bluemix_notm}}“仪表板”中查看有关 {{site.data.keyword.DRA_short}} 的信息，并访问包含它的某些工具链模板。  

## 步骤 1：将 DevOps Insights 添加到工具链
{: #catalog}

通过与 {{site.data.keyword.contdelivery_full}} 工具链集成提供了 {{site.data.keyword.DRA_short}}。通过从工具集成目录中选择 {{site.data.keyword.DRA_short}}，可以将其添加到任何工具链。

{{site.data.keyword.DRA_short}} 是许多工具链模板的一部分。如果要通过包含 {{site.data.keyword.DRA_short}} 的模板创建工具链，请确保 {{site.data.keyword.DRA_short}} 设置为**高级**。然后，创建工具链，并跳至[步骤 2](/docs/services/DevOpsInsights/index.html#using)。
{: tip}

1. 单击**添加工具**。

2. 单击 **{{site.data.keyword.DRA_short}}**。

3. 单击**创建集成**。

现在，{{site.data.keyword.DRA_short}} 在工具链的“概述”页面上可用。此时，将自动扫描存储库和问题跟踪系统，以获取相关数据。 

## 步骤 2：探索项目数据
{: #using}

如果工具链包含 GitHub、GitLab 或 JIRA，那么在一些初始数据收集和分析后，{{site.data.keyword.DRA_short}} 会自动提供有关您代码库和团队的信息。如果工具链不包含其中任何集成，请添加其中一个集成。
{: tip}

1. 在工具链的“概述”页面中，单击 **{{site.data.keyword.DRA_short}}**。

2. 单击 **Team** 或 **Developer Insights**，然后选择数据类别。 

3. 通过查看该数据类别中的仪表板，探索项目数据。如果要了解有关图或可使用图中信息执行哪些操作的更多信息，请单击**信息**或**指导**。

## 后续步骤
{: #next_steps}

探索 Team 和 Developer Insights 后，请配置 [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) 以帮助您强制实施代码质量。Deployment Risk 与 Delivery Pipeline for {{site.data.keyword.contdelivery_short}} 和 Jenkins 兼容。
