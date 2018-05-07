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

# 關於 Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk 針對部署提供豐富的相關資訊，尤其是風險。您可以利用它，透過原則和閘道將 Delivery Pipeline 中的品質保護作業自動化。它會提供關於建置及部署頻率的資料，以及程式碼涵蓋面及測試趨勢。
{:shortdesc}

從工具鏈開啟 {{site.data.keyword.DRA_short}} 之後，按一下 **Deployment Risk**。您可以從這裡選取分析種類，以深入分析部署發生什麼事。  

Deployment Risk 可讓您透過原則和閘道，在工具鏈中強制執行品質標準。原則包含規則集；閘道可強制執行原則。例如，您可以建立「單元測試和測試涵蓋面」原則，要求建置需符合單元測試和測試涵蓋面標準。然後，將參照該原則的閘道新增至持續交付程序。不符合原則的建置會在該閘道被阻擋下來。 

## 風險分析

使用風險分析，您會得到與編譯打包及正式作業環境中之應用程式相關聯的風險概觀。您可以往下探查，以瞭解程式碼涵蓋面、測試效能和安全報告。儀表板會自動移入管線的 {{site.data.keyword.DRA_short}} 測試中的最新資訊。

## 部署頻率

您可以檢視正式作業、編譯打包或其他環境的部署頻率趨勢。此視圖也會顯示部署成功及失敗。您可以按一下特定部署來看到它的詳細資料。如果您身在敏捷團隊中，您應該看到一段時間的部署頻率趨勢。 

## 建置頻率

您可以檢視長時間執行分支的建置頻率趨勢。此視圖也會顯示建置成功及失敗。您可以按一下有興趣的點，查看建置詳細資料。如果您身在敏捷團隊中，您會想看到整合分支上的眾多每日建置。否則，您的團隊便未經常合併程式碼。

## 單元測試趨勢

您可以針對來自特定分支或是部署到特定環境的建置，檢視其單元測試的趨勢。例如，您可以查看來自主要分支之建置的測試趨勢。如果已經正式作業的建置有部分測試失敗，建議您採取某個行動。此外，如果測試的數目隨時間減少，那可能是要考量的原因。

## 功能驗證測試趨勢

您可以針對來自特定分支或是部署到特定環境的建置，檢視其功能驗證測試的趨勢。例如，您可以查看來自主要分支之建置的測試趨勢。如果已經正式作業的建置有部分測試失敗，建議您採取某個行動。此外，如果測試的數目隨時間減少，那可能是要考量的原因。

## 程式碼涵蓋面趨勢

您可以針對部署到特定環境的建置，檢視其程式碼涵蓋面趨勢。例如，您可以針對正式作業的建置查看其程式碼涵蓋面趨勢。在理想情況下，您應該看到正式作業的建置程式碼涵蓋面會隨時間改善。如果程式碼涵蓋面縮減，建議您採取動作。

## 原則

原則是在交付管線中用來控制閘道的規則集。如果您的程式碼不符合或超出特定閘道制定的原則，則會中止部署，以防止釋出有風險的變更。


## 必要條件
{: #prerequisites}

除了[開始使用 {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) 中所說明的內容，Deployment Risk 還需要一些配置。

若要使用 Deployment Risk，您需要以下兩項：

* {{site.data.keyword.deliverypipeline}} 實例或 Jenkins 專案
* 您要用來評估專案的測試

## 整合資訊

Deployment Risk 會與 {{site.data.keyword.deliverypipeline}}（隸屬於 {{site.data.keyword.contdelivery_full}}）和 Jenkins 專案整合。使用其中任一項的方法大致都相同。  

如果是使用 {{site.data.keyword.deliverypipeline}}，請遵循下列步驟：

1. [建立原則和規則](risk_policies.html)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [準備管線的階段](risk_cd.html)，以與 {{site.data.keyword.DRA_short}} 整合。
3. 在管線中[建立或編輯測試工作](risk_cd.html)，以將結果上傳至 {{site.data.keyword.DRA_short}}。
4. [新增閘道](risk_cd.html)至管線，以根據那些結果和您的原則來制定升級決策。
5. 執行管線並[檢視結果](results.html)。

如果是使用 Jenkins，請遵循下列步驟：

1. [建立原則和規則](risk_policies.html)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [安裝並配置 Jenkins 外掛程式](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin)。
3. [依照外掛程式指示的說明來建立測試工作和閘道](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin)。測試會將結果上傳至 {{site.data.keyword.DRA_short}} 以進行分析，而閘道會使用那些結果來制定升級決策。
4. 執行專案並[檢視結果](results.html)。 

無論您如何建置及部署程式碼，結果皆相同：符合標準的建置將會通過 Deployment Risk 閘道，而不符合標準的建置就會被阻擋下來。 
