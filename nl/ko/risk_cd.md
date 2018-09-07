---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk 분석을 Continuous Delivery와 통합

{{site.data.keyword.DRA_short}}는 공개하는 테스트 데이터를 기반으로 배치 위험성을 추적합니다. 이 데이터는 단위 테스트, 코드 적용 범위, 기능 검증 테스트, SonarQube 데이터 또는 IBM Application Security on Cloud의 스캔 데이터를 포함할 수 있습니다. 이 데이터를 공개하고 나면 위험성 정책을 만족하지 않는 빌드를 중지할 수 있도록 파이프라인에 게이트를 추가할 수 있습니다.

{{site.data.keyword.DRA_short}}의 Deployment Risk 분석에 대한 상위 레벨 설명을 보려면 [Deployment Risk 정보](./about_risk.html)를 참조하십시오.

Continuous Delivery 파이프라인에 대한 자세한 정보는 [공식 문서](../ContinuousDelivery/pipeline_working.html)를 참조하십시오.

## 개요
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}}는 배치 위험성을 분석하기 위해 파이프라인의 다음 정보가 필요합니다.

* 빌드 레코드
* 배치 레코드
* 테스트 결과

테스트 결과는 다음과 같은 지원되는 형식으로 데이터를 제공해야 합니다.

|테스트 유형                    |지원되는 형식                                               |
|------------------------------|-----------------------------------------------------------------|
|기능 검증 테스트 |Mocha, xUnit                                                    |
|단위 테스트                    |Mocha, xUnit, Karma/Mocha                                       |
|코드 적용 범위                |Istanbul, Blanket.js, Cobertura, lcov                                           |
|정적 앱 스캔              |IBM Application Security on Cloud에서 제공하는 정적 앱 스캔  |
|동적 앱 스캔             |IBM Application Security on Cloud에서 제공하는 동적 앱 스캔 |
|SonarQube                    |SonarQube 스캔에서 제공하는 스캔 데이터                           |

파이프라인에 정의하는 환경 변수는 이러한 레코드를 공개하기 위해 컨텍스트를 제공합니다. 작업의 스크립트에서 `export` 명령을 사용하여 환경 변수를 정의할 수 있습니다. 또한 각 파이프라인 단계의 환경 특성 메뉴에서 환경 변수를 설정할 수 있습니다.

환경 변수:

|환경 변수  |목적 |필수인 경우 |
|-----------------------|-------- |-------------|
|`LOGICAL_APP_NAME`    |대시 보드의 앱 이름입니다. |{{site.data.keyword.DRA_short}} 위험성 정책을 빌드하고, 테스트하고, 배치하고, 적용하는 모든 작업. |
|`BUILD_PREFIX`  |단계의 빌드에 접두부로 추가되는 텍스트입니다. 이 텍스트도 대시보드에 표시됩니다. |{{site.data.keyword.DRA_short}} 위험성 정책을 빌드하고, 테스트하고, 배치하고, 적용하는 모든 작업. |
|`LOGICAL_ENV_NAME`  |애플리케이션을 실행하는 환경입니다. |테스트 및 배치 작업. |

이러한 변수를 다음과 같이 일관되게 사용해야 합니다.

* 특정 애플리케이션에 대한 모든 작업 또는 단계에서 동일한 `LOGICAL_APP_NAME`을 사용하십시오. 
* 특정 앱 및 빌드 유형에 대해 `BUILD_PREFIX` 값이 동일해야 합니다. 예를 들어, 마스터 분기의 빌드인 경우 `BUILD_PREFIX`가 `"master"`일 수 있습니다. 
* 해당 배치 작업 및 테스트 작업에서 동일한 `LOGICAL_ENVIRONMENT_NAME` 값을 사용하십시오. 배치 작업에서 `"PRODUCTION"`의 `LOGICAL_ENVIRONMENT_NAME` 값을 사용하는 경우 해당 환경에서 실행한 다른 테스트의 결과를 공개할 때 동일한 값을 사용하십시오.

## 빌드 작업 환경 변수

단계의 마지막 빌드 작업에 대해 애플리케이션 이름 및 빌드 접두부에 대한 환경 변수를 설정하십시오. 예제 스크립트에는 다음 명령이 포함됩니다.

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

이 빌드 작업이 완료되면 파이프라인은 SampleApp 빌드가 완료되었다는 메시지를 {{site.data.keyword.DRA_short}}에 공개합니다.

## 배치 작업 환경 변수

단계의 마지막 배치 작업에 대해 애플리케이션 이름, 빌드 접두부 및 환경 이름을 설정하십시오. 예제 스크립트에는 다음 명령이 포함됩니다.

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

배치 작업이 완료되면 파이프라인은 지정된 빌드 및 앱이 환경에 배치되었다는 메시지를 {{site.data.keyword.DRA_short}}에 공개합니다.

## 테스트 작업 환경 변수

테스트 결과를 생성하는 모든 작업에 대해 애플리케이션 이름 및 빌드 접두부를 설정하십시오.

