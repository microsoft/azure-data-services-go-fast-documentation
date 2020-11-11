# Orchestration Pattern 
The primary orchestration pattern is controlled by two timer triggered Azure functions: 

1. PrepareFrameworkTasks (Timer Trigger)
	* CheckLongRunningPipelines
	* CountRunnningPipelines
	* Calculate Concurrency Slots Available 
 		- FrameworkWideMaxConcurrency less count of  RunnningPipelines
	* CreateTaskInstances
	* DistributeConcurrencySlots
		- Get all TaskGroups which have tasks with a status of "untried" or "failedretry". This is achieved using a the stored procedure [dbo.GetTaskGroups](#dbogettaskgroups).
		- Calculate the number of tasks to be assigned to each task group. Note this is done based on an even distribution. Also note that if the calculated even distribution is less than one (ie. there are more task groups than available concurrency slots) then the number of task groups participating in task distribution will be limited to the top X where X is equal to the number of available concurrency slots. 
		- Loop through each task group and attempt to evenly assign available concurrency slots. Note, if a task group has less tasks to run than the available concurrency slots allocated to the group then the system will cap the concurrency slots distributed and keep the remainder as "surplus" concurrency slots. 
		- Once all groups have been assigend their concurrency slots the system checks to see if there are any "surplus" concurrency slots. If so, another round of concurrency slot allocation is performed until there are no longer any available concurrency slots. 

2. RunFrameworkTasks (Timer Trigger)
	* CheckForIdleFrameworkTaskRunners
	* Async Execute RunFrameworkTasks for Each Idle Runner
	* Retrieve Untried & FailedRetry tasks assigned to current TaskRunner
	* For each task Execute ADF pipeline for task passing in JSON object.


1. Azure Function Runs on Timed Schedule (eg. Every 5 minutes)

    - [] Check status of running pipelines and calculate available "slots" based on max concurrency settings
    - [] Generate new task instances based on task master and schedules
    - [] Identify tasks due to be run or overdue. Fetch top # tasks to be run based on available slots - simultaneously mark these as "InProgress". 
    - [] Async initiate pipeline execution for tasks - Persist status of these taskinstanceexections as "InProgress"
    - [] 

## Scheduling Tasks
The schedule can be configured in 2 different ways:
1. in development, a simple schedule could be used for everything - eg defining it as running every minute - but without having an external triggering mechanism. The task can be triggered manually as described below.  
1. in production, by specifying correct cron scheduling expressions and establishing an external period trigger of the Task Execution mechanism.

## Development Task Execution
The task can be triggered 2 different ways:
- execute the Data Master pipeline within Azure Data Factory - supplying the correct JSON payload
- initiating the RunFrameworkTasksHttpTrigger function. This can be done a number of ways:
  - if running the framework locally, use PostMan to hit the API: http://localhost:7071/api/RunFrameworkTasksHttpTrigger
  - if running against an Azure deployed framework:
    - use the Azure portal to execute the function
    - use PostMan to hit the remote API: https://adsgofastfuncapp.azurewebsites.net/api/RunFrameworkTasksHttpTrigger


## Production Task Execution
When in Production, the tasks wil be scheduled by establishing a periodic initiation of the RunFrameworkTasksHttpTrigger function.  This is typically done via a Timer-triggered function. See [documentation](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-scheduled-function#create-a-timer-triggered-function) for details.

## Task Processing

The most common task definition is for copying data from source to target. Some general aspects of this are described below:

### Data Extraction Schema

When data is extracted from a structured source (SQL Database), the schema is persisted where possible. For example, an extract from a table called FinancialStatement will yeild the following schema in a file named FinancialStatement.json:

```json
[
  {
    "ORDINAL_POSITION": 1,
    "COLUMN_NAME": "Segment",
    "DATA_TYPE": "nvarchar",
    "IS_NULLABLE": true,
    "NUMERIC_PRECISION": null,
    "CHARACTER_MAXIMUM_LENGTH": -1,
    "NUMERIC_SCALE": null,
    "IS_IDENTITY": false,
    "IS_COMPUTED": false,
    "KEY_COLUMN": false,
    "PKEY_COLUMN": false
  },
  {
    "ORDINAL_POSITION": 2,
    "COLUMN_NAME": "Country",
    "DATA_TYPE": "nvarchar",
    "IS_NULLABLE": true,
    "NUMERIC_PRECISION": null,
    "CHARACTER_MAXIMUM_LENGTH": -1,
    "NUMERIC_SCALE": null,
    "IS_IDENTITY": false,
    "IS_COMPUTED": false,
    "KEY_COLUMN": false,
    "PKEY_COLUMN": false
  },
```
In addition, a Parquet style schema will also be persisted. In this case, it would be named FinancialStatement.parquetschema.json:
```json
[
  {
    "name": "Segment",
    "type": "String"
  },
  {
    "name": "Country",
    "type": "String"
  },
  {
    "name": "Product",
    "type": "String"
  },
  {
    "name": "DiscountBand",
    "type": "String"
  },
```
###  SQL Staging Process
When copying data to an SQL destination, an intermediate staging table is always used, and then an SQL Merge process performed to copy data to the target table.

**Note:** the staging table and target tables are always required, regardless of the copy type being incremental or full.

There are two options for the merge SQL statement:
* auto - specify "AutoGenerateMerge": "True" to have the system generate a Merge statement
* manual - specify "AutoGenerateMerge": "False", and supply a specific SQL Merge statement for the "MergeSQL" field

If the auto option is used, the system will use:
* the schema for the source table
* the schema for the target table
* and then generate an appropriate Merge SQL statement.

The template for the Merge statement is:
```sql
MERGE {TargetFullName} AS a  
    USING (SELECT * from {SourceFullName}) AS b   
    ON ({PrimaryKeyJoin_AB})  
    WHEN MATCHED THEN
        UPDATE SET {UpdateClause}  
    WHEN NOT MATCHED THEN  
        INSERT ({InsertList})  
        VALUES ({SelectListForInsert});  
```
An example of the generated SQL is shown below. The Primary Key is on the customerid column:
```sql
Begin TRY 
MERGE [SalesLT].[CustomerCopy] AS a      
USING (SELECT * from [SalesLT].[stg_CustomerCopy]) AS b     
ON (b.[customerid] = a.[customerid])      
WHEN MATCHED THEN         
UPDATE SET [namestyle] = b.[namestyle],
	[title] = b.[title],
	[firstname] = b.[firstname],
	[middlename] = b.[middlename],
	[lastname] = b.[lastname],
	[suffix] = b.[suffix],
	[companyname] = b.[companyname],
	[salesperson] = b.[salesperson],
	[emailaddress] = b.[emailaddress],
	[phone] = b.[phone],
	[passwordhash] = b.[passwordhash],
	[passwordsalt] = b.[passwordsalt],
	[rowguid] = b.[rowguid],
	[modifieddate] = b.[modifieddate]      
WHEN NOT MATCHED THEN          
	INSERT ([customerid],[namestyle],[title],[firstname],[middlename],
	[lastname],[suffix],[companyname],[salesperson],[emailaddress],[phone],
	[passwordhash],[passwordsalt],[rowguid],[modifieddate])         
	VALUES (b.[customerid],b.[namestyle],b.[title],b.[firstname],
	b.[middlename],b.[lastname],b.[suffix],b.[companyname],
	b.[salesperson],b.[emailaddress],b.[phone],
	b.[passwordhash],b.[passwordsalt],b.[rowguid],b.[modifieddate]);  
END TRY
Begin Catch
	-- Raise an error with the details of the exception
	DECLARE @ErrMsg nvarchar(4000), @ErrSeverity int  
	SELECT @ErrMsg = ERROR_MESSAGE(),
			@ErrSeverity = ERROR_SEVERITY()
	RAISERROR(@ErrMsg, @ErrSeverity, 1)
End Catch
Select 1 
```
If a full load is being performed, then an actual Merge statement may not be required. In this case, supply a simple statement like the following for the MergeSQL value:

```sql
TRUNCATE TABLE [dbo].[FinancialLicenses] 
INSERT INTO [dbo].[FinancialLicenses] 
SELECT * FROM [dbo].[staging_FinancialLicenses]
```

## Define Schedule

Add a row to the ScheduleMaster table indicating when this task should run. The specification of when to run is supplied via the ScheduleCronExpression column, and is in standard cron format. See [CronMaker](http://www.cronmaker.com/) for a handy tool to simplify creating cron expressions.

### Regular Scheduling

A simple schedule entry for development purposes:
``` sql
INSERT INTO [dbo].[ScheduleMaster] ([ScheduleMasterId],[ScheduleCronExpression],[ScheduleDesciption],[ActiveYN])
VALUES  ('0 * * * * *','Every Minute',1)
```
A specific schedule entry to run at 10:30 every weekday:
``` sql
INSERT INTO [dbo].[ScheduleMaster] ([ScheduleMasterId],[ScheduleCronExpression],[ScheduleDesciption],[ActiveYN])
VALUES  ('0 30 10 ? * MON-FRI *','10:30 every weekday morning',1)
```

### Adhoc Scheduling
There are two options available to support adhoc scheduling.

* RunOnce - where a task will only execute once
* Regular - but with silent failure if data not available

#### RunOnce

To configure a run once task, ensure that there is a special entry in the ScheduleMaster table by specifying a cron expresson of "N/A":
``` sql
INSERT INTO [dbo].[ScheduleMaster] ([ScheduleMasterId],[ScheduleCronExpression],[ScheduleDesciption],[ActiveYN])
VALUES  ('N/A','Run Once',1)
```
And then create a TaskMaster entry associated with that schedule. When the ActiveYN column is set to 1, the task will be scheduled for execution. 

Note: The task will run only once. After execution, it will be automatically set to inactive. In order to have it scheduled again, you will need to update the ActiveYN column back to 1 to make it Active again:
``` sql
-- set adhoc task to execute again
update [dbo].[TaskMaster]
 set activeYN = 1
where TaskMasterId = 14
```

## Dependent Tasks


When configuring dependent tasks, it will normally be required to have a common location which is shared between the parent and child tasks. For example, if a chain of tasks is configured to:
* TaskGroup1 - copy from on Prem SQL to Data Lake
* TaskGroup2 - copy from Data Lake to Azure SQL
then a specific, but dynamic, location should be used for the Target of the first task, and the Source for the second:

```JSON
"Target": {
     "Type": "Parquet",
       "RelativePath": "AdventureWorks2017/{@TableSchema@}/{@TableName@}/{yyyy}/{MM}/{dd}/{hh}/{mm}/",
       "DataFileName": "{@TableSchema@}.{@TableName@}.parquet",
       "SchemaFileName": "{@TableSchema@}.{@TableName@}.json"
   },
```


#### Regular

This use case would allow for a regular task to run at a scheduled time - but can silently fail if the source object is not present. 

To configure a task like this:
* define the required schedule entry - eg, 10:00 every day
* define the required TaskMaster entry as normal
* configure the **magic: special column which specifies to fail silently if source not present**


## Define a Task Group

A Task Group is used to collect a set of tasks that should be executed at the same time. In general, these will be scheduled to all run in parallel, subject to the following constraints:

* the maximum number of slots defined - specified via a configuration parameter, and the framework maximum concurrency 
* the current default number of tasks per group - which is computed each time as (number of available slots / number of active task groups)
* the specified number of tasks for this specific group (if this is greater than the current default number of task groups)

The TaskGroupPriority is used to specify which Task Groups should be executed first.

For example, the following statement defines a group with a maximum concurrency of 10:
``` sql
INSERT INTO [dbo].[TaskGroup] ([TaskGroupName],[TaskGroupPriority],[TaskGroupConcurrency],[TaskGroupJSON],[ActiveYN])
Values ('Load Excel',0,10,null,1))
```

## Define Source and Target Systems

Every source and target system must be defined in the SourceAndTargetSystems table.


## Define the Data Factory Instance
Add a row to the DataFactory table registering the specific attirbutes of that instance:

``` sql
INSERT INTO [dbo].[DataFactory] ([Name],[ResourceGroup],[SubscriptionUid],[DefaultKeyVaultURL]) 
VALUES ('adsgofast-datafactory','sandbox','be93c61e-e7f3-4c5c-9e04-2e86a04bb6bb','adsgofast-keyvault')
```
## Define Task Types

## Define Task Type Mappings

## Define Task Masters

The TaskMaster table is used to specify the exact details of the activity to be performed.  As the table description below shows, there are a number of fixed reference fields, while specific details are specified with the SystemJSON column.

The exact format to use depends on the Source and Target types. The generic format is:
``` js
{ "Source": { 
	... 
}, 
{ "Target": { 
	... 
}
```

Source System Type = ADLS or Azure Blob

``` js
{ "Source": { 
    "Type": "Excel",
	"RelativePath": "/data/sampledata/",
	"DataFileName": "FinancialSample.xlsx",
	"SchemaFileName": "",
	"FirstRowAsHeader": "True",
	"SheetName": "Sheet1",
	"SkipLineCount": 3,
	"MaxConCurrentConnections": 1
}
```
Source System Type = "Azure SQL"

``` js
{ "Source": {
    "Type": "Table",
    "IncrementalType": "??",
    "IncrementalField": "??",
    "IncrementalColumnType": "??", -- DateTime or BigInt
	"TableSchema": "dbo",
	"TableName": "FinancialLicenses",
	"ChunkField": "",
	"ChunkSize": ""
	"SQLStatement": ""
}
```
Target System Type = ADLS or Azure Blob

``` js
{ "Target": { 
    "Type": "Excel",
	"TargetRelativePath": "/data/sampledata/",
	"DataFileName": "FinancialSample.xlsx",
	"SchemaFileName": "",
	"FirstRowAsHeader": "True",
	"SheetName": "Sheet1",
	"SkipLineCount": 3,
	"MaxConCurrentConnections": 1
}
```
Target System Type = "Azure SQL"

``` js
{ "Target": {
	"Type": "Table",
	"StagingTableSchema": "dbo",
	"StagingTableName": "stg_AUFinancialLicenses",
	"AutoCreateTable": "False",
	"TableSchema": "dbo",
	"TableName": "AUFinancialLicenses",
	"PreCopySQL": "IF OBJECT_ID('dbo.stg_AUFinancialLicenses') 
	               IS NOT NULL Truncate Table dbo.stg_AUFinancialLicenses",
	"PostCopySQL": "",
	"MergeSQL": "",
	"AutoGenerateMerge": "False"
}
```
