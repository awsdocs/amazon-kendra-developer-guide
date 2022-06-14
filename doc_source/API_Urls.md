--------

--------

# Urls<a name="API_Urls"></a>

Provides the configuration information of the URLs to crawl\.

You can only crawl websites that use the secure communication protocol, Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive an error when crawling a website, it could be that the website is blocked from crawling\.

 *When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\.* 

## Contents<a name="API_Urls_Contents"></a>

 ** SeedUrlConfiguration **   <a name="Kendra-Type-Urls-SeedUrlConfiguration"></a>
Configuration of the seed or starting point URLs of the websites you want to crawl\.  
You can choose to crawl only the website host names, or the website host names with subdomains, or the website host names with subdomains and other domains that the webpages link to\.  
You can list up to 100 seed URLs\.  
Type: [SeedUrlConfiguration](API_SeedUrlConfiguration.md) object  
Required: No

 ** SiteMapsConfiguration **   <a name="Kendra-Type-Urls-SiteMapsConfiguration"></a>
Configuration of the sitemap URLs of the websites you want to crawl\.  
Only URLs belonging to the same website host names are crawled\. You can list up to three sitemap URLs\.  
Type: [SiteMapsConfiguration](API_SiteMapsConfiguration.md) object  
Required: No

## See Also<a name="API_Urls_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Urls) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Urls) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Urls) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Urls) 