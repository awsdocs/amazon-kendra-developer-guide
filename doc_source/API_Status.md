--------

--------

# Status<a name="API_Status"></a>

Provides information about the status of documents submitted for indexing\.

## Contents<a name="API_Status_Contents"></a>

<<<<<<< HEAD
 ** DocumentId **   <a name="Kendra-Type-Status-DocumentId"></a>
=======
 **DocumentId**   <a name="Kendra-Type-Status-DocumentId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

<<<<<<< HEAD
 ** DocumentStatus **   <a name="Kendra-Type-Status-DocumentStatus"></a>
=======
 **DocumentStatus**   <a name="Kendra-Type-Status-DocumentStatus"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The current status of a document\.  
If the document was submitted for deletion, the status is `NOT_FOUND` after the document is deleted\.  
Type: String  
Valid Values:` NOT_FOUND | PROCESSING | INDEXED | UPDATED | FAILED | UPDATE_FAILED`   
Required: No

<<<<<<< HEAD
 ** FailureCode **   <a name="Kendra-Type-Status-FailureCode"></a>
=======
 **FailureCode**   <a name="Kendra-Type-Status-FailureCode"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Indicates the source of the error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

<<<<<<< HEAD
 ** FailureReason **   <a name="Kendra-Type-Status-FailureReason"></a>
=======
 **FailureReason**   <a name="Kendra-Type-Status-FailureReason"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Provides detailed information about why the document couldn't be indexed\. Use this information to correct the error before you resubmit the document for indexing\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_Status_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Status) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Status) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Status) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Status) 