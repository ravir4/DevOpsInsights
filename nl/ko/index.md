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

# 시작하기 튜토리얼(베타)
{: #gettingstarted}

{{site.data.keyword.DRA_full}}는 가장 활발하게 진행 중인 DevOps 프로젝트에 개발자, 팀 및 배치 분석을 적용합니다. 이를 사용하여 팀이 DevOps 및 개발자 우수 사례를 준수하는 방법을 배우고, 코드 베이스에서 위험성을 관리하며, Continuous Delivery 프로젝트에서 자동으로 품질 표준을 적용할 수 있습니다. 
{:shortdesc}

{{site.data.keyword.DRA_short}}는 미국 남부 지역에서만 사용할 수 있습니다.
{: tip}

{{site.data.keyword.DRA_short}}를 사용하려면 도구 체인에 추가해야 합니다. 많은 도구 체인 템플리트에 이미 {{site.data.keyword.DRA_short}}가 포함되어 있습니다. 또한 {{site.data.keyword.DRA_short}}에 대한 정보를 확인하고 {{site.data.keyword.Bluemix_notm}} 대시보드에서 이를 포함하는 일부 도구 체인 템플리트에 액세스할 수 있도록 [이를 {{site.data.keyword.Bluemix_notm}} 리소스 그룹 또는 조직에 서비스로 추가](/docs/services/reqnsi.html)하십시오.   

## 1단계: 도구 체인에 DevOps Insights 추가
{: #catalog}

{{site.data.keyword.DRA_short}}는 {{site.data.keyword.contdelivery_full}} 도구 체인과의 통합을 통해 사용 가능합니다. 도구 통합 카탈로그에서 선택하여 도구 체인에 {{site.data.keyword.DRA_short}}를 추가할 수 있습니다.

{{site.data.keyword.DRA_short}}는 여러 도구 체인 템플리트의 일부입니다. {{site.data.keyword.DRA_short}}를 포함하는 템플리트에서 도구 체인을 작성하는 경우 {{site.data.keyword.DRA_short}}가 **고급**으로 설정되었는지 확인하십시오. 그런 다음 도구 체인을 작성하고 [2단계](/docs/services/DevOpsInsights/index.html#using)로 건너뛰십시오.
{: tip}

1. **도구에 추가**를 클릭하십시오.

2. **{{site.data.keyword.DRA_short}}**를 클릭하십시오.

3. **통합 작성**을 클릭하십시오.

{{site.data.keyword.DRA_short}}는 이제 도구 체인의 개요 페이지에서 사용할 수 있습니다.  사용자의 저장소 및 문제 추적 시스템이 데이터를 찾기 위해 자동으로 스캔됩니다. 

## 2단계: 프로젝트의 데이터 탐색
{: #using}

도구 체인에 GitHub, GitLab 또는 JIRA가 포함되어 있으면 {{site.data.keyword.DRA_short}}에서 초기 데이터 수집 및 분석 후에 자동으로 코드 베이스와 팀에 대한 정보를 제공합니다. 도구 체인이 이러한 통합을 포함하지 않는 경우에는 이러한 통합 중 하나를 추가하십시오.
{: tip}

1. 도구 체인의 개요 페이지에서 **{{site.data.keyword.DRA_short}}**를 클릭하십시오.

2. **Team ** 또는 **Developer Insights**를 클릭한 후 데이터 카테고리를 선택하십시오. 

3. 데이터 카테고리에서 대시보드를 확인하여 프로젝트의 데이터를 탐색하십시오. 그래프에 대한 자세한 정보 또는 이 정보를 사용하여 수행할 수 있는 작업에 대해 알아보려면 **정보** 또는 **안내**를 클릭하십시오.

## 다음 단계
{: #next_steps}

Team 및 Developer Insights를 탐색한 후에 코드 품질을 적용할 수 있도록 [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html)를 구성하십시오. Deployment Risk는 {{site.data.keyword.contdelivery_short}}의 Delivery Pipeline 및 Jenkins 둘 다와 호환 가능합니다.
