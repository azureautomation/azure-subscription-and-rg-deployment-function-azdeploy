Azure Subscription and RG Deployment Function AzDeploy
======================================================

            

 


**This script does Resource Group or Subscription deployments.**

Enable-AzureRmAlias
<# 
.Synopsis 
Deploy ARM Templates in a custom way, to streamline deployments 

.DESCRIPTION 
This is a customization of the deployment scripts available on the Quickstart or within Visual Studio Resource group Deployment Solution.
Some of the efficiencies built into this are:
1) Templates from the same project always upload to the same Storage Account Container
2) Only files that have been modified are re-uploaded to the Storage Container.
2.1) This uses git -C $ArtifactStagingDirectory diff --name-only to determine which files have been modified
3) Only DSC files/Module are repackaged and uploaded if the DSC ps1 files are modified
4) You can still upload all of the files by using the -FullUpload Switch
5) You can skip all uploads by using the -NoUpload Switch
6) You will have to set the $ArtifactStagingDirectory to the working directory where you save your project.
6.1) You could also just set that to the $pwd, then set your location to the directory with your templates before deploying
7) You set the Default orchestration template to deploy with $TemplateFile, however you can also pass in the Template File Path to deploy an alternate template file.
8) You set the Default parameter file with $TemplateParametersFile
9) You should modify the Parameters to match your naming standard for your Resource Groups
9.1) I use AZE2-ADF-RG-D1,AZE2-ADF-RG-T2,AZE2-ADF-RG-P3 for Dev, Test, Prod RG's
10) If you currently deploy from Visual Studio I would recommend to try this Script in VS Code
10.1) It's super fast to deploy by commandline, without having to use the mouse
10.2) Not having to upload the artifacts each time saves to much time, your Dev cycles will be enhanced.
10.3) Create a workspace in VS Code with all of your Repo Directories, than access all your code from the single place
11) Let me know if you have any ideas or feedback

.EXAMPLE 
AZDeploy -DP D1

WARNING: Using parameter file: D:\Repos\AZE2-ADF-RG-D01\AZE2-ADF-RG-D01\azuredeploy.1-dev.parameters.json
WARNING: Using template file: D:\Repos\AZE2-ADF-RG-D01\AZE2-ADF-RG-D01\0-azuredeploy-ALL.json

VERBOSE: _artifactsLocation
WARNING: https://stageeus2.blob.core.windows.net/aze2-adf-rg-stageartifacts
VERBOSE: Environment
WARNING: D
VERBOSE: DeploymentDebugLogLevel
WARNING: None
VERBOSE: DeploymentID
WARNING: 1
VERBOSE: _artifactsLocationSasToken
WARNING: System.Security.SecureString
VERBOSE: TemplateFile
WARNING: D:\Repos\AZE2-ADF-RG-D01\AZE2-ADF-RG-D01\0-azuredeploy-ALL.json
VERBOSE: TemplateParameterFile
WARNING: D:\Repos\AZE2-ADF-RG-D01\AZE2-ADF-RG-D01\azuredeploy.1-dev.parameters.json
 
Name Length LastModified
---- ------ ------------
5-azuredeploy-VMApp.json 32669 4/19/2018 5:06:23 AM +00:00

VERBOSE: Performing the operation 'Creating Deployment' on target 'AZE2-ADF-RG-D1'.
VERBOSE: 11:12:52 PM - Template is valid.
VERBOSE: 11:12:54 PM - Create template deployment '0-azuredeploy-ALL-2018-04-18-2312'
VERBOSE: 11:12:54 PM - Checking deployment status in 5 seconds
VERBOSE: 11:13:00 PM - Checking deployment status in 5 seconds 

.EXAMPLE
AZDeploy -DP D2 -TF .\5-azuredeploy-VMApp.json -DeploymentName AppServers
#>


 




You can also stop a deployment using this other function

[https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Resource-Group-867ad678 ](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Resource-Group-867ad678)


 


 


        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
