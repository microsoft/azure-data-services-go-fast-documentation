---
sort: 6
---

# Task Types Glossary Table

<table>
<colgroup>
<col style="width: 35%" />
<col style="width: 14%" />
<col style="width: 49%" />
</colgroup>
<thead>
<th><strong>Task Master Input</strong></th>
<th><strong>Input Type</strong></th>
<th><strong>Description</strong></th>
</thead>
<tbody>
<tr class="odd">
<td>AutoCreateTable</td>
<td>Dropdown</td>
<td>If the table does not already exist within the targeted database, it
will create a new one automatically.</td>
</tr>
<tr class="even">
<td>AutoGenerateMerge</td>
<td>Dropdown</td>
<td>Allows for an automatically generated SQL merge based on the primary
key of the targeted table.</td>
</tr>
<tr class="odd">
<td>CDCSource</td>
<td>Dropdown</td>
<td>Whether the Source data is from a CDC enabled database. This is used
to modify the way in which the data is manipulated as CDC tables include
additional data.</td>
</tr>
<tr class="even">
<td>ChunkField</td>
<td>Text</td>
<td>If wanting to break down the extraction into multiple files, use the
column names to break it apart.</td>
</tr>
<tr class="odd">
<td>ChunkSize</td>
<td>Integer</td>
<td>The amount of rows to be used for each ‘chunk’ of data
extracted.</td>
</tr>
<tr class="even">
<td>CustomDefinitions</td>
<td>Text</td>
<td>This field is used for the user if they wish to define anything of
their own.</td>
</tr>
<tr class="odd">
<td>DataFileName</td>
<td>Text</td>
<td>Name of the file being referenced, filetype included. NOTE: In the
case of a target file name, this may be a folder if it is being created
by a spark cluster (Synapse). This may also reference a folder if it is
being used by a spark cluster as a source.</td>
</tr>
<tr class="even">
<td>DeleteAfterCompletion</td>
<td>Dropdown</td>
<td>This will delete the source files after a successful run of the
activity.</td>
</tr>
<tr class="odd">
<td>ExecuteNotebook</td>
<td>Text</td>
<td>The notebook that the user wishes to execute for the activity. Many
task types will have this prefilled with the Lockbox supplied notebook
for the task. If the user has a custom notebook for the task they can
reference it here.</td>
</tr>
<tr class="even">
<td>ExtractionSQL</td>
<td>SQL</td>
<td>A custom SQL statement to be used to extract the data. This is
ignored if you have selected a Table sub type.</td>
</tr>
<tr class="odd">
<td>FirstRowAsHeader</td>
<td>Dropdown</td>
<td>Whether the user wants the first row to be used as the column names
(header columns).</td>
</tr>
<tr class="even">
<td>IncrementalType</td>
<td>Dropdown</td>
<td>Whether the user wishes to do a full extraction or a watermark based
extraction of the data.</td>
</tr>
<tr class="odd">
<td>MaxConcurrentConnections</td>
<td>Integer</td>
<td>The limit of concurrent connections to the file allowed during the
execution of the task.</td>
</tr>
<tr class="even">
<td>MergeSQL</td>
<td>SQL</td>
<td>A custom merge SQL statement. This will be ignored if
AutoGenerateMerge is true.</td>
</tr>
<tr class="odd">
<td>Pagination</td>
<td>Dropdown</td>
<td>This will toggle whether the notebook will attempt to execute
pagination on the request using the chosen key (found in the
SystemJson). This is an experimental feature and may not work on every
use case, please refer to the RestAPINotebook for several examples of
pagination and cater towards your API’s by using a custom
RestAPINotebook in the case it does not work for your REST source. More
information regarding how to use this feature can be found in the Task
Types section</td>
</tr>
<tr class="even">
<td>PostCopySQL</td>
<td>SQL</td>
<td>A custom SQL statement to be run AFTER the copy of the table has
been completed.</td>
</tr>
<tr class="odd">
<td>PreCopySQL</td>
<td>SQL</td>
<td>A custom SQL statement to be run BEFORE the copy of the table has
been completed.</td>
</tr>
<tr class="even">
<td>Purview</td>
<td>Dropdown</td>
<td>Whether the user wishes to write the pipeline execution to the
Purview account registered with the selected Execution Engine (which is
done in the next step). This must be a Synapse Workspace based Execution
Engine.</td>
</tr>
<tr class="odd">
<td>QualifiedIDAssociation</td>
<td>Dropdown</td>
<td>Allows the user to decide which identifier to use for the Purview
unique ID (when creating the objects for Purview Lineage) of the
pipeline when writing to the Purview API.</td>
</tr>
<tr class="even">
<td>QueryTimeout</td>
<td>HH:MM:SS</td>
<td>The timeout limit for the relevant SQL query, this is done in the
hh:MM:ss format.</td>
</tr>
<tr class="odd">
<td>Recursively</td>
<td>Dropdown</td>
<td>Whether you wish to target any subfolders found within the directory
provided. This is useful if the file is split into parts or subfolders
depending on something such as dates.</td>
</tr>
<tr class="even">
<td>RelativePath</td>
<td>Text</td>
<td><p>The full relative path of the file.  Pattern match characters can
be used.</p>
<p> </p></td>
</tr>
<tr class="odd">
<td>RelativeUrl</td>
<td>Text</td>
<td>The Relative URL for the REST API being referenced.</td>
</tr>
<tr class="even">
<td>RequestBody</td>
<td>JSON</td>
<td>The request body of a REST API request, this will be blank for a GET
request. The response of the request will be stored in the target
system.</td>
</tr>
<tr class="odd">
<td>RequestMethod</td>
<td>Text</td>
<td>The Request method to be used with the REST API call.</td>
</tr>
<tr class="even">
<td>SchemaFileName</td>
<td>Text</td>
<td>The name of the Schema file to be used when generating the table. If
one is not provided, one will be generated. It is expected for the
schema to be within the same relative path as the DataFileName.</td>
</tr>
<tr class="odd">
<td>SheetName</td>
<td>Text</td>
<td>The name of the targeted excel sheet.</td>
</tr>
<tr class="even">
<td>SkipLineCount</td>
<td>Text</td>
<td>Number of rows (if any) to skip or ignore.</td>
</tr>
<tr class="odd">
<td>SparkTableCreate</td>
<td>Dropdown</td>
<td>Whether the user wishes to additionally write the source data to a
Spark Table upon completion.</td>
</tr>
<tr class="even">
<td>SparkTableDBName</td>
<td>Text</td>
<td>The name of the database for the spark table being created.</td>
</tr>
<tr class="odd">
<td>SparkTableName</td>
<td>Text</td>
<td>The name of the spark table to write the data to.</td>
</tr>
<tr class="even">
<td>SQLPoolName</td>
<td>Text</td>
<td>The name of the SQL Dedicated Pool to have the corresponding action
taken against</td>
</tr>
<tr class="odd">
<td>SQLPoolOperation</td>
<td>Dropdown</td>
<td>Whether the user wishes to start or pause the specified SQL
Dedicated Pool.</td>
</tr>
<tr class="even">
<td>SQLStatement</td>
<td>SQL</td>
<td>SQL statement to execute for the task.</td>
</tr>
<tr class="odd">
<td>StagingTableName</td>
<td>Text</td>
<td>The table name of the transient table which is used before being
merged into the final table.</td>
</tr>
<tr class="even">
<td>TableName</td>
<td>Text</td>
<td>The table name of the final table for the data to be merged
into.</td>
</tr>
<tr class="odd">
<td>TableSchema</td>
<td>Text</td>
<td>The schema name of the final table for the data to be merged
into.</td>
</tr>
<tr class="even">
<td>TriggerUsingAzureStorageCache</td>
<td>Checkbox</td>
<td>Whether you wish to use the storage cache instead of polling the
storage account.</td>
</tr>
<tr class="odd">
<td>UseNotebookActivity</td>
<td>Dropdown</td>
<td>Whether the user wishes to use a notebook pipeline activity to
execute the notebook or not. If disabled, it will use an azure function
to call it.</td>
</tr>
</tbody>
</table>
