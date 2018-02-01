---

copyright:
  years: 2017, 2018

lastupdated: "2017-07-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Showing data from IBM UrbanCode Deploy servers
{: #connect_ucd}

To see data from an IBM UrbanCode Deploy server in Delivery Insights, you must set up an instance of DevOps Connect, install a patch on the server, and then connect that server to DevOps Connect.
{:shortdesc}

## Prerequisites
{: #prereqs}

To see information from your IBM UrbanCode Deploy servers in {{site.data.keyword.DRA_short}}, you must host an instance of DevOps Connect on a system that can connect to your IBM UrbanCode Deploy servers. This system can be a physical computer or a virtual machine. 

The system that hosts DevOps Connect must have the following prerequisites:
- The system must have a Java Runtime Environment (JRE) version 8 or later.
- The system `PATH` variable must include the location of the JRE.
- The system must allow DevOps Connect to create outgoing connections to IBM Bluemix.

Also, your IBM UrbanCode Deploy server must be at version 6.2 or later.

## Configuring the {{site.data.keyword.DRA_short}} service
{: #configure_service}

If you do not have the {{site.data.keyword.DRA_short}} service, add it:
1. Log in to {{site.data.keyword.Bluemix}} and click **Services > Dashboard**.
1. Click **Create service**.
1. Click the {{site.data.keyword.DRA_short}} service.
1. Select a pricing plan and then click **Create**.
1. Click **Manage** and then, under "Gain insights into UrbanCode deployments", click **Start here**.
1. In the toolchain template window, click **Create**.  
Delivery Insights creates a toolchain for your organization. Toolchains are collections of tool integrations, and in this case, IBM UrbanCode Deploy and {{site.data.keyword.DRA_short}} are part of your toolchain. For more information about toolchains, see [Working with toolchains](../ContinuousDelivery/toolchains_working.html).
1. In the toolchain, click the IBM UrbanCode Deploy tool.
1. Click the settings button and then click **Setup**.

In the future, you can get to {{site.data.keyword.DRA_short}} by clicking **Services > Dashboard** and clicking your instance of the {{site.data.keyword.DRA_short}} service.

If you already have a toolchain, you can add the IBM UrbanCode Deploy and {{site.data.keyword.DRA_short}} tools to it and access Delivery Insights through those tools. Then, click the IBM UrbanCode Deploy tool, click the settings button and then click **Setup**.

Now you can follow the instructions on the **Setup Instructions** page to install DevOps Connect and connect it to {{site.data.keyword.DRA_short}}, as described in the next section.

## Installing DevOps Connect and connecting it to {{site.data.keyword.DRA_short}}
{: #install_connect}

1. On the **Setup Instructions** page, follow the steps to set up DevOps Connect and connect your IBM UrbanCode Deploy servers. These steps include:
{: #set_up_connect}
  1. Set up a system to run DevOps Connect, as described in the [Prerequisites](uc_insights_connect_ucd.html#prereqs).
  1. Download DevOps Connect, which is provided in a runnable JAR file.

  1. If you use a proxy to connect to the internet, set the system variable `_JAVA_OPTIONS` to the following value:
    * If the proxy uses HTTPS, set `_JAVA_OPTIONS` to `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT`, where `HOSTNAME` is the host name of the proxy server and `PORT` is the HTTPS port of the proxy server.
    * If the proxy uses HTTP, set `_JAVA_OPTIONS` to `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT`, where `HOSTNAME` is the host name of the proxy server and `PORT` is the HTTP port of the proxy server.

  1. Copy the command from the **Setup Instructions** page. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. DevOps Connect runs on port 8443 by default, which is the same port that the IBM UrbanCode Deploy server runs on by default. Therefore, if the IBM UrbanCode Deploy server or any other service is running on port 844s, change the port for DevOps Connect by adding the parameter `-Dserver.port` to the command. For example, to set DevOps Connect to use port 8888, the beginning of the command looks like this:  
```java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888```  
  The full command contains information about your Bluemix account, which configures DevOps Connect automatically, as in the following example:  
```java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```
  1. Run the command and wait for DevOps connect to start.

  1. Connect your IBM UrbanCode Deploy servers to DevOps connect, as described in the next section.

## Connecting IBM UrbanCode Deploy servers to DevOps Connect
{: #connect_ucd_to_connect}

1. If your IBM UrbanCode Deploy server is earlier than version 6.2.5, install a patch on the server. Versions 6.2.5 and later do not require a patch.
  1. Download the correct patch for your version of IBM UrbanCode Deploy from the following page. For example, the patch file for IBM UrbanCode Deploy 6.2.4.x is named  [ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar).  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Stop the server. See [Starting and stopping the server](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Put the patch files in the <code><em>application_data</em>/patches</code> folder, where <code><em>application_data</em></code> is the server application data folder. The default application data folder is `/opt/ibm-ucd/server/appdata` on Linux and `C:\Program Files\ibm-ucd\server\appdata` on Windows. On high-availability systems, the application data folder is always on a shared network drive that each server can access.

  1. Optional: While the server is stopped, to increase performance of the data import from this server, run the following SQL commands on the database. These commands are not needed on version 6.2.5 and later.  
  ```create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);```  
  ```create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);```  
  Use the name of your database for `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Start the server. 

    **Note:** You might need to wait longer than you typically do for the IBM UrbanCode Deploy server to start. If the server does not eventually start, or is not working correctly, delete the patch files and then restart the server. The patch files do not permanently affect the server.

1. Some versions of IBM UrbanCode Deploy require an additional patch for the server to connect to DevOps Connect. If you are using IBM UrbanCode Deploy version 6.2 through 6.2.1.2, you must install the following additional patch on the server:
  1. Download the patch:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Stop the server.
  1. Put the patch file in the <code><em>application_data</em>/patches</code> folder.
  1. Start the server.

1. Create an integration between DevOps Connect and the IBM UrbanCode Deploy server:  

  **Important:** The first time that the integration runs, DevOps Connect retrieves data for the previous 90 days. If you have a large amount of deployment data, this process can take a long time. To retrieve data for less than 90 days, see [Troubleshooting](uc_insights_connect_ucd.html#troubleshooting).
  1. In IBM UrbanCode Deploy, create an authentication token. See [Tokens](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. In DevOps Connect, click **Integrations**, and then click **Add New**.
  1. Specify a name and description for the integration. The default location of DevOps Connect is `https://hostname:8443/`, where `hostname` is the host name of the system that hosts DevOps Connect.
  1. From the **Integration Type** list, select **IBM UrbanCode Deploy for Cloud Reporting**.
  1. In the **Server URI** field, enter the public URL of the IBM UrbanCode Deploy server, such as `https://my_UCD.example.com:8447`.
  1. In the **Authentication Token** field, enter or paste the authentication token that was generated by IBM UrbanCode Deploy.
  1. In the **Admin User** field, enter a comma-separated list of IBMids to give access to the DevOps Connect interface.
  1. Optional: Click **Run Integration** to run the integration immediately. By default, integrations run every minute.
  1. Click **Save**.

  ![Setting up the integration in DevOps Connect](images/uc_insights_dc_integration.gif)

Now your data is synchronized with Delivery Insights. You can now create and view reports that are based on this data. Next, map the environments on your IBM UrbanCode Deploy servers to logical environments in Delivery Insights.

## Mapping environments to reports
{: #mapping}

### Logical environments

Delivery Insights groups your IBM UrbanCode Deploy environments (also called *physical environments*) into one or more logical environments. This way, you can collect environments into groups that make sense to you and your organization. For example, if you have several production environments for several applications, you can group all of those environments into a single logical environment and combine metrics for all of those environments into a single production environment dashboard. Mapping happens by search string, so you can group environments in any way that makes sense for your IBM UrbanCode Deploy servers.

### Default logical environments

By default, your reports include logical environments that match IBM UrbanCode Deploy environments by using strings. For example, all environments with "dev" in the name are mapped to the DEV logical environment, and all environments with "prod" in the name are mapped to the PROD logical environment.

![The default logical environments](images/uc_insights_mapping.gif)

### Mapping environments to logical environments

You can manually map physical environments to logical environments, or you can use patterns to associate physical environments with logical environments dynamically.

To map physical environments to logical environments, follow these steps:

1. Open Delivery Insights, click the settings button, and click **Map Environments**.
1. On the Environment Mapping page, click an existing logical environment or create a logical environment by clicking **Add Logical Environment**.
1. With a logical environment selected, you can specify patterns to map environments to the logical environment. Under **Included Patterns**, click **Add Pattern** and specify a pattern to use. All environments with names that match the pattern, including environments that you create later, are added to the logical environment. You can use the asterisk (*) as a wildcard. For example, the pattern `env` matches the environments `env1`, `env2`, and `env`.
1. To map environments to logical environments manually, click **Add Manually** and select the environments to add or remove.
1. Verify that the logical environment contains the environments that you want.

![Setting up the logical environment mapping](images/uc_insights_mapping_manually.gif)

Now that you have mapped environments to logical environments, you can aggregate report information by those logical environments.

## Mapping applications to lines of business
{: #lines}

Lines of business are groups of applications that serve a common business purpose. You can map your applications to lines of business to make it easier to filter the applications in charts. You can also create charts that are based on lines of business.

To set up lines of business (LOBs), follow these steps:

1. In {{site.data.keyword.DRA_short}}, click **Delivery Insights**, click the settings button, and then click **Map Lines of Business**.
1. On the Lines of Business Mapping page, click an existing LOB, or create an LOB by typing a name and clicking **Create**.
1. With an LOB selected, you can specify patterns to map applications to the LOB. Under **Included Patterns**, click **Add Pattern** and specify a pattern to use. All applications with names that match the pattern, including applications  that you create later, are added to the LOB.  You can use the asterisk (*) as a wildcard. For example, the pattern `env` matches the environments `env1`, `env2`, and `env`.
1. You can also map applications to the LOP manually by clicking **Individually Mapped Applications** and then clicking **Add Applications**.

After your set up LOBs, you can filter charts to show only the applications in certain LOBs. Other charts show metrics based on LOBs.

## Creating reports

To create a report, open {{site.data.keyword.DRA_short}}, click **Delivery Insights**, and then click **Add Report**. If you don't see **Add Report**, your IBM UrbanCode Deploy servers are not connected. Click the settings button and then click **Setup** to connect your servers.

From within the report, you can add cards to the **Metrics** section, filter the activity under **Recent application activity**, and add charts to the **Report Details** section. Each chart in the **Report Details** section is individually filterable and customizable. To see the raw data behind a chart, at the top right of the chart, click the chart Settings button and then click **Report Data**.

To change the order of the charts, at the top right of the page, click the Settings button and then click **Edit Chart Layout**. Then you can drag and drop the charts to set the order on the report.

## Sharing reports
By default, only you can see your Delivery Insights reports. You can share the report with other users in your Bluemix org. To share a report with someone in your Bluemix org, open the report and then at the top right of the report, click the Settings button and then click **Share**.  

![Sharing a report](images/uc_insights_sharing.gif).

## Creating audit reports

Audit reports show a complete list of all activity that meets the filters that you set, as a PDF. To create an audit report, click **Delivery Insights**, click the settings button, and then click **Create Audit Report**. Then, specify the information for the report, including a name. Also, set the context for the report, such as for an application, a logical environment, or an environment on an IBM UrbanCode Deploy server (a physical environment). From there, select the data to show in the report and click **Create**. 

## Troubleshooting
{: #troubleshooting}

If many application and component process requests are stored in your IBM UrbanCode Deploy server database, errors can occur during the retrieval process. A message similar to the following text is recorded in the server output log:

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

To work around this behavior, edit the `plugin.properties` file for the plug-in to reduce the number of days worth of data to retrieve. The `plugin.properties` file is in the `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` directory on the computer where you installed DevOps Connect. Edit the following line to remove the number sign (#) and to reduce the number of days:

`#numDaysToRetrieve=90`

For example, change the line to the following text to retrieve only the previous 30 days worth of data:

`numDaysToRetrieve=30`

Save the file, and then run the integration again. Check the server logs to ensure that the error no longer occurs.
