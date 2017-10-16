---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Delivery Insights について
{: #about_delivery}

{{site.data.keyword.DRA_short}} の一部である Delivery Insights は、IBM UrbanCode Deploy インストール済み環境に関するデプロイメントの統計やメトリックなどの情報を表示します。
例えば、デプロイメントの期間、成功、失敗のグラフを、論理的に分類した環境別にすべてソートした状態で表示することができます。
{:shortdesc}

Delivery Insights を使用するには、DevOps Connect のインストールが必要です。セットアップ情報については、[IBM UrbanCode Deploy サーバーにあるデータの表示](uc_insights_connect_ucd.html)を参照してください。

![UrbanCode Insights デモ・データに基づく 2 つのグラフ](images/uc_insights_demo_data.gif)

Delivery Insights で表示できる情報の中には、以下のものが含まれます。


- デプロイメントに関する統計。デプロイメントの期間や時間経過とともに変化するデプロイメント・ボリュームを含む。
- アプリケーション別、また環境別のデプロイメントの失敗率に関する統計。
- コンポーネントのデプロイメントに関する統計。失敗率、デプロイメント時刻、期間などを含む。

## システムの概要
{: #systems_overview}

Delivery Insights のトポロジーには、IBM UrbanCode Deploy や DevOps Connect ユーティリティーの 1 つ以上のオンプレミス・インストール済み環境が含まれます。<!-- (and optionally IBM UrbanCode Release) -->


以下の図は、それらのシステムの標準的なインストールを示しています。


![UrbanCode Insights のトポロジーの概要。これにはお客様のオンプレミス・システムと IBM クラウド・サービスが含まれます](images/uc_insights_overview_topology_multi_ucd.png)

- **IBM UrbanCode Deploy** のインストール済み環境は、成功したデプロイメントと失敗したデプロイメントについての情報をメトリック用に提供します。
IBM UrbanCode Deploy には、IBM Bluemix DevOps Connect と通信するためのパッチが必要です。


<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect** (旧称 IBM UrbanCode Sync Utility) は、IBM UrbanCode Deploy のオンプレミス・インストール済み環境と、IBM ホストのサービス (UrbanCode Insights など) との間の通信を調整します。<!-- and IBM UrbanCode Release -->
DevOps Connect は、オンプレミス・サーバーとのセキュア HTTPS 通信とトークン認証を使用することにより、UrbanCode Insights にデータを提供します。


  DevOps Connect が、トポロジー内の他のシステムと接続するためには、プラグインが必要です。


- {{site.data.keyword.DRA_short}} の一部である **Delivery Insights** は、IBM UrbanCode Deploy 上のデプロイメント・アクティビティーに関するメトリックを提供します。
これには、デプロイメントの回数や、環境グループごとの失敗率が含まれます。
権限は、{{site.data.keyword.Bluemix}} アカウントによって制御されます。

