---

copyright:
  years: 2016, 2017
lastupdated: "2017-07-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating with Deployment Risk analytics with Continuous Delivery

You can instrument pipelines for {{site.data.keyword.contdelivery_full}} to use {{site.data.keyword.DRA_short}}' Deployment Risk analysis capabilities. For more information about Continuous Delivery pipelines, see [the official documentation](../ContinuousDelivery/pipeline_working.html).

Once you add {{site.data.keyword.DRA_short}} to your toolchain, define policies for it. Then, you can instrument your pipelines to send data to {{site.data.keyword.DRA_short}} and enforce those policies.

## Preparing pipeline stages and jobs
{: #integrate_pipeline}

To get started, you need to instrument your pipeline to communicate with {{site.data.keyword.DRA_short}}. You do this by defining specific environment variables for all of your pipeline jobs that build, test, and deploy code. 

The following variables are used for this instrumentation. You can define them by using the `export` command in your jobs' scripts. You can also set them in each pipeline stages' Environment Properties menu.

Environment variables:

| Property  | Purpose | Required in |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | The app's name on the dashboard. | All jobs that build, test, deploy and invoke {{site.data.keyword.DRA_short}} policies. |
| `BUILD_PREFIX`  | Text that is prepended to the stage's builds. This text also appears on the dashboard. | All jobs that build, test, deploy and invoke {{site.data.keyword.DRA_short}} policies. |
| `LOGICAL_ENV_NAME`  | The environment in which the application runs. | Test and deploy jobs. |

### Configuring build jobs

For build jobs in your pipeline, set environment variables for an application name and build prefix. An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

### Configuring deploy jobs

For the last deployment job in the stage, set an application name, build prefix, and environment name. An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

### Configuring test jobs

For all jobs that use Advanced Tester job type, set an application name and build prefix.

If the job publishes functional verification test (FVT) results, you must also set the logical environment name to wherever those tests run.

An example script would include these commands:

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Make sure that application names and environments match where appropriate. For example, you would want a production test job that runs against a production deployment to have identical `LOGICAL_ENV_NAME` values.


## Adding test jobs
{: #configure_pipeline_jobs}

You integrate {{site.data.keyword.DRA_short}} into your pipeline by using two kinds of test jobs: ones that upload results to {{site.data.keyword.DRA_short}} for analysis, and gates that act on that analysis. 

First, you add Advanced Tester jobs to your pipeline to run tests and upload the results. 

**Note:** If you want to update a test job to upload results to {{site.data.keyword.DRA_short}}, save its configurations in a convenient place before you proceed. Then, open its job configuration menu and skip to step 3. 

1. On the stage where you want to add the job that uploads results, click the **Stage Configuration** icon ![Pipeline stage configuration icon](images/pipeline-stage-configuration-icon.png). Click **Configure Stage**.
2. Create a test job and type a name for it. 
3. For the job type, select **Advanced Tester**.
4. Complete the **Test Command** and **Working Directory** fields as you would for a normal pipeline test job. 
5. Complete the remaining fields to upload the test results for a particular test type. 

 1. Choose the type of metric that matches what you defined in the {{site.data.keyword.DRA_short}} policy that you want to use.
 2. Type a result file location. This location is relative to the working directory. 

6. If you want to upload results for a second test type in the same job, complete the fields that are prefixed with *Additional*.
7. Click **Save** to return to the pipeline.

The values for the **Type of Metric** and **Result File Location** fields must match the correct format:

<table><thead>
<tr>
<th>Type of metric</th>
<th>Supported formats</th>
</tr>
</thead><tbody>
<tr>
<td>Functional Verification Test</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Unit Test</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Code Coverage</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

Figure 1 shows a test job that is configured to run unit tests, upload the results in Mocha format, and upload the code coverage results in Istanbul format.

![DevOps Insights upload job](images/insights_upload_job.png)
*Figure 1. Upload results to DevOps Insights*

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
