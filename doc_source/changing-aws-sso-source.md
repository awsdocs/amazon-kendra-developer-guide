--------

--------

# Changing your IAM Identity Center identity source<a name="changing-aws-sso-source"></a>

**Warning**  
Changing your identity source in IAM Identity Center **Settings** might affect the preservation of user and group information\. To do this safely, it is recommended you review [Considerations for changing your identity source](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-considerations.html)\. When you change your identity source, a new identity source ID is generated\. Check you are using the correct ID before you set the mode to `AWS_SSO` in [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html)\.

**To change your IAM Identity Centeridentity source**

1. Open the [IAM Identity Center> console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, under **Identity source**, choose **Change**\.

1. On the **Change identity source** page, select your preferred identity source, and then choose **Next**\.