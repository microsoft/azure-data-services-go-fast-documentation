# Metadata
The following table describes the tables used to operate the framework. Each description includes a specific verb:
* **describes** means that this is a record of an instance which exists elsewhere
* **defines** means that this is the primary Definition of these entities
* **records** means that this table contains rows which are generated while the framework is operating

|Table Name|Type|Description|
|:-------|:-------|:-------|
|ActivityLevelLogs|Log/Audit Table|Records Log events from Azure Function|
|ADFActivityErrors|Log/Audit Table|Records Azure Data Factory activities errors|
|ADFActivityRun|Log/Audit Table|Records Azure Data Factory activities details|
|ADFPipelineRun|Log/Audit Table|Records Azure Data Factory pipeline details|
|ADFPipelineStats|Log/Audit Table|Records Azure Data Factory pipeline statistics|
|AzureStorageChangeFeed|System Table|Defines Azure Storage change feed|
|AzureStorageChangeFeedCursor|System Table|Defines Azure Storage change feed cursor|
|AzureStorageListing|System Table|Describes Azure Storage path for uploaded file from web base app|
|DataFactory|User Table|Describes DataFactory instances|
|Execution|System Table|Records each invocation of the framework|
|FrameworkTaskRunner|User Table|Describes number of parallel Framework Task Runner|
|ScheduleInstance|System Table|Records the instances of a ScheduledMaster|
|ScheduleMaster|User Table|Defines framework schedules types via a Cron expression|
|SourceAndTargetSystems|User Table|Defines Source and Target systems such as, SQL Server, Azure SQL, Blob Storage and Azure Data Lake Storage|
|SourceAndTargetSystems_JsonSchema|User Table|Defines accepted/required properties for each SystemType (Azure SQL, ADLS, Blob) on table SourceAndTargetSystems - SystemJSON column|
|TaskGroup|User Table|Decribes Group of Tasks|
|TaskGroupDependency|User Table|Describes dependency on Task Groups|
|TaskInstance|System Table|Records a scheduled execution of a TaskMaster|
|TaskInstanceExecution|System Table|Records the number of attempts for a TaskMasterInstance|
|TaskMaster|User Table|Defines a task between source and target systems|
|TaskMasterDependency|User Table|Defines dependency of TaskMaster|
|TaskMasterWaterMark|User Table|Defines watermark for tasks specified on TaskMaster|
|TaskType|User Table|Defines the different types of task, such as "Azure Storage to SQL Database", "Azure Storage to Azure Storage", "Execute SQL Stored Procedure"|
|TaskTypeMapping|User Table|Defines the mapping between ADF Pipeline name based on type of Source and Target System|

An Entity Relationship diagram of this database is shown below:

![ERD](media/database-erd.jpg)


## ActivityLevelLogs

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
ActivityType|varchar|YES||
Comment|varchar|YES||
ExecutionUid|uniqueidentifier|YES||
LogDateTimeOffset|datetime|YES||
LogDateUTC|datetime|YES||
LogSource|varchar|YES||
message|varchar|YES||
operation_Id|varchar|YES||
operation_Name|varchar|YES||
severityLevel|int|YES||
Status|varchar|YES||
TaskInstanceId|int|YES||
TaskMasterId|int|YES||
timestamp|datetime|YES||

## ADFActivityErrors

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
ActivityIterationCount|int|YES||
ActivityName|varchar|YES||
ActivityRunId|varchar|YES||
ActivityType|varchar|YES||
Annotations|varchar|YES||
Category|varchar|YES||
CorrelationId|uniqueidentifier|NO||
DatafactoryId|bigint|YES||
EffectiveIntegrationRuntime|varchar|YES||
End|datetime|YES||
Error|varchar|YES||
ErrorCode|int|YES||
ErrorMessage|varchar|YES||
EventMessage|varchar|YES||
FailureType|varchar|YES||
Input|varchar|YES||
Level|varchar|YES||
LinkedServiceName|varchar|YES||
Location|varchar|YES||
OperationName|varchar|YES||
Output|varchar|YES||
PipelineName|varchar|YES||
PipelineRunId|uniqueidentifier|YES||
ResourceId|varchar|YES||
SourceSystem|varchar|YES||
Start|datetime|YES||
Status|varchar|YES||
Tags|varchar|YES||
TenantId|varchar|YES||
TimeGenerated|datetime|YES||
Type|varchar|YES||
UserProperties|varchar|YES||

## ADFActivityRun

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
Activities|bigint|YES||
CloudOrchestrationCost|real|YES||
CloudPipelineActivityCost|real|YES||
DataFactoryId|bigint|NO||
dataRead|bigint|YES||
dataWritten|bigint|YES||
End|datetimeoffset|YES||
FailedActivities|bigint|YES||
MaxActivityTimeGenerated|datetimeoffset|YES||
PipelineRunUid|uniqueidentifier|NO||
rowsCopied|bigint|YES||
SelfHostedDataMovementCost|real|YES||
SelfHostedOrchestrationCost|real|YES||
SelfHostedPipelineActivityCost|real|YES||
Start|datetimeoffset|YES||
TaskExecutionStatus|varchar|YES||
TotalCost|real|YES||

## ADFPipelineRun

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
Activities|bigint|YES||
CloudOrchestrationCost|real|YES||
CloudPipelineActivityCost|real|YES||
DatafactoryId|int|NO||
DatafactoryId|bigint|NO||
dataRead|bigint|YES||
dataWritten|bigint|YES||
End|datetimeoffset|YES||
End|datetimeoffset|YES||
ExecutionUid|uniqueidentifier|NO||
ExecutionUid|uniqueidentifier|NO||
FailedActivities|bigint|YES||
MaxActivityTimeGenerated|datetimeoffset|YES||
MaxPipelineTimeGenerated|datetimeoffset|NO||
MaxPipelineTimeGenerated|datetimeoffset|NO||
PipelineName|varchar|YES||
PipelineRunStatus|varchar|NO||
PipelineRunStatus|varchar|NO||
PipelineRunUid|uniqueidentifier|NO||
PipelineRunUid|uniqueidentifier|NO||
rowsCopied|bigint|YES||
SelfHostedDataMovementCost|real|YES||
SelfHostedOrchestrationCost|real|YES||
SelfHostedPipelineActivityCost|real|YES||
Start|datetimeoffset|YES||
Start|datetimeoffset|YES||
TaskExecutionStatus|varchar|YES||
TaskInstanceId|bigint|NO||
TaskInstanceId|int|NO||
TotalCost|real|YES||

## ADFPipelineStats

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
Activities|bigint|YES||
Activities|bigint|YES||
CloudOrchestrationCost|real|YES||
CloudOrchestrationCost|real|YES||
CloudPipelineActivityCost|real|YES||
CloudPipelineActivityCost|real|YES||
DataFactoryId|bigint|NO||
DataFactoryId|bigint|YES||
dataRead|bigint|YES||
dataRead|bigint|YES||
dataWritten|bigint|YES||
dataWritten|bigint|YES||
End|datetimeoffset|YES||
End|datetimeoffset|YES||
ExecutionUid|uniqueidentifier|NO||
ExecutionUid|uniqueidentifier|NO||
FailedActivities|bigint|YES||
FailedActivities|bigint|YES||
MaxActivityDateGenerated|date|YES||
MaxActivityTimeGenerated|datetimeoffset|YES||
MaxActivityTimeGenerated|datetimeoffset|YES||
MaxPipelineDateGenerated|date|YES||
MaxPipelineTimeGenerated|datetimeoffset|NO||
PipelineRunStatus|varchar|NO||
PipelineRunUid|uniqueidentifier|YES||
rowsCopied|bigint|YES||
rowsCopied|bigint|YES||
SelfHostedDataMovementCost|real|YES||
SelfHostedDataMovementCost|real|YES||
SelfHostedOrchestrationCost|real|YES||
SelfHostedOrchestrationCost|real|YES||
SelfHostedPipelineActivityCost|real|YES||
SelfHostedPipelineActivityCost|real|YES||
Start|datetimeoffset|YES||
Start|datetimeoffset|YES||
TaskExecutionStatus|varchar|YES||
TaskExecutionStatus|varchar|YES||
TaskInstanceId|bigint|NO||
TaskInstanceId|int|NO||
TotalCost|real|YES||
TotalCost|real|YES||

## AzureStorageChangeFeed

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
EventData.BlobOperationName|varchar|YES||
EventData.BlobType|varchar|YES||
EventTime|datetimeoffset|YES||
EventType|varchar|YES||
Pkey1ebebb3a-d7af-4315-93c8-a438fe7a36ff|bigint|NO||
Subject|varchar|YES||
Topic|varchar|YES||

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
AzureStorageChangeFeedCursor	SourceSystemId|bigint|NO
AzureStorageChangeFeedCursor	ChangeFeedCursor|varchar|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
AzureStorageListing	SystemId|bigint|NO
AzureStorageListing	PartitionKey|varchar|NO
AzureStorageListing	RowKey|varchar|NO
AzureStorageListing	FilePath|varchar|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
DataFactory	Id|bigint|NO
DataFactory	Name|varchar|YES
DataFactory	ResourceGroup|varchar|YES
DataFactory	SubscriptionUid|uniqueidentifier|YES
DataFactory	DefaultKeyVaultURL|varchar|YES
DataFactory	LogAnalyticsWorkspaceId|uniqueidentifier|YES


|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
Execution	ExecutionUid|uniqueidentifier|NO
Execution	StartDateTime|datetimeoffset|YES
Execution	EndDateTime|datetimeoffset|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
FrameworkTaskRunner	TaskRunnerId|int|NO
FrameworkTaskRunner	TaskRunnerName|varchar|YES
FrameworkTaskRunner	ActiveYN|bit|YES
FrameworkTaskRunner	Status|varchar|YES
FrameworkTaskRunner	MaxConcurrentTasks|int|YES
FrameworkTaskRunner	LastExecutionStartDateTime|datetimeoffset|YES
FrameworkTaskRunner	LastExecutionEndDateTime|datetimeoffset|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
ScheduleInstance	ScheduleInstanceId|bigint|NO
ScheduleInstance	ScheduleMasterId|bigint|YES
ScheduleInstance	ScheduledDateUtc|datetime|YES
ScheduleInstance	ScheduledDateTimeOffset|datetimeoffset|YES
ScheduleInstance	ActiveYN|bit|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
ScheduleMaster	ScheduleMasterId|bigint|NO
ScheduleMaster	ScheduleCronExpression|nvarchar|NO
ScheduleMaster	ScheduleDesciption|varchar|NO
ScheduleMaster	ActiveYN|bit|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
SourceAndTargetSystems	SystemId|bigint|NO
SourceAndTargetSystems	SystemName|nvarchar|NO
SourceAndTargetSystems	SystemType|nvarchar|NO
SourceAndTargetSystems	SystemDescription|nvarchar|NO
SourceAndTargetSystems	SystemServer|nvarchar|NO
SourceAndTargetSystems	SystemAuthType|nvarchar|NO
SourceAndTargetSystems	SystemUserName|nvarchar|YES
SourceAndTargetSystems	SystemSecretName|nvarchar|YES
SourceAndTargetSystems	SystemKeyVaultBaseUrl|nvarchar|YES
SourceAndTargetSystems	SystemJSON|nvarchar|YES
SourceAndTargetSystems	ActiveYN|bit|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
SourceAndTargetSystems_JsonSchema	SystemType|varchar|NO
SourceAndTargetSystems_JsonSchema	JsonSchema|nvarchar|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskGroup	TaskGroupId|bigint|NO
TaskGroup	TaskGroupName|nvarchar|NO
TaskGroup	TaskGroupPriority|int|NO
TaskGroup	TaskGroupConcurrency|int|NO
TaskGroup	TaskGroupJSON|nvarchar|YES
TaskGroup	MaximumTaskRetries|int|NO
TaskGroup	ActiveYN|bit|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskGroupDependency	AncestorTaskGroupId|bigint|NO
TaskGroupDependency	DescendantTaskGroupId|bigint|NO
TaskGroupDependency	DependencyType|varchar|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskGroupStats	TaskGroupId|bigint|NO
TaskGroupStats	TaskGroupName|nvarchar|NO
TaskGroupStats	Tasks|int|YES
TaskGroupStats	TaskInstances|int|YES
TaskGroupStats	Schedules|int|YES
TaskGroupStats	ScheduleInstances|int|YES
TaskGroupStats	Executions|int|YES
TaskGroupStats	EstimatedCost|float|YES
TaskGroupStats	RowsCopied|bigint|YES
TaskGroupStats	DataRead|bigint|YES
TaskGroupStats	DataWritten|bigint|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskInstance	TaskInstanceId|bigint|NO
TaskInstance	TaskMasterId|bigint|NO
TaskInstance	ScheduleInstanceId|bigint|NO
TaskInstance	ExecutionUid|uniqueidentifier|NO
TaskInstance	ADFPipeline|nvarchar|NO
TaskInstance	TaskInstanceJson|nvarchar|YES
TaskInstance	LastExecutionStatus|varchar|YES
TaskInstance	LastExecutionUid|uniqueidentifier|YES
TaskInstance	LastExecutionComment|varchar|YES
TaskInstance	NumberOfRetries|int|NO
TaskInstance	ActiveYN|bit|YES
TaskInstance	CreatedOn|datetimeoffset|YES
TaskInstance	UpdatedOn|datetimeoffset|YES
TaskInstance	TaskRunnerId|int|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskInstanceAndScheduleInstance	TaskInstanceId|bigint|NO
TaskInstanceAndScheduleInstance	TaskMasterId|bigint|NO
TaskInstanceAndScheduleInstance	ScheduleInstanceId|bigint|NO
TaskInstanceAndScheduleInstance	ExecutionUid|uniqueidentifier|NO
TaskInstanceAndScheduleInstance	ADFPipeline|nvarchar|NO
TaskInstanceAndScheduleInstance	TaskInstanceJson|nvarchar|YES
TaskInstanceAndScheduleInstance	LastExecutionStatus|varchar|YES
TaskInstanceAndScheduleInstance	LastExecutionComment|varchar|YES
TaskInstanceAndScheduleInstance	NumberOfRetries|int|NO
TaskInstanceAndScheduleInstance	ActiveYN|bit|YES
TaskInstanceAndScheduleInstance	CreatedOn|datetimeoffset|YES
TaskInstanceAndScheduleInstance	TaskRunnerId|int|YES
TaskInstanceAndScheduleInstance	ScheduledDateUtc|datetime|YES
TaskInstanceAndScheduleInstance	ScheduledDateTimeOffset|datetimeoffset|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskInstanceExecution	ExecutionUid|uniqueidentifier|NO
TaskInstanceExecution	TaskInstanceId|bigint|NO
TaskInstanceExecution	DatafactorySubscriptionUid|uniqueidentifier|YES
TaskInstanceExecution	DatafactoryResourceGroup|varchar|YES
TaskInstanceExecution	DatafactoryName|varchar|YES
TaskInstanceExecution	PipelineName|varchar|YES
TaskInstanceExecution	AdfRunUid|uniqueidentifier|YES
TaskInstanceExecution	StartDateTime|datetimeoffset|YES
TaskInstanceExecution	EndDateTime|datetimeoffset|YES
TaskInstanceExecution	Status|varchar|NO
TaskInstanceExecution	Comment|varchar|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskMaster	TaskMasterId|bigint|NO
TaskMaster	TaskMasterName|nvarchar|NO
TaskMaster	TaskTypeId|int|NO
TaskMaster	TaskGroupId|bigint|NO
TaskMaster	ScheduleMasterId|bigint|NO
TaskMaster	SourceSystemId|bigint|NO
TaskMaster	TargetSystemId|bigint|NO
TaskMaster	DegreeOfCopyParallelism|int|NO
TaskMaster	AllowMultipleActiveInstances|bit|NO
TaskMaster	TaskDatafactoryIR|nvarchar|NO
TaskMaster	TaskMasterJSON|nvarchar|YES
TaskMaster	ActiveYN|bit|NO
TaskMaster	DependencyChainTag|varchar|YES
TaskMaster	DataFactoryId|bigint|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskMasterDependency	AncestorTaskMasterId|bigint|NO
TaskMasterDependency	DescendantTaskMasterId|bigint|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskMasterStats	TaskGroupId|bigint|NO
TaskMasterStats	TaskGroupName|nvarchar|NO
TaskMasterStats	TaskMasterId|bigint|NO
TaskMasterStats	TaskMasterName|nvarchar|NO
TaskMasterStats	Tasks|int|YES
TaskMasterStats	TaskInstances|int|YES
TaskMasterStats	Schedules|int|YES
TaskMasterStats	ScheduleInstances|int|YES
TaskMasterStats	Executions|int|YES
TaskMasterStats	EstimatedCost|float|YES
TaskMasterStats	RowsCopied|bigint|YES
TaskMasterStats	DataRead|bigint|YES
TaskMasterStats	DataWritten|bigint|YES

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskMasterWaterMark	TaskMasterId|bigint|NO
TaskMasterWaterMark	TaskMasterWaterMarkColumn|nvarchar|NO
TaskMasterWaterMark	TaskMasterWaterMarkColumnType|nvarchar|NO
TaskMasterWaterMark	TaskMasterWaterMark_DateTime|datetime|YES
TaskMasterWaterMark	TaskMasterWaterMark_BigInt|bigint|YES
TaskMasterWaterMark	TaskWaterMarkJSON|nvarchar|YES
TaskMasterWaterMark	ActiveYN|bit|NO
TaskMasterWaterMark	UpdatedOn|datetimeoffset|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskType	TaskTypeId|int|NO
TaskType	TaskTypeName|nvarchar|NO
TaskType	TaskExecutionType|nvarchar|NO
TaskType	TaskTypeJson|nvarchar|YES
TaskType	ActiveYN|bit|NO

