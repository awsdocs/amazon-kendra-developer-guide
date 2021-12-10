--------

--------

# UserIdentityConfiguration<a name="API_UserIdentityConfiguration"></a>

Configuration information for the identifiers of your users\.

## Contents<a name="API_UserIdentityConfiguration_Contents"></a>

 ** IdentityAttributeName **   <a name="Kendra-Type-UserIdentityConfiguration-IdentityAttributeName"></a>
The AWS SSO field name that contains the identifiers of your users, such as their emails\. This is used for [user context filtering](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html) and for granting access to your Amazon Kendra experience\. You must set up AWS SSO with Amazon Kendra\. You must include your users and groups in your Access Control List when you ingest documents into your index\. For more information, see [Getting started with an AWS SSO identity source](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-aws-sso.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

## See Also<a name="API_UserIdentityConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UserIdentityConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UserIdentityConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UserIdentityConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UserIdentityConfiguration) 