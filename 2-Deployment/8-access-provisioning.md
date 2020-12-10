---
sort: 8
---
# Access provisioning
The following sections will guide you through the processes required to set-up the required rights and privleges for service accounts and credentials used.

## Cloud Deployment Credentials

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

## Local Development Credentials

- To facilitate local development Service Principals are used. Provision a service principal to act as a proxy for each of the MSI's in the list above. Once provisioned, grant these MSI's the equivalent rights so that they can appropriatley mimic the MSI's. Note, it is recommended that you only provision these service principals in NON-PRODUCTION environments. 