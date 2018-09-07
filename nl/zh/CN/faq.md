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

# 常见问题
{: #faqs}

获取有关使用 {{site.data.keyword.DRA_full}} 的常见问题的答案。

## 如何除去 {{site.data.keyword.DRA_short}} 从存储库中挖掘的数据？

更改存储库数据过滤器，以排除要除去的数据。 

要更改 {{site.data.keyword.DRA_short}} 的数据过滤器，请单击**设置**，然后单击**过滤器**。 

## 我的一些问题不见了。该如何进行添加？

如果问题跟踪服务不是工具链的一部分，请添加该服务。{{site.data.keyword.DRA_short}} 仅挖掘属于工具链的服务。 

如果问题跟踪服务是工具链的一部分，请检查 {{site.data.keyword.DRA_short}} 的标签是否映射到该服务使用的标签。单击**设置** > **标签**，然后验证映射。

最后一个办法是，先从工具链中除去问题跟踪服务。然后，重新添加该服务。这样，{{site.data.keyword.DRA_short}} 将从头开始挖掘该服务。挖掘过程可能需要数个小时。 

## 如何重新挖掘存储库？

要重新挖掘存储库，请删除工具链中的 {{site.data.keyword.DRA_short}} 集成。然后，重新添加该服务。

## 如何添加要挖掘的存储库？

通过单击工具链的“概述”页面上的**添加工具**，将所需存储库添加到工具链。在存储库成为工具链的一部分后，Insights 将重新挖掘数据以包含该存储库。

在添加存储库以支持问题挖掘时，选中**启用 GitHub Issues** 框。 

## 为什么我看不到任何构建或部署？

DevOps Insights 会自动挖掘作为工具链一部分的代码存储库和问题，但是您必须为其配置管道才能监视构建和部署。 

首先，确保工具链中具有 Continuous Delivery 或 Jenkins Pipeline。 

然后，验证是否已将管道配置用于监视构建和部署。要了解如何配置管道，请参阅 [Continuous Delivery 集成文档](risk_cd.html)或 [Jenkins 集成文档](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin)。
