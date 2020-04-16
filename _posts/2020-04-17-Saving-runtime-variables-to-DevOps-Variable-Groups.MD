---
title: "Saving runtime variables to DevOps Variable Groups"
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
---

*Today's post comes from guest contributor Rodney Almeida. Coming from a System’s Administrator background, he enjoys working on projects from the ground up and playing with new technologies. He has been exploring Azure for a while and has recently started dipping his toes in Azure DevOps.* [Linkedin](https://www.linkedin.com/in/rodney-almeida-2ab1042b).

We use outputs
When creating and running Azure DevOps pipelines, you may need at times to get outputs from previous steps and store them as variables to be consumed further down the pipeline. The following blog post already details this process really well [blog post](https://github.com/starkfell/100DaysOfIaC/blob/master/articles/day.67.outputs.md).

However once the pipeline is finished these variables are lost and therefore if you need to refer them at a later stage you will need to find the deployment task in azure (if it still exists) and manually get the outputs again. Here you can see the outputs in the Azure Portal:
![Output](https://github.com/starkfell/100DaysOfIaC/blob/master/images/day67/Outputs.png?raw=true)


Unless you save these variables to a variable group in Azure DevOps which can then be referred to in other pipelines. This article will show you how to use Azure CLI to create a new variable group in Azure DevOps and save your runtime variables to it.

## Requirements
First you need to assign the **<Project>'s Build Service (<Organisation>)** Create Access to the Variable Groups.

![create access]({{ site.url }}/assets/images/2020-04-17-AssignAccessToVariableGroups.png)

## Update Pipeline
Next, well add a couple of tasks to our pipeline to login to Azure DevOps CLI from within the pipeline using the `$(System.AccessToken)`. More on this can be [found here:](https://docs.microsoft.com/en-us/azure/devops/cli/azure-devops-cli-in-yaml?view=azure-devops).

Next we will add a PowerShell Task to our pipeline to create the Variable Group and populate the first variable.

```yml
  - script: echo $(System.AccessToken) | az devops login
    env:
      AZURE_DEVOPS_CLI_PAT: $(System.AccessToken)
    displayName: 'Login Azure DevOps Extension'
  - script: az devops configure --defaults organization=https://dev.azure.com/###### project="IaC" --use-git-aliases true
    displayName: 'Set default Azure DevOps organization and project'
  - task: PowerShell@2
    displayName: 'Create Variable Group'
    inputs:
      targetType: 'inline'
      script: |

        # Setting $ErrorActionPreference required to prevent script from returning a false error for feature preview warnings
        $ErrorActionPreference = 'SilentlyContinue'

        # Create Variable Group and Get Variable Group ID for reference in later tasks

        $variablegroup = az pipelines variable-group create --name "OutputVariables_$(Build.BuildNumber)" --variables "OutputsFrom=$(Build.BuildNumber)" | Convertfrom-Json
        Write-Output "##vso[task.setvariable variable=VariableGroupID]$($variablegroup.id)"
        Write-Output "Added VSTS variable 'VariableGroupID' with value '$($variablegroup.id)'"
```

> Note: Although in Microsoft's documentation it mentions to use `echo ${AZURE_DEVOPS_CLI_PAT} | az devops login` to login, I was getting error message when creating the Variable Group. Therefore I use `echo $(System.AccessToken) | az devops login` instead.

## Modify output script
In our pipeline to retrieve outputs from ARM templates we use a powershell tasks to run to capture the JSON outputs and use the captured output in following steps. You can find more information regardin the output sript [here](https://github.com/starkfell/100DaysOfIaC/blob/master/articles/day.67.outputs.md#convert-json-output-to-string).

> Note: I had already previously made other modifications to the script to handle Object type variables and read 1 level further into those Objects.

We will modify the output.ps1 script to add an extra parameter called VariableGroupID. This is the VariableGroupID variable that we captured when we created the variable group in the PowerShell task in the previous step. If this parameter is passed it will record whatever variable it is creating as a new entry into the variable group with the variable group id.

```powershell
<#
Script reads the JSON output from a previous step ($armOutputString) and saves the values as variables.
If there is a $VariableGroupID passed it will also save the value as a variable in the VariableGroup.
Script assumes you have already logged into az devops and set the default org and project values.
#>

param (
    [Parameter(Mandatory=$true)]
    [string] $armOutputString = '',
    [string] $VariableGroupID
)

$ErrorActionPreference = 'SilentlyContinue'
Write-Output "Retrieved input: $armOutputString"
$armOutputObj = $armOutputString | convertfrom-json
$armOutputObj.PSObject.Properties | ForEach-Object {
    $type = ($_.value.type).ToLower()
    $keyname = "Output_"+$_.name
    $value = $_.value.value
    switch ($type) {
        securestring {
            Write-Output "##vso[task.setvariable variable=$keyname;issecret=true]$value"
            Write-Output "Added VSTS variable '$keyname' ('$type')"
            If ($VariableGroupID) {
                az pipelines variable-group variable create --group-id $VariableGroupID --name $keyname --value $value --secret $true
            }
        }
        string {
            Write-Output "##vso[task.setvariable variable=$keyname]$value"
            Write-Output "Added VSTS variable '$keyname' ('$type') with value '$value'"
            If ($VariableGroupID) {
                az pipelines variable-group variable create --group-id $VariableGroupID --name $keyname --value $value
            }
        }
        array {
            Write-Output "##vso[task.setvariable variable=$keyname]$value"
            Write-Output "Added VSTS variable '$keyname' ('$type') with value '$value'"
            If ($VariableGroupID) {
                az pipelines variable-group variable create --group-id $VariableGroupID --name $keyname --value "$($value)"
            }
        }
        object {
            $Value.PSObject.Properties | ForEach-Object {
                Write-Output "##vso[task.setvariable variable=$($keyname+"_"+$_.name)]$($_.value)"
                Write-Output "Added VSTS variable '$($keyname+"_"+$_.name)' ('$type') with value '$($_.value)'"
                If ($VariableGroupID) {
                    az pipelines variable-group variable create --group-id $VariableGroupID --name $($keyname+"_"+$_.name) --value "$($_.value)"
                }
            }
        }
        secureobject {
            $Value.PSObject.Properties | ForEach-Object {
                Write-Output "##vso[task.setvariable variable=$($keyname+"_"+$_.name);issecret=true]$($_.value)"
                Write-Output "Added VSTS variable '$($keyname+"_"+$_.name)' ('$type') with value '$($_.value)'"
                If ($VariableGroupID) {
                    az pipelines variable-group variable create --group-id $VariableGroupID --name $($keyname+"_"+$_.name) --value "$($_.value)" --secret $true
                }
            }    
        }
        default {
            Throw "Type '$type' is not supported for '$keyname'"
        }
    }
}

```
## Running the pipeline
Now we kick off our pipeline and see the results.
![Pipeline Execution]({{ site.url }}/assets/images/2020-04-17-PipelineExecution.PNG)

We can see that after the pipeline completes the following variable group is created
![Variable Group Created]({{ site.url }}/assets/images/2020-04-17-VariableGroupCreated.png)

And all outputs from the pipeline are stored inside that variable group to be referenced at a later stage by different pipelines for example
![Variable Group Content]({{ site.url }}/assets/images/2020-04-17-VariableGroupContent.png)


