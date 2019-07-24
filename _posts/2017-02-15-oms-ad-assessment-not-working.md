---
id: 17811
title: OMS AD assessment not working, no data found.
date: 2017-02-15T16:52:15+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=17811
permalink: /oms-ad-assessment-not-working/
sc_member_order:
  - "0"
  - "0"
  - "0"
post_views_count:
  - "7644"
  - "7644"
image: /wp-content/uploads/2017/02/ok-150x150.png
categories:
  - Azure
  - OMS
tags:
  - Azure
  - cubesys
  - OMS
---
Hi all,

This week I encountered a rather strange issue with the AD Assessment solution within OMS. The OMS agent installation went fine, and we were able to collect events, security and auditing and performance data but as you can see here the AD Assessment solution wasn&#8217;t working:

<img class="alignnone size-full wp-image-17881" src="http://www.mscloud.be/wp-content/uploads/2017/02/ad.png" alt="ad" width="374" height="213" srcset="/wp-content/uploads/2017/02/ad.png 374w, /wp-content/uploads/2017/02/ad-300x171.png 300w" sizes="(max-width: 374px) 100vw, 374px" /> 

I first verified that all the requirements for the solution were met:

<ul class="lf-text-block lf-block" data-lf-anchor-id="87e46c2ddd99f7f73b4dcc574501475d:0">
  <li>
    Agents must be installed on domain controllers that are members of the domain to be evaluated.
  </li>
  <li>
    The Active Directory Assessment solution requires .NET Framework 4 installed on each computer that has an OMS agent.
  </li>
  <li>
    Add the Active Directory Assessment solution to your OMS workspace using the process described in <a href="https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions">Add Log Analytics solutions from the Solutions Gallery</a>. There is no further configuration required.
  </li>
</ul>

I also verified that the AdvisorAssessment.exe file was&nbsp;added to servers with agents.

In OMS I ran the following query to confirm my domain controllers were meeting the requirements:

<table class="crayon-table">
  <tr class="crayon-row">
    <td class="crayon-code">
      <div class="crayon-pre">
        <div id="crayon-589d77ce2a0df280943596-1" class="crayon-line">
          <span class="crayon-r ">Type</span><span class="crayon-o">=</span><span class="crayon-e">Operation </span><span class="crayon-e">and </span><span class="crayon-i">Solution</span><span class="crayon-o">=</span><span class="crayon-i">ADAssessment</span> <span class="crayon-o">|</span> <span class="crayon-r ">sort</span> <span class="crayon-i">OperationStatus</span>
        </div>
      </div>
    </td>
  </tr>
</table>

<img class="alignnone size-full wp-image-17981" src="http://www.mscloud.be/wp-content/uploads/2017/02/req.png" alt="req" width="1525" height="268" /> 

Of course I had already cleared the health service cache and restarted the Monitoring Agent service several times,&nbsp;and forced the AD Assessment to run again by deleting the LastExecuted&nbsp;registry key since&nbsp;normally it runs only every 7 days:

HKLM\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<Your MG Name Here>\Solutions\ADAssessment

<img class="alignnone size-full wp-image-17831" src="http://www.mscloud.be/wp-content/uploads/2017/02/regedit.png" alt="regedit" width="905" height="194" srcset="/wp-content/uploads/2017/02/regedit.png 905w, /wp-content/uploads/2017/02/regedit-300x64.png 300w, /wp-content/uploads/2017/02/regedit-768x165.png 768w" sizes="(max-width: 905px) 100vw, 905px" /> 

When you remove that key and restart the health service the OMS agent will think that the AD Assessment has never run and will force it to run again.

That&#8217;s when I discovered the following error in the OperationsManager log:

<img class="alignnone size-full wp-image-17841" src="http://www.mscloud.be/wp-content/uploads/2017/02/error.png" alt="error" width="746" height="420" srcset="/wp-content/uploads/2017/02/error.png 746w, /wp-content/uploads/2017/02/error-300x169.png 300w" sizes="(max-width: 746px) 100vw, 746px" /> 

After analyzing the error several times the first thing that came into my mind was a .Net compilation error. But .Net Framework 4 was installed right? So this could not be the issue?

Just to be 100% sure, I verified which version of .Net was installed. It was indeed Framework 4 but the Client Profile version:

<img class="alignnone size-full wp-image-18101" src="http://www.mscloud.be/wp-content/uploads/2017/02/client.png" alt="client" width="754" height="162" srcset="/wp-content/uploads/2017/02/client.png 754w, /wp-content/uploads/2017/02/client-300x64.png 300w" sizes="(max-width: 754px) 100vw, 754px" /> 

This [version is not the same as the full version](http://stackoverflow.com/questions/2759228/differences-between-microsoft-net-4-0-full-framework-and-client-profile). It is smaller in size and some DLL&#8217;s will not be installed. So, I installed the full [.Net version](https://www.microsoft.com/en-us/download/details.aspx?id=17718), hoping this would solve my problem.&nbsp;

> This customer had a requirement to still &nbsp;use.Net Framework 4.0 which is not recommended as it&#8217;s end of life and not supported anymore by Microsoft. Please ensure you are using the latest version if you can.

<img class="alignnone size-full wp-image-17851" src="http://www.mscloud.be/wp-content/uploads/2017/02/net4.png" alt="net4" width="757" height="202" srcset="/wp-content/uploads/2017/02/net4.png 757w, /wp-content/uploads/2017/02/net4-300x80.png 300w" sizes="(max-width: 757px) 100vw, 757px" /> 

I deleted the registry key to force the AD Assessment to run again, restarted the Monitoring agent and couple of minutes later AD Assessment data started to show up in OMS:

<img class="alignnone size-full wp-image-17821" src="http://www.mscloud.be/wp-content/uploads/2017/02/ok.png" alt="ok" width="882" height="327" srcset="/wp-content/uploads/2017/02/ok.png 882w, /wp-content/uploads/2017/02/ok-300x111.png 300w, /wp-content/uploads/2017/02/ok-768x285.png 768w" sizes="(max-width: 882px) 100vw, 882px" /> 

**So be careful which version of .Net you are installing. It needs to be the full version of .Net.**

Starting with the .NET Framework 4.5, the Client Profile has been discontinued and only the full redistributable package is available. Optimizations provided by the .NET Framework 4.5, such as smaller download size and faster deployment, have eliminated the need for a separate deployment package. The single redistributable streamlines the installation process and simplifies your app&#8217;s deployment options.

Hope this helps,

Kind regards,  
Alexandre Verkinderen

&nbsp;