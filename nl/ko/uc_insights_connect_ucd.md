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

# IBM UrbanCode Deploy 서버의 데이터 표시
{: #connect_ucd}

Delivery Insights에서 IBM UrbanCode Deploy 서버의 데이터를 보려면 DevOps Connect의 인스턴스를 설정하고 서버에 패치를 설치한 후에 해당 서버를 DevOps Connect에 연결해야 합니다.
{:shortdesc}

## 전제조건
{: #prereqs}

{{site.data.keyword.DRA_short}}의 IBM UrbanCode Deploy 서버에서 정보를 보려면 IBM UrbanCode Deploy 서버에 연결할 수 있는 DevOps Connect 인스턴스를 시스템에서 호스팅해야 합니다. 이 시스템은 실제 컴퓨터 또는 가상 머신일 수 있습니다. 

DevOps Connect를 호스팅하는 시스템에는 다음과 같은 전제조건이 있어야 합니다.
- 시스템에는 JRE(Java Runtime Environment) 버전 8 이상이 있어야 합니다.
- 시스템 `PATH` 변수에는 JRE 위치가 포함되어야 합니다.
- 시스템에서 DevOps Connect를 통해 IBM Bluemix에 대한 출력 연결을 작성할 수 있어야 합니다.

또한 IBM UrbanCode Deploy 서버는 버전 6.2 이상이어야 합니다. 

## {{site.data.keyword.DRA_short}} 서비스 구성
{: #configure_service}

{{site.data.keyword.DRA_short}} 서비스가 없는 경우 다음을 수행하십시오. 
1. {{site.data.keyword.Bluemix}}에 로그인하여 **서비스 > 대시보드**를 클릭하십시오.
1. **서비스 작성**을 클릭하십시오.
1. {{site.data.keyword.DRA_short}} 서비스를 클릭하십시오.
1. 가격 책정 플랜을 선택한 다음 **작성**을 클릭하십시오.
1. **관리**를 클릭한 다음 "UrbanCode 배치에 대해 통찰하기" 아래에서 **여기서 시작**을 클릭하십시오.
1. 도구 체인 템플리트 창에서 **작성**을 클릭하십시오.  
Delivery Insights가 조직의 도구 체인을 작성합니다. 도구 체인은 도구 통합의 콜렉션이며, 이 경우에 IBM UrbanCode Deploy 및 {{site.data.keyword.DRA_short}}는 도구 체인의 일부입니다. 도구 체인에 대한 자세한 정보는 [도구 체인 작업](../ContinuousDelivery/toolchains_working.html)을 참조하십시오.
1. 도구 체인에서 IBM UrbanCode Deploy 도구를 클릭하십시오.
1. 설정 단추를 클릭한 다음 **설정**을 클릭하십시오.

나중에 **서비스 > 대시보드**를 클릭하고 {{site.data.keyword.DRA_short}} 서비스의 인스턴스를 클릭하여 {{site.data.keyword.DRA_short}}로 이동할 수 있습니다. 

이미 도구 체인이 있으면 IBM UrbanCode Deploy 및 {{site.data.keyword.DRA_short}} 도구를 도구 체인에 추가하여 도구를 통해 Delivery Insights에 액세스할 수 있습니다. 그런 다음 IBM UrbanCode Deploy 도구를 클릭하고 설정 단추를 클릭한 다음 **설정**을 클릭하십시오.

이제 다음 절에서 설명하는 대로 **설정 지시사항** 페이지의 지시사항에 따라 DevOps Connect를 설치하고 이를 {{site.data.keyword.DRA_short}}에 연결할 수 있습니다. 

## DevOps Connect를 설치하고 이를 {{site.data.keyword.DRA_short}}에 연결
{: #install_connect}

1. **설정 지시사항** 페이지에서 DevOps Connect를 설정하고 IBM UrbanCode Deploy 서버에 연결하는 단계를 따르십시오.  이러한 단계에는 다음이 포함됩니다.
{: #set_up_connect}
  1. [전제조건](uc_insights_connect_ucd.html#prereqs)에서 설명한 대로 DevOps Connect를 실행하도록 시스템을 설정하십시오. 
  1. 실행 가능 JAR 파일에서 제공된 DevOps Connect를 다운로드하십시오. 

  1. 프록시를 사용하여 인터넷에 연결하는 경우 시스템 변수 `_JAVA_OPTIONS`를 다음 값으로 설정하십시오. 
    * 프록시가 HTTPS를 사용하는 경우 `_JAVA_OPTIONS`를 `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT`로 설정하십시오. 여기서 `HOSTNAME`은 프록시 서버의 호스트 이름이고 `PORT`는 프록시 서버의 HTTPS 포트입니다. 
    * 프록시가 HTTP를 사용하는 경우 `_JAVA_OPTIONS`를 `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT`로 설정하십시오. 여기서 `HOSTNAME`은 프록시 서버의 호스트 이름이고 `PORT`는 프록시 서버의 HTTP 포트입니다. 

  1. **설정 지시시항** 페이지에서 명령을 복사하십시오. 이 명령은 {{site.data.keyword.Bluemix}}에서 조직에 대한 연결을 허용하는 토큰으로 DevOps Connect를 시작합니다. 
  1. 기본적으로, DevOps Connect는 IBM UrbanCode Deploy 서버가 기본적으로 실행되는 동일한 포트인 포트 8443에서 실행됩니다. 그러므로 IBM UrbanCode Deploy 서버 또는 기타 서비스가 포트 844s에서 실행되는 경우 매개변수 `-Dserver.port`를 명령에 추가하여 DevOps Connect의 포트를 변경하십시오. 예를 들어, 포트 8888을 사용하도록 DevOps Connect를 설정하기 위해 명령은 다음과 같이 시작됩니다.   
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

전체 명령에는 다음 예제와 같이 DevOps Connect를 자동으로 구성하는 Bluemix 계정에 대한 정보가 포함됩니다. 

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. 명령을 실행하고 DevOps 연결이 시작될 때까지 기다리십시오. 

  1. 다음 절에서 설명하는 대로 IBM UrbanCode Deploy 서버를 DevOps Connect에 연결하십시오. 

## IBM UrbanCode Deploy 서버를 DevOps Connect에 연결
{: #connect_ucd_to_connect}

1. IBM UrbanCode Deploy 서버가 버전 6.2.5 이전인 경우 서버에 패치를 설치하십시오. 버전 6.2.5 이상에서는 패치가 필요하지 않습니다. 
  1. 다음 페이지에서 사용자의 IBM UrbanCode Deploy 버전에 적합한 올바른 패치를 다운로드하십시오. 예를 들어, IBM UrbanCode Deploy 6.2.4.x의 패치 파일 이름은 [ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar)입니다.  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. 서버를 중지하십시오. [서버 시작 및 중지](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html)를 참조하십시오.

  1. <code><em>application_data</em>/patches</code> 폴더에 배치 파일을 두십시오. 여기서 <code><em>application_data</em></code>는 서버 애플리케이션 데이터 폴더입니다. 기본 애플리케이션 데이터 폴더는 Linux에서는 `/opt/ibm-ucd/server/appdata`이며, Windows에서는 `C:\Program Files\ibm-ucd\server\appdata`입니다. 고가용성 시스템에서 애플리케이션 데이터 폴더는 항상 각 서버가 액세스할 수 있는 공유 네트워크 드라이브에 있습니다.

  1. 선택사항: 서버가 중지된 동안 이 서버에서 데이터 가져오기의 성능을 높이려면 데이터베이스에서 다음 SQL 명령을 실행하십시오. 버전 6.2.5 이상에서는 이 명령이 필요하지 않습니다.   
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  `MyUCDDatabase`의 데이터베이스 이름을 사용하십시오.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. 서버를 시작하십시오. 

    **참고:** IBM UrbanCode Deploy 서버가 시작되기까지 평소보다 더 오랜 시간을 기다려야 할 수도 있습니다. 서버가 끝내 시작되지 않거나 제대로 작동하지 않으면 패치 파일을 삭제한 후에 서버를 다시 시작하십시오. 패치 파일은 영구적으로 서버에 영향을 미치지 않습니다.

1. 서버가 DevOps Connect에 연결하려면 일부 IBM UrbanCode Deploy 버전에 추가 패치가 필요합니다. IBM UrbanCode Deploy 버전 6.2 - 6.2.1.2를 사용 중인 경우 서버에서 다음 추가 패치를 설치해야 합니다.
  1. 다음 패치를 다운로드하십시오. [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. 서버를 중지하십시오. 
  1. 패치 파일을 <code><em>application_data</em>/patches</code> 폴더에 두십시오.
  1. 서버를 시작하십시오.

1. DevOps Connect와 IBM UrbanCode Deploy 서버 사이에 통합을 작성하십시오.  

  **중요:** 통합을 처음 실행할 때 DevOps Connect에서 이전 90일 동안의 데이터를 검색합니다. 다량의 배치 데이터가 있으면 이 프로세스는 시간이 오래 걸릴 수 있습니다. 90일 미만 동안의 데이터를 검색하려면 [문제점 해결](uc_insights_connect_ucd.html#troubleshooting)을 참조하십시오.
  1. IBM UrbanCode Deploy에서 인증 토큰을 작성하십시오. [토큰](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html)을 참조하십시오.
  1. DevOps Connect에서 **통합**을 클릭한 다음 **새로 추가**를 클릭하십시오.
  1. 통합의 이름과 설명을 지정하십시오. DevOps Connect의 기본 위치는 `https://hostname:8443/`입니다. 여기서 `hostname`은 DevOps Connect를 호스트하는 시스템의 호스트 이름입니다.
  1. **통합 유형** 목록에서 **IBM UrbanCode Deploy for Cloud Reporting**을 선택하십시오.
  1. **서버 URI** 필드에 IBM UrbanCode Deploy 서버의 공용 URL(예: `https://my_UCD.example.com:8447`)을 입력하십시오.
  1. **인증 토큰** 필드 IBM UrbanCode Deploy를 통해 생성한 인증 토큰을 입력하거나 붙여넣으십시오.
  1. **관리 사용자** 필드에 쉼표로 구분된 IBM ID 목록을 입력하여 DevOps Connect 인터페이스에 대한 액세스 권한을 제공하십시오.
  1. 선택사항: **통합 실행**을 클릭하여 즉시 통합을 실행하십시오. 기본적으로 통합은 1분마다 실행됩니다.
  1. **저장**을 클릭하십시오. 

  ![DevOps Connect에서 통합 설정](images/uc_insights_dc_integration.gif)

이제 데이터가 Delivery Insights와 동기화됩니다. 이제 이 데이터를 기반으로 하는 보고서를 작성하고 볼 수 있습니다. 그 다음에는 IBM UrbanCode Deploy 서버의 환경을 Delivery Insights의 논리 환경에 맵핑하십시오. 

## 보고서에 환경 맵핑
{: #mapping}

### 논리 환경

Delivery Insights는 IBM UrbanCode Deploy 환경(*실제 환경*이라고도 함)을 하나 이상의 논리 환경으로 그룹화합니다. 이 방식으로 조직에 적합한 그룹으로 환경을 수집할 수 있습니다. 예를 들어 여러 애플리케이션에 맞는 여러 프로덕션 환경이 있으면 이 모든 환경을 하나의 논리 환경으로 그룹화하고 이 모든 환경의 메트릭을 단일 프로덕션 환경 대시보드로 결합할 수 있습니다. IBM UrbanCode Deploy 서버에 적합한 방식으로 환경을 그룹화할 수 있도록 검색 문자열별로 맵핑을 수행합니다.

### 기본 논리 환경

기본적으로 보고서에는 문자열을 사용하여 IBM UrbanCode Deploy 환경과 일치되는 논리 환경이 포함됩니다. 예를 들어, 이름에 "dev"가 포함된 모든 환경이 DEV 논리 환경에 맵핑되고 이름에 "prod"가 포함된 모든 환경이 PROD 논리 환경에 맵핑됩니다.

![기본 논리 환경](images/uc_insights_mapping.gif)

### 환경을 논리 환경에 맵핑

수동으로 실제 환경을 논리 환경에 맵핑하거나 패턴을 사용하여 동적으로 실제 환경을 논리 환경에 연관시킬 수 있습니다.

실제 환경을 논리 환경에 맵핑하려면 다음 단계를 따르십시오.

1. Delivery Insights를 열어 설정 단추를 클릭한 다음 **맵 환경**을 클릭하십시오.
1. 환경 맵핑 페이지에서 기존 논리 환경을 클릭하거나 **논리 환경 추가**를 클릭하여 논리 환경을 작성하십시오. 
1. 선택한 논리 환경을 통해 논리 환경에 환경을 맵핑하도록 패턴을 지정할 수 있습니다. **포함된 패턴**에서 **패턴 추가**를 클릭하고 사용할 패턴을 지정하십시오. 나중에 작성하는 환경을 포함하여 패턴과 일치하는 이름을 가진 모든 환경은 논리 환경에 추가됩니다. 별표(*)를 와일드카드로 사용할 수 있습니다. 예를 들어, `env` 패턴은 `env1`, `env2` 및 `env` 환경과 일치합니다.
1. 수동으로 환경을 논리 환경에 맵핑하려면 **수동으로 추가**를 클릭하고 추가 또는 제거할 환경을 선택하십시오.
1. 논리 환경에 원하는 환경이 포함되어 있는지 확인하십시오.

![논리 환경 맵핑 설정](images/uc_insights_mapping_manually.gif)

이제 논리 환경으로 환경을 맵핑했으므로, 해당 논리 환경으로 보고서 정보를 집계할 수 있습니다. 

## 애플리케이션을 LOB(Lines of Business)에 맵핑
{: #lines}

LOB(Lines of Business)는 공통 비즈니스 목적에 부합하는 애플리케이션의 그룹입니다. 애플리케이션을 LOB(Lines of Business)에 맵핑하여 차트에서 보다 쉽게 애플리케이션을 필터링할 수 있습니다. 또한 LOB(Lines of Business)를 기반으로 한 차트를 작성할 수 있습니다. 

LOB(Lines of Business)를 설정하려면 다음 단계를 따르십시오. 

1. {{site.data.keyword.DRA_short}}에서 **Delivery Insights**를 클릭하고 설정 단추를 클릭한 다음 **LOB(Lines of Business) 맵핑**을 클릭하십시오. 
1. LOB(Lines of Business) 페이지에서 기존 LOB를 클릭하거나 이름을 입력하고 **작성**을 클릭하여 LOB를 작성하십시오. 
1. 선택한 LOB를 통해 LOB에 애플리케이션을 맵핑하도록 패턴을 지정할 수 있습니다. **포함된 패턴**에서 **패턴 추가**를 클릭하고 사용할 패턴을 지정하십시오. 나중에 작성하는 애플리케이션을 포함하여 패턴과 일치하는 이름을 가진 모든 애플리케이션은 논리 환경에 추가됩니다. 별표(*)를 와일드카드로 사용할 수 있습니다. 예를 들어, `env` 패턴은 `env1`, `env2` 및 `env` 환경과 일치합니다.
1. **개별적으로 맵핑된 애플리케이션**을 클릭한 다음 **애플리케이션 추가**를 클릭하여 애플리케이션을 LOB에 수동으로 맵핑할 수 있습니다.

LOB를 설정한 후 차트를 필터링하여 특정 LOB에 애플리케이션만 표시할 수 있습니다. 다른 차트는 LOB 기반의 메트릭만 표시합니다. 

## 보고서 작성

보고서를 작성하려면 {{site.data.keyword.DRA_short}}를 열고 **Delivery Insights**를 클릭한 다음 **보고서 추가**를 클릭하십시오. **보고서 추가**가 표시되지 않으면 IBM UrbanCode Deploy 서버가 연결되지 않은 것입니다. 설정 단추를 클릭한 다음 **설정**을 클릭하여 서버에 연결하십시오. 

보고서에서 **메트릭** 섹션에 카드를 추가하고 **최근 애플리케이션 활동**에서 활동을 필터링한 다음 **보고서 세부사항** 섹션에 차트를 추가할 수 있습니다. **보고서 세부사항** 섹션의 각 차트는 개별적으로 필터링할 수 있고 사용자 정의할 수 있습니다. 차트 이면의 원시 데이터를 보려면 차트의 맨 위 오른쪽에서 차트 설정 단추를 클릭하고 **보고서 데이터**를 클릭하십시오.

차트의 순서를 변경하려면 페이지의 맨 위 오른쪽에서 설정 단추를 클릭하고 **차트 레이아웃 편집**을 클릭하십시오. 그런 다음 차트를 끌어서 놓아 보고서에서 순서를 설정할 수 있습니다.

## 보고서 공유
기본적으로 Delivery Insights 보고서만 볼 수 있습니다. Bluemix 조직의 다른 사용자와 보고서를 공유할 수 있습니다. Bluemix 조직의 사용자와 보고서를 공유하려면 보고서를 열고 보고서의 맨 위 오른쪽에서 설정 단추를 클릭한 다음 **공유**를 클릭하십시오.  

![보고서 공유](images/uc_insights_sharing.gif).

## 감사 보고서 작성

감사 보고서는 설정한 필터를 만족하는 모든 활동의 전체 목록을 PDF로 보여줍니다. 감사 보고서를 작성하려면 **Delivery Insights**를 클릭하고 설정 단추를 클릭한 다음 **감사 보고서 작성**을 클릭하십시오. 그런 다음 이름을 포함하여 보고서의 정보를 지정하십시오. IBM UrbanCode Deploy 서버(실제 환경)의 환경, 논리 환경 및 애플리케이션 등의 보고서 컨텍스트도 설정하십시오. 여기에서 보고서에 표시할 데이터를 선택하고 **작성**을 클릭하십시오. 

## 문제점 해결
{: #troubleshooting}

여러 애플리케이션과 컴포넌트 프로세스 요청이 IBM UrbanCode Deploy 서버 데이터베이스에 저장되어 있으면 검색 프로세스 중에 오류가 발생할 수 있습니다. 다음 텍스트와 비슷한 메시지가 서버 출력 로그에 기록됩니다.

`ORA-01652: 테이블스페이스 TEMP에서 임시 세그먼트를 128만큼 확장할 수 없음`

이 동작을 임시로 해결하려면 플러그인의 `plugin.properties` 파일을 편집하여 검색할 데이터 기간(일)을 줄이십시오. `plugin.properties` 파일은 DevOps Connect를 설치한 컴퓨터의 `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` 디렉토리에 있습니다. 다음 행을 편집하여 번호 부호(#)를 제거하고 기간(일)을 줄이십시오.

`#numDaysToRetrieve=90`

예를 들어, 행을 다음 텍스트로 변경하여 이전 30일 동안의 데이터만 검색하십시오.

`numDaysToRetrieve=30`

파일을 저장한 다음 통합을 다시 실행하십시오. 서버 로그를 확인하여 오류가 더 이상 발생하지 않는지 확인하십시오.
