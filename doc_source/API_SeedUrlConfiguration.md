--------

--------

# SeedUrlConfiguration<a name="API_SeedUrlConfiguration"></a>

Provides the configuration information for the seed or starting point URLs to crawl\.

 *When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\.* 

## Contents<a name="API_SeedUrlConfiguration_Contents"></a>

 ** SeedUrls **   <a name="Kendra-Type-SeedUrlConfiguration-SeedUrls"></a>
The list of seed or starting point URLs of the websites you want to crawl\.  
The list can include a maximum of 100 seed URLs\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?):\/\/([^\s]*)`   
Required: Yes

 ** WebCrawlerMode **   <a name="Kendra-Type-SeedUrlConfiguration-WebCrawlerMode"></a>
You can choose one of the following modes:  
+  `HOST_ONLY` – crawl only the website host names\. For example, if the seed URL is "abc\.example\.com", then only URLs with host name "abc\.example\.com" are crawled\.
+  `SUBDOMAINS` – crawl the website host names with subdomains\. For example, if the seed URL is "abc\.example\.com", then "a\.abc\.example\.com" and "b\.abc\.example\.com" are also crawled\.
+  `EVERYTHING` – crawl the website host names with subdomains and other domains that the webpages link to\.
The default mode is set to `HOST_ONLY`\.  
Type: String  
Valid Values:` HOST_ONLY | SUBDOMAINS | EVERYTHING`   
Required: No

## See Also<a name="API_SeedUrlConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SeedUrlConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SeedUrlConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SeedUrlConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SeedUrlConfiguration) 