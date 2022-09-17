--------

--------

# FailedEntity<a name="API_FailedEntity"></a>

Information on the users or groups in your IAM Identity Center identity source that failed to properly configure with your Amazon Kendra experience\.

## Contents<a name="API_FailedEntity_Contents"></a>

 ** EntityId **   <a name="Kendra-Type-FailedEntity-EntityId"></a>
The identifier of the user or group in your IAM Identity Center identity source\. For example, a user ID could be an email\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: No

 ** ErrorMessage **   <a name="Kendra-Type-FailedEntity-ErrorMessage"></a>
The reason the user or group in your IAM Identity Center identity source failed to properly configure with your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

## See Also<a name="API_FailedEntity_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FailedEntity) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FailedEntity) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FailedEntity) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FailedEntity) 