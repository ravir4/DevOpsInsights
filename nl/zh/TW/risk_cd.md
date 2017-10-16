---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 整合 Deployment Risk 分析與 Continuous Delivery

您可以檢測 {{site.data.keyword.contdelivery_full}} 的管線以使用 {{site.data.keyword.DRA_short}} 的 Deployment Risk 分析功能。接著，您可以從那些工作發佈資料，以及新增強制執行風險原則的閘道。

若要查看高階的 {{site.data.keyword.DRA_short}} Deployment Risk 分析說明，請參閱[關於 Deployment Risk](./about_risk.html)。

如需 Continuous Delivery 管線的相關資訊，請參閱[正式文件](../ContinuousDelivery/pipeline_working.html)。

## 準備管線階段及工作
{: #integrate_pipeline}

若要開始使用，您需要檢測您的管線以便與 {{site.data.keyword.DRA_short}} 通訊。要這麼做，請為建置、測試或部署程式碼的所有管線工作定義特定的環境變數。您也必須新增環境變數至測試工作，使用 DevOps Insights Gate 測試者類型強制執行風險原則。

* 建置記錄
* 部署記錄
* 測試結果

測試結果必須以下列其中一種支援的格式提供資料：

| 測試類型| 支援的格式|
|------------------------------|-----------------------------------------------------------------|
| 功能驗證測試| Mocha、xUnit|
| 單元測試| Mocha、xUnit、Karma/Mocha|
| 程式碼涵蓋面| Istanbul、Blanket.js、Cobertura、lcov                                           |
| 靜態應用程式掃描| IBM Application Security on Cloud 提供的靜態應用程式掃描|
| 動態應用程式掃描| IBM Application Security on Cloud 提供的動態應用程式掃描|
| SonarQube                    | SonarQube 掃描提供的掃描資料|

您在管線中定義的環境變數，會提供發佈這些記錄用的環境定義。您可以在工作 Script 中使用 `export` 指令來定義它們。也可以在每個管線階段的「環境內容」功能表中設定。

環境變數：

| 環境變數| 目的| 需要之處|
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | 儀表板上的應用程式名稱。| 建置、測試、部署及強制執行 {{site.data.keyword.DRA_short}} 風險原則的所有工作。|
| `BUILD_PREFIX`  | 新增為階段建置字首的文字。此文字也會顯示在儀表板上。| 建置、測試、部署及強制執行 {{site.data.keyword.DRA_short}} 風險原則的所有工作。|
| `LOGICAL_ENV_NAME`  | 應用程式執行所在的環境。| 測試及部署工作。|

### 配置建置工作

針對階段中的最後一個建置工作，請為應用程式名稱和建置字首設定環境變數。範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

當此建置工作完成時，管線會發佈 SampleApp 已完成的訊息給 {{site.data.keyword.DRA_short}}。

### 配置部署工作

針對階段中的最後一個部署工作，請設定應用程式名稱、建置字首及環境名稱。範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

當部署工作完成時，管線會發佈指定建置及應用程式已部署至環境的訊息給 {{site.data.keyword.DRA_short}}。

### 配置測試工作

針對產生測試結果的所有工作，請設定應用程式名稱及建置字首。

如果工作產生功能驗證測試 (FVT) 結果，您也必須將邏輯環境名稱設為那些測試執行的任意處。

範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

請確定應用程式名稱及環境在適當處相符。例如，您會想要針對正式作業部署執行的正式作業測試工作，有相同的 `LOGICAL_ENV_NAME` 值。

## 將測試資料發佈至 DevOps Insights
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} 使用來自您工作的測試結果來產生報告及強制執行風險原則。您可以發佈所有工作類型的測試資料。

發佈測試結果有兩個選項：

* 在工作 Script 中呼叫簡單的指令行介面 (CLI)。

* 將具有「進階測試者」類型的測試工作新增至您的管線。

當您使用「進階測試者」方法時，不會使用 CLI 發佈測試結果。而是在管線工作中指定結果檔案的位置，工作會在結果變成可用時上傳結果。

不論您使用哪種發佈方法，測試結果都必須是 {{site.data.keyword.DRA_short}} 支援的其中一種格式：

<table><thead>
<tr>
<th>測試類型</th>
<th>支援的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能驗證測試</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>單元測試</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>程式碼涵蓋面</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

### 從任何工作類型發佈測試資料

在管線中，您可以使用任何工作類型來執行測試。執行該測試之後，您可以將它的結果上傳至 {{site.data.keyword.DRA_short}}。上傳結果的方法是在工作的 Shell Script 中呼叫 CLI。 

您可以從 CLI 上傳這些類型的測試結果：

* 單元測試
* 程式碼涵蓋面
* 功能驗證測試
* 來自 IBM Application Security on Cloud 的靜態及動態應用程式掃描。 

以下範例 Script 會執行測試，然後將結果上傳至 {{site.data.keyword.DRA_short}}： 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

若要進一步瞭解 `idra` 指令，請參閱 [npm 上的 grunt-idra3 套件頁面](https://www.npmjs.com/package/grunt-idra3)。 

### 從進階測試者工作發佈測試資料

您可以將具有「進階測試者」類型的測試工作新增至管線。執行之後，它們會自動將結果上傳至 {{site.data.keyword.DRA_short}}。 

1. 在要新增上傳結果工作的階段，按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png)。按一下**配置階段**。
2. 建立測試工作，並鍵入其名稱。 
3. 針對工作類型，選取**進階測試者**。
4. 完成**測試指令**和**工作目錄**欄位，如同一般管線測試工作一樣。 
5. 完成其餘欄位，以上傳特定測試類型的測試結果。 

 1. 選擇度量值類型，需符合您要使用的 {{site.data.keyword.DRA_short}} 原則中定義的內容。
 2. 鍵入結果檔案位置。此位置相對於工作目錄。 

6. 如果您要上傳相同工作中第二個測試類型的結果，請完成前面加上*其他* 字首的欄位。
7. 按一下**儲存**，以回到管線。

圖 1 顯示一個測試工作，其配置成執行單元測試、上傳 Mocha 格式的結果，以及上傳 Istanbul 格式的程式碼涵蓋面結果。

![DevOps Insights 上傳工作](images/insights_upload_job.png)
*圖 1. 將結果上傳至 DevOps Insights*



## 定義閘道
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 閘道會檢查測試結果是否符合所定義的原則。如果不符合原則，依預設，{{site.data.keyword.DRA_short}} 閘道會失敗。您也可以將閘道配置為以諮詢角色運作，以允許管線即使失敗後仍可繼續進行。

在編譯打包部署工作之後，Deployment Risk 儀表板需要有閘道存在。如果您想要使用此儀表板，請確定在部署至編譯打包環境之後，且部署至正式作業環境之前，有閘道存在。

通常在管線中，閘道會放在建置升級前面。這些位置很適合用來根據原則檢查建置品質，以確保可以安心從某個環境升級至另一個環境。不過，您可以在管線中任何想要檢查特定準則的位置放置閘道。在您部署至編譯打包環境之前設置的閘道仍會強制執行原則，但不會出現在 Deployment Risk 儀表板上。

1. 在階段上，依序按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 及**配置階段**。
2. 按一下**新增工作**。針對工作類型，選取**測試**。
3. 針對測試者類型，選取 **{{site.data.keyword.DRA_short}} 閘道**。
4. 指定環境名稱。請確定此值符合[環境內容](#toolchain_pipeline_props)中所定義的值。
5. 輸入要在此閘道檢查的原則名稱。

 此名稱必須完全符合您定義的其中一個原則名稱。您只能指定在與工具鏈相同的 {{site.data.keyword.Bluemix_notm}} 組織中所定義的原則。

6. 選用項目：若要讓閘道以諮詢模式運作，請清除**此工作失敗時停止執行這個階段**勾選框。在諮詢模式中，{{site.data.keyword.DRA_short}} 會在閘道上完成相同的原則分析並產生報告，但是失敗時不會停止管線。
7. 按一下**儲存**，以回到管線。
8. 重複這些步驟，以設定所有 {{site.data.keyword.DRA_short}} 原則的閘道。

![Deployment Risk Mocha 工作](images/insights_gate_job.png)
*圖 2. DevOps Insights 閘道*

配置管線之後，請開始使用 {{site.data.keyword.DRA_short}}。 
