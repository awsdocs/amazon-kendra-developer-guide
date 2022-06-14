--------

--------

# ExperienceConfiguration<a name="API_ExperienceConfiguration"></a>

Provides the configuration information for your Amazon Kendra experience\. This includes the data source IDs and/or FAQ IDs, and user or group information to grant access to your Amazon Kendra experience\.

## Contents<a name="API_ExperienceConfiguration_Contents"></a>

 ** ContentSourceConfiguration **   <a name="Kendra-Type-ExperienceConfiguration-ContentSourceConfiguration"></a>
The identifiers of your data sources and FAQs\. Or, you can specify that you want to use documents indexed via the `BatchPutDocument` API\. This is the content you want to use for your Amazon Kendra experience\.  
Type: [ContentSourceConfiguration](API_ContentSourceConfiguration.md) object  
Required: No

 ** UserIdentityConfiguration **   <a name="Kendra-Type-ExperienceConfiguration-UserIdentityConfiguration"></a>
The AWS SSO field name that contains the identifiers of your users, such as their emails\.  
Type: [UserIdentityConfiguration](API_UserIdentityConfiguration.md) object  
Required: No

## See Also<a name="API_ExperienceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ExperienceConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ExperienceConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ExperienceConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ExperienceConfiguration) 