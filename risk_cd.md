---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating Deployment Risk analytics with Continuous Delivery

{{site.data.keyword.DRA_short}} tracks deployment risk based on the test data that you publish to it. This data might include unit tests, code coverage, functional verification tests, SonarQube data, or scan data from IBM Application Security on Cloud. After you publish this data, you can add gates to your pipelines so that you can stop builds that don't meet risk policies.

To see a high-level explanation of {{site.data.keyword.DRA_short}}' Deployment Risk analysis, see [About Deployment Risk](./about_risk.html).

For more information about Continuous Delivery pipelines, see [the official documentation](../ContinuousDelivery/pipeline_working.html).

## Overview
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} requires this information from your pipeline to analyze deployment risk:

* Build records
* Deployment records
* Test results

Test results must provide data in one of these supported formats:

| Test type                    | Supported formats                                               |
|------------------------------|-----------------------------------------------------------------|
| Functional verification test | Mocha, xUnit                                                    |
| Unit test                    | Mocha, xUnit, Karma/Mocha                                       |
| Code coverage                | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Static App Scan              | Static App Scans provided by IBM Application Security on Cloud  |
| Dynamic App Scan             | Dynamic App Scans provided by IBM Application Security on Cloud |
| SonarQube                    | Scan data provided by SonarQube scans                           |

Environment variables that you define in the pipeline provide context for publishing these records. You can define them by using the `export` command in your jobs' scripts. You can also set them in each pipeline stages' Environment Properties menu.

Environment variables:

| Environment Variable  | Purpose | Required in |
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`    | The app's name on the dashboard. | All jobs that build, test, deploy, and enforce {{site.data.keyword.DRA_short}} risk policies. |
| `BUILD_PREFIX`  | Text that is added as a prefix to the stage's builds. This text also appears on the dashboard. | All jobs that build, test, deploy, and enforce {{site.data.keyword.DRA_short}} risk policies. |
| `LOGICAL_ENV_NAME`  | The environment in which the application runs. | Test and deploy jobs. |

Be sure to use these variables consistently:

* For a particular application, use the same `LOGICAL_APP_NAME` in all jobs or stages. 
* The `BUILD_PREFIX` value should be the same for a particular app and build type. For example, for builds from the master branch, `BUILD_PREFIX` could be `"master"`. 
* Use the same `LOGICAL_ENVIRONMENT_NAME` value in corresponding deploy jobs and test jobs. If you use the `LOGICAL_ENVIRONMENT_NAME` value of `"PRODUCTION"` in a deploy job, use that same value when you publish results from tests that also ran in that environment.

## Build job environment variables

For the last build job in a stage, set environment variables for an application name and build prefix. An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

When this build job completes, the pipeline would publish a message to {{site.data.keyword.DRA_short}} that a SampleApp build is completed.

## Deploy job environment variables

For the last deployment job in the stage, set an application name, build prefix, and environment name. An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

When your deployment job ends, the pipeline would publish a message to {{site.data.keyword.DRA_short}} that the specified build and app was deployed to an environment.

## Test job environment variables

For all jobs that produce test results, set an application name and build prefix.

If the job generates functional verification test (FVT) results, you must also set the logical environment name to wherever those tests run.

An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## Publishing test results
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} uses the test results from your jobs to generate reports and enforce risk policies.

In a pipeline, you can use any job type to run a test. After you run that test, you can upload its results to {{site.data.keyword.DRA_short}}. You upload the results by invoking a CLI in the job's shell script. 

You can upload these types of test results from the CLI:

* Unit tests
* Code coverage
* Functional verification tests
* SonarQube results
* Static and Dynamic app scan results from IBM Application Security on Cloud. 

This is an example script that runs tests and then uploads the results to {{site.data.keyword.DRA_short}}: 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

In that example, the `idra` command run with the `--publishtestresult` flag specifies that the script will upload results. The `--filelocation` flag indicates the location of the test results file relative to the root directory of the job. The `--type` flag indicates the type of tests that run.

The `idra` command supports the following `type` values: 

| Type | Description |
|------|-------------|
| `unittest` | Unit test results | 
| `fvt` | Functional verification test results |
| `code` | Code coverage results | 
| `sonarqube` | SonarQube scan results | 
| `staticsecurityscan` | Static security scan results from IBM Application Security on Cloud |
| `dynamicsecurityscan` | Dynamic security scan results from IBM Application Security on Cloud |

To learn more about the `idra` command, see [the grunt-idra3 package's page on npm](https://www.npmjs.com/package/grunt-idra3). 

## Defining gates
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} gates check whether your test results comply with a defined policy. If the policy is not met, the {{site.data.keyword.DRA_short}} gate fails by default. You can also configure gates to act in an advisory role to permit pipeline progression even after failure.

The Deployment Risk dashboard relies on the presence of a gate after a staging deployment job. If you want to use the dashboard, make sure that you have a gate after you deploy to the staging environment, but before you deploy to a production environment.

Usually, gates are placed before build promotion in your pipeline. These locations are ideal to check the quality of the build against your policies to ensure that it is safe to promote from one environment to another. However, you can put gates anywhere in the pipeline where you want a specific criterion to be checked. Gates that are placed before you deploy to a staging environment will still enforce policies, but they will not appear on the Deployment Risk dashboard.

1. On a stage, click the **Stage Configuration** icon ![Pipeline stage configuration icon](images/pipeline-stage-configuration-icon.png) and click **Configure Stage**.
2. Click **Add Job**. For the job type, select **Test**.
3. For tester type, select **{{site.data.keyword.DRA_short}} Gate**.
4. Specify the environment name. Make sure that this value matches what was defined in your [environment properties](#toolchain_pipeline_props).
5. Enter the policy name to check at this gate.

 This name must exactly match one of the policy names that you defined. You can specify only policies that are defined in the same {{site.data.keyword.Bluemix_notm}} organization as your toolchain.

6. Optional: To make a gate function in advisory mode, clear the **Stop running this stage if this job fails** check box. In advisory mode, {{site.data.keyword.DRA_short}} completes the same policy analysis at the gate and generates reports, but if a failure occurs, the pipeline is not stopped.
7. Click **Save** to return to the pipeline.
8. Set up gates for all of your {{site.data.keyword.DRA_short}} policies by repeating these steps.

![Deployment Risk Mocha job](images/insights_gate_job.png)
*Figure 2. DevOps Insights gate*

After your pipeline is configured, start to use {{site.data.keyword.DRA_short}}. 
