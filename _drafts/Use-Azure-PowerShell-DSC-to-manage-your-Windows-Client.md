---
id: 17491
title: Use Azure PowerShell DSC to manage your Windows Client
date: 2017-01-31T10:51:33+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=17491
permalink: /?p=17491
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "0"
  - "0"
  - "0"
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - DSC
  - powershell
---
Hi all,

Couple of weeks ago I was teaching a course about Azure and PowerShell DSC. The attendees had to create and manage a PowerShell DSC configuration. This made me think about using Azure Automation DSC to manage my own laptops and computers. I could use Azure Automation DSC to ensure the state of all my machines are the same: updates, sofware installed, PowerShell modules, etc.

Let&#8217;s have a quick introduction of PowerShell DSC before we have a look at our DSC solution.

# Introduction

With Azure Automation Desired State Configuration (DSC), you can consistently deploy, reliably monitor, and automatically update the desired state of all your IT resources, at scale from the cloud.

### Configuration {#configuration}

<p class="lf-text-block lf-block" data-lf-anchor-id="07c52709c79100991bac9ddaed226731:0">
  PowerShell DSC introduced a new concept called configurations. Configurations allow you to define, via PowerShell syntax, the desired state of your environment.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="07c52709c79100991bac9ddaed226731:0">
  Running (compiling) a DSC configuration will produce one or more DSC node configurations (MOF documents), which are what DSC nodes apply to comply with desired state.
</p>

### Node Configuration {#node-configuration}

<p class="lf-text-block lf-block" data-lf-anchor-id="07c52709c79100991bac9ddaed226731:0">
  When a DSC Configuration is compiled, one or more node configurations are produced depending on the Node blocks defined in the configuration.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="07c52709c79100991bac9ddaed226731:0">
  PS DSC nodes become aware of node configurations they should enact via either DSC push, or pull methods. Azure Automation DSC relies on the DSC pull method, where nodes request node configurations they should apply from the Azure Automation DSC pull server. Because the nodes make the request to Azure Automation DSC, nodes can be behind firewalls, have all inbound ports closed, etc. They only need outbound access to the Internet (either directly or via a proxy).
</p>

### Pull Server {#node}

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  A DSC web pull server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  <strong>The cool thing when using Azure Automation DSC is that you dont need to install, configure and maintain a pull server. It comes as a service 🙂</strong>
</p>

### Node {#node}

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  A DSC node is any machine that has its configuration managed by DSC. his could be a Windows or Linux Azure VM, on-premises VM / physical host, or machine in another public cloud.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  <strong>So if we want to manage our client machines we need to onboard our clients as nodes.</strong>
</p>

<h3 class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  Resources
</h3>

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  DSC comes with a set of built-in resources such as those for files and folders, server features and roles, registry settings, environment variables, and services and processes. DSC resources can also be imported as part of PowerShell Modules to extend the set of built-in DSC resources. Non-default resources will be pulled down by DSC nodes from the DSC pull server.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="8c454f2145a918bd18c1495745776630:0">
  <strong>To manage our software packages and keeping our PowerShell modules up to date, we will have to import custom Resources.</strong>
</p>

# Solution

  1. Configure Azure Automation DSC
  2. Setup your clients as DSC Nodes
  3. Create your DSC configuration
  4. Complie your DSC configuration

&nbsp;

## 1: Configure Azure Automation DSC

sd.

## 2: Setup your clients as DSC Nodes

sd.

&nbsp;

## 3: Create your DSC configuration

sd.

&nbsp;

## 4:Complie your DSC configuration

sd.