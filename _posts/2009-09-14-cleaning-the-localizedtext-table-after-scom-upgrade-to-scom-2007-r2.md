---
id: 19696
title: Cleaning the Localizedtext Table after SCOM upgrade to SCOM 2007 R2
date: 2009-09-14T13:48:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/09/14/cleaning-the-localizedtext-table-after-scom-upgrade-to-scom-2007-r2.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1808"
  - "1808"
  - "1808"
  - "1808"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - opsmgr
  - Opsmgr DB
  - opsmgr R2
  - Script
  - sql
  - upgrade
---
After upgrading your OpsMgr 2007 components and upgrading your SQL environment to SQL Server 2008, you will need to run some post installation steps. These post installation steps are only needed if you have done an upgrade from OpsMgr 2007 to OpsMgr 2007 R2.

OpsMgr 2007 SP 1 had an issue with the localized text table continuing to grow. The main cause of this was converted MOM 2005 management packs running a lot of backwards-compatibility scripts, such as the converted Exchange 2007 management pack. The issue was that each event wrote additional data to the localized text table, which is not groomed. Over time, the Operational database continued to grow, which had a tremendous impact on OpsMgr performance. Kevin Holman writes about this at <http://blogs.technet.com/kevinholman/archive/2008/10/13/does-your-opsdb-keep-growing-is-your-localizedtext-table-using-all-the-space.aspx>; it is also documented on the SCUG.BE blog at [http://scug.be/blogs/scom/archive/2009/05/28/optimizing-the-performance-of-your-opsmgr-console-and-reducing-db-size.aspx](/blogs/scom/archive/2009/05/28/optimizing-the-performance-of-your-opsmgr-console-and-reducing-db-size.aspx) .

&nbsp;

I&rsquo;ve just did an upgrade at a customer site and after completing the post-installation steps as mentioned here [http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx](http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx "http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx") and I was very surprised by the results!!

&nbsp;

<img height="94" width="125" src="http://2.bp.blogspot.com/_wFWqWIH-WFU/Rl_nDN7UEPI/AAAAAAAABGc/vvJDrBtz5rw/s400/surprised%2520monkey.jpg" /> 

&nbsp;

I checked the database size and the localizedtext table before running the cleanup script.

  * Database size before the cleanup script

[<img height="163" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3DAF3A3E.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_1B57A4C5.png)

28 gig of space!

[<img height="244" width="208" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_126AA337.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_4B818039.png)

  * 12.700.000 records in the localizedtext table before running the cleanup script.

&nbsp;

In OpsMgr 2007 R2, the localizedtext table issue is gone. The table still exists but Microsoft has resolved the growing issue. Even if the issue is gone you will need to run the following SQL query once after the upgade to initially clean up the localizedtext and publishermessage tables. You can copy/paste the script from here [http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx](http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx "http://technet.microsoft.com/nl-nl/library/dd789073(en-us).aspx")&nbsp;

&nbsp;

The script has run for about 4 hours!

[<img height="244" width="235" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_042C2A47.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_446243C1.png)

Now the results! 🙂

&nbsp;

Disk space after the clean up script:

[<img height="215" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_58E7933F.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_26EFF2B5.png)

7 gig of disk space; So that&rsquo;s a gain of 20 gig of disk space! That&rsquo;s amazing!

[<img height="244" width="231" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_51C856C7.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_38CC8682.png)

780.000 records found in the localizedtext table after running the clean up script !! So that&rsquo;s about 12 million records lesser!!

&nbsp;

For completing the post-upgrade steps I did a reindex of the database.

[<img height="233" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6D6CE2BD.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_469ECC7D.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

And now my console is running very fast and I&rsquo;ve less data to backup! So after upgrading to SCOM 2007 R2 you will definitely have to run the clean up script!!

<img height="143" width="74" src="http://www.salotteries.com.au/library/Results-winner.jpg" /> 

&nbsp;

Greetings,  
Alexandre Verkinderen
