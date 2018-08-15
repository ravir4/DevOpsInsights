---

copyright:
  years: 2016, 2018
lastupdated: "2018-8-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# FAQs
{: #faqs}

Get answers to frequently asked questions about using {{site.data.keyword.DRA_full}}.

## How do I remove data that {{site.data.keyword.DRA_short}} mined from a repository?

Change the repository’s data filter so that it excludes the data that you want to remove. 

To change {{site.data.keyword.DRA_short}}’ data filter, click **Settings** and then **Filters**. 

## Some of my issues are missing. How do I add them?

If the issue-tracking service isn’t part of your toolchain, add it. {{site.data.keyword.DRA_short}} only mines services that are a part of the toolchain. 

If the issue-tracking service is part of your toolchain, check that {{site.data.keyword.DRA_short}}’ labels are mapped to the labels that your service uses. Click **Settings**, click **Labels**, and then verify the mapping.

As a last resort, remove the issue-tracking service from your toolchain. Then, add it back. {{site.data.keyword.DRA_short}} will mine the service from scratch. The mining can take a few hours. 

## How do I remine a repository?

To remine a repository, delete the {{site.data.keyword.DRA_short}} integration from your toolchain. Then, add it back.

## How can I add a repository to be mined?

Add it to a toolchain by clicking **Add a tool** on the toolchain’s overview page. After the repository is part of your toolchain, Insights will remine your data to include that repository.

Check the **Enable GitHub Issues** box while adding a repository to enable issue mining. 

## Why don’t I see any builds or deployments?

DevOps Insights automatically mines code repositories and issues that are part of a toolchain, but you must configure your pipeline for it to monitor builds and deployments. 

First, ensure that you have a Continuous Delivery or Jenkins pipeline in your toolchain. 

Then, verify that your pipeline is configured for build and deployment monitoring. To learn how to configure your pipeline, see the [Continuous Delivery integration documentation](risk_cd.html) or the [Jenkins integration documentation](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
