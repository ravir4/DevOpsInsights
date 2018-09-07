---

copyright:
  years:  2018
lastupdated: "2018-7-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 使用 Identity and Access Management 管理用户访问权

{{site.data.keyword.DRA_full}} 服务将访问权控制委派给它绑定到的工具链。在 Cloud Foundry 组织中或资源组中，用户可以将 {{site.data.keyword.DRA_short}} 用于工具链。 

在 Cloud Foundry 组织中，如果用户是该组织的成员，就可以将 {{site.data.keyword.DRA_short}} 用于工具链。

在资源组中，如果为用户分配了 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 策略，该策略授予任何查看者、操作员、编辑者或管理员角色，并且该策略适用于它所属的工具链或资源组，那么该用户可以将 {{site.data.keyword.DRA_short}} 用于工具链。

有关资源组中工具链访问控制的更多信息，请参阅[管理资源组中对工具链的访问权](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_resource_groups)。有关 Cloud Foundry 组织中工具链访问控制的更多信息，请参阅[管理 Cloud Foundry 组织中对工具链的访问权](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_orgs)。
