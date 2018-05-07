---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 整合 Deployment Risk 分析與 Continuous Delivery

{{site.data.keyword.DRA_short}} 會根據您發佈給它的測試資料來追蹤部署風險。此資料可能包含單元測試、程式碼涵蓋面、功能驗證測試、SonarQube 資料，或來自 IBM Application Security on Cloud 的掃描資料。發佈此資料之後，您可以為管線新增閘道，以便停止不符合風險原則的建置。

若要查看高階的 {{site.data.keyword.DRA_short}} Deployment Risk 分析說明，請參閱[關於 Deployment Risk](./about_risk.html)。

如需 Continuous Delivery 管線的相關資訊，請參閱[正式文件](../ContinuousDelivery/pipeline_working.html)。

## 概觀
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} 需要來自您的管線的下列資訊才能分析部署風險：

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
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`  | 儀表板上的應用程式名稱。| 建置、測試、部署及強制執行 {{site.data.keyword.DRA_short}} 風險原則的所有工作。|
| `BUILD_PREFIX`  | 新增為階段建置字首的文字。此文字也會顯示在儀表板上。| 建置、測試、部署及強制執行 {{site.data.keyword.DRA_short}} 風險原則的所有工作。|
| `LOGICAL_ENV_NAME`  | 應用程式執行所在的環境。| 測試及部署工作。|

使用這些變數時請務必保持一致：

* 對於特定應用程式，請在所有工作或階段中使用相同的 `LOGICAL_APP_NAME`。 
* 對於特定應用程式及建置類型，`BUILD_PREFIX` 值應該相同。例如，對於來自主要分支的建置，`BUILD_PREFIX` 可以是 `"master"`。 
* 在對應的部署工作及測試工作，請使用相同的 `LOGICAL_ENVIRONMENT_NAME` 值。如果您在部署工作中使用 `LOGICAL_ENVIRONMENT_NAME` 值 `"PRODUCTION"`，當您發佈來自也在該環境執行之測試的結果時，也請使用該相同值。

## 建置工作環境變數

針對階段中的最後一個建置工作，請為應用程式名稱和建置字首設定環境變數。範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

當此建置工作完成時，管線會發佈 SampleApp 已完成的訊息給 {{site.data.keyword.DRA_short}}。

## 部署工作環境變數

針對階段中的最後一個部署工作，請設定應用程式名稱、建置字首及環境名稱。範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

當部署工作完成時，管線會發佈指定建置及應用程式已部署至環境的訊息給 {{site.data.keyword.DRA_short}}。

## 測試工作環境變數

針對產生測試結果的所有工作，請設定應用程式名稱及建置字首。

如果工作產生功能驗證測試 (FVT) 結果，您也必須將邏輯環境名稱設為那些測試執行的任意處。

範例 Script 會包含下列指令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## 發佈測試結果
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} 使用來自您工作的測試結果來產生報告及強制執行風險原則。

在管線中，您可以使用任何工作類型來執行測試。執行該測試之後，您可以將它的結果上傳至 {{site.data.keyword.DRA_short}}。上傳結果的方法是在工作的 Shell Script 中呼叫 CLI。 

您可以從 CLI 上傳這些類型的測試結果：

* 單元測試
* 程式碼涵蓋面
* 功能驗證測試
* SonarQube 結果
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

在該範例中，`idra` 指令在執行時使用 `--publishtestresult` 旗標，這樣會指定 Script 將上傳結果。`--filelocation` 旗標指出測試結果檔案的位置（相對於工作的根目錄）。`--type` 旗標指出執行之測試的類型。

`idra` 指令支援下列 `type` 值： 

| 類型| 說明|
|------|-------------|
| `unittest` | 單元測試結果| 
| `fvt` | 功能驗證測試結果|
| `code` | 程式碼涵蓋面結果| 
| `sonarqube` | SonarQube 掃描結果| 
| `staticsecurityscan` | 來自 IBM Application Security on Cloud 的靜態安全掃描結果|
| `dynamicsecurityscan` | 來自 IBM Application Security on Cloud 的動態安全掃描結果|

若要進一步瞭解 `idra` 指令，請參閱 [npm 上的 grunt-idra3 套件頁面](https://www.npmjs.com/package/grunt-idra3)。 

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
