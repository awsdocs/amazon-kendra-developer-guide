--------

--------

# BatchDeleteFeaturedResultsSetError<a name="API_BatchDeleteFeaturedResultsSetError"></a>

Provides information about a set of featured results that couldn't be removed from an index by the [BatchDeleteFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchDeleteFeaturedResultsSet.html) API\.

## Contents<a name="API_BatchDeleteFeaturedResultsSetError_Contents"></a>

 ** ErrorCode **   <a name="Kendra-Type-BatchDeleteFeaturedResultsSetError-ErrorCode"></a>
The error code for why the set of featured results couldn't be removed from the index\.  
Type: String  
Valid Values:` InternalError | InvalidRequest`   
Required: Yes

 ** ErrorMessage **   <a name="Kendra-Type-BatchDeleteFeaturedResultsSetError-ErrorMessage"></a>
An explanation for why the set of featured results couldn't be removed from the index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: Yes

 ** Id **   <a name="Kendra-Type-BatchDeleteFeaturedResultsSetError-Id"></a>
The identifier of the set of featured results that couldn't be removed from the index\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*`   
Required: Yes

## See Also<a name="API_BatchDeleteFeaturedResultsSetError_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BatchDeleteFeaturedResultsSetError) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BatchDeleteFeaturedResultsSetError) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BatchDeleteFeaturedResultsSetError) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BatchDeleteFeaturedResultsSetError) 