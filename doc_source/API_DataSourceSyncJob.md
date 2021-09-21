--------

--------

# DataSourceSyncJob<a name="API_DataSourceSyncJob"></a>

Provides information about a synchronization job\.

## Contents<a name="API_DataSourceSyncJob_Contents"></a>

<<<<<<< HEAD
 ** DataSourceErrorCode **   <a name="Kendra-Type-DataSourceSyncJob-DataSourceErrorCode"></a>
=======
 **DataSourceErrorCode**   <a name="Kendra-Type-DataSourceSyncJob-DataSourceErrorCode"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the reason that the synchronization failed is due to an error with the underlying data source, this field contains a code that identifies the error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

<<<<<<< HEAD
 ** EndTime **   <a name="Kendra-Type-DataSourceSyncJob-EndTime"></a>
=======
 **EndTime**   <a name="Kendra-Type-DataSourceSyncJob-EndTime"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The UNIX datetime that the synchronization job was completed\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** ErrorCode **   <a name="Kendra-Type-DataSourceSyncJob-ErrorCode"></a>
=======
 **ErrorCode**   <a name="Kendra-Type-DataSourceSyncJob-ErrorCode"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the `Status` field is set to `FAILED`, the `ErrorCode` field contains a the reason that the synchronization failed\.  
Type: String  
Valid Values:` InternalError | InvalidRequest`   
Required: No

<<<<<<< HEAD
 ** ErrorMessage **   <a name="Kendra-Type-DataSourceSyncJob-ErrorMessage"></a>
=======
 **ErrorMessage**   <a name="Kendra-Type-DataSourceSyncJob-ErrorMessage"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the `Status` field is set to `ERROR`, the `ErrorMessage` field contains a description of the error that caused the synchronization to fail\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** ExecutionId **   <a name="Kendra-Type-DataSourceSyncJob-ExecutionId"></a>
=======
 **ExecutionId**   <a name="Kendra-Type-DataSourceSyncJob-ExecutionId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A unique identifier for the synchronization job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

<<<<<<< HEAD
 ** Metrics **   <a name="Kendra-Type-DataSourceSyncJob-Metrics"></a>
Maps a batch delete document request to a specific data source sync job\. This is optional and should only be supplied when documents are deleted by a data source connector\.  
Type: [ DataSourceSyncJobMetrics ](API_DataSourceSyncJobMetrics.md) object  
Required: No

 ** StartTime **   <a name="Kendra-Type-DataSourceSyncJob-StartTime"></a>
=======
 **Metrics**   <a name="Kendra-Type-DataSourceSyncJob-Metrics"></a>
Maps a batch delete document request to a specific data source sync job\. This is optional and should only be supplied when documents are deleted by a data source connector\.  
Type: [DataSourceSyncJobMetrics](API_DataSourceSyncJobMetrics.md) object  
Required: No

 **StartTime**   <a name="Kendra-Type-DataSourceSyncJob-StartTime"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The UNIX datetime that the synchronization job was started\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** Status **   <a name="Kendra-Type-DataSourceSyncJob-Status"></a>
=======
 **Status**   <a name="Kendra-Type-DataSourceSyncJob-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The execution status of the synchronization job\. When the `Status` field is set to `SUCCEEDED`, the synchronization job is done\. If the status code is set to `FAILED`, the `ErrorCode` and `ErrorMessage` fields give you the reason for the failure\.  
Type: String  
Valid Values:` FAILED | SUCCEEDED | SYNCING | INCOMPLETE | STOPPING | ABORTED | SYNCING_INDEXING`   
Required: No

## See Also<a name="API_DataSourceSyncJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DataSourceSyncJob) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DataSourceSyncJob) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DataSourceSyncJob) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DataSourceSyncJob) 