---
title: "Define a hierarchical structure for your Azure DevOps branches"
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
header:
  og_image: /assets/images/2020-05-23-AZDO-Folders.png
---

I like my Azure DevOps branches to be well structured and well named.

When we create a new ARM template a new feature branch is created based on the name of the template. This branch is short lived, typically only a few days and max 2 weeks. Once the development of the template is done, a pull request is created, the branch gets merged if all tests are passed and the branch gets deleted. We also have branches that will be created in the rare case a bug has been discovered in one of our ARM templates. These branches are even more short lived, typically only a few hours to maximum a few days.

![Devops Branches]({{ site.url }}/assets/images/2020-05-23-AZDO-Branches.png)

We use the following naming convention for our branches:

- Feature/ARM-template-name
- Bugs/ARM-template-name

When working with lots of different people in the same AzDo project the number of branches can increase exponentially and it can quickly become a mess. Hierarchical branch folders is an easy solution to keep your branches clean and well structured. In Azure DevOps when you create a new folder with `/` it will automatically create that new branch under a folder.

The following standards have been defined in our AzDo environment:

- Only Dev and Master branch will be allowed to exist under the root
- Contributors will be forced to create new branches under the Features or Bugs folders

## Requirements

To be able to enforce folders in Azure DevOps we will need to use Team Foundation version control command (`tf.exe`). You can find tf.exe if you have installed Visual Studio in the following location: `C:\Program Files (x86)\Microsoft Visual Studio\2019\TeamExplorer\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer`. You will also need the AzDo organization name, the project name, the repository name and full permissions to change branch permissions. So in my case it is the following:

1. Organization Name = azurelns
2. Team Project Name = Todo
3. Repository name = Todo

![AZDO organization]({{ site.url }}/assets/images/2020-05-23-AZDO-organization-repo.png)

## Enforce Branch Folder structure

Open the Developer Command Prompt, under Start > Visual Studio > Developer Command Prompt and go to the location of tf.exe.

First, let's block the creation of new branches under the root

`tf git permission /deny:CreateBranch /group:[Todo]\Contributors /collection:https://dev.azure.com/azurelns/ /teamproject:Todo /repository:Todo`

Then allow contributors to create new branches under the Features folder

`tf git permission /allow:CreateBranch /group:[Todo]\Contributors /collection:https://dev.azure.com/azurelns/ /teamproject:Todo /repository:Todo /branch:Feature`

and the bugs folder

`tf git permission /allow:CreateBranch /group:[Todo]\Contributors /collection:https://dev.azure.com/azurelns/ /teamproject:Todo /repository:Todo /branch:Bugs`

Finally, allow administrators to create a branch called master and dev (in case it ever gets deleted accidentally) :man_shrugging: .

`tf git permission /allow:CreateBranch /group:"[Todo]\Project Administrators" /collection:https://dev.azure.com/azurelns/ /teamproject:Todo /repository:Todo /branch:master`

`tf git permission /allow:CreateBranch /group:"[Todo]\Project Administrators" /collection:https://dev.azure.com/azurelns/ /teamproject:Todo /repository:Todo /branch:dev`

Now when I want to create a new branch directly under the root it will blocked as I'm not following the correct naming convention.

![AZDO organization]({{ site.url }}/assets/images/2020-05-23-AZDO-creation-blocked.png)

To create this branch I would need to place it in a folder like this: "Feature/testbranch"

## Conclusion

When working with multiple people on a project it is important to define some kind of hierarchical branch structure. The Team Foundation version control command lets you enforce that structure.

![Devops Folders]({{ site.url }}/assets/images/2020-05-23-AZDO-Folders.png)

Hope this helps,
Alex
