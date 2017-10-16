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

# Deployment Risk 分析と継続的デリバリーの統合

{{site.data.keyword.contdelivery_full}}用のパイプラインを装備すると、{{site.data.keyword.DRA_short}} の Deployment Risk 分析機能を使用できます。その後、それらのジョブからデータを公開してリスク・ポリシーを実施するゲートを追加することができます。

{{site.data.keyword.DRA_short}} の Deployment Risk 分析の概説については、[Deployment Risk について](./about_risk.html)を参照してください。

継続的デリバリーのパイプラインについて詳しくは、[公式のドキュメンテーション](../ContinuousDelivery/pipeline_working.html)を参照してください。

## パイプラインのステージとジョブの準備
{: #integrate_pipeline}

始めに、{{site.data.keyword.DRA_short}} と通信するためのパイプラインを装備する必要があります。これを行うには、コードのビルド、テスト、デプロイを行うすべてのパイプライン・ジョブについて、特定の環境変数を定義します。さらに、DevOps Insights ゲート・テスター・タイプを使用してリスク・ポリシーを実施するテスト・ジョブに環境変数を追加する必要もあります。

* ビルド・レコード
* デプロイメント・レコード
* テスト結果

テスト結果では、サポート対象となる以下のいずれかの形式でデータを提供する必要があります。

| テスト・タイプ               | サポートされる形式|
|------------------------------|-----------------------------------------------------------------|
| 機能検証テスト               | Mocha、xUnit|
| 単体テスト                   | Mocha、xUnit、Karma/Mocha|
| コード・カバレッジ           | Istanbul、Blanket.js、Cobertura、lcov                                           |
| 静的アプリ・スキャン         | IBM Application Security on Cloud で提供される静的アプリ・スキャン |
| 動的アプリ・スキャン         | IBM Application Security on Cloud で提供される動的アプリ・スキャン |
| SonarQube                    | SonarQube スキャンで提供されるスキャン・データ                  |

パイプラインで定義する環境変数は、これらのレコードを公開するためのコンテキストを提供します。これらの環境変数は、ご使用のジョブのスクリプト内の `export` コマンドを使用して定義できます。また、各パイプライン・ステージの「環境プロパティー」メニューでも設定できます。

環境変数:

| 環境変数            | 目的 | 必要なジョブ |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | ダッシュボード上のアプリの名前。| {{site.data.keyword.DRA_short}} のリスク・ポリシーのビルド、テスト、デプロイ、実施を行うすべてのジョブ。|
| `BUILD_PREFIX`  | ステージのビルドに接頭部として追加されるテキスト。このテキストは、ダッシュボードにも表示されます。| {{site.data.keyword.DRA_short}} のリスク・ポリシーのビルド、テスト、デプロイ、実施を行うすべてのジョブ。|
| `LOGICAL_ENV_NAME`  | アプリケーションが実行される環境。| テスト・ジョブとデプロイ・ジョブ。|

### ビルド・ジョブの構成

ステージ内の最後のビルド・ジョブについて、アプリケーション名とビルド接頭部の環境変数を設定します。サンプル・スクリプトには以下のコマンドが含まれます。

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

このビルド・ジョブが完了すると、パイプラインが {{site.data.keyword.DRA_short}} に、SampleApp ビルドが完了したことを示すメッセージを公開します。

### デプロイメント・ジョブの構成

ステージ内の最後のデプロイメント・ジョブについて、アプリケーション名、ビルド接頭部、環境名を設定します。サンプル・スクリプトには以下のコマンドが含まれます。

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

デプロイメント・ジョブが終了すると、パイプラインが {{site.data.keyword.DRA_short}} に、指定されたビルドとアプリが環境にデプロイされたことを示すメッセージを公開します。

### テスト・ジョブの構成

テスト結果を生成するすべてのジョブについて、アプリケーション名とビルド接頭部を設定します。

ジョブによって機能検証テスト (FVT) の結果が生成される場合は、テストが実行されるすべての場所に論理環境名を設定する必要もあります。

サンプル・スクリプトには以下のコマンドが含まれます。

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

該当するテスト対象においてアプリケーション名と環境が一致するようにします。例えば、実動デプロイメントに対して実行する実動テスト・ジョブが両者同一の `LOGICAL_ENV_NAME` 値を持つようにします。

## DevOps Insights へのテスト・データの公開
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} は、ジョブのテスト結果を使用してレポートを生成し、リスク・ポリシーを実施します。テスト・データは、すべてのジョブ・タイプから公開できます。

テスト結果を公開するためのオプションとして、次の 2 つがあります。

* ジョブ・スクリプトで単純なコマンド・ライン・インターフェース (CLI) を呼び出す。

* 詳細テスター・タイプのテスト・ジョブをパイプラインに追加する。

詳細テスター方式を使用すると、テスト結果を公開するときに CLI は使用しません。代わりに、パイプライン・ジョブで結果ファイルの場所を指定します。結果を利用できるようになると、パイプライン・ジョブが結果をアップロードします。

どちらの公開方式を使用する場合でも、テスト結果は {{site.data.keyword.DRA_short}} がサポートする以下のいずれかの形式でなければなりません。

<table><thead>
<tr>
<th>テスト・タイプ</th>
<th>サポートされる形式</th>
</tr>
</thead><tbody>
<tr>
<td>機能検証テスト</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>単体テスト</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>コード・カバレッジ</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

