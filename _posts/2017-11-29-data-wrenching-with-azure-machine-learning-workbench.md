---
id: 19781
title: Data wrenching with Azure Machine Learning Workbench
date: 2017-11-29T12:20:00+10:00
author: alexandre@verkinderen.com
guid: http://mscloud.be/?p=19781
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
bpxl_standard_single_hide:
  - "0"
bpxl_image_excerpt_home:
  - "0"
bpxl_image_single_hide:
  - "0"
bpxl_audio_excerpt_home:
  - "0"
bpxl_audio_single_hide:
  - "0"
bpxl_video_excerpt_home:
  - "0"
bpxl_video_single_hide:
  - "0"
bpxl_link_excerpt_home:
  - "0"
bpxl_link_single_hide:
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
bpxl_gallery_single_hide:
  - "0"
bpxl_status_excerpt_home:
  - "0"
bpxl_status_single_hide:
  - "0"
bpxl_singlerelated:
  - "0"
post_views_count:
  - "4273"
  - "4273"
categories:
  - Azure
tags:
  - Azure
  - Azure ML
  - Machine Learning
  - Workbench
---
Hi all,

This blog post will cover how to transform data with Azure Machine Learning Workbench. One of the most important aspects in any Machine learning project is how accurate and how good your data is. If you have un-accurate or bad data the learning or simulation models will generate bad results.

The main components of Azure Machine Learning are:

* Azure Machine Learning Workbench (which is what we will use today to prepare our data)
  * Azure Machine Learning Experimentation Service (to be able to use Azure ML Workbench we need an Experimentation Service)
  * Azure Machine Learning Model Management Service
  * Microsoft Machine Learning Libraries for Apache Spark (MMLSpark Library)
  * Visual Studio Code Tools for AI

Have a look here for a quick overview of <a href="https://docs.microsoft.com/en-au/azure/machine-learning/preview/overview-what-is-azure-ml" target="_blank" rel="noopener">Azure Machine Learning</a> and a detailed description of the different Machine learning components.

We will create a new Azure ML Experimentation Service first, after which we will download and install Azure ML Workbench.

# Azure Machine Learning Experimentation Service

The Experimentation Service handles the execution of machine learning experiments. It also supports the Workbench by providing project management, Git integration, access control, roaming, and sharing.

Through easy configuration, you can execute your experiments across a range of compute environment options:

* Local native
  * Local Docker container
  * Docker container on a remote VM
  * Scale out Spark cluster in Azure

Today we will not execute any experiments. We will just show how to transform the data. Let&#8217;s create our new Azure ML learning account:

  1. Select the **New** button (+) in the upper-left corner of the Azure portal.
  2. Enter **Machine Learning** in the search bar. Select the search result named **Machine Learning Experimentation (preview)**.

I selected the DevTest SKU

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb.png" alt="image" width="244" height="233" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image.png)

After filling in the required information and submitting the deployment you should see the following:

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-1.png" alt="image" width="244" height="101" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-1.png)

# Azure Machine Learning Workbench

Now that we have our Azure ML Learning account we can install Azure ML Workbench. Azure ML Workbench is a desktop application plus command-line tools, supported on both Windows and macOS. It allows you to manage machine learning solutions through the entire data science life cycle:

* Data ingestion and preparation
  * Model development and experiment management
  * Model deployment in various target environments

You can install Azure Machine Learning Workbench on your computer running Windows 10, Windows Server 2016, or newer.

  1. Download the latest Azure Machine Learning Workbench installer [AmlWorkbenchSetup.msi](https://aka.ms/azureml-wb-msi).

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-2.png" alt="image" width="244" height="180" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-2.png)

Double-click the downloaded installer **AmlWorkbenchSetup.msi** from File Explorer. The installer downloads all the necessary dependent components, such as Python, Miniconda, and other related libraries. The installation might take around half an hour to finish all the components.

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-3.png" alt="image" width="244" height="181" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-3.png)

  1. After the installation process is complete, select the **Launch Workbench** button on the last screen of the installer.
  2. Sign in to Workbench by using the same account that you used earlier to provision your Azure resources.
  3. When the sign-in process has succeeded, Workbench attempts to find the Machine Learning Experimentation accounts that you created earlier. It searches for all Azure subscriptions to which your credential has access. When at least one Experimentation account is found, Workbench opens with that account. It then lists the workspaces and projects found in that account.

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-4.png" alt="image" width="244" height="134" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-4.png)

## Create a new project

  1. Start the Azure Machine Learning Workbench app and sign in.
  2. Select **File** > **New Project** (or select the **+** sign in the **PROJECTS** pane).
  3. Fill in the **Project name** and **Project directory** boxes. **Project description** is optional but helpful. Leave the **Visualstudio.com GIT Repository URL** box blank for now

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-5.png" alt="image" width="244" height="92" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-5.png)

Select Blank Project:

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-6.png" alt="image" width="125" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-6.png)

I downloaded a dataset from https://www.kaggle.com/datasets that I will be using here as an example. To bring data into a project using the data source wizard. Select the **+** button next to the search box in the data view and choose Add Data Source

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-7.png" alt="image" width="244" height="172" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-7.png)

In my case I used Excel as the data source

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-8.png" alt="image" width="244" height="199" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-8.png)

You can specify one or more sampling strategies for the dataset, and choose one as the active strategy. The default is to load the Top 100 rows. I changed it to load the full file

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-9.png" alt="image" width="244" height="73" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-9.png)

Once the data has been imported you will see the following screen

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-10.png" alt="image" width="244" height="134" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-10.png)

# Create a Data Preparation Package

Now that we have our datasource we will prepare our data by creating a **Data Preparation Package** that we will use to transform our data.

  1. Click the ‘Data’ icon again
  2. Right click on the `flights` data source and click ‘Prepare’
  3. Add a ‘Data Preparation Package Name’ then press ‘OK’

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-11.png" alt="image" width="193" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-11.png)

This will then create a flights`.dprep` file in your project directory, and will show a page almost similar to what we’ve seen after we’ve added a data source.

# Derive Column By Example Transformation

We will now transform our month column from numeric values to a string with the derive column by example. Azure ML Workbench synthesizes a program based on the examples provided by you and applies the same program on remaining rows. All other rows are automatically populated based on the example you provided. Workbench also analyzes your data and tries to identify edge cases.

Select the column you want to transform, click derive column by example

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-12.png" alt="image" width="207" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-12.png)

A new column will appear with null values. Click in the first empty cell in the new column and provide an example. In my case I typed January to transform my numeric value of 1 (first month of the year) to January.

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-13.png" alt="image" width="157" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-13.png)

Select OK to accept the changes. You should now see the following:

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-14.png" alt="image" width="244" height="39" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-14.png)

That’s how easy it is to transform data with Azure ML Workbench. Imagine doing this with Excel?! For more examples regarding data transformation have a look <a href="https://docs.microsoft.com/en-au/azure/machine-learning/preview/tutorial-bikeshare-dataprep#use-by-example-transformations" target="_blank" rel="noopener">here</a>.

Thanks,

Alex
