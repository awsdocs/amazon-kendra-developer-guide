--------

--------

# BatchPutDocumentResponseFailedDocument<a name="API_BatchPutDocumentResponseFailedDocument"></a>

Provides information about a document that could not be indexed\.

## Contents<a name="API_BatchPutDocumentResponseFailedDocument_Contents"></a>

<<<<<<< HEAD
 ** ErrorCode **   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-ErrorCode"></a>
=======
 **ErrorCode**   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-ErrorCode"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The type of error that caused the document to fail to be indexed\.  
Type: String  
Valid Values:` InternalError | InvalidRequest`   
Required: No

<<<<<<< HEAD
 ** ErrorMessage **   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-ErrorMessage"></a>
=======
 **ErrorMessage**   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-ErrorMessage"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A description of the reason why the document could not be indexed\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** Id **   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-Id"></a>
=======
 **Id**   <a name="Kendra-Type-BatchPutDocumentResponseFailedDocument-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_BatchPutDocumentResponseFailedDocument_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BatchPutDocumentResponseFailedDocument) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BatchPutDocumentResponseFailedDocument) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BatchPutDocumentResponseFailedDocument) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BatchPutDocumentResponseFailedDocument) 