--------

--------

# Status<a name="API_Status"></a>

Provides information about the status of documents submitted for indexing\.

## Contents<a name="API_Status_Contents"></a>

 ** DocumentId **   <a name="Kendra-Type-Status-DocumentId"></a>
The unique identifier of the document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** DocumentStatus **   <a name="Kendra-Type-Status-DocumentStatus"></a>
The current status of a document\.  
If the document was submitted for deletion, the status is `NOT_FOUND` after the document is deleted\.  
Type: String  
Valid Values:` NOT_FOUND | PROCESSING | INDEXED | UPDATED | FAILED | UPDATE_FAILED`   
Required: No

 ** FailureCode **   <a name="Kendra-Type-Status-FailureCode"></a>
Indicates the source of the error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** FailureReason **   <a name="Kendra-Type-Status-FailureReason"></a>
Provides detailed information about why the document couldn't be indexed\. Use this information to correct the error before you resubmit the document for indexing\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_Status_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Status) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Status) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Status) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Status) 