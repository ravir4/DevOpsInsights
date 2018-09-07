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

# 入門指導教學（測試版）
{: #gettingstarted}

{{site.data.keyword.DRA_full}} 將開發人員、團隊和部署分析套用至您最忙碌的 DevOps 專案。您可以用它來瞭解團隊符合 DevOps 和開發人員作法的程度、管理程式碼庫中的風險，以及在持續交付專案中自動強制執行品質標準。
{:shortdesc}

{{site.data.keyword.DRA_short}} 只提供於美國南部地區。
{: tip}

若要使用 {{site.data.keyword.DRA_short}}，您必須將它新增至工具鏈。許多工具鏈範本都已包括 {{site.data.keyword.DRA_short}}。此外，也務必[將它新增至 {{site.data.keyword.Bluemix_notm}} 資源群組或組織作為服務](/docs/services/reqnsi.html)，讓您能夠查看 {{site.data.keyword.DRA_short}} 的相關資訊，以及從 {{site.data.keyword.Bluemix_notm}} 儀表板存取包括它的一些工具鏈範本。  

## 步驟 1：將 DevOps Insights 新增至工具鏈
{: #catalog}

{{site.data.keyword.DRA_short}} 可以透過與 {{site.data.keyword.contdelivery_full}} 工具鍊的整合而取得。您可以從工具整合型錄中選取 {{site.data.keyword.DRA_short}}，以將它新增至任何工具鏈。

{{site.data.keyword.DRA_short}} 是許多工具鏈範本的一部分。如果您要從包括 {{site.data.keyword.DRA_short}} 的範本建立工具鏈，請確定 {{site.data.keyword.DRA_short}} 設為**進階**。然後，建立工具鏈，並跳至[步驟 2](/docs/services/DevOpsInsights/index.html#using)。
{: tip}

1. 按一下**新增工具**。

2. 按一下 **{{site.data.keyword.DRA_short}}**。

3. 按一下**建立整合**。

現在即可在工具鏈的「概觀」頁面上使用 {{site.data.keyword.DRA_short}}。會自動掃描您的儲存庫和問題追蹤系統是否有資料。 

## 步驟 2：探索專案資料
{: #using}

如果您的工具鏈包括 GitHub、GitLab 或 JIRA，{{site.data.keyword.DRA_short}} 會在進行一些起始資料收集及分析之後，自動提供程式碼庫和團隊的相關資訊給您。如果工具鏈不包括上述任何整合，請新增其中一項。
{: tip}

1. 從工具鏈的「概觀」頁面中，按一下 **{{site.data.keyword.DRA_short}}**。

2. 按一下 **Team** 或 **Developer Insights**，然後選擇一個資料種類。 

3. 檢視該資料種類中的儀表板，以探索專案的資料。如果您要進一步瞭解某個圖形，或是瞭解可以使用其資訊做什麼，請按一下**資訊**或**指引**。

## 後續步驟
{: #next_steps}

探索 Team 和 Developer Insights 之後，請配置 [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html)，以協助您強制執行程式碼品質。Deployment Risk 與 {{site.data.keyword.contdelivery_short}} 和 Jenkins 都相容。
