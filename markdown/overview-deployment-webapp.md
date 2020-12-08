# Deploy and Configure Web Application

* Open the Web Application solution found at "\solution\WebApplication\WebApplication.sln". 
* Restore Nuget Packages
* Restore Libman packages
* Publish Application to the App Service Plan created during deployment
* Once published you will need to set the Web Application settings using Kudu. Use the **App Settings Template** provided below to create the appropriate settings. Note, you may not have some of the required information yet as some of it is created later in the deployment and configuration process. If you don't know what to fill out just leave a placeholder value there for now.  
* For local development and testing create an "AppSettings.json" file in the solution using the **App Settings Template** template. Note, you may not have some of the required information yet as some of it is created later in the deployment and configuration process. If you don't know what to fill out just leave a placeholder value there for now.

**App Settings Template**
```jsonc
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AZURE_TENANT_ID": "" //Azure Tenant Id,
  "AZURE_CLIENT_ID": "" //Service Prinicpal Client Id. Only needed for local development environment,
  "AZURE_CLIENT_SECRET": "" //Service Prinicpal secret. Only needed for local development environment,
  "UseMSI": false ///Set to true for Azure deployments and false for local developement deployments,
  "AdsGoFastTaskMetaDataDatabaseServer": "" //Address of the framework configuration database,
  "AdsGoFastTaskMetaDataDatabaseName": "" //Db name of the framework configuration database,
  "AppInsightsWorkspaceId": "" //Application Insights Workspace Id for the Azure Function Application that you deployed previously. This allows the web applicication to display function activity information for monitoring purposes ,
  "AdGroups": [
  ],
  "AllowedHosts": "*",
  "SecurityModelOptions": {
    "SecurityRoles": [
      {
        "SecurityGroupId": "",
        "Name": "Administrators",
        "AllowActions": [
        ]
      }
    ],
    "GlobalAllowActions": [
      "ADFActivityErrors",
      "ADFPipelineStats",
      "AFExecutionSummary",
      "AFLogMonitor",
      "Dashboard",
      "DataFactory",
      "FrameworkTaskRunner",
      "FrameworkTaskRunnerDapper",
      "ReportsAndStatistics",
      "ScheduleInstance",
      "ScheduleMaster",
      "SourceAndTargetSystems",
      "SourceAndTargetSystemsJsonSchema",
      "SubjectArea",
      "TaskGroup",
      "TaskGroupDependency",
      "TaskInstance",
      "TaskInstanceExecution",
      "TaskMaster",
      "TaskMasterWaterMark",
      "TaskType",
      "TaskTypeMapping",
      "Wizards"

    ],
    "GlobalDenyActions": [
      "Customisations.Delete",
      "DataFactory.Delete",
      "FrameworkTaskRunner.Delete",
      "FrameworkTaskRunnerDapper.Delete",
      "ScheduleInstance.Delete",
      "ScheduleMaster.Delete",
      "SourceAndTargetSystems.Delete",
      "SourceAndTargetSystemsJsonSchema.Delete",
      "TaskGroup.Delete",
      "TaskGroupDependency.Delete",
      "TaskGroupDependency.DeletePlus",
      "TaskInstance.Delete",
      "TaskMaster.Delete",
      "TaskMasterWaterMark.Delete",
      "TaskType.Delete",
      "TaskTypeMapping.Delete"
    ]
  },
  //Details below are specificly for AAD integration. You will need to create an App Registration specifically for AAD integration. Do this using the Azure Portal and enable AAD integration for your web app either using the express settup method or by doing it manually. Fill in the relevant info below
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "",
    "TenantId": "",
    "ClientId": "",
    "CallbackPath": "/signin-oidc",
    "SignedOutCallbackPath ": "/signout-callback-oidc"
  }

}
```