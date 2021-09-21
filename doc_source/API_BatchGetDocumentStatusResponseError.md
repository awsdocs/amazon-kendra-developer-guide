--------

--------

# BatchGetDocumentStatusResponseError<a name="API_BatchGetDocumentStatusResponseError"></a>

Provides a response when the status of a document could not be retrieved\.

## Contents<a name="API_BatchGetDocumentStatusResponseError_Contents"></a>

<<<<<<< HEAD
 ** DocumentId **   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-DocumentId"></a>
=======
 **DocumentId**   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-DocumentId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the document whose status could not be retrieved\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

<<<<<<< HEAD
 ** ErrorCode **   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-ErrorCode"></a>
=======
 **ErrorCode**   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-ErrorCode"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Indicates the source of the error\.  
Type: String  
Valid Values:` InternalError | InvalidRequest`   
Required: No

<<<<<<< HEAD
 ** ErrorMessage **   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-ErrorMessage"></a>
=======
 **ErrorMessage**   <a name="Kendra-Type-BatchGetDocumentStatusResponseError-ErrorMessage"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
States that the API could not get the status of a document\. This could be because the request is not valid or there is a system error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

## See Also<a name="API_BatchGetDocumentStatusResponseError_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BatchGetDocumentStatusResponseError) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BatchGetDocumentStatusResponseError) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BatchGetDocumentStatusResponseError) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BatchGetDocumentStatusResponseError) 