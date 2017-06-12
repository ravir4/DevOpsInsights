---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Delivery Insights 정보
{: #about_delivery}

{{site.data.keyword.DRA_short}}의 일부인 Delivery Insights는 IBM UrbanCode Deploy 설치에 대한 배치 통계, 메트릭 및 기타 정보를 보여줍니다. 예를 들어 배치 기간, 성공 및 실패 차트를 보여주며 모두 논리적으로 그룹화된 환경별로 정렬합니다.
{:shortdesc}

Delivery Insights에서는 DevOps Connect의 설치가 필요합니다. 설치 정보는 [IBM UrbanCode Deploy 서버의 데이터 표시](uc_insights_connect_ucd.html)를 참조하십시오. 

![UrbanCode Insights 데모 데이터의 두 차트](images/uc_insights_demo_data.gif)

Delivery Insights에서 볼 수 있는 정보에는 다음이 포함됩니다.

- 배치 기간 및 시간 경과에 따른 배치 볼륨을 포함하는 배치에 대한 통계.
- 애플리케이션 및 환경별 배치 실패율에 대한 통계.
- 실패율, 배치 시간 및 기간 등의 컴포넌트 배치에 대한 통계.

## 시스템 개요
{: #systems_overview}

Delivery Insights의 토폴로지에는 온프레미스에 설치된 하나 이상의 IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> 및 DevOps Connect 유틸리티가 포함됩니다.

다음 다이어그램은 이러한 시스템의 일반적인 설치를 보여줍니다.

![고객 온프레미스 시스템과 IBM Cloud Services를 포함하는 UrbanCode Insights의 개요 토폴로지](images/uc_insights_overview_topology_multi_ucd.png)

- **IBM UrbanCode Deploy** 설치에서는 측정을 위해 성공 및 실패한 배치에 대한 정보를 제공합니다. IBM Bluemix DevOps Connect와 통신하려면 IBM UrbanCode Deploy에 패치가 필요합니다.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- 이전에는 IBM UrbanCode Sync Utility라고 한 **IBM Bluemix DevOps Connect**는 온프레미스에 설치된 IBM UrbanCode Deploy<!-- and IBM UrbanCode Release -->와 IBM 호스트 서비스(예: UrbanCode Insights) 사이의 통신을 조정합니다. DevOps Connect는 온프레미스 서버에 대해 안전한 HTTPS 통신과 토큰 인증을 사용하여 UrbanCode Insights에 데이터를 제공합니다. 

  토폴로지의 다른 시스템에 연결하려면 DevOps Connect에 플러그인이 필요합니다.

- {{site.data.keyword.DRA_short}}의 일부인 **Delivery Insights**는 IBM UrbanCode Deploy에서 배치 활동에 대한 메트릭을 제공하며, 이 메트릭에는 환경 그룹에 따라 배치 시간과 실패율이 포함됩니다. 권한은 {{site.data.keyword.Bluemix}} 계정별로 제어됩니다.
