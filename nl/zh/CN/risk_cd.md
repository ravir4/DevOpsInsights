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

# 将 Deployment Risk 分析与持续交付集成

您可以为 {{site.data.keyword.contdelivery_full}} 安装管道，以使用 {{site.data.keyword.DRA_short}} 的 Deployment Risk 分析功能。然后，可发布这些作业的数据，并添加强制实施风险策略的检测点。

要查看 {{site.data.keyword.DRA_short}} 的 Deployment Risk 分析的高级说明，请参阅[关于 Deployment Risk](./about_risk.html)。

有关持续交付管道的更多信息，请参阅[正式文档](../ContinuousDelivery/pipeline_working.html)。

## 准备管道阶段和作业
{: #integrate_pipeline}

首先，您需要安装管道，以与 {{site.data.keyword.DRA_short}} 通信。通过为构建、测试或部署编码的所有管道作业定义特定环境变量，可实现此目标。您还必须使用 DevOps Insights 检测点测试器类型，将环境变量添加到强制实施风险策略的测试作业。

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
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | 仪表板上应用程序的名称。| 构建、测试、部署和强制实施 {{site.data.keyword.DRA_short}} 风险策略的所有作业。|
| `BUILD_PREFIX`  | 作为前缀添加到阶段构建中的文本。此文本还会在仪表板中出现。| 构建、测试、部署和强制实施 {{site.data.keyword.DRA_short}} 风险策略的所有作业。|
| `LOGICAL_ENV_NAME`  | 运行应用程序的环境。| 测试和部署作业。|

### 配置构建作业

对于阶段中的最后一个构建作业，请为应用程序名称和构建前缀设置环境变量。示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

此构建作业完成之后，管道会向 {{site.data.keyword.DRA_short}} 发布一条消息，指示 SampleApp 构建完成。

### 配置部署作业

对于阶段中的最后一个部署作业，请设置应用程序名称、构建前缀和环境名称。示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

部署作业结束之后，管道会向 {{site.data.keyword.DRA_short}} 发布一条消息，指示已将指定的构建和应用程序部署到环境中。

### 配置测试作业

对于生成测试结果的所有作业，请设置应用程序名称和构建前缀。

如果作业生成功能验证测试 (FVT) 结果，那么您还必须为这些测试运行的环境设置逻辑环境名称。

示例脚本中包含了以下命令：

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

确保应用程序名称和环境适当匹配。例如，您会希望针对生产部署运行的生产测试作业具有相同的 `LOGICAL_ENV_NAME` 值。

## 将测试数据发布到 DevOps Insights
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} 使用作业的测试结果来生成报告，并强制实施风险策略。您可以发布所有作业类型的测试数据。

发布测试结果时可使用以下两个选项：

* 调用作业脚本中的简单命令行界面 (CLI)。

* 将“高级测试器”类型的测试作业添加到管道中。

使用“高级测试器”方法时，将不会使用 CLI 来发布测试结果。而是指定管道作业中结果文件的位置，然后作业会在结果变为可用时进行上传。

无论使用哪种发布方法，测试结果必须采用 {{site.data.keyword.DRA_short}} 支持的其中一种格式：

<table><thead>
<tr>
<th>测试类型</th>
<th>支持的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能验证测试</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>单元测试</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>代码覆盖</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

### 发布任何作业类型的测试数据

在管道中，可使用任何作业类型来运行测试。运行该测试之后，可将其结果上传到 {{site.data.keyword.DRA_short}}。通过调用作业 shell 脚本中的 CLI 可上传结果。 

可从 CLI 上传以下类型的测试结果：

* 单元测试
* 代码覆盖
* 功能验证测试
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

要了解 `idra` 命令的更多信息，请参阅 [the grunt-idra3 package's page on npm](https://www.npmjs.com/package/grunt-idra3)。 

### 发布高级测试器作业的测试数据

可将“高级测试器”类型的测试作业添加到管道中。这些作业在运行之后会将其结果自动上传到 {{site.data.keyword.DRA_short}}。 

1. 在要添加用于上传结果的作业的阶段中，单击**阶段配置**图标 ![“管道阶段配置”图标](images/pipeline-stage-configuration-icon.png)。单击**配置阶段**。
2. 创建测试作业，然后输入其名称。 
3. 对于作业类型，选择**高级测试器**。
4. 填写**测试命令**和**工作目录**字段，就像对普通管道测试作业那样。 
5. 填写其余字段，以上传特定测试类型的测试结果。 

 1. 选择与要使用的 {{site.data.keyword.DRA_short}} 策略中所定义类型相匹配的度量类型。
 2. 输入结果文件位置。此位置是工作目录的相对位置。 

6. 如果要在同一作业中上传另一种测试类型的结果，请填写前缀为*其他*的字段。
7. 单击**保存**以返回管道。

图 1 显示的测试作业配置为运行单元测试、以 Mocha 格式上传结果，以及以 Istanbul 格式上传代码覆盖结果。

![DevOps Insights 上传作业](images/insights_upload_job.png)
*图 1. 将结果上传到 DevOps Insights*



## 定义检测点
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 检测点用于检查测试结果是否符合所定义的策略。如果不符合策略，那么缺省情况下 {{site.data.keyword.DRA_short}} 检测点将失败。您还可以将检测点配置为以建议角色执行操作，以允许管道在即便发生失败后仍继续运行。

Deployment Risk 仪表板依赖于编译打包部署作业后存在检测点。如果要使用该仪表板，请确保您在部署到编译打包环境后，但在部署到生产环境之前拥有检测点。

通常，检测点在管道中构建升级之前放置。这些位置非常适合根据策略检查构建的质量，以确保构建能够安全地从一个环境升级到另一个环境。但是，您可以将检测点放置在管道中您要检查特定条件的任何位置。在部署到编译打包环境之前放置的检测点仍将强制实施策略，但这些检测点不会在 Deployment Risk 仪表板上显示。

1. 在阶段上，单击**阶段配置**图标 ![管道阶段配置图标](images/pipeline-stage-configuration-icon.png)，并单击**配置阶段**。
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
