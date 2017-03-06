#Azure SQL DB Auditing log integration into OMS

This is **sample application** that runs in Azure and utilizes OMS public APIs to push SQL audit logs into OMS.

It allows using OMS Log Analytics to explore and analyze your database activity, and gain insight into discrepancies and anomalies that could indicate potential business concerns or suspected security violations.  

[Azure SQL Database Auditing](http://go.microsoft.com/fwlink/?LinkId=403539) tracks database events and writes them to an audit log in your Azure Storage account. Azure SQL Database Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.

[Operations Management Suite (OMS) Log Analytics](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-log-searches/) helps you correlate, search, and act on log and performance data generated by operating systems, applications and databases. It gives you real-time operational insights using integrated search and custom dashboards to readily analyze millions of records across all of your workloads and servers. For additional useful information about OMS Log Analytics search language and commands, see [Log Analytics search reference](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-log-searches/).

# Prerequisites 
1. Applies only to [Azure SQL Databases](https://azure.microsoft.com/en-us/services/sql-database/) with [Blob Auditing](http://go.microsoft.com/fwlink/?LinkId=403539) enabled
2. Azure Subscription with resource creation permissions
3. OMS workspace with Administrator or Contributor permissions

#Estimated Cost of Deployed Resources


|  Resource      | Cost/Month           | Cost/Hr  |
| :------------- |:-------------|:-----|
| [B1 App Service Plan](https://azure.microsoft.com/en-us/pricing/details/app-service/)		| $55.80 | $0.075 |
| [Storage Plan](https://azure.microsoft.com/en-us/pricing/details/storage/)				| ~$0      |   $0.0036 / transaction |

#Setup Guide


###<a id="subheading-2-1">Retrieve SQL DB Auditing - Storage Connection String</a>

1. Launch the [Azure Portal](https://portal.azure.com) at https://portal.azure.com.

2. Navigate to the **Access keys** blade of the storage account. Then click on the **Context Menu** ("...") to the right of key1, and click on **View connection string**. Copy & Save the Connection String for use in following steps.

	![Navigation Pane][1]

<br>
###<a id="subheading-2-2">Retrieve OMS Workspace ID and Access key</a>

1. Launch the [Microsoft Operations Management Suite (OMS)](https://mms.microsoft.com) at https://mms.microsoft.com.

2. Choose the relevant workspace.

3. In the top menu bar, click on the **Settings** icon.

	![Navigation Pane][2]

4. Click on **Connected Sources**, then click on **Windows Servers**. Copy & Save the **Workspace ID** and **Primary Key** for use in following steps.

	![Navigation Pane][3]

<br>
###<a id="subheading-2-3">Deploy sample application to Azure</a>

1. Click on the **Deploy to Azure** button below to initiate deployment process. 

	> During deployment, use the **Storage Connection String**, **Workspace ID**, and **Primary Key** that you saved in the previous steps. 

	<a href="https://azuredeploy.net/" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>

2. When deployment is completed, you can close the web application browser window. 
	
	> You will not be required to access this application, it will be running in the background, periodically pushing the audit logs to OMS.

> [!IMPORTANT]
> It can take up to 5-10 minutes for initial data to start appearing in your OMS workspace.

<br>
###<a id="subheading-2-4">Import Azure SQL DB audit sample dashboard to OMS</a>

1. Download [SQLDatabaseAudit.omsview][101] to your PC.

2. From the OMS dashboard, click on the **View Designer** tile.

	![Navigation Pane][4]

3. At the top of the View Designer page, click on **Import**. An **Upload from computer** will appear at the bottom of the page - choose the **SQLDatabaseAudit.omsview** file that you downloaded to your PC in step 1. Then click **Save** at the top.

	![Navigation Pane][5]

4. A **SQL Database Audit** tile will now appear on your dashboard. 

	![Navigation Pane][6]

5. Click on the **SQL Database Audit** tile to view the database activity report.

	![Navigation Pane][7]


<br>
# Troubleshooting

If you've completed the setup process but don't see audit data in your OMS workspace, you'll be able to review the logs for the import operation job in the Azure portal to try and identify the problem:

1. Go to the App Service that you created during the deployment of the sample application.

2. Click on "WebJobs" on the left menu and then on "Logs" in the top menu.
	
	![Navigation Pane][9]

3. In the page that opens, you'll be able to view the logs for a specific run by clicking on the relevant job run link:

	![Navigation Pane][10]


[1]: ./media/1_storage_access_keys.png
[2]: ./media/2_oms_settings.png
[3]: ./media/3_oms_connected_resources.png
[4]: ./media/4_view_designer_tile.png
[5]: ./media/5_view_designer.png
[6]: ./media/6_sql_database_audit_tile.png
[7]: ./media/7_sql_database_audit_report.png
[8]: http://azuredeploy.net/deploybutton.png
[9]: ./media/9_webjobs_logs.png
[10]: ./media/10_webjobs_logs_2.png

[101]: https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration/blob/master/SQLDatabaseAudit.omsview


