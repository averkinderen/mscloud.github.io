---
id: 8821
title: Windows Azure Pack UR6
date: 2015-04-21T20:00:23+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=8821
permalink: /windows-azure-pack-ur6-2/
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_standard_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_image_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_image_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_audio_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_audio_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_video_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_video_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_link_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_link_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_gallery_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_status_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_status_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_singlerelated:
  - "0"
  - "0"
  - "0"
post_views_count:
  - "4693"
  - "4693"
  - "4693"
categories:
  - WAP
tags:
  - WAP
---
Microsoft just send out their Windows Azure pack Newsletter to announce that UR6 will be available as of April 28! If you didn&#8217;t received the latest newsletter you can still register here: <a href="http://www.microsoft.com/web/wap/" target="_blank">http://www.microsoft.com/web/wap/</a>

&nbsp;

# Issues that are fixed in Windows Azure Pack UR6

&nbsp;

This article addresses the following issues:

## Issue 1

Adds support for Webjobs in Windows Azure Pack Websites.

**Symptom** Tenant users cannot setup and execute background tasks to perform batch jobs related to their websites. The Windows Azure Webjobs functionality is not supported in the Windows Azure Pack (WAP) Websites Resource Provider.

**Resolution** Tenant users now have access to this functionality through the WAP Websites Resource Provider. It is enabled in the Admin Site when configuring a plan and made available to Tenants in the Tenants Site. This functionality offers creation of Webjobs to be executed manually or continuously in the background.

## Issue 2

Adds support for Deployment Slots in Windows Azure Pack Websites.

**Symptom** Tenant users cannot deploy to separate slots other than their production slot when using WAP Websites. The Slots or Staging environments for Websites currently available in public Azure’s Web App Service is not available in the WAP Websites Resource Provider.

**Resolution** Tenants can now use deployment slots associated to their websites. Web app content and configurations elements can be swapped between two deployment slots, including the production slot.

## Issue 3

Adds support for Virtual Machine Checkpoint.

**Symptom** Tenant users cannot create a checkpoint of the current state of a Virtual Machine through the VMM/SPF Resource Provider.

**Resolution** Tenants can now create a checkpoint of a Virtual Machine and restore it at will when needed. The difference with regular VM Checkpoints is that in the WAP case it can only create a single Checkpoint and every time a Checkpoint is created it overwrites the previous one.

## Issue 4

Adds support for updating Windows Azure Pack components through Windows PowerShell Desired State Configuration (DSC).

**Symptom** Datacenter Administrators cannot use DSC to deploy updates of Windows Azure Pack.

**Resolution** whenever there is a new update available of Windows Azure Pack, the Administrator can take advantage of DSC to deploy the update across a distributed environment.

## Issue 5

Adds support to maintain Data Consistency between the SQL Resource Provider configured properties for resources (such as databases, resourcepools, and workload groups) with the actual provisioned resources on the SQL Server Hosting machine(s). This allows for synchronization of the SQL Resource Provider configuration data after Administrators make changes to the SQL Server directly.

**Symptom** SQL Server RP configuration data can get out of sync with the actual resources deployed in the target SQL Servers if changes are made directly to the servers and not through the WAP SQL Server RP.

**Resolution** A new set of RESTful API calls that allow the resynchronization of the SQL RP configuration data with the actual state of the target SQL Server.

## Issue 6

Compatibility with next version of Windows Server

## Issue 7

Fixes several SQL Server Resource Provider issues:

  1. A wrong error message is displayed when Database creation fails due to total server capacity is exceeded by the consumption defined in the Plan.
  2. Get-MgmtSvcSqlResourcePoolByTemplate does not provided expected output when it is provided with an invalid RG template ID.
  3. A Tenant can delete any unmanaged database by guessing its name
  4. Tenants cannot increase the size of their DBs even after the Administrator increases the quota for the plan

## Issue 8

  1. IaaS: Fixes the Tenant Site SPF UI button label for “VM Detach” to “VM Delete” to reflect what it actually does
  2. Other minor fixes

&nbsp;