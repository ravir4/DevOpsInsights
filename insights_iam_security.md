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


# Managing user access with Identity and Access Management

The {{site.data.keyword.DRA_full}} service delegates access control to the toolchain that it is bound to. A user can use {{site.data.keyword.DRA_short}} for a toolchain in a Cloud Foundry org or in a resource group. 

A user can use {{site.data.keyword.DRA_short}} with a toolchain in a Cloud Foundry org if they are a member of that org.

A user can use {{site.data.keyword.DRA_short}} with a toolchain in a resource group if they are assigned an {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) policy that grants any of the Viewer, Operator, Editor, or Administrator roles, and that policy is applied to the toolchain or the resource group that it is part of.

For more information about access control for toolchains in resource groups, see [Managing access to toolchains in resource groups](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_resource_groups). For more information about access control for toolchains in Cloud Foundry orgs, see [Managing access to toolchains in Cloud Foundry orgs](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access_orgs).
