# Solution Architecture 



## Components

|Azure Service||Recommended SKU*|
|:-------|:-------|:-------|
|Azure Data Factory|Data Orchestration Engine to move data and trigger data transformations (ELT)|Azure Data Factory v2|
|Azure KeyVault|Centralizing storage of secrets/password, such as OnPremises SQL Server password/connection string|Standard|
|Azure Functions|Severless compute service used to control ADS Go Fast framework (C# and Windows OS)|Consumption plan|
|Azure Data Lake Storage Gen2|Data Lake|LRS - StorageV2|
|Azure Blob Storage|Storage account for Logs|LRS - StorageV2|
|Azure SQL Database|ADSGoFast database (Framework Metada) |S0 DTU10|
|Azure Virtual Machine|Virtual Machine for Azure Data Factory Integration RunTime|Standard_B2ms|
|Azure Bastion|Secure RDP to VMs in Azure virtual network, without the need of public IP||
|Azure Monitor (Application Insights)|Monitor the availability, performance, and usage for Azure Functions, Azure SQL, Azure Data Factory and more||

***Minimum required for development. Production environment requirements will depend on data ingestion rate, size, security and HA/DR.**