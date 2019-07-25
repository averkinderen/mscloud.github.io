---
id: 1681
title: How to Deploy Operations Manager 2007 ACS Reporting
date: 2008-08-27T19:11:06+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/08/27/how-to-deploy-operations-manager-2007-acs-reporting.aspx
permalink: /how-to-deploy-operations-manager-2007-acs-reporting/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1726"
  - "1726"
  - "1726"
  - "1726"
  - "1726"
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
Audit Collection Services (ACS) reporting can be installed in two configurations.

  * A Microsoft SQL Server 2005 Reporting Services (SRS) SP1 or SP2 instance with Operations Manager Reporting already installed. A benefit of this is the ability to view ACS Reports in the Operations Console. 
      * A SRS instance without Operations Manager Reporting installed.</ul> 
    The installation procedures for ACS Reporting do not differ, but the application of access control is different. By deploying ACS Reporting on the same SQL Server 2005 Reporting Services instance as your Operations Manager 2007 Reporting, the same role-based security applies to all reports. This means that ACS Reporting users need to be assigned to the Operations Manager Report Operator Role to access the ACS reports.
    
    In addition to membership in the Operations Manager Reporting Role, ACS report users must also be assigned db_datareader role on the ACS database (OperationsManagerAC) in order to run ACS reports. This is requirement is independent of the presence of Operations Manager Reporting
    
    If you choose to install ACS Reporting independently of Operations Manager Reporting, you can also use SRS security to secure the reports. See the SQL Server 2005 Books Online Reporting Services Tutorials, Setting Permissions in Reporting Services for more information.
    
    &nbsp;
    
    I installed my ACS reporting on the same instance as my scom reports.
    
    #### <a name="_Toc207433314">Before You Start</a>
    
    Deploy ACS as described in my <a href="http://scug.be/blogs/scom/archive/2008/08/27/installing-audit-collection-services-acs.aspx" target="_blank">previous post</a> before setting up ACS reporting.
    
    ###### <a name="_Toc207433315"></a>&nbsp;
    
    1. The Root Management Server for your management group must be installed and ACS must be configured, on either the RMS or a management server. For more information, see [About Audit Collection Services (ACS) in Operations Manager 2007](http://technet.microsoft.com/en-us/library/bb381373.aspx).
    
    2. An instance of Microsoft SQL Server 2005 Reporting Services must be installed on the target computer.
    
    3. During this procedure, you need to be logged on as member of Operations Manager Report Operator user role.
    
    4. IIS must be installed on the hosting system. IIS will have already been installed if you are co-locating with a Reporting Server.
    
    5. You need to have access to the ACS database.
    
    6. You need the Operations Manager 2007 installation media.
    
    #### <a name="_Toc207433316">Deploying ACS Reporting</a>
    
    ###### &nbsp;
    
    1. Logon to the server that will be used to host ACS reporting as a user that is an administrator of the SRS instance.
    
    2. Create a temporary folder, such as **C:acs**.
    
    3. On your installation media, go to **ReportModelsacs** and copy the directory contents to the temporary installation folder.
    
    There are two folders (**Models** and **Reports**) and a file named **UploadAuditReports.cmd**.
    
    4. On your installation media, go to **SupportTools** and copy the file **ReportingConfig.exe** into the temporary **acs** folder.
    
    [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="125" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_thumb.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_2.png)
    
    &nbsp;
    
    5.Launch a Command Prompt window and change directories to the temporary **acs** folder.
    
    6. Run the following command.  
    **UploadAuditReports “<AuditDBServerInstance>” “<Reporting Server URL>” “<path of the copied acs folder>”**  
    For example: **UploadAuditReports “myAuditDbServerInstance1” “http://myReportServer/ReportServer$instance1” “C:acs”**
    
    This example creates a new data source called **Db Audit**, uploads the reporting models **Audit.smdl** and **Audit5.smdl**, and uploads all reports in the **acsreports** directory.
    
    ******Note** 
    
    The reporting server URL needs the reporting server virtual directory (**ReportingServer$<InstanceName>**) instead of the reporting manager directory (**Reports$<InstanceName>**).
    
    [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="77" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_thumb_6.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_14.png)
    
    7. Open Internet Explorer and enter the following address to view the **SQL Reporting Services Home** page. **http://<yourReportingServerName>/Reports$<InstanceName>**
    
    [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="139" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_thumb_2.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_6.png)
    
    8. Click **Audit Reports** in the body of the page and then click **Show Details** in the upper right part of the page.
    
    9. Click the **Db Audit** data source.
    
    10. In the **Connect Using** section, select **Windows Integrated Security** and click **Apply**.
    
    [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="177" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_thumb_5.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_12.png)
    
    &nbsp;
    
    [<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="177" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_thumb_1.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtoDeployOperationsManager2007ACSRepor_D484/image_7.png) 
    
    &nbsp;
    
    That&#8217;s it! 
    
    &nbsp;
    
    Greetz,
    
    Alexandre Verkinderen
    
    <http://scug.be/blogs/scom>
