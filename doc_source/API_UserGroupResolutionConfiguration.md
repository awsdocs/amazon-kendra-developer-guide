--------

--------

# UserGroupResolutionConfiguration<a name="API_UserGroupResolutionConfiguration"></a>

Provides the configuration information to fetch access levels of groups and users from an AWS IAM Identity Center \(successor to AWS Single Sign\-On\) identity source\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. You can also use the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API to map users to their groups so that you only need to provide the user ID when you issue the query\.

To set up an IAM Identity Center identity source in the console to use with Amazon Kendra, see [Getting started with an IAM Identity Center identity source](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-aws-sso.html)\. You must also grant the required permissions to use IAM Identity Center with Amazon Kendra\. For more information, see [IAM roles for IAM Identity Center](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-aws-sso)\.

Amazon Kendra currently does not support using `UserGroupResolutionConfiguration` with an AWS organization member account for your IAM Identity Center identify source\. You must create your index in the management account for the organization in order to use `UserGroupResolutionConfiguration`\.

## Contents<a name="API_UserGroupResolutionConfiguration_Contents"></a>

 ** UserGroupResolutionMode **   <a name="Kendra-Type-UserGroupResolutionConfiguration-UserGroupResolutionMode"></a>
The identity store provider \(mode\) you want to use to fetch access levels of groups and users\. AWS IAM Identity Center \(successor to AWS Single Sign\-On\) is currently the only available mode\. Your users and groups must exist in an IAM Identity Center identity source in order to use this mode\.  
Type: String  
Valid Values:` AWS_SSO | NONE`   
Required: Yes

## See Also<a name="API_UserGroupResolutionConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UserGroupResolutionConfiguration) 