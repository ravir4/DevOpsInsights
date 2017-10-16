---

copyright:
  years: 2017

lastupdated: "2017-07-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM UrbanCode Deploy サーバーにあるデータの表示
{: #connect_ucd}

IBM UrbanCode Deploy サーバーにあるデータを Delivery Insights で表示するには、DevOps Connect のインスタンスをセットアップし、そのサーバー上にパッチをインストールした後、そのサーバーを DevOps Connect に接続する必要があります。
{:shortdesc}

## 前提条件
{: #prereqs}

IBM UrbanCode Deploy サーバーからの情報を {{site.data.keyword.DRA_short}} で表示するには、IBM UrbanCode Deploy サーバーに接続可能なシステム上に、DevOps Connect のインスタンスをホストする必要があります。
このシステムは、物理コンピューターと仮想マシンのどちらであってもかまいません。 

DevOps Connect をホストするシステムでは、以下の前提条件が揃っていなければなりません。

- そのシステムには、Java ランタイム環境 (JRE) バージョン 8 以降がなければなりません。
- システムの `PATH` 変数に、その JRE の場所が含まれていなければなりません。
- そのシステムは、DevOps Connect が IBM Bluemix への発信接続を作成することを許可していなければなりません。

また、IBM UrbanCode Deploy サーバーは、バージョン 6.2 以降でなければなりません。

## {{site.data.keyword.DRA_short}} サービスの構成
{: #configure_service}

{{site.data.keyword.DRA_short}} サービスがない場合は、それを追加します。
1. {{site.data.keyword.Bluemix}} にログインして、**「サービス」>「ダッシュボード」**をクリックします。
1. **「サービスの作成」**をクリックします。
1. {{site.data.keyword.DRA_short}} サービスをクリックします。
1. 価格プランを選択して、**「作成」**をクリックします。
1. **「管理」**をクリックしてから、「UrbanCode デプロイメントを考察する (Gain insights into UrbanCode deployments)」の下の**「ここから開始します」**をクリックします。
1. ツールチェーン・テンプレート・ウィンドウで、**「作成」**をクリックします。  
組織に合わせたツールチェーンが Delivery Insights によって作成されます。ツールチェーンは統合ツールのコレクションであり、この例では、IBM UrbanCode Deploy と {{site.data.keyword.DRA_short}} はツールチェーンの一部です。ツールチェーンについて詳しくは、[ツールチェーンを使用した作業](../ContinuousDelivery/toolchains_working.html)を参照してください。
1. ツールチェーンで、IBM UrbanCode Deploy ツールをクリックします。
1. 設定ボタンをクリックしてから**「セットアップ」**をクリックします。

今後 {{site.data.keyword.DRA_short}} にアクセスするには、**「サービス」>「ダッシュボード」**をクリックし、{{site.data.keyword.DRA_short}} サービスのインスタンスをクリックします。

既にツールチェーンがある場合は、IBM UrbanCode Deploy と {{site.data.keyword.DRA_short}} ツールをそこに追加し、それらのツールを介して Delivery Insights にアクセスできます。その後、IBM UrbanCode Deploy ツールをクリックし、設定ボタンをクリックしてから、**「セットアップ」**をクリックします。

これで次のセクションに進み、**「セットアップ手順」**ページの手順に従う準備ができました。次のセクションでは、DevOps Connect をインストールし、それを {{site.data.keyword.DRA_short}} に接続する方法を説明します。

## DevOps Connect のインストールと {{site.data.keyword.DRA_short}} への接続
{: #install_connect}

1. **「セットアップ手順」**ページで、DevOps Connect のセットアップ手順を実行し、IBM UrbanCode Deploy サーバーを接続します。これには以下の手順が含まれます。
{: #set_up_connect}
  1. [前提条件](uc_insights_connect_ucd.html#prereqs)で説明しているように、DevOps Connect を実行するためにシステムをセットアップします。
  1. DevOps Connect をダウンロードします。これは、実行可能な JAR ファイルで提供されています。

  1. インターネットへの接続にプロキシーを使用する場合は、システム変数 `_JAVA_OPTIONS` を以下の値に設定します。
    * プロキシーで HTTPS を使用する場合、`_JAVA_OPTIONS` を `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT` に設定します。ここで、`HOSTNAME` はプロキシー・サーバーのホスト名、`PORT` はプロキシー・サーバーの HTTPS ポートです。
    * プロキシーで HTTP を使用する場合、`_JAVA_OPTIONS` を `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT` に設定します。ここで、`HOSTNAME` はプロキシー・サーバーのホスト名、`PORT` はプロキシー・サーバーの HTTP ポートです。

  1. **「セットアップ手順」**ページからコマンドをコピーします。このコマンドにより、{{site.data.keyword.Bluemix}} の組織への接続を許可するトークンを使用して DevOps Connect が開始されます。
  1. DevOps Connect は、デフォルトではポート 8443 で実行されます。これは IBM UrbanCode Deploy サーバーがデフォルトで実行されるポートと同じです。そのため、IBM UrbanCode Deploy サーバーまたは他のいずれかのサービスがポート 844s で実行されている場合には、コマンドにパラメーター `-Dserver.port` を追加して DevOps Connect のポートを変更してください。例えば、DevOps Connect がポート 8888 を使用するように設定する場合、コマンドの先頭部分は次のようになります。  
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

コマンド全体としては、以下の例のように、DevOps Connect を自動的に構成する Bluemix アカウントに関する情報が含まれます。

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. コマンドを実行して DevOps Connect が開始するのを待ちます。

  1. 次のセクションの説明に従って、IBM UrbanCode Deploy サーバーを DevOps Connect に接続します。

## IBM UrbanCode Deploy サーバーを DevOps Connect に接続する
{: #connect_ucd_to_connect}

1. IBM UrbanCode Deploy サーバーのバージョンが 6.2.5 より前のバージョンである場合、サーバーにパッチをインストールします。バージョンが 6.2.5 以降であればパッチは必要ありません。
  1. 使用しているバージョンの IBM UrbanCode Deploy に該当する適切なパッチを以下のページからダウンロードします。例えば、IBM UrbanCode Deploy 6.2.4.x のパッチ・ファイルの名前は、[ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar) です。  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. サーバーを停止します。
[サーバーの開始と停止](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html)を参照してください。


  1. パッチ・ファイルを <code><em>application_data</em>/patches</code> フォルダーに入れます (<code><em>application_data</em></code> はサーバー・アプリケーション・データ・フォルダー)。
デフォルト・アプリケーション・データ・フォルダーは、`/opt/ibm-ucd/server/appdata` (Linux の場合)、および `C:&#xa5;Program Files&#xa5;ibm-ucd&#xa5;server&#xa5;appdata` (Windows の場合) です。
高可用性システムでは、アプリケーション・データ・フォルダーは常に各サーバーからアクセス可能な共有ネットワーク・ドライブ上にあります。


  1. オプション: サーバーが停止している間、このサーバーからのデータ・インポートのパフォーマンスを上げるために、以下の SQL コマンドをデータベースに対して実行します。バージョン 6.2.5 以降では、これらのコマンドは必要ありません。  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
`MyUCDDatabase` には、実際のデータベースの名前を使用します。


  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. サーバーを起動します。
 

    **注:** 待ち時間は、IBM UrbanCode Deploy サーバーの通常の起動時間よりも長いことがあります。
いつまでたってもサーバーが始動しない場合、または正しく動作しない場合は、パッチ・ファイルを削除してからサーバーを再始動してください。パッチ・ファイルは、サーバーに対して永続的な影響があるわけではありません。


1. IBM UrbanCode Deploy の一部のバージョンでは、サーバーが DevOps Connect に接続するために付加的なパッチが必要です。
6.2 から 6.2.1.2 までのバージョンの IBM UrbanCode Deploy を使用している場合は、以下の付加的なパッチをサーバーにインストールする必要があります。

  1. パッチをダウンロードします:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar)。

  1. サーバーを停止します。

  1. パッチ・ファイルを <code><em>application_data</em>/patches</code> フォルダーに入れます。

  1. サーバーを起動します。


1. DevOps Connect と IBM UrbanCode Deploy サーバーの間の統合を作成します。
  

  **重要:** 統合を初めて実行する際、DevOps Connect は過去 90 日間のデータを取り出します。
デプロイメント・データが大量にある場合、このプロセスに長い時間がかかることがあります。
90 日間未満のデータを取り出すようにするには、[『トラブルシューティング』](uc_insights_connect_ucd.html#troubleshooting)を参照してください。

  1. IBM UrbanCode Deploy で、認証トークンを作成します。
[トークン](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html)を参照してください。

  1. DevOps Connect で、**「統合」**をクリックしてから、**「新規追加」**をクリックします。

  1. 統合の名前と説明を指定します。
DevOps Connect の場所のデフォルトは `https://hostname:8443/` です (`hostname` は DevOps Connect のホストであるシステムのホスト名)。

  1. **「統合タイプ」**リストから、 **「IBM UrbanCode Deploy for Cloud のレポート (IBM UrbanCode Deploy for Cloud Reporting)」**を選択します。

  1. **「サーバー URI」**フィールドに、IBM UrbanCode Deploy サーバーのパブリック URL を入力します。例えば、`https://my_UCD.example.com:8447` など。

  1. **「認証トークン」**フィールドに、IBM UrbanCode Deploy によって生成された認証トークンを入力するか貼り付けます。

  1. **「管理ユーザー」**フィールドに、DevOps Connect インターフェースへのアクセス権を付与する IBMid のコンマ区切りリストを入力します。

  1. オプション: 即時統合を実行するには、**「統合の実行」**をクリックします。
デフォルトでは、1 分ごとに統合が実行されます。

  1. **「保存」**をクリックします。

  ![DevOps Connect での統合のセットアップ](images/uc_insights_dc_integration.gif)

これで、データが Delivery Insights と同期されます。
この段階で、このデータに基づくレポートを作成し、表示することができます。
次に、IBM UrbanCode Deploy サーバーの環境を Delivery Insights の論理環境にマップします。

## 環境からレポートへのマッピング
{: #mapping}

### 論理環境

Delivery Insights は、IBM UrbanCode Deploy 環境 (*物理環境* とも呼ばれる) を、1 つ以上の論理環境にグループ化します。そのようにして、環境を、自分や自分の属する組織にとって意味のあるグループにまとめることができます。
例えば、複数のアプリケーションのための複数の実稼働環境がある場合、それらの環境すべてを単一の論理環境に分類し、それらのすべての環境のメトリックを単一の実稼働環境ダッシュボードにまとめて表示することができます。
マッピングは検索文字列によって実行されるため、IBM UrbanCode Deploy サーバーにとって意味のある任意の方法で環境を分類することができます。


### デフォルトの論理環境

デフォルトでは、レポートは、文字列を使用して IBM UrbanCode Deploy 環境にマッチする論理環境を組み込みます。
例えば、名前に「dev」が含まれるすべての環境が DEV 論理環境にマップされ、名前に「prod」が含まれるすべての環境が PROD 論理環境にマップされます。


![デフォルトの論理環境](images/uc_insights_mapping.gif)

### 環境から論理環境へのマッピング

物理環境から論理環境へのマップは手動で行うことができます。
または、パターンを使用して、物理環境を論理環境に動的に関連付けることもできます。


物理環境を論理環境にマップするには、以下の手順を実行します。

1. Delivery Insights を開き、設定ボタンをクリックし、**「環境のマップ (Map Environments)」**をクリックします。
1. 「環境マッピング (Environment Mapping)」ページで、既存の論理環境をクリックするか、**「論理環境の追加 (Add Logical Environment)」**をクリックして論理環境を作成します。
1. 論理環境を選択したら、環境を論理環境にマップするためのパターンを指定できます。**「組み込まれているパターン (Included Patterns)」**の下で**「パターンの追加 (Add Pattern)」**をクリックして、使用するパターンを指定します。パターンに一致する名前を持つすべての環境 (これから作成する環境を含む) が論理環境に追加されます。ワイルドカードとしてアスタリスク (*) を使用できます。
例えば、パターン `env` は環境 `env1`、`env2`、`env` と一致します。

1. 環境を論理環境に手動でマップするには、**「手動での追加」**をクリックし、追加または削除する環境を選択します。

1. 意図した環境が論理環境に含まれていることを確認します。


![論理環境マッピングのセットアップ](images/uc_insights_mapping_manually.gif)

環境を論理環境にマップしたので、それらの論理環境ごとにレポート情報を集約することができます。

## 基幹業務への適用業務のマッピング
{: #lines}

基幹業務とは、共通の事業目的を果たす適用業務のグループです。適用業務を基幹業務にマップすると、グラフの中で適用業務のフィルター操作が容易になります。また、基幹業務に基づくグラフを作成することもできます。

基幹業務 (LOB: Line Of Business) をセットアップするには、以下の手順に従います。

1. {{site.data.keyword.DRA_short}} で**「Delivery Insights」**をクリックし、設定ボタンをクリックしてから、**「基幹業務のマップ (Map Lines of Business)」**をクリックします。
1. 「基幹業務のマッピング (Lines of Business Mapping)」ページで、既存の LOB をクリックするか、名前を入力して**「作成」**をクリックすることによって LOB を作成します。
1. LOB を選択したら、適用業務を LOB にマップするためのパターンを指定できます。**「組み込まれているパターン (Included Patterns)」**の下で**「パターンの追加 (Add Pattern)」**をクリックして、使用するパターンを指定します。パターンに一致する名前を持つすべての適用業務 (これから作成する適用業務を含む) が LOB に追加されます。ワイルドカードとしてアスタリスク (*) を使用できます。
例えば、パターン `env` は環境 `env1`、`env2`、`env` と一致します。

1. 適用業務を LOP に手動でマップすることもできます。これを行うには、**「個別にマップされた適用業務 (Individually Mapped Applications)」**をクリックしてから**「適用業務の追加 (Add Applications)」**をクリックします。

LOB をセットアップした後、グラフをフィルター操作して、特定の LOB に属する適用業務のみを表示することができます。他のグラフには、LOB に基づいてメトリックが表示されます。

## レポートの作成

レポートを作成するには、{{site.data.keyword.DRA_short}} を開き、**「Delivery Insights」**をクリックした後、**「レポートの追加」**をクリックします。**「レポートの追加」**が表示されない場合、IBM UrbanCode Deploy サーバーが接続されていません。設定ボタンをクリックしてから**「セットアップ」**をクリックして、サーバーを接続してください。

レポート内から、**「メトリック」**セクションにカードを追加したり、**「最近のアプリケーション・アクティビティー (Recent application activity)」**の下のアクティビティーをフィルター処理したり、**「レポートの詳細」**セクションにグラフを追加したりすることができます。
**「レポートの詳細」**セクション内のグラフは、それぞれ個別にフィルター処理やカスタマイズが可能です。
グラフの背後にある生データを見るには、グラフの右上で、グラフの「設定」ボタンをクリックして**「レポート・データ」**をクリックします。


グラフの順序を変更するには、ページの右上での「設定」ボタンをクリックした後、**「グラフのレイアウトの編集 (Edit Chart Layout)」**をクリックします。
次に、グラフをドラッグ・アンド・ドロップして、レポート上で順序を設定します。


## レポートの共有
デフォルトでは、Delivery Insights レポートを見ることができるのは作成した本人だけです。
Bluemix org 内の他のユーザーとレポートを共有することができます。
Bluemix org 内のだれかとレポートを共有するには、そのレポートを開き、レポートの右上にある「設定」ボタンをクリックした後、**「共有」**をクリックします。
  

![レポートの共有](images/uc_insights_sharing.gif)。


## 監査レポートの作成

監査レポートには、設定するフィルターに一致するすべてのアクティビティーのリストが PDF として表示されます。
監査レポートを作成するには、**「Delivery Insights」**をクリックし、設定ボタンをクリックしてから、**「監査レポートの作成 (Create Audit Report)」**をクリックします。次に、名前など、レポートの情報を指定します。
また、レポートのコンテキスト (アプリケーション、論理環境、IBM UrbanCode Deploy サーバー (物理環境) 上の環境など) も設定します。
そこから、レポートに表示するデータを選択して、**「作成」**をクリックします。
 

## トラブルシューティング
{: #troubleshooting}

多くのアプリケーションやコンポーネント・プロセスの要求が IBM UrbanCode Deploy サーバー・データベースに保管されている場合、取得プロセス中にエラーが発生する場合があります。
以下のテキストのようなメッセージが、サーバー出力ログに記録されます。


`ORA-01652: 表スペース TEMP で一時セグメントを 128 拡張できませんでした`

この動作を回避するには、プラグインの `plugin.properties` ファイルを編集して、何日分のデータを取り出すかを示す日数を削減します。`plugin.properties` ファイルは、DevOps Connect のインストール先コンピューター上の `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` ディレクトリーにあります。
以下の行を編集し、番号記号 (#) を削除して日数を減らしてください。


`#numDaysToRetrieve=90`

例えば、過去 30 日のデータのみ取り出すには、この行を下記のテキストに変更します。


`numDaysToRetrieve=30`

ファイルを保存し、統合を再び実行します。
サーバー・ログを調べて、エラーがもう発生しなくなっていることを確認してください。

