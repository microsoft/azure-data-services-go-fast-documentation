---
sort: 4
---

# Database Deployment

- Navigate to the folder shown below:
``` fs_name
{RepoCloneDir}\solution\Database\ADSGoFastDatabase
```
- Within this folder find the file ADSGoFastDatabase.sln and open it using SQL Server Data Tools. Note that this is a Visual Studio Data Tools project file and will require Visual Studio data tools to be installed on your machine. 
- Deploy the database project to the new Azure SQL Server instance that has been created in your sandbox environment by the deployment process. 
- Run the Post Deployment scripts located on your local storage at the address shown below: 
``` fs_name
{RepoCloneDir}\solution\Database\ADSGoFastDatabase\ADSGoFastDatabase\Scripts\
```
- Note that your newly created database should be the target for the post deployment scripts. 

