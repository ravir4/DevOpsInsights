---

copyright:
  years: 2018
lastupdated: "2018-4-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在 DevOps Insights 中管理個人資料
{: insights_personal_data}

您可以刪除已收集並儲存在 {{site.data.keyword.DRA_full}} 中的個人資料。
{: shortdesc}

儲存在 {{site.data.keyword.DRA_short}} 中的資料是依工具鏈 ID 進行檢索。當您刪除工具鏈時，與工具鏈當中收集之儲存庫相關的所有資料都會刪除。

## 從 {{site.data.keyword.DRA_short}} 刪除資料
{: #insights_delete_data}

下表列出從 {{site.data.keyword.DRA_short}} 刪除資料的情境，並說明它們對每個 {{site.data.keyword.DRA_short}} 種類有何影響。

|  | Developer 及 Team Insights | Deployment Risk| Security Insights |
|---------|-------------|-------------|-------------|
| [刪除儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	與儲存庫相關的所有資料都會刪除。| N/A | N/A |
| [刪除 {{site.data.keyword.DRA_short}} 工具整合 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	與儲存庫相關的所有資料都會刪除。| 與工具整合所屬工具鏈相關聯的所有資料都會刪除。| 與工具整合所屬工具鏈相關聯之儲存庫相關的所有資料都會刪除。|
| [刪除工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | 與工具鏈相關聯之儲存庫相關的所有資料都會刪除。| 與工具鏈相關聯的所有資料都會刪除。| 與工具鏈相關聯的所有資料都會刪除。|
| [刪除管線 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/A | N/A | N/A |
{:caption="表 1. 資料刪除情境" caption-side="top"}

## 刪除 {{site.data.keyword.DRA_short}} 工具整合
{: #insights_delete_integration}

如果您從工具鏈中刪除工具整合，則無法復原刪除。

1. 在 DevOps 儀表板的**工具鏈**頁面上按一下工具鏈，以開啟其「概觀」頁面。或者，在應用程式的「概觀」頁面、Continuous Delivery 卡上，按一下**檢視工具鏈**，然後按一下**概觀**。
1. 在您要刪除的 {{site.data.keyword.DRA_short}} 工具整合的卡上，按一下功能表以存取配置選項。
1. 若要從工具鏈中刪除工具整合，請按一下**刪除**。

  ![配置功能表](images/delete_insights_integration.png)

1. 按一下**刪除**來進行確認。 