|Column Name|Type|IsNull|Description|
|:----------|:----|:----|:-------|
TaskTypeMapping	TaskTypeMappingId|int|NO
TaskTypeMapping	TaskTypeId|int|NO
TaskTypeMapping	MappingType|nvarchar|NO
TaskTypeMapping	MappingName|nvarchar|NO
TaskTypeMapping	SourceSystemType|nvarchar|NO
TaskTypeMapping	SourceType|nvarchar|NO
TaskTypeMapping	TargetSystemType|nvarchar|NO
TaskTypeMapping	TargetType|nvarchar|NO
TaskTypeMapping	TaskDatafactoryIR|nvarchar|NO
TaskTypeMapping	TaskTypeJson|nvarchar|YES
TaskTypeMapping	ActiveYN|bit|NO
TaskTypeMapping	TaskMasterJsonSchema|varchar|YES
TaskTypeMapping	TaskInstanceJsonSchema|varchar|YES

## ADFActivityErrors

## ADFActivityRun

## ADFPipelineRun

## ADFPipelineStats

## AzureStorageChangeFeed

## AzureStorageChangeFeedCursor

## AzureStorageListing

## DataFactory

## Execution

## FrameworkTaskRunner

## ScheduleInstance

## ScheduleMaster

## SourceAndTargetSystems

## SourceAndTargetSystems_JsonSchema

## TaskGroup

## TaskGroupDependency

## TaskInstance

## TaskInstanceExecution

## TaskMaster

## TaskMasterDependency

## TaskMasterWaterMark

## TaskType

## TaskTypeMapping

# Other Objects (Stored Procedure, Views and Functions)

## ActivityAudit
This table records Log events from the framework.

|Column Name|Type|Description|
|:----------|:----|:-------|
|ActivityAuditUid|uniqueidentifier|
|ExecutionUid|uniqueidentifier|
|StartDateTimeOffSet|datetimeoffset|
|EndDateTimeOffSet|datetimeoffset|
|RowsInserted|bigint|
|RowsUpdated|bigint|
|Status|nvarchar|
|Comment|nvarchar|
|TaskInstanceId|bigint|
|AdfRunUid|uniqueidentifier|
|LogTypeId|int| 1 Error, 2 Warning, 3 Info, 4 Performance, 5 Debug
|LogSource|nvarchar| ADF, Azure Function, SQL
|ActivityType|nvarchar|
|FileCount|bigint|
|LogDateUTC|date|
|LogDateTimeOffSet|datetimeoffset|

## DataFactory
describes DataFactory instances

|Column Name|Type|Description|
|:----------|:----|:-------|
|Id|bigint| Unique Identifier (PK)
|Name|varchar|
|ResourceGroup|varchar|
|SubscriptionUid|uniqueidentifier|
|DefaultKeyVaultURL|varchar|

## Execution
records each invocation of the framework
|Column Name|Type|Description|
|:----------|:----|:-------|
|Id|bigint|
|Name|varchar|
|ResourceGroup|varchar|
|SubscriptionUid|uniqueidentifier|
|DefaultKeyVaultURL|varchar|

## ScheduleInstance
records the instances of a ScheduleMaster

|Column Name|Type|Description|
|:----------|:----|:-------|
|ScheduleInstanceId|bigint| Unique Identifier (PK)
|ScheduleMasterId|bigint|
|ScheduledDateUtc|datetime|
|ScheduledDateTimeOffset|datetimeoffset|
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

## ScheduleMaster
defines a specific schedules via a Cron expression

|Column Name|Type|Description|
|:----------|:----|:-------|
|ScheduleMasterId|bigint| Unique Identifier (PK)
|ScheduleCronExpression|nvarchar|
|ScheduleDesciption|varchar|
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

## SourceAndTargetSystems
The SourceAndTargetSystems table describes Source and Target systems such as, SQL Server, Blob Storage and Azure Data Lake Storage. Columns are used for the main attributes, but due to the variability of the specific attributes, these are stored within the SystemJSON column.

For example:
``` js
    { "Database" : "AdsGoFastStaging" }
```
or 
``` js
    { "Container" : "data" }
```
or, if SystemAuthType = "Username/Password", the Key Vault secret names should be supplied within the JSON:
``` js
	{ "Database" : "AdsGoFastStaging",
	  "UsernameKeyVaultSecretName": "usernamekey"
	  "PasswordKeyVaultSecretName": "passwordkey"
    }
```


|Column Name|Type|Description|
|:----------|:----|:-------|
|SystemId|bigint| Unique Identifier (PK)
|SystemName|nvarchar| short name 
|SystemType|nvarchar| type of system, as described below
|SystemDescription|nvarchar| description of this stem
|SystemServer|nvarchar|
|SystemAuthType|nvarchar| one of: MSI; Trusted; SQLAuth; WindowsAuth; Username/Password
|SystemUserName|nvarchar| if SQL or Windows auth is used, the UserName 
|SystemSecretName|nvarchar| if SQL or Windows auth is used, the Password secret id from the Key Vault
|SystemKeyVaultBaseUrl|nvarchar| if SQL or Windows auth is used,the URL of the Key Vault
|SystemJSON|nvarchar| a detailed spefication of this system in JSON, as described above
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

The SystemType value must be one of:
* Azure SQL
* Azure Blob
* ADLS
* File
* MsSqlServer

## TaskGroup
The TaskGroup table describes a group of tasks which may all be executed at the same time.

|Column Name|Type|Description|
|:----------|:----|:-------|
|TaskGroupId|bigint|Unique Identifier (PK)
|TaskGroupName|nvarchar| name of this Task Group
|TaskGroupPriority|int| the relative priority of this Task Group
|TaskGroupConcurrency|int| the maximum number of tasks which can run concurrently within this group. Null = use default calculation
|TaskGroupJSON|nvarchar| extension field
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

## TaskGroupDependency
This table describes the dependency between 2 TaskGroups. In order for one task to depend on another, the following configuration must be established:
* a row in the TaskGroupDependency table - with a reference to the Ancestor and Descendent task groups
* for each pair of dependent tasks (one from each group) - a matching value in the TaskMaster row for each task. This should be a value unique to this pairing - eg, a Table name, or filename.

The current dependency types available are:
* TasksMatchedByTagAndSchedule

|Column Name|Type|Description|
|:----------|:----|:-------|
|AncestorTaskGroupId|bigint| reference to the Ancestor task group
|DescendantTaskGroupId|bigint| reference to the Descendent task group
|DependencyType|varchar| the dependency type.

## TaskInstance
This table records a scheduled execution of a TaskMaster.

The LastExecutionStatus has a number of states:
* Untried
* InProgress
* Complete
* Failed 

|Column Name|Type|Description|
|:----------|:----|:-------|
|TaskInstanceId|bigint| Unique Identifier (PK)
|TaskMasterId|bigint|
|CreatedOn|datetimeoffset|
|ScheduleInstanceId|bigint|
|ExecutionUid|uniqueidentifier|
|ADFPipeline|nvarchar|
|TaskInstanceJson|nvarchar|
|LastExecutionStatus|varchar|
|LastExecutionComment|varchar|
|NumberOfRetries|int|
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

## TaskInstanceExecution
This table records a number of attempts at execution of a TaskMasterInstance. A number of attempts may be performed, if a single attempt fails and a re-run is performed. 

The Status has a number of states:
* InProgress
* Complete
* Failed

|Column Name|Type|Description|
|:----------|:----|:-------|
|ExecutionUid|uniqueidentifier| reference to the Execution row (PK)
|TaskInstanceId|bigint| reference to the TaskInstance row (PK)
|Comment|varchar|
|DatafactorySubscriptionUid|uniqueidentifier| details of the Data Factory executing this task
|DatafactoryResourceGroup|varchar|details of the Data Factory executing this task
|DatafactoryName|varchar|details of the Data Factory executing this task
|PipelineName|varchar| name of Pipeline being executed to satisfy this instance
|AdfRunUid|uniqueidentifier| the unique RunUid of this pipeline
|StartDateTime|datetimeoffset| timestamp when started
|EndDateTime|datetimeoffset| timestamp when ended 
|Status|varchar| the execution status of this Task Instance Execution

## Task Master
This table defines a copy task between source and target systems.  In general, it references other tables for:
* TaskType - for the type of task
* TaskGroup and ScheduleMaster - for when this task should be scheduled
* two references to the SourceAndTargetSystems table - for the Source and Target system

The detailed specification for the source and target details is contained in JSON format in the TaskMasterJSON column. 

An example of this type of format is:
``` js
{ "Source": { 
    "Type": "Excel",
	"RelativePath": "/data/sampledata/",
	"DataFileName": "FinancialSample.xlsx",
	"SchemaFileName": "",
	"FirstRowAsHeader": "True",
	"SheetName": "Sheet1"
},    
"Target": 
{  "Type": "Table",
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
}}
```

|Column Name|Type|Description|
|:----------|:----|:-------|
|TaskMasterId| bigint| Primary Key
|TaskMasterName| nvarchar(200)| name of this task
|TaskTypeId|int| reference to TaskType
|TaskGroupId| bigint | reference to TaskGroup
|ScheduleMasterId|bigint|reference to ScheduleMaster
|SourceSystemId|bigint|reference to Source system - in SourceAndTargetSystem
|TargetSystemId|bigint|reference to Target system - in SourceAndTargetSystem
|DegreeOfCopyParallelism|int| |
|AllowMultipleActiveInstances|bit| 
|TaskDatafactoryIR|nvarchar(20) | name of Integration Runtime
|TaskMasterJSON|nvarchar](4000)| detailed specification of copy activity required 
|ActiveYN|bit| indicates if this row is active or not: 1 = Active
|DependencyChainTag|varchar(50)|
|DataFactoryId|bigint| reference to DataFactory

## TaskType
This table defines the different types of task, such as "Azure Storage to SQL Database".

|Column Name|Type|Description|
|:----------|:----|:-------|
|TaskTypeId|int|
|TaskTypeName|nvarchar|
|TaskTypeJson|nvarchar|
|ActiveYN|bit| indicates if this row is active or not: 1 = Active

## TaskTypeMapping
This table defines the variations of each TaskType - linking to a specific Pipeline name to process that comnination.

|Column Name|Type|Description|
|:----------|:----|:-------|

## TaskWaterMark
watermark

|Column Name|Type|Description|
|:----------|:----|:-------|


## System

|Column Name|Description|
|:-------|:-------|
|SystemId|Unique Identifier (PK)|
|SystemType|Source or Target system types. Supported Types are AzureSqlDatabase,AzureBlobFS,AzureBlobStorage and SqlServer|
|SystemDescription|Description such as database "AdventureWorks (Dev)"|
|SystemName|Database name|
|SystemServer|Host/Server name for a Database or Storage Account|
|SystemUserName|Source or Target system user name|
|SystemSecret|Keyvault Secret Name for Password/Key|
|IsActive|Active flag with 0 (FALSE) or 1 (TRUE)|
|CreatedOn|Record Created date & time|
|ModifiedOn|Record Modified date & time|





CREATE TABLE [dbo].[ActivityAudit](
|ActivityAuditUid|uniqueidentifier|NULL,
|ExecutionUid|uniqueidentifier]  NULL,
|TaskInstanceId|bigint]  NULL,
|AdfRunUid|uniqueidentifier]  NULL,
|LogTypeId|int|NULL, -- 1 Error, 2 Warning, 3 Info, 4 Performance, 5 Debug
|LogSource|nvarchar](50) NOT NULL, --ADF, Azure Function, SQL
|ActivityType|nvarchar](200) NULL,
|FileCount|bigint] NULL,
|LogDateUTC|Date|NULL,
|LogDateTimeOffSet|datetimeoffset|NULL,
|StartDateTimeOffSet|datetimeoffset|NULL,
|EndDateTimeOffSet|datetimeoffset] NULL,
|RowsInserted|bigint] NULL,
|RowsUpdated|bigint] NULL,
|Status|nvarchar](50) NULL,
|Comment|nvarchar](4000) NULL,
PRIMARY KEY CLUSTERED 