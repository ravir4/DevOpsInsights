---

copyright:
  years: 2016, 2018
lastupdated: "2018-4-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# DevOps Insights の概説 (ベータ)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} は、開発者、チーム、デプロイメントの分析を、最も忙しい DevOps プロジェクトに適用します。 それを使用することにより、チームが DevOps と開発者のプラクティスにどの程度準拠しているかを調べたり、コードベースのリスクを管理したり、継続的デリバリー・プロジェクトで品質基準を自動的に適用したりすることができます。
{:shortdesc}

**注**: {{site.data.keyword.DRA_short}} は、米国南部地域でのみ利用可能です。

{{site.data.keyword.DRA_short}} は、いくつかの機能グループで構成されています。

   * Developer Insights には、プロジェクトの開発成熟度を検討するための包括的な方法が用意されています。 エラーが発生しやすいファイルを識別したり、開発者プラクティスに対するプロジェクトの適合性を表示したりできます。

   * Team では、ソーシャル・コーディング分析を使用し、チームのコラボレーションの状況を調べて改善方法を理解することができます。


   * Deployment Risk は、継続的デリバリーのためのセーフティー・ネットのようなものです。デプロイメント・プロセス内の指定されたゲートで、単体テスト、機能テスト、セキュリティー・スキャン、アプリケーション・スキャン、およびコード・カバレッジ・ツールによる結果を分析し、リスクのある変更がリリースされるのを防ぎます。 コード・カバレッジ、ビルド、およびデプロイメントの傾向を示すグラフが表示されます。

{{site.data.keyword.DRA_short}} は、Bluemix オープン・ツールチェーン・カタログ内の統合の 1 つです。 ツールチェーンについて詳しくは、[ツールチェーンを使用した作業](/docs/services/ContinuousDelivery/toolchains_working.html)を参照してください。

{{site.data.keyword.DRA_short}} を使用するには、それをツールチェーンに追加する必要があります。 多くのツールチェーン・テンプレートには、{{site.data.keyword.DRA_short}} が既に含まれています。 さらに、[それを {{site.data.keyword.Bluemix_notm}} org にサービスとして追加する](/docs/services/reqnsi.html)ことにより、{{site.data.keyword.DRA_short}} に関する情報を表示したり、それを含むツールチェーン・テンプレートのいくつかに {{site.data.keyword.Bluemix_notm}} ダッシュボードからアクセスしたりできるようにしてください。  

さらに IBM は、GitHub 上で大成功を収めた数多くのオープン・ソース・プロジェクトに対して Developer Insights と Team を実行しています。それらの開発とチームのデータを参照するには、[DevOpsInsights.io](http://devopsinsights.io/) にアクセスしてください。

## DevOps Insights をツールチェーンに追加する
{: #catalog}

{{site.data.keyword.DRA_short}} は、{{site.data.keyword.contdelivery_full}} ツールチェーンとの統合によって使用できます。 ツール統合カタログから選択することにより、任意のツールチェーンに {{site.data.keyword.DRA_short}} を追加することができます。

{{site.data.keyword.DRA_short}} は、多くのツールチェーン・テンプレートの一部ともなっています。 {{site.data.keyword.DRA_short}} を含むテンプレートからツールチェーンを作成する場合、{{site.data.keyword.DRA_short}} が**「詳細」**に設定されていることを確認してください。 その上で、ツールチェーンを作成し、[「Insights の使用」](/docs/services/DevOpsInsights/index.html#using)に進んでください。

{{site.data.keyword.DRA_short}} をツールチェーンに追加するには、次のようにします。

1. **「ツールの追加 (Add a Tool)」**をクリックします。

2. **「{{site.data.keyword.DRA_short}}」** をクリックします。

3. **「統合の作成 (Create Integration)」**をクリックします。

{{site.data.keyword.DRA_short}} は、ツールチェーンの概要ページから利用できるようになりました。 ご使用のリポジトリーと問題追跡システムでデータを見つけるためのスキャンが自動的に実行されます。

## DevOps Insights の使用
{: #using}

ツールチェーンに GitHub、GitLab、JIRA が含まれている場合、{{site.data.keyword.DRA_short}} は、いくらかの初期データ収集と分析の後に、コードベースについての情報を自動的に提供します。 ツールチェーンにそれらの統合のどれも含まれていない場合は、それらのうちのいずれか 1 つを追加してから、以下の手順を実行します。

1. ツールチェーンの概要ページから、**「{{site.data.keyword.DRA_short}}」**をクリックします。

2. **「Team」**または**「Developer Insights」**をクリックした後、データのカテゴリーを選択します。

3. そのデータ・カテゴリーの中のダッシュボードを表示することにより、プロジェクトのデータを調べます。 グラフについて、またその情報の処理方法については、**「情報」**または**「ガイダンス」**をクリックしてください。

Team や Developer Insights で調べた後、[Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) を構成して、コード品質を強制的に確保することができます。Deployment Risk は、{{site.data.keyword.contdelivery_short}} 用 Delivery Pipeline と Jenkins の両方と互換性があります。
