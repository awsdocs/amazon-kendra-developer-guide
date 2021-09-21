--------

--------

# BatchGetDocumentStatus<a name="API_BatchGetDocumentStatus"></a>

Returns the indexing status for one or more documents submitted with the [ BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) operation\.

When you use the `BatchPutDocument` operation, documents are indexed asynchronously\. You can use the `BatchGetDocumentStatus` operation to get the current status of a list of documents so that you can determine if they have been successfully indexed\.

You can also use the `BatchGetDocumentStatus` operation to check the status of the [ BatchDeleteDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchDeleteDocument.html) operation\. When a document is deleted from the index, Amazon Kendra returns `NOT_FOUND` as the status\.

## Request Syntax<a name="API_BatchGetDocumentStatus_RequestSyntax"></a>

```
{
   "DocumentInfoList": [ 
      { 
         "Attributes": [ 
            { 
               "Key": "string",
               "Value": { 
                  "DateValue": number,
                  "LongValue": number,
                  "StringListValue": [ "string" ],
                  "StringValue": "string"
               }
            }
         ],
         "DocumentId": "string"
      }
   ],
   "IndexId": "string"
}
```

## Request Parameters<a name="API_BatchGetDocumentStatus_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ DocumentInfoList ](#API_BatchGetDocumentStatus_RequestSyntax) **   <a name="Kendra-BatchGetDocumentStatus-request-DocumentInfoList"></a>
A list of `DocumentInfo` objects that identify the documents for which to get the status\. You identify the documents by their document ID and optional attributes\.  
Type: Array of [ DocumentInfo ](API_DocumentInfo.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 10 items\.  
Required: Yes

 ** [ IndexId ](#API_BatchGetDocumentStatus_RequestSyntax) **   <a name="Kendra-BatchGetDocumentStatus-request-IndexId"></a>
=======
 ** [DocumentInfoList](#API_BatchGetDocumentStatus_RequestSyntax) **   <a name="Kendra-BatchGetDocumentStatus-request-DocumentInfoList"></a>
A list of `DocumentInfo` objects that identify the documents for which to get the status\. You identify the documents by their document ID and optional attributes\.  
Type: Array of [DocumentInfo](API_DocumentInfo.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 10 items\.  
Required: Yes

 ** [IndexId](#API_BatchGetDocumentStatus_RequestSyntax) **   <a name="Kendra-BatchGetDocumentStatus-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index to add documents to\. The index ID is returned by the [ CreateIndex ](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateIndex.html) operation\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_BatchGetDocumentStatus_ResponseSyntax"></a>

```
{
   "DocumentStatusList": [ 
      { 
         "DocumentId": "string",
         "DocumentStatus": "string",
         "FailureCode": "string",
         "FailureReason": "string"
      }
   ],
   "Errors": [ 
      { 
         "DocumentId": "string",
         "ErrorCode": "string",
         "ErrorMessage": "string"
      }
   ]
}
```

## Response Elements<a name="API_BatchGetDocumentStatus_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ DocumentStatusList ](#API_BatchGetDocumentStatus_ResponseSyntax) **   <a name="Kendra-BatchGetDocumentStatus-response-DocumentStatusList"></a>
The status of documents\. The status indicates if the document is waiting to be indexed, is in the process of indexing, has completed indexing, or failed indexing\. If a document failed indexing, the status provides the reason why\.  
Type: Array of [ Status ](API_Status.md) objects

 ** [ Errors ](#API_BatchGetDocumentStatus_ResponseSyntax) **   <a name="Kendra-BatchGetDocumentStatus-response-Errors"></a>
A list of documents that Amazon Kendra couldn't get the status for\. The list includes the ID of the document and the reason that the status couldn't be found\.  
Type: Array of [ BatchGetDocumentStatusResponseError ](API_BatchGetDocumentStatusResponseError.md) objects
=======
 ** [DocumentStatusList](#API_BatchGetDocumentStatus_ResponseSyntax) **   <a name="Kendra-BatchGetDocumentStatus-response-DocumentStatusList"></a>
The status of documents\. The status indicates if the document is waiting to be indexed, is in the process of indexing, has completed indexing, or failed indexing\. If a document failed indexing, the status provides the reason why\.  
Type: Array of [Status](API_Status.md) objects

 ** [Errors](#API_BatchGetDocumentStatus_ResponseSyntax) **   <a name="Kendra-BatchGetDocumentStatus-response-Errors"></a>
A list of documents that Amazon Kendra couldn't get the status for\. The list includes the ID of the document and the reason that the status couldn't be found\.  
Type: Array of [BatchGetDocumentStatusResponseError](API_BatchGetDocumentStatusResponseError.md) objects
>>>>>>> parent of 2b1c178 (updating tutorial)

## Errors<a name="API_BatchGetDocumentStatus_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

<<<<<<< HEAD
 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** ConflictException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
=======
 **AccessDeniedException**   
  
HTTP Status Code: 400

 **ConflictException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_BatchGetDocumentStatus_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/BatchGetDocumentStatus) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BatchGetDocumentStatus) 