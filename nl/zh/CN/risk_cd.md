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

# 将 Deployment Risk 分析与 Continuous Delivery 集成

{{site.data.keyword.DRA_short}} 根据您向其发布的测试数据来跟踪部署风险。这些数据可能包括单元测试、代码覆盖、功能验证测试、SonarQube 数据或者来自 IBM Application Security on Cloud 的扫描数据。发布这些数据后，可以向管道添加检查点，使得可以停止不符合风险策略的构建。

要查看 {{site.data.keyword.DRA_short}} 的 Deployment Risk 分析的高级说明，请参阅[关于 Deployment Risk](./about_risk.html)。

有关 Continuous Delivery Pipeline 的更多信息，请参阅[正式文档](../ContinuousDelivery/pipeline_working.html)。

## 概述
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} 需要从管道获取以下信息以分析部署风险：

* 构建记录
* 部署记录
* 测试结果

测试结果必须采用以下某个支持的格式提供数据：

| 测试类型                     | 支持的格式|
|------------------------------|-----------------------------------------------------------------|
| 功能验证测试                 | Mocha、xUnit|
| 单元测试                     | Mocha、xUnit、Karma/Mocha|
| 代码覆盖                     | Istanbul、Blanket.js、Cobertura 和 lcov                                           |
| 静态应用程序扫描             | IBM Application Security on Cloud 提供的静态应用程序扫描   |
| 动态应用程序扫描             | IBM Application Security on Cloud 提供的动态应用程序扫描   |
| SonarQube                    | SonarQube 扫描提供的扫描数据                            |

您在管道中定义的环境变量会提供用于发布这些记录的上下文。您可以在作业脚本中使用 `export` 命令进行定义。还可以在每个管道阶段的“环境属性”菜单中进行设置。

环境变量：

| 环境变量      | 用途 | 何时需要 |
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`  | 仪表板上应用程序的名称。| 构建、测试、部署和强制实施 {{site.data.keyword.DRA_short}} 风险策略的所有作业。|
| `BUILD_PREFIX`  | 作为前缀添加到阶段构建中的文本。此文本还会在仪表板中出现。| 构建、测试、部署和强制实施 {{site.data.keyword.DRA_short}} 风险策略的所有作业。|
| `LOGICAL_ENV_NAME`  | 运行应用程序的环境。| 测试和部署作业。|

使用以下变量时务必保持一致：

* 对于特定应用程序，在所有作业或阶段均使用相同的 `LOGICAL_APP_NAME`。 
* 对于特定应用程序和构建类型，`BUILD_PREFIX` 值应该相同。例如，对于主分支中的构建，`BUILD_PREFIX` 可为 `"master"`。 
* 在相应的部署作业和测试作业中，使用相同的 `LOGICAL_ENVIRONMENT_NAME` 值。如果在部署作业中使用的 `LOGICAL_ENVIRONMENT_NAME` 的值为 `"PRODUCTION"`，那么发布同样在该环境中运行的测试的结果时，请使用相同的值。

## 构建作业环境变量

对于阶段中的最后一个构建作业，请为应用程序名称和构建前缀设置环境变量。示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

此构建作业完成之后，管道会向 {{site.data.keyword.DRA_short}} 发布一条消息，指示 SampleApp 构建完成。

## 部署作业环境变量

对于阶段中的最后一个部署作业，请设置应用程序名称、构建前缀和环境名称。示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

部署作业结束之后，管道会向 {{site.data.keyword.DRA_short}} 发布一条消息，指示已将指定的构建和应用程序部署到环境中。

## 测试作业环境变量

对于生成测试结果的所有作业，请设置应用程序名称和构建前缀。

如果作业生成功能验证测试 (FVT) 结果，那么您还必须为这些测试运行的环境设置逻辑环境名称。

示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## 发布测试结果
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} 使用作业的测试结果来生成报告，并强制实施风险策略。

在管道中，可使用任何作业类型来运行测试。运行该测试之后，可将其结果上传到 {{site.data.keyword.DRA_short}}。通过调用作业 shell 脚本中的 CLI 可上传结果。 

可从 CLI 上传以下类型的测试结果：

* 单元测试
* 代码覆盖
* 功能验证测试
* SonarQube 结果
* 来自 IBM Application Security on Cloud 的静态和动态应用程序扫描结果。 

以下提供了用于运行测试并将结果上传到 {{site.data.keyword.DRA_short}} 的示例脚本： 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

在该示例中，使用 `--publishtestresult` 标志运行的 `idra` 命令指定脚本将上传结果。`--filelocation` 标志指示测试结果文件相对于作业根目录的位置。`--type` 标志指示运行的测试类型。

`idra` 命令支持以下 `type` 值： 

| Type| 描述|
|------|-------------|
| `unittest`| 单元测试结果| 
| `fvt`| 功能验证测试结果|
| `code`| 代码覆盖结果| 
| `sonarqube`| SonarQube 扫描结果| 
| `staticsecurityscan`| 来自 IBM Application Security on Cloud 的静态安全扫描结果|
| `dynamicsecurityscan`| 来自 IBM Application Security on Cloud 的动态安全扫描结果|

要了解 `idra` 命令的更多信息，请参阅 [the grunt-idra3 package's page on npm](https://www.npmjs.com/package/grunt-idra3)。 

## 定义检测点
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 检测点用于检查测试结果是否符合所定义的策略。如果不符合策略，那么缺省情况下 {{site.data.keyword.DRA_short}} 检测点将失败。您还可以将检测点配置为以建议角色执行操作，以允许管道在即便发生失败后仍继续运行。

Deployment Risk 仪表板依赖于编译打包部署作业后存在检测点。如果要使用该仪表板，请确保您在部署到编译打包环境后，但在部署到生产环境之前拥有检测点。

通常，检测点在管道中构建升级之前放置。这些位置非常适合根据策略检查构建的质量，以确保构建能够安全地从一个环境升级到另一个环境。但是，您可以将检测点放置在管道中您要检查特定条件的任何位置。在部署到编译打包环境之前放置的检测点仍将强制实施策略，但这些检测点不会在 Deployment Risk 仪表板上显示。

1. 在阶段上，单击**阶段配置**图标 ![“管道阶段配置”图标](images/pipeline-stage-configuration-icon.png)，并单击**配置阶段**。
2. 单击**添加作业**。对于作业类型，选择**测试**。
3. 对于测试器类型，选择 **{{site.data.keyword.DRA_short}} 检测点**。
4. 指定环境名称。确保此值匹配[环境属性](#toolchain_pipeline_props)中所定义的内容。
5. 输入要在此检测点检查的策略名称。

 此名称必须与所定义的其中一个策略名称完全匹配。在与工具链相同的 {{site.data.keyword.Bluemix_notm}} 组织中，您仅可以指定一个所定义的策略。

6. 可选：要使检测点在建议方式下发挥作用，请清除**此作业失败时停止运行此阶段**复选框。在建议方式下，{{site.data.keyword.DRA_short}} 会在该检测点完成相同的策略分析并生成报告，但是如果发生失败，却不会停止管道。
7. 单击**保存**以返回管道。
8. 重复以上步骤，为所有 {{site.data.keyword.DRA_short}} 策略设置检测点。

![Deployment Risk Mocha 作业](images/insights_gate_job.png)
*图 2. DevOps Insights 检测点*

配置管道之后，开始使用 {{site.data.keyword.DRA_short}}。 
