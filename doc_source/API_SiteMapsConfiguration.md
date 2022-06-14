--------

--------

# SiteMapsConfiguration<a name="API_SiteMapsConfiguration"></a>

Provides the configuration information for the sitemap URLs to crawl\.

 *When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\.* 

## Contents<a name="API_SiteMapsConfiguration_Contents"></a>

 ** SiteMaps **   <a name="Kendra-Type-SiteMapsConfiguration-SiteMaps"></a>
The list of sitemap URLs of the websites you want to crawl\.  
The list can include a maximum of three sitemap URLs\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 3 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?):\/\/([^\s]*)`   
Required: Yes

## See Also<a name="API_SiteMapsConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SiteMapsConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SiteMapsConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SiteMapsConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SiteMapsConfiguration) 