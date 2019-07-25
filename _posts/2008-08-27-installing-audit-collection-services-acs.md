---
id: 520
title: Installing Audit Collection Services ( ACS )
date: 2008-08-27T19:05:11+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/08/27/installing-audit-collection-services-acs.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "4685"
  - "4685"
  - "4685"
  - "4685"
  - "4685"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - acs
  - audit collection service
  - manuals
  - Operations Manager 2007
  - opsmgr
  - scom
---
I&#8217;m going to make some procedures for ACS. First I&#8217;m going to install the audit collection services, after that I&#8217;m going to deploy the ACS reporting and last but not least enable the acs forwarding on the agents. I&#8217;m going to use the info on the technet site as a basis.

&nbsp;

The ACS database runs on Microsoft SQL Server 2005. The Audit Collection Services Collector Setup wizard creates the ACS database on an existing installation of Microsoft SQL Server 2005. To complete the installation procedure, you must be a member of the local Administrators group on both the ACS collector and the ACS database computers as well as a database administrator on the ACS database. As a best practice for security, consider using Run As to perform this procedure.

&nbsp;

### To install an ACS collector and an ACS database

1. Insert the Operations Manager 2007 CD in the Management Server that you selected to be the ACS collector.

2. On the root of the CD, double-click **SetupOM.exe**. In the **Install** section, click **Install Audit Collection Server**. The Audit Collection Services Collector Setup wizard starts.

3. On the **Welcome** page, click **Next**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="188" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_2.png)

4. On the **License Agreement** page, read the licensing terms and then click **I accept the agreement**. Click **Next**.

5. On the **Database Installation Options** page, click **Create a new database** and then click **Next**.[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="189" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_1.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_4.png)

6. On the **Data Source** page, type a name that you want to use as the Open Database Connectivity (ODBC) data source name for your ACS database in the **Data Source Name** box. By default, this name is **OpsMgrAC**. Click **Next**.

&nbsp;[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="185" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_2.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_6.png)

7. On the **Database** page, if the database is on a separate server than the ACS collector, click **Remote Database Server** and then type the computer name of the database server that will host the database for this installation of ACS. Otherwise, click **Database server running locally**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="185" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_3.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_8.png)

8. In the **Database server instance name** field, type the name of the database that will be created for ACS. If you leave this field blank, the default name is used. In the **Database** name field, the default database name of **OperationsManagerAC** is automatically entered. You can select the text and type in a different name or leave the default name. Click **Next**.

******Note** 

To display a list of SQL Server Instances, click **Start**, point to **Programs** and **Microsoft SQL Server 2005**, and then click **SQL Server Management Studio** on the database computer. Under **Server name**, click **Browse for more** and then expand **Database Engine**. All databases are listed as server namedatabase name.

9. On the **Database Authentication** page, click to select one authentication method. If the ACS collector and the ACS database are members of the same domain, you can select **Windows authentication**; otherwise, select **SQL authentication** and then click **Next**.

******Note** 

If you select **SQL authentication** and click **Next**, the **Database Credentials** page displays. Enter the name of the user account that has access to the SQL Server in the **SQL login name** box and the password for that account in the **SQL password** box, and then click **Next**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="187" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_4.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_10.png)

10. On the **Database Creation Options** page, click **Use SQL Server&#8217;s default data and log file directories** to use SQL Server&#8217;s default folders. Otherwise, click **Specify directories** and enter the full path, including drive letter, to the location you want for the ACS database and log file, for example C:Program FilesMicrosoft SQL ServerMSSQL.1MSSQLData. Click **Next**.

11. On the **Event Retention Schedule** page, click **Local hour of day to perform daily database maintenance**. Choose a time when there is the amount of expected security events are low. During the database maintenance window, database performance will be impacted. Type the number of days ACS should keep events in the ACS database before the events are removed during database grooming in **Number of days to retain events**. The default value is 14 days. Click **Next**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="188" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_5.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_12.png)

12. On the **ACS Stored Timestamp Format** page, click to choose **Local** or **Universal Coordinated Time**, formerly known to as Greenwich Mean Time, and then click **Next**

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="184" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_6.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_14.png)

13. The **Summary** page displays a list of actions that the installation program will perform to install ACS. Review the list, and then click **Next** to begin the installation.

******Note** 

If a **SQL server login** dialog box displays and the database authentication is set to **Windows authentication,** click the correct database and verify that the **Use Trusted Connection** check box is checked. Otherwise click to remove the check and enter the SQL login name and password. Click **OK**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="192" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_7.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_16.png)

14. When the installation is complete, click **Finish**.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="191" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_8.png" width="244" border="0" />](http://
scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_18.png)

Check in the opsmgr console if your collector is healthy.

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="184" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_thumb_9.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/InstallingAuditCollectionServicesACS_D403/image_20.png)

&nbsp;

That&#8217;s it!

&nbsp;

Greetz,

Alexandre Verkinderen

<http://scug.be/blogs/scom>
