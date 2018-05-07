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

# 常見問題集
{: #faqs}

此頁面是 {{site.data.keyword.DRA_full}} 常見問題集的清單，且經常更新。

## 如何移除 {{site.data.keyword.DRA_short}} 從儲存庫發掘的資料？

請變更儲存庫的資料過濾器，使它排除您想要移除的資料。 

若要變更 {{site.data.keyword.DRA_short}} 的資料過濾器，請按一下**設定**，然後按一下**過濾器**。 

## 我的部分問題遺失了。如何新增？

如果問題追蹤服務不在您的工具鏈當中，請予以新增。{{site.data.keyword.DRA_short}} 只會發掘屬於工具鏈一部分的服務。 

如果問題追蹤服務是您工具鏈的一部分，請確認 {{site.data.keyword.DRA_short}} 的標籤對映到您的服務使用的標籤。請按一下**設定**、**標籤**，然後驗證對映。

在萬不得已時，從您的工具鏈移除問題追蹤服務。然後再將它新增回來。{{site.data.keyword.DRA_short}} 會從頭開始發掘服務。發掘可能會耗時數小時。 

## 如何重新發掘儲存庫？

若要重新發掘儲存庫，請從工具鏈刪除 {{site.data.keyword.DRA_short}} 整合。然後再將它新增回來。

## 如何新增要發掘的儲存庫？

請在工具鏈的概觀頁面按一下**新增工具**，將儲存庫新增到工具鏈。儲存庫成為工具鏈的一部分之後，Insights 會重新發掘您的資料，以包含該儲存庫。

新增儲存庫時請勾選**啟用 GitHub Issues** 方框，以啟用問題發掘。 

## 我為何看不到任何建置或部署？

DevOps Insights 會自動發掘屬於工具鏈一部分的程式碼儲存庫及問題，但您必須配置管線，它才能監視建置及部署。 

首先，請確定您的工具鏈中有 Continuous Delivery 或 Jenkins 管線。 

然後，驗證您的管線已配置進行建置及部署監視。若要了解如何配置管線，請參閱 [Continuous Delivery 整合文件](risk_cd.html)或 [Jenkins 整合文件](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin)。