### 任意のジョブ・タイプからのテスト・データの公開

パイプラインでは、テストを実行するために任意のジョブ・タイプを使用できます。そのテストを実行した後、その結果を {{site.data.keyword.DRA_short}} にアップロードすることができます。結果をアップロードするには、ジョブのシェル・スクリプトで CLI を呼び出します。 

以下のタイプのテスト結果を CLI からアップロードできます。

* 単体テスト
* コード・カバレッジ
* 機能検証テスト
* IBM Application Security on Cloud からの静的アプリ・スキャンと動的アプリ・スキャンの結果 

テストを実行してから結果を {{site.data.keyword.DRA_short}} にアップロードするためのサンプル・スクリプトを以下に示します。 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

`idra` コマンドについて詳しくは、[npm の grunt-idra3 パッケージのページ](https://www.npmjs.com/package/grunt-idra3)を参照してください。 

### 詳細テスター・ジョブからのテスト・データの公開

詳細テスター・タイプのテスト・ジョブをパイプラインに追加することができます。ジョブの実行後、その結果が {{site.data.keyword.DRA_short}} に自動的にアップロードされます。 

1. 結果をアップロードするジョブを追加するステージで、**「ステージ構成」**アイコン ![パイプライン・ステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックします。
**「ステージの構成 (Configure Stage)」**をクリックします。
2. テスト・ジョブを作成し、その名前を入力します。
 
3. ジョブ・タイプとして、**「詳細テスター (Advanced Tester)」**を選択します。

4. 通常のパイプライン・テスト・ジョブの場合と同じようにして、**「テスト・コマンド」**と**「作業ディレクトリー」**のフィールドに情報を入力します。
 
5. 特定のテスト・タイプのテスト結果をアップロードするための、その他のフィールドに入力します。
 

 1. 使用する {{site.data.keyword.DRA_short}} ポリシーの中で定義したものと合致するメトリック・タイプを選択します。

 2. 結果ファイルの場所を入力します。
この場所は作業ディレクトリーを基準とする相対位置です。
 

6. 同じジョブで別のテスト・タイプの結果をアップロードする場合は、*「追加 (Additional)」*と先頭に示されたフィールドに入力します。

7. **「保存」**をクリックして、パイプラインに戻ります。

図 1 に示すテスト・ジョブは、単体テストを実行し、結果を Mocha 形式でアップロードし、コード・カバレッジ結果を Istanbul 形式でアップロードするように構成されています。


![DevOps Insights アップロード・ジョブ](images/insights_upload_job.png)
*図 1. 結果を DevOps Insights にアップロードする*



## ゲートの定義
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} ゲートは、定義されたポリシーにテスト結果が準拠しているかどうかを検査します。
ポリシーに準拠していない場合、デフォルトで {{site.data.keyword.DRA_short}} ゲートは失敗します。
また、アドバイザリー・ロールで機能するようにゲートを構成して、失敗の後もパイプラインが先へ進むことを許可することができます。


Deployment Risk ダッシュボードは、ステージング・デプロイメント・ジョブの後にゲートが存在することに依存しています。
ダッシュボードを使用する場合は、ステージング環境へのデプロイの後、実稼働環境へのデプロイの前にゲートを配置してください。


通常、ゲートは、パイプラインの中でビルド・プロモーションの前に配置されます。
この場所は、ビルドの品質をポリシーに照らして検査して、それが別の環境に安全にプロモートできるものであることを確認するのに理想的な場所です。しかし、ゲートは、特定の基準の検査を必要とする、パイプライン内の任意の場所に配置することが可能です。ステージング環境へのデプロイの前に配置されるゲートでも、ポリシーが適用されますが、それらは Deployment Risk ダッシュボードに表示されません。


1. ステージで**「ステージ構成 (Stage Configuration)」**アイコン ![パイプラインのステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックし、**「ステージの構成 (Configure Stage)」**をクリックします。
2. **「ジョブの追加 (Add Job)」**をクリックします。ジョブ・タイプとして**「テスト」**を選択します。
3. テスター・タイプとして**「{{site.data.keyword.DRA_short}} ゲート ({{site.data.keyword.DRA_short}} Gate)」**を選択します。
4. 環境名を指定します。この値が、[環境プロパティー](#toolchain_pipeline_props)で定義したものと一致することを確認してください。
5. このゲートにおいてチェックするポリシー名を入力します。


 この名前は、定義したポリシー名のいずれかと完全に一致していなければなりません。ご使用のツールチェーンと同じ {{site.data.keyword.Bluemix_notm}} 組織で定義されたポリシーのみを指定できます。

6. オプション: ゲートを推奨モードで機能させるには、**「このジョブが失敗した場合、このステージの実行を停止する (Stop running this stage if this job fails)」**チェック・ボックスをクリアします。推奨モードでは、{{site.data.keyword.DRA_short}} は同じポリシー分析をゲートで実行し、レポートを生成しますが、失敗となった場合でもパイプラインは停止されません。
7. **「保存」**をクリックして、パイプラインに戻ります。
8. 上記のステップを繰り返して、すべての {{site.data.keyword.DRA_short}} ポリシーについてゲートをセットアップします。

![Deployment Risk の Mocha ジョブ](images/insights_gate_job.png)
*図 2. DevOps Insights ゲート*

パイプラインを構成した後、{{site.data.keyword.DRA_short}} の使用を開始します。 