작업이 기능 검증 테스트(FVT) 결과를 생성하는 경우 해당 테스트가 실행되는 모든 위치에 논리 환경도 설정해야 합니다.

예제 스크립트에는 다음 명령이 포함됩니다.

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## 테스트 결과 공개
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}}는 작업에서 테스트 결과를 사용하여 보고서를 생성하고 위험성 정책을 적용합니다.

파이프라인에서 모든 작업 유형을 사용하여 테스트를 실행할 수 있습니다. 해당 테스트를 실행한 후 결과를 {{site.data.keyword.DRA_short}}에 업로드할 수 있습니다. 작업의 쉘 스크립트에서 CLI를 호출하여 결과를 업로드합니다. 

CLI에서 다음 유형의 테스트 결과를 업로드할 수 있습니다.

* 단위 테스트
* 코드 적용 범위
* 기능 검증 테스트
* SonarQube 결과
* IBM Application Security on Cloud의 정적 및 동적 앱 스캔 결과 

다음은 테스트를 실행한 후 {{site.data.keyword.DRA_short}}에 결과를 업로드하는 예제 스크립트입니다. 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

해당 예제에서 `idra` 명령을 `--publishtestresult` 플래그와 함께 실행하면 스크립트가 결과를 업로드합니다. `--filelocation` 플래그는 작업의 루트 디렉토리에 상대적인 위치로 테스트 결과 파일의 위치를 표시합니다. `--type` 플래그는 실행하는 테스트의 유형을 표시합니다.

`idra` 명령은 다음 `type` 값을 지원합니다. 

|유형 |설명 |
|------|-------------|
|`unittest` |단위 테스트 결과 | 
|`fvt` |기능 검증 테스트 결과 |
|`code` |코드 적용 범위 결과 | 
|`sonarqube` |SonarQube 스캔 결과 | 
|`staticsecurityscan` |IBM Application Security on Cloud의 정적 보안 스캔 결과 |
|`dynamicsecurityscan` |IBM Application Security on Cloud의 동적 보안 스캔 결과 |

`idra` 명령에 대해 자세히 알아보려면 [grunt-idra3 package's page on npm](https://www.npmjs.com/package/grunt-idra3)을 참조하십시오. 

## 게이트 정의
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 게이트는 테스트 결과가 정의된 정책을 준수하는지 확인합니다. 정책을 준수하지 못하는 경우 기본적으로 {{site.data.keyword.DRA_short}} 게이트가 실패합니다. 실패한 후에도 파이프라인이 진행할 수 있도록 자문 역할로 조치를 수행하도록 게이트를 구성할 수 있습니다.

Deployment Risk 대시보드는 스테이징 배치 작업 후의 게이트 존재에 따라 달라집니다. 대시보드를 사용하려면 스테이징 환경에 배치한 후, 프로덕션 환경에 배치하기 전에 게이트가 있는지 확인하십시오.

일반적으로 파이프라인의 빌드 승격 전에 게이트를 배치합니다. 이 위치는 정책에 대해 빌드 품질을 점검하여 하나의 환경에서 다른 환경으로 승격하기에 안전한지 확인하는 데 적합합니다. 그러나 게이트는 특정 기준을 점검할 파이프라인의 임의의 위치에 배치할 수 있습니다. 스테이징 환경에 배치하기 전에 배치한 게이트가 여전히 정책을 적용하지만 Deployment Risk 대시보드에 표시되지 않습니다.

1. 단계에서 **단계 구성** 아이콘 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)을 클릭한 다음 **단계 구성**를 클릭하십시오.
2. **작업 추가**를 클릭하십시오. 작업 유형에 **테스트**를 선택하십시오.
3. 테스터 유형으로 **{{site.data.keyword.DRA_short}} 게이트**를 선택하십시오.
4. 환경 이름을 지정하십시오. 이 값이 [환경 특성](#toolchain_pipeline_props)에 정의된 값과 일치하는지 확인하십시오.
5. 이 게이트에서 검사할 정책 이름을 입력하십시오.

 이 이름은 정의된 정책 이름 중 하나와 정확히 일치해야 합니다. 같은 {{site.data.keyword.Bluemix_notm}} 조직에 정의된 정책만 도구 체인으로 지정할 수 있습니다.

6. 선택사항: 게이트 기능을 권장 모드로 작성하려면 **작업 실패 시 이 단계 실행 중지** 선택란을 선택 취소하십시오. 권장 모드에서는 {{site.data.keyword.DRA_short}}가 게이트에서 동일한 정책 분석을 완료하고 보고서를 생성하지만 실패하는 경우 파이프라인이 중지되지 않습니다.
7. **저장**을 클릭하여 파이프라인을 리턴하십시오.
8. 이러한 단계를 반복하여 모든 {{site.data.keyword.DRA_short}} 정책의 게이트를 설정하십시오.

![Deployment Risk Mocha 작업](images/insights_gate_job.png)
*그림 2. DevOps Insights 게이트*

파이프라인이 구성되고 나면 {{site.data.keyword.DRA_short}} 사용을 시작하십시오. 
