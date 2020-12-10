---
sort: 1
---

# Azure Services to be deployed

Please note that these instuctions will deploy the following Azure Services into your subscription:

Name                        | Type | Pricing Tier | Pricing Info |
----------------------------|------|--------------|--------------|
ADFIR-*suffix*	                | Virtual machine | Standard_B2ms | https://azure.microsoft.com/en-us/pricing/details/virtual-machines/windows/
ADFIR-*suffix*OsDisk            | Disk | E10 | https://azure.microsoft.com/en-us/pricing/details/managed-disks/
ADFIR-*suffix*NetInt            | Network interface ||
ads-kv-*suffix*                 | Azure KeyVault| Standard | https://azure.microsoft.com/en-au/pricing/details/key-vault/
adsgofast-srv-*suffix*          | SQL server || 
adsgofast                       | Azure SQL Database (Framework Metadata) | S0 DTU10 | https://azure.microsoft.com/en-us/pricing/details/sql-database/single/
AdventureWorksLT                | Azure SQL Database (Sample DB used for testing) | S0 DTU10 | https://azure.microsoft.com/en-us/pricing/details/sql-database/single/
adsgofast-vnet                  | Virtual network || https://azure.microsoft.com/en-us/pricing/details/virtual-network/
ADSGoFastADF-*suffix*           | Data factory (V2) | Data pipelines | https://azure.microsoft.com/en-us/pricing/details/data-factory/
appinsights-adsgofast           | Azure Monitor (Application Insights) || https://azure.microsoft.com/en-us/pricing/details/monitor/
azure-bastion-ads-go-fast       | Bastion | | https://azure.microsoft.com/en-au/pricing/details/azure-bastion/
azure-bastion-ads-go-fast-pip   | Public IP address || https://azure.microsoft.com/en-us/pricing/details/ip-addresses/
datalakestg*suffix*             | Azure Data Lake Storage Gen2 | LRS - StorageV2 | https://azure.microsoft.com/en-us/pricing/details/storage/data-lake/
FuncApp-*suffix*                | Azure Functions | Consumption plan | https://azure.microsoft.com/en-au/pricing/details/functions/
hpn-DM-ADSGoFast-Dev-RG         | App Service plan ||
logstg*suffix*                  | Azure Blob Storage | LRS - StorageV2 | https://azure.microsoft.com/en-us/pricing/details/storage/blobs/

<br>**IMPORTANT**: When you deploy the resources in your own subscription you are responsible for the charges related to the use of the services provisioned. If you don't want any extra charges associated with the resources you should delete the resource group and all resources in it.