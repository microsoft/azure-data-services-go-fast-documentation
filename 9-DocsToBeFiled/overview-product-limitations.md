# Supported Data Sources

- **Azure SQL Database**
- **Azure Storage (Blob and ADLS Gen2)** files in the following formats JSON, Parquet, XLS and CSV
- **SQL Server IaaS/OnPrem instances**

# Authentication 

- Azure Data Factory uses MSI to authenticate to Azure SQL Database, Azure KeyVault and Azure Storage;
- Azure Data Factory use SQL Authentication to authenticate to On-Prem SQL Server;