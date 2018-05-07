---

copyright:
  years: 2016, 2018
lastupdated: "2018-3-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 자주 묻는 질문(FAQ)
{: #faqs}

이 페이지는 {{site.data.keyword.DRA_full}}에 대한 자주 업데이트되는 FAQ 목록입니다. 

## {{site.data.keyword.DRA_short}}가 저장소에서 마이닝한 데이터를 어떻게 제거하나요?

제거하려는 데이터를 제외하도록 저장소의 데이터 필터를 변경하십시오.  

{{site.data.keyword.DRA_short}}의 데이터 필터를 변경하려면, **설정**을 클릭한 후 **필터**를 클릭하십시오. 

## 내 문제 중 몇 가지가 누락되었습니다. 어떻게 추가하나요? 

문제 추적 서비스가 도구 체인의 일부가 아닌 경우 이를 추가하십시오. {{site.data.keyword.DRA_short}}는 도구 체인의 일부인 서비스만 마이닝합니다.  

문제 추적 서비스가 도구 체인의 일부라면 {{site.data.keyword.DRA_short}}의 레이블이 서비스가 사용하는 레이블에 맵핑되어 있는지 확인하십시오. **설정**을 클릭하고 **레이블**을 클릭한 후 맵핑을 확인하십시오.

마지막 방법으로 도구 체인에서 문제 추적 서비스를 제거하십시오. 그런 다음 이를 다시 추가하십시오. {{site.data.keyword.DRA_short}}가 서비스를 처음부터 새로 마이닝합니다. 마이닝 작업은 몇 시간 정도 걸릴 수 있습니다.  

## 저장소를 다시 마이닝하려면 어떻게 해야 하나요?

저장소를 다시 마이닝하려면, 도구 체인에서 {{site.data.keyword.DRA_short}} 통합을 삭제하십시오. 그런 다음 이를 다시 추가하십시오. 

## 마이닝할 저장소를 어떻게 추가할 수 있나요?

도구 체인의 개요 페이지에서 **도구 추가**를 클릭하여 도구 체인에 이를 추가하십시오. 저장소가 도구 체인의 일부가 되면 Insights에서 해당 저장소를 포함하도록 데이터를 다시 마이닝합니다. 

문제 마이닝이 사용으로 설정되도록 저장소를 추가하는 동안 **GitHub 문제 사용** 상자를 선택하십시오.  

## 빌드 또는 배치가 보이지 않는 이유는 무엇인가요? 

DevOps Insights는 도구 체인의 일부인 문제 및 코드 저장소를 자동으로 마이닝하지만 빌드 및 배치를 모니터하려면 파이프라인을 구성해야 합니다.  

먼저 도구 체인에 Continuous Delivery 또는 Jenkins 파이프라인이 있는지 확인하십시오.  

그런 다음 파이프라인이 빌드 및 배치 모니터링에 대해 구성되어 있는지 확인하십시오. 파이프라인을 구성하는 방법에 대해서는 [Continuous Delivery 통합 문서](risk_cd.html) 또는 [Jenkins 통합 문서](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin)를 참조하십시오. 
