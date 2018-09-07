---

copyright:
  years: 2018
lastupdated: "2018-8-2"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# DevOps Insights での個人データの管理
{: insights_personal_data}

収集されて {{site.data.keyword.DRA_full}} に保管されている個人データを削除することができます。
{: shortdesc}

{{site.data.keyword.DRA_short}} に保管されているデータには、ツールチェーン ID でインデックス付けされます。 ツールチェーンを削除すると、ツールチェーンの一部として収集されたリポジトリーに関連するすべてのデータが削除されます。

IBM では、{{site.data.keyword.DRA_short}} サービス内にあるデータを管理しません。{{site.data.keyword.DRA_short}} サービスを終了する前に、ユーザー自身のデータを削除する必要があります。このデータを削除するには、ツールチェーンから {{site.data.keyword.DRA_short}} ツール統合を削除してください。{{site.data.keyword.DRA_short}} ツール統合が 7 日以内に再度ツールチェーンに追加されない場合、そのデータは削除されます。
{: tip}

## {{site.data.keyword.DRA_short}} からのデータの削除
{: #insights_delete_data}

次の表に、{{site.data.keyword.DRA_short}} からデータを削除するシナリオと、{{site.data.keyword.DRA_short}} の各カテゴリーへの影響をリストします。

|  |Developer Insights と Team Insights |Deployment Risk|Security Insights |
|---------|-------------|-------------|-------------|
| [リポジトリーの削除 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	リポジトリーに関連するすべてのデータが削除されます。  | N/A | N/A |
| [{{site.data.keyword.DRA_short}} ツール統合の削除 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	リポジトリーに関連するすべてのデータが削除されます。  |ツール統合が含まれているツールチェーンに関連付けられているすべてのデータが削除されます。 |ツール統合が含まれているツールチェーンに関連付けられているリポジトリーに関連するすべてのデータが削除されます。  |
| [ツールチェーンの削除 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |ツールチェーンに関連付けられているリポジトリーに関連するすべてのデータが削除されます。 |ツールチェーンに関連付けられているすべてのデータが削除されます。  |ツールチェーンに関連付けられているすべてのデータが削除されます。  |
| [パイプラインの削除 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/A | N/A | N/A |
{:caption="表 1. データ削除のシナリオ" caption-side="top"}

## {{site.data.keyword.DRA_short}} ツール統合の削除
{: #insights_delete_integration}

ツール統合をツールチェーンから削除すると、その削除を取り消すことはできません。

1. DevOps ダッシュボードの**「ツールチェーン」**ページでツールチェーンをクリックして、そのツールチェーンの「概要」ページを開きます。 あるいは、アプリケーションの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックしてから**「概要」**をクリックします。
1. 削除する {{site.data.keyword.DRA_short}} ツール統合のカードで、メニューをクリックして構成オプションにアクセスします。
1. ツール統合をツールチェーンから削除するために、**「削除」**をクリックします。

  ![構成メニュー](images/delete_insights_integration.png)

1. 確認のため**「削除」**をクリックします。 
