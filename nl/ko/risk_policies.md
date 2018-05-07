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

# 정책 및 규칙 작성
{: #policies_and_rules}

정책은 Delivery Pipeline에서 게이트를 제어하는 규칙 세트입니다. 코드가 특정 게이트에서 규정되는 정책을 만족하지 않거나 초과하는 경우 위험한 변경사항이 릴리스되지 못하도록 배치가 정지됩니다.

{{site.data.keyword.DRA_short}}에서 정책을 정의합니다. 정책은 {{site.data.keyword.DRA_short}}가 포함된 {{site.data.keyword.Bluemix_notm}} 조직(org)에 작성됩니다. 동일 조직의 모든 애플리케이션에서 이 정책을 사용할 수 있습니다. 

## 정책 작성
{: #create_policies}

정책을 작성하려면 다음을 수행하십시오.

1. {{site.data.keyword.DRA_short}} 탐색 메뉴에서 **설정**을 클릭하십시오.

2. **정책**을 클릭하십시오.

3. **정책 작성**을 클릭한 다음 새 정책의 이름과 설명을 입력하십시오.

4. **다음**을 클릭하십시오.

4. 정책에 규칙을 하나 이상 추가하십시오.
  1. **정책에 규칙 추가**를 클릭하십시오.
  2. 규칙 유형을 선택하십시오.
  3. 규칙의 세부사항과 조건을 입력하십시오.
  4. **저장**을 클릭하십시오.

5. 정책에 규칙을 추가한 다음 **완료**를 클릭하십시오.

## 규칙 작성
{: #creating_rules}

성공 또는 실패를 판단하기 위해 규칙을 통해 정책에서 사용하는 기준을 정의합니다. 단위 테스트가 80% 성공해야 하는 단위 테스트 규칙과 100% 코드가 적용되어야 하는 테스트 적용 범위 규칙을 포함하는 "단위 테스트 및 테스트 적용 범위" 정책을 작성할 수 있습니다. 파이프라인에서 이 규칙을 나타내는 게이트를 추가하면 게이트에서 이 두 규칙을 모두 만족하지 않는 빌드를 처리하지 못하게 합니다. 

테스트를 중요로 표시하여 테스트가 항상 성공이 되도록 할 수 있습니다. 규칙을 작성하려면 정책을 선택한 다음 **정책에 규칙 추가**를 클릭하십시오. 

### 기능 검증 테스트 규칙 작성
{: #criteria_fvt}

1. 설명을 입력하고 형식을 선택하십시오.

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오.

3. 중요한 테스트 케이스를 정의하십시오. 테스트 케이스 이름을 결정하려면 [테스트 결과 형식 및 도구](#criteria_formats)를 참조하십시오.

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오.

5. **저장**을 클릭하십시오.


### 단위 테스트 규칙 작성
{: #criteria_ut}

1. 설명을 입력하고 형식을 선택하십시오.

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오.

3. 중요한 테스트 케이스를 정의하십시오. 테스트 케이스 이름을 결정하려면 [테스트 결과 형식 및 도구](#criteria_formats)를 참조하십시오.

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오.

5. **저장**을 클릭하십시오.


### 코드 적용 범위 규칙 작성
{: #criteria_codecoverage}

1. 설명을 입력하고 형식을 선택하십시오.

2. 성공한 것으로 선언하는 데 필요한 코드 적용 범위의 백분율을 지정하십시오.

3. 코드 적용 범위 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오.

4. **저장**을 클릭하십시오.

### 정적 보안 스캔 규칙 작성
{: #criteria_static}

{{site.data.keyword.DRA_short}}를 IBM Application Security on Cloud와 통합하여 정적 코드 및 동적 앱 스캔을 실행할 수 있습니다. Application Security on Cloud에 대한 자세한 정보는 [공식 문서](/docs/services/ApplicationSecurityonCloud/index.html)를 참조하십시오.

1. 설명을 입력하십시오.

2. 규칙에서 허용하는 심각도가 높음, 중간 및 낮음인 문제의 최대수를 지정하십시오. 

3. **저장**을 클릭하십시오.

### 동적 보안 스캔 규칙 작성
{: #criteria_dynamic}

{{site.data.keyword.DRA_short}}와 {{site.data.keyword.appseccloudfull}}를 통합하여 동적 앱 스캔을 실행할 수 있습니다. Application Security on Cloud에 대한 자세한 정보는 [공식 문서](/docs/services/ApplicationSecurityonCloud/index.html)를 참조하십시오.

1. 설명을 입력하십시오.

2. 규칙에서 허용하는 심각도가 높음, 중간 및 낮음인 문제의 최대수를 지정하십시오. 

3. **저장**을 클릭하십시오.

## 결과 형식과 도구 테스트
{: #criteria_formats}

테스트 결과에 대해 {{site.data.keyword.DRA_short}}는 다음 유형의 메트릭과 형식을 지원합니다.

* 기능 검증 테스트(Mocha, xUnit)
* 단위 테스트(Mocha, xUnit, Karma/Mocha)
* 코드 적용 범위(Cobertura, lcov, JSON 요약 보고서 형식의 Istanbul, Blanket.js)

{{site.data.keyword.DRA_short}}는 Selenium과 Jasmine 테스트도 지원합니다. 이러한 테스트는 공식 지원 도구(예: xUnit 및 Mocha)에 포함되어 있어야 합니다. {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}}, Selenium을 함께 사용하는 방법을 보려면 [Delivery Pipeline의 명령행에서 Selenium 테스트 실행](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)의 내용을 참조하십시오.

테스트 케이스가 있는 항목의 경우 중요 테스트 케이스(허용 가능한 백분율에 관계없이 패스해야 하는 테스트)를 지정할 수 있습니다. 중요 테스트 케이스 이름은 테스트 케이스의 `full title` 속성과 일치해야 합니다.    
* Karma/Mocha 테스트의 경우 `describe()` 및 `it()` 설명 문자열이 공백을 사용하여 함께 연결됩니다.
* xUnit 테스트의 경우, 패키지 이름, 클래스 이름, 기능 이름이 공백을 사용하여 함께 연결됩니다. 다음 예제에서는 이를 보여줍니다.
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  이 예제는 다음과 같은 테스트 케이스 이름을 생성합니다.
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Sauce Labs 도구 통합을 파이프라인에 추가하여 Sauce Labs을 {{site.data.keyword.DRA_short}}와 함께 사용할 수 있습니다. 그러면 `SAUCE_USERNAME` 및 `SAUCE_ACCESS_KEY` 환경 변수를 신임 정보로 사용하여 Selenium 테스트에 통합할 수 있습니다.

실행 후 로그에서 전체 테스트의 전체 제목을 볼 수 있습니다.  

**참고:**
* {{site.data.keyword.DRA_short}}는 전체 제목 안에 하이픈이 포함된 중요 테스트를 지원하지 않습니다.    
* 조직 이름을 변경하는 경우, 이전 이름과 연관된 정책을 다시 작성해야 합니다. 이름 변경 전에 생성된 모든 의사결정 보고서에 대한 액세스는 유실됩니다.
