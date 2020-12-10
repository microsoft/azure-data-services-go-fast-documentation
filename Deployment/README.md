---
sort: 0
---

# Azure Data Service Go Fast - Deployment

In this section you will automatically provision all of the Azure resources required to run ADSGoFast Framework. We will use a pre-defined ARM template with the definition of all Azure services used for a small development environment. After the core services have been provisioned we will then deploy and configure the solution code base.  

## Azure services




--------------------------------------



## Obtain the source code
Get a copy of the source code by either donwloading it as a zip file from git or cloning the repository. 

## Solution Deployment and Configuration
In this section you will use Azure DevOps to deploy the Database project, Data Factory components (Pipeline, Datasets, LinkedServices and Integration Runtime), Azure Function Application, and Administrative Web Application. Click through the links below and follow the instructions provided.


1. [Deploy Azure SQL Database](./overview-deployment-azuresql.md)

1. [Deploy Azure Data Factory Artefacts Application](./overview-deployment-adf.md)

1. [Deploy Azure Function Application](./overview-deployment-funcapp.md)

1. [Deploy Web Application](./overview-deployment-webapp.md)


## Access provisioning
The following sections will guide you through the processes required to set-up the required rights and privleges for service accounts and credentials used.

### Deployment Credentials

- Azure Data Factory MSI - Grant the managed service identity for Azure Data Factory rights as per the list below: 
    - Adventureworks Azure SQL Sample database [Read]
    - Key Vault [Read Secrets]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - On-Prem SQL Server (Proxied by Azure VM in Demo Environment) [Read];
- Azure Functions MSI - Grant the managed service identity  rights as per the list below
    - ADS Go Fast metadata database [Read,Write and Execute]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - Azure Data Factory [Contributor Role];
    - Application Insights for Function App & Web App [Read];
    - Log Analytics for Data Factory [Read]
- Web Application MSI - Grant the managed service identity  rights as per the list below
    - ADS Go Fast metadata database [Read,Write and Execute]
    - Datalake Storage Accounts [Blob Storage Contributor Role]
    - Application Insights for Function App & Web App [Read];
    - Log Analytics for Data Factory [Read]

### Local Development Credentials

- To facilitate local development Service Principals are used. Provision a service principal to act as a proxy for each of the MSI's in the list above. Once provisioned, grant these MSI's the equivalent rights so that they can appropriatley mimic the MSI's. Note, it is recommended that you only provision these service principals in NON-PRODUCTION environments. 

# TODO
## ADD to ARM Template
    - Create Staging database
    - Create Storage Container "datalakeraw and datalakelanding" on Data Lake Storage
    - Create Transient Storage Account and add Containers "transientin and transientout"
        - Create Storage Table "Filelist"
    - Create SendGrid Resource
    - Create Log Analytics





