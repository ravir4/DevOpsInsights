---

copyright:
  years: 2016, 2018
lastupdated: "2018-8-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 入門チュートリアル (ベータ)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} は、開発者、チーム、デプロイメントの分析を、最も忙しい DevOps プロジェクトに適用します。 DevOps Insights を使用することにより、チームが DevOps や開発者のプラクティスにどの程度準拠しているかを確認したり、コードベースのリスクを管理したり、継続的デリバリー・プロジェクトで品質基準を自動的に適用したりすることができます。
{:shortdesc}

{{site.data.keyword.DRA_short}} は、米国南部地域でのみ利用可能です。
{: tip}

{{site.data.keyword.DRA_short}} を使用するには、それをツールチェーンに追加する必要があります。 多くのツールチェーン・テンプレートには、{{site.data.keyword.DRA_short}} が既に含まれています。 さらに、[DevOps Insights を {{site.data.keyword.Bluemix_notm}} のリソース・グループまたは組織にサービスとして追加](/docs/services/reqnsi.html)するようにしてください。これにより、{{site.data.keyword.Bluemix_notm}} ダッシュボードに {{site.data.keyword.DRA_short}} に関する情報を表示したり、{{site.data.keyword.Bluemix_notm}} ダッシュボードから DevOps Insights を含むツールチェーン・テンプレートのいくつかにアクセスしたりできるようになります。  

## ステップ 1: DevOps Insights をツールチェーンに追加する
{: #catalog}

{{site.data.keyword.DRA_short}} は、{{site.data.keyword.contdelivery_full}} ツールチェーンと統合することによって使用できるようになります。ツール統合カタログから選択することにより、任意のツールチェーンに {{site.data.keyword.DRA_short}} を追加することができます。

{{site.data.keyword.DRA_short}} は、多くのツールチェーン・テンプレートに含まれています。{{site.data.keyword.DRA_short}} を含むテンプレートからツールチェーンを作成する場合、{{site.data.keyword.DRA_short}} が**「詳細」**に設定されていることを確認してください。 その上で、ツールチェーンを作成してから、[「ステップ 2」](/docs/services/DevOpsInsights/index.html#using)に進んでください。{: tip}

1. **「ツールの追加 (Add a Tool)」**をクリックします。

2. **「{{site.data.keyword.DRA_short}}」** をクリックします。

3. **「統合の作成 (Create Integration)」**をクリックします。

{{site.data.keyword.DRA_short}} は、ツールチェーンの概要ページから利用できるようになりました。 ご使用のリポジトリーと問題追跡システムでデータを見つけるためのスキャンが自動的に実行されます。 

## ステップ 2: プロジェクトのデータを調べる
{: #using}

ツールチェーンに GitHub、GitLab、JIRA が含まれている場合、{{site.data.keyword.DRA_short}} は、いくらかの初期データ収集と分析の後に、コードベースについての情報を自動的に提供します。 ツールチェーンにそれらの統合のうちどれも含まれていない場合は、いずれか 1 つを追加します。
{: tip}

1. ツールチェーンの概要ページから、**「{{site.data.keyword.DRA_short}}」**をクリックします。

2. **「Team」**または**「Developer Insights」**をクリックした後、データのカテゴリーを選択します。 

3. そのデータ・カテゴリーの中のダッシュボードを表示することにより、プロジェクトのデータを調べます。 グラフについて、またその情報の処理方法については、**「情報」**または**「ガイダンス」**をクリックしてください。

## 次のステップ
{: #next_steps}

Team や Developer Insights で調べた後、[Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) を構成して、コード品質を強制的に確保することができます。 Deployment Risk は、{{site.data.keyword.contdelivery_short}} 用 Delivery Pipeline と Jenkins の両方と互換性があります。
