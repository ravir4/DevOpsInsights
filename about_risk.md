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

# About Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk provides a wealth of information about your deployments, particularly risk. You can use it to automate quality protection in your delivery pipeline by using policies and gates. It provides data about build and deployment frequency, along with code coverage and testing trends.
{:shortdesc}

After you open {{site.data.keyword.DRA_short}} from your toolchain, click **Deployment Risk**. From there, you can select an analytic category to dive deeper into what is happening with your deployments.  

You can use Deployment Risk to enforce quality standards in your toolchain through policies and gates. Policies comprise sets of rules; gates enforce policies. For example, you might create a "Unit Testing and Test Coverage" policy that requires builds to meet unit testing and test coverage standards. You then add a gate that refers to the policy to your continuous delivery process. Builds that do not satisfy the policy are stopped at that gate. 

## Risk analysis

With risk analysis, you get an overview of the risks associated with applications in your staging and production environments. You can drill down to understand code coverage, test performance, and security reports. The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} tests.

## Deployment frequency

You can view deployment frequency trends for your production, staging, or other environments. This view also shows deployment success and failures. You can click a particular deployment to see details about it. If you're on an agile team, you should see the deployment frequency trend upward over time. 

## Build frequency

You can view build frequency trends for your long-running branches. This view also shows build successes and failures. You can click a point of interest and see build details. If you're on an agile team, you want to see a lot of daily builds on the integration branch. Otherwise, your team is not merging their code frequently.

## Unit test trends

You can view trends for unit tests for the builds that are from a certain branch or are deployed to a certain environment. For example, you can see test trends for builds from the master branch. If some tests fail for builds that went to production, you might want to take some action. Also, if the number of tests are dwindling over time, that might be a cause for concern.

## Function verification test trends

You can view trends for functional verification tests for the builds that are from a certain branch or are deployed to a certain environment. For example, you can see test trends for builds from the master branch. If some tests fail for builds that went to production, you might want to take some action. Also, if the number of tests are dwindling over time, that might be a cause for concern.

## Code Coverage trends

You can view code coverage trends for the builds that are deployed to a certain environment. For example, you can see code coverage trends for builds that went to production. Ideally, you should see that code coverage improves over time for builds that go to production. If code coverage is decreasing, you might want to take action.

## Policies

Policies are sets of rules that control the gates in your delivery pipeline. If your code does not meet or exceed a policy that is enacted at a particular gate, the deployment is halted to prevent risky changes from being released.


## Prerequisites
{: #prerequisites}

Deployment Risk requires some configuration beyond what is described in [Getting Started with {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

To use Deployment Risk, you need two things:

* An instance of {{site.data.keyword.deliverypipeline}} or a Jenkins project
* Tests that you want to use to evaluate your project

## Integration information

Deployment Risk integrates with {{site.data.keyword.deliverypipeline}}, which is part of {{site.data.keyword.contdelivery_full}}, and with Jenkins projects. At a high level, the instructions for using either are similar.  

If you are using {{site.data.keyword.deliverypipeline}}, follow these steps:

1. [Create policies and rules](risk_policies.html) for {{site.data.keyword.DRA_short}} to manage.
2. [Prepare your pipeline's stages](risk_cd.html) for integration with {{site.data.keyword.DRA_short}}.
3. [Create or edit test jobs](risk_cd.html) in the pipeline that upload results to {{site.data.keyword.DRA_short}}.
4. [Add gates](risk_cd.html) to the pipeline that makes promotion decisions based on those results and your policies.
5. Run the pipeline and [view the results](results.html).

If you are using Jenkins, follow these steps:

1. [Create policies and rules](risk_policies.html) for {{site.data.keyword.DRA_short}} to manage.
2. [Install and configure the Jenkins plugin](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Create test jobs and gates as described in the plugin instructions](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). The tests upload results to {{site.data.keyword.DRA_short}} for analysis and the gates use those results to make promotion decisions.
4. Run the project and [view the results](results.html). 

No matter how you build and deploy your code, the results are the same: the builds that meet standards will move past the Deployment Risk gates, and builds that don't meet standards are stopped. 
