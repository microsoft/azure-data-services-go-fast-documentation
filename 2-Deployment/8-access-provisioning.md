---
sort: 8
---
# Access provisioning
The following sections will guide you through the processes required to set-up the required rights and privleges for service accounts and credentials used.

## Cloud Deployment Credentials

### Azure Data Factory MSI
Grant the managed service identity for Azure Data Factory rights as per the table below: 

| Tables   |      Are      |  Cool |
|----------|:-------------:|------:|
| col 1 is |  left-aligned | $1600 |
| col 2 is |    centered   |   $12 |
| col 3 is | right-aligned |    $1 |


| Resource | Rights Required | 
| --------------- | --------------- | 
|Adventureworks Azure SQL Sample database | [Read] |
|Key Vault | [Read Secrets] |
|Datalake Storage Accounts | [Blob Storage Contributor Role] |
|On-Prem SQL Server (Proxied by Azure VM in Demo Environment) | [Read] |

### Azure Functions MSI 
Grant the managed service identity  rights as per the table below:
| Resource | Rights Required | 
| --------------- | --------------- | 
| ADS Go Fast metadata database [Read,Write and Execute] |
| Datalake Storage Accounts | [Blob Storage Contributor Role] |
| Azure Data Factory | [Contributor Role] |
| Application Insights for Function App & Web App | [Read] |
|Log Analytics for Data Factory | [Read]
### Web Application MSI 
Grant the managed service identity  rights as per the table below:
| Resource | Rights Required | 
| --------------- | --------------- | 
| ADS Go Fast metadata database | [Read,Write and Execute] |
| Datalake Storage Accounts | [Blob Storage Contributor Role] |
| Application Insights for Function App & Web App | [Read] |
| Log Analytics for Data Factory | [Read] |

## EasyAuth & AAD Integration for the Web Application and Function Applications
You will need to integrate both your function application and your web application with AAD. Do this by navigating to the deployed applications in the Azure portal and enable AAD integration using Easyauth. The function application makes self referencing, MSI based calls to other functions within the application. Consequently, your will need to ensure that the MSI for the function application has been placed in the appropriate role such that it is allowed to make the function call. To do this first create a role called "All" in your function app. Next assign the application's MSI to that new role. The link below contains instructions on how to do this. 

[Creating and Assigning Application Roles](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps#declare-roles-for-an-application)

## Local Development Credentials

- To facilitate local development Service Principals are used. Provision a service principal to act as a proxy for each of the MSI's in the list above. Once provisioned, grant these MSI's the equivalent rights so that they can appropriatley mimic the MSI's. Note, it is recommended that you only provision these service principals in NON-PRODUCTION environments. 
