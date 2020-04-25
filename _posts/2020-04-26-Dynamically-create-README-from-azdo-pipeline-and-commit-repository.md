---
title: "Dynamically create README Files from Azure DevOps Pipeline and Commit to Repository"
author: Rodney Almeida
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
---

Bernie White has a Powershell Module ([PSDocs](https://github.com/BernieWhite/PSDocs)) that can generate mark down files (*.md) and Stefan Stranger's [blog post](https://stefanstranger.github.io/2020/04/12/CreatingAzureDevOpsWIKIPagesFromWithApipeline/) shows us how to upload these to Azure DevOps Wiki. We started investigating this as we saw this being a great feature to automate the creation and maintenance of our README.md files within our IaC Templates. The only issue is that our README.md files live side by side with our ARM Templates in the Azure DevOps Repositories and not in the Wiki section that Stefan's post updates.
So the challenge is, how do we make our Azure Pipelines write back the README.md files it dynamically creates on the build agent to the repository?

The solution was to use Git within the pipeline to commit the new or updated README file to the repository.

## Requirements

First thing we found was this Microsoft [documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/scripts/git-commands?view=azure-devops&tabs=yaml) which specifies additional access requirements for the **Project Collection Build Service**. However, we found that our pipelines were using the `<Project>'s Build Service (<Organisation>)` account instead and therefore we had to assign the additional access to that account.

> Note: Permissions "Read" and "Create Tag" where already Inherited so not need to reassign again.

![create access]({{ site.url }}/assets/images/2020-04-24-Permissions.png)

## Create ReadMe Template and Calling Script

Next, we created our own PowerShell template file called `ReadMe.doc.ps1` using Bernie's [ARM Template example](https://github.com/BernieWhite/PSDocs/blob/master/docs/scenarios/arm-template/arm-template.doc.ps1) as a base. For more information regarding how to create the template PowerShell script have a look at Bernie's example.

```powershell
#
# Azure Resource Manager documentation definitions
#

# A function to break out parameters from an ARM template
function GetTemplateParameter {
    param (
        [Parameter(Mandatory = $True)]
        [String]$Path
    )

    process {
        $template = Get-Content $Path | ConvertFrom-Json;
        foreach ($property in $template.parameters.PSObject.Properties) {
            [PSCustomObject]@{
                Name = $property.Name
                Description = $property.Value.metadata.description
            }
        }
    }
}

# A function to import metadata
function GetTemplateMetadata {
    param (
        [Parameter(Mandatory = $True)]
        [String]$Path
    )

    process {
        $metadata = Get-Content $Path | ConvertFrom-Json;
        return $metadata;
    }
}

# Description: A definition to generate markdown for an ARM template
document 'README' {

    # Read JSON files
    $metadata = GetTemplateMetadata -Path $InputObject.MetadataFile;
    $parameters = GetTemplateParameter -Path $InputObject.ARMTemplate;

    "[![Build Status](https://dev.azure.com/#######/IaC/_apis/build/status/$($InputObject.PipelineName)?branchName=Dev)](https://dev.azure.com/#######/IaC/_build/latest?definitionId=$($InputObject.PipelineID)&branchName=Dev)"

    # Set document title
    Title $metadata.itemDisplayName

    # Write opening line
    $metadata.Description

    # Add each parameter to a table
    Section 'Parameters' {
        $parameters | Table -Property @{ Name = 'Parameter name'; Expression = { $_.Name }},Description
    }

    # Generate example command line
    Section 'Use the template' {
        Section 'PowerShell' {
            'New-AzResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile <path-to-template>' | Code powershell
        }

        Section 'Azure CLI' {
            'az group deployment create --name <deployment-name> --resource-group <resource-group-name> --template-file <path-to-template>' | Code text
        }

        Section 'Azure Custom Template' {
            "[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/$($InputObject.LinkedTemplateURI))"
        }
    }
}
```

We will also create a PowerShell script called `CreateReadMe.ps1` that will call the `ReadMe.doc.ps1` and pass on the required parameters like our ARM template file and metadafile.

```powershell
param (
	[Parameter(Mandatory=$true)]
    [string]$WorkingDir,
    [Parameter(Mandatory=$true)]
    [string]$PipelineName,
    [Parameter(Mandatory=$true)]
    [string]$PipelineID,
    [string]$DocTemplatePath = '000-Scripts\ReadMe.doc.ps1',
    [string]$LinkedTemplatePath = 'https://<storageaccount>.blob.core.windows.net/arm/'
)

Install-Module -Name PSDocs -Force

$templatefile = "$WorkingDir\$PipelineName\azuredeploy.json"
$metadatafile = "$WorkingDir\$PipelineName\metadata.json"

$PSDocsInputObject = New-Object PsObject -property @{
    'MetadataFile' = $metadatafile
    'ARMTemplate' = $templatefile
    'LinkedTemplateURI' = [uri]::EscapeDataString($LinkedTemplatePath + $PipelineName +"/azuredeploy.json")
    'PipelineID' = $PipelineID
    'PipelineName' = $PipelineName
}

Invoke-PSDocument -Path "$WorkingDir\$DocTemplatePath" -InputObject $PSDocsInputObject -OutputPath "$WorkingDir\$PipelineName" -Instance README
```

## Create a BASH script to run the git commands and commit the new README file to the repository

Last we also need to create a BASH script called `GITCommitReadMeFile.sh`. This will run the necessary git commands needed to upload our new README file to our repository.

```bash
BRANCH=$1
FILETOCOMMIT=$2
BUILDNAME=$3

ECHO "Setting git config..."
git config --global user.email "IaCBuildServiceAccount@<domain>"
git config --global user.name "IaC Build Service Account"

ECHO "CHECK GIT STATUS..."
git status

ECHO "CHECK OUT BRANCH..."
git checkout -b $BRANCH

ECHO "GIT ADD..."
git add $FILETOCOMMIT

ECHO "Commiting the changes..."
git commit -m "ReadMe Update from Build $BUILDNAME"

ECHO "Pushing the changes..."
git push -u origin $BRANCH

ECHO "CHECK GIT STATUS..."
git status
```

> Note: We are using `git add $FILETOCOMMIT` to only commit the README.md file to minimise the risk of this process completely destroying our repository.

## Creating a Pipeline Job

Let's put everything together into a pipeline job. The first task will call the Readme.doc.ps1 file with the required parameters as mentioned above, the second task will add and commit the new file to our repository.

```yml
  - job: UpdateReadMe
    displayName: "Update Template ReadMe File"
    steps:
    - checkout: self
      persistCredentials: true
    - task: PowerShell@2
      name: 'CreateReadMe'
      displayName: 'Create ReadMe File'
      inputs:
        filePath: '$(System.DefaultWorkingDirectory)\000-Scripts\CreateReadMe.ps1'
        arguments: '-WorkingDir $(System.DefaultWorkingDirectory) -PipelineName $(Build.DefinitionName) -PipelineID $(System.DefinitionId) -DocTemplatePath 000-Scripts\ReadMe.doc.ps1 -LinkedTemplatePath $(LinkedTemplatePrefix)'
        errorActionPreference: 'silentlyContinue'
    - task: Bash@3
      name: 'CommitReadMe'
      displayName: 'Upload ReadMe File'
      inputs:
        filePath: '$(System.DefaultWorkingDirectory)\000-Scripts\GITCommitReadMeFile.sh'
        arguments: '$(Build.SourceBranchName) "$(Build.DefinitionName)/README.md" $(Build.BuildNumber)'
```

## Running the pipeline

Now we kick off our pipeline and have a look at the results.
![Pipeline Execution]({{ site.url }}/assets/images/2020-04-24-PipelineExecution.png)

We can see that after the pipeline completes the README.md file has been updated.
![ReadMe File]({{ site.url }}/assets/images/2020-04-24-ReadMeFile.png)
