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

# About Code
{: #gettingstarted}

{{site.data.keyword.DRA_full}} provides a comprehensive way to explore your project’s development risk. You can identify files with high error proneness and get a compliance view of the project against DevOps practices.
{:shortdesc}

After you open {{site.data.keyword.DRA_short}} from your toolchain, click **Code**. From there, you can select an analytic category to dive deeper into your project's codebase. What each set of data indicates can vary from team to team, and you can drill down into each visualization for help and guidance. You can filter the data by date, as well as many other criteria.

## Data categories
The data that {{site.data.keyword.DRA_short}} uses to populate its dashboards is mined automatically from your team's source-control repository. You can get more information about what the data means and how you can apply it to your project by clicking **Information** or **Guidance** on the Best Practices charts. You can also look at the Findings and Details that are part of the other visualizations for more information.

### Best practices

DevOps Insights provides a number of charts that measure your project against good DevOps and developer practices. Use this category to get a high-level view of your project's maturity, health, and efficiency.

### Issues

The Issues category displays all of your team's work-tracking issues in one place. The issues are automatically grouped by type, priority, and tag, and can be shown over time.

These issue groupings can vary in meaning from team to team. One team may tag issues to keep track of them but another team may not tag issues and instead use priority to drive their workloads. 

The trending tab shows issue trends over the timeframe.

### Commits

The Commits category displays all of your team's commits in one place. The commits are automatically grouped by type, tag, and priority. You can see them over a period of time that you choose.

Commits indicate the work that your team members are contributing to your codebase. Examine your commit data to understand where effort is being expended historically and how you can better balance your team members' workloads.

The trending tab shows issue trends over the timeframe.

The Error proneness tab highlights the commits that have a high probability of being error prone. A set of features derived from past issues, commits , authors (e.g frequency of files appearing in successive commits, large scale changes in files, average experience of authors in the project etc) are used to derive these probabilities, using Machine Learning.

### Files

The Files category shows which of your project's files are the busiest. Whether by number of line changes, commits, or defects, this data indicates where your team is most active.

The Error proneness tab highlights, in a sunburst view, the files that have a high probability of being error prone. Machine learning is used to derive these probabilities as discussed in the commits section.  The objective is to provide the developement team with a more focused list of files to code review to reduce future risk.

### Pull requests

The Pull requests category shows the team's pull requests in one place for the specified timeframe. The pull requests are evaluated for error proneness using machine learning (similar to commits and files as described above).  You can quickly see which pull requests are adding risk to your codebase.


## File extension filtering

DevOps Insights ignores files that have these extensions:

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml
