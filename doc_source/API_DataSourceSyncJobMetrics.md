--------

--------

# DataSourceSyncJobMetrics<a name="API_DataSourceSyncJobMetrics"></a>

Maps a batch delete document request to a specific data source sync job\. This is optional and should only be supplied when documents are deleted by a data source connector\.

## Contents<a name="API_DataSourceSyncJobMetrics_Contents"></a>

<<<<<<< HEAD
 ** DocumentsAdded **   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsAdded"></a>
=======
 **DocumentsAdded**   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsAdded"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The number of documents added from the data source up to now in the data source sync\.  
Type: String  
Pattern: `(([1-9][0-9]*)|0)`   
Required: No

<<<<<<< HEAD
 ** DocumentsDeleted **   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsDeleted"></a>
=======
 **DocumentsDeleted**   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsDeleted"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The number of documents deleted from the data source up to now in the data source sync run\.  
Type: String  
Pattern: `(([1-9][0-9]*)|0)`   
Required: No

<<<<<<< HEAD
 ** DocumentsFailed **   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsFailed"></a>
=======
 **DocumentsFailed**   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsFailed"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The number of documents that failed to sync from the data source up to now in the data source sync run\.  
Type: String  
Pattern: `(([1-9][0-9]*)|0)`   
Required: No

<<<<<<< HEAD
 ** DocumentsModified **   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsModified"></a>
=======
 **DocumentsModified**   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsModified"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The number of documents modified in the data source up to now in the data source sync run\.  
Type: String  
Pattern: `(([1-9][0-9]*)|0)`   
Required: No

<<<<<<< HEAD
 ** DocumentsScanned **   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsScanned"></a>
=======
 **DocumentsScanned**   <a name="Kendra-Type-DataSourceSyncJobMetrics-DocumentsScanned"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The current number of documents crawled by the current sync job in the data source\.  
Type: String  
Pattern: `(([1-9][0-9]*)|0)`   
Required: No

## See Also<a name="API_DataSourceSyncJobMetrics_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DataSourceSyncJobMetrics) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DataSourceSyncJobMetrics) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DataSourceSyncJobMetrics) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DataSourceSyncJobMetrics) 