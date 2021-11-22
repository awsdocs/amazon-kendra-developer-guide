--------

--------

# UserGroupResolutionConfiguration<a name="API_UserGroupResolutionConfiguration"></a>

Provides the configuration information to fetch access levels of groups and users from an AWS Single Sign\-On identity source\. This is useful for setting up user context filtering, where Amazon Kendra filters search results for different users based on their group's access to documents\. You can also map your users to their groups for user context filtering using the [PutPrincipalMapping operation](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)\.

To set up an AWS SSO identity source in the console to use with Amazon Kendra, see [Getting started with an AWS SSO identity source](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-aws-sso.html)\. You must also grant the required permissions to use AWS SSO with Amazon Kendra\. For more information, see [IAM roles for AWS SSO ](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-aws-sso)\.

## Contents<a name="API_UserGroupResolutionConfiguration_Contents"></a>

 ** UserGroupResolutionMode **   <a name="Kendra-Type-UserGroupResolutionConfiguration-UserGroupResolutionMode"></a>
The identity store provider \(mode\) you want to use to fetch access levels of groups and users\. AWS Single Sign\-On is currently the only available mode\. Your users and groups must exist in an AWS SSO identity source in order to use this mode\.  
Type: String  
Valid Values:` AWS_SSO | NONE`   
Required: Yes

## See Also<a name="API_UserGroupResolutionConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UserGroupResolutionConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UserGroupResolutionConfiguration) 