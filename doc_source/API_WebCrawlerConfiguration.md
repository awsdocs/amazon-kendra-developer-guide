--------

--------

# WebCrawlerConfiguration<a name="API_WebCrawlerConfiguration"></a>

Provides the configuration information required for Amazon Kendra Web Crawler\.

## Contents<a name="API_WebCrawlerConfiguration_Contents"></a>

 ** AuthenticationConfiguration **   <a name="Kendra-Type-WebCrawlerConfiguration-AuthenticationConfiguration"></a>
Configuration information required to connect to websites using authentication\.  
You can connect to websites using basic authentication of user name and password\. You use a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) to store your authentication credentials\.  
You must provide the website host name and port number\. For example, the host name of https://a\.example\.com/page1\.html is "a\.example\.com" and the port is 443, the standard port for HTTPS\.  
Type: [AuthenticationConfiguration](API_AuthenticationConfiguration.md) object  
Required: No

 ** CrawlDepth **   <a name="Kendra-Type-WebCrawlerConfiguration-CrawlDepth"></a>
Specifies the number of levels in a website that you want to crawl\.  
The first level begins from the website seed or starting point URL\. For example, if a website has three levels—index level \(the seed in this example\), sections level, and subsections level—and you are only interested in crawling information up to the sections level \(levels 0\-1\), you can set your depth to 1\.  
The default crawl depth is set to 2\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 10\.  
Required: No

 ** MaxContentSizePerPageInMegaBytes **   <a name="Kendra-Type-WebCrawlerConfiguration-MaxContentSizePerPageInMegaBytes"></a>
The maximum size \(in MB\) of a web page or attachment to crawl\.  
Files larger than this size \(in MB\) are skipped/not crawled\.  
The default maximum size of a web page or attachment is set to 50 MB\.  
Type: Float  
Valid Range: Minimum value of 1\.0e\-06\. Maximum value of 50\.  
Required: No

 ** MaxLinksPerPage **   <a name="Kendra-Type-WebCrawlerConfiguration-MaxLinksPerPage"></a>
The maximum number of URLs on a web page to include when crawling a website\. This number is per web page\.  
As a website’s web pages are crawled, any URLs the web pages link to are also crawled\. URLs on a web page are crawled in order of appearance\.  
The default maximum links per page is 100\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 1000\.  
Required: No

 ** MaxUrlsPerMinuteCrawlRate **   <a name="Kendra-Type-WebCrawlerConfiguration-MaxUrlsPerMinuteCrawlRate"></a>
The maximum number of URLs crawled per website host per minute\.  
A minimum of one URL is required\.  
The default maximum number of URLs crawled per website host per minute is 300\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 300\.  
Required: No

 ** ProxyConfiguration **   <a name="Kendra-Type-WebCrawlerConfiguration-ProxyConfiguration"></a>
Configuration information required to connect to your internal websites via a web proxy\.  
You must provide the website host name and port number\. For example, the host name of https://a\.example\.com/page1\.html is "a\.example\.com" and the port is 443, the standard port for HTTPS\.  
Web proxy credentials are optional and you can use them to connect to a web proxy server that requires basic authentication\. To store web proxy credentials, you use a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.  
Type: [ProxyConfiguration](API_ProxyConfiguration.md) object  
Required: No

 ** UrlExclusionPatterns **   <a name="Kendra-Type-WebCrawlerConfiguration-UrlExclusionPatterns"></a>
A list of regular expression patterns to exclude certain URLs to crawl\. URLs that match the patterns are excluded from the index\. URLs that don't match the patterns are included in the index\. If a URL matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the URL file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** UrlInclusionPatterns **   <a name="Kendra-Type-WebCrawlerConfiguration-UrlInclusionPatterns"></a>
A list of regular expression patterns to include certain URLs to crawl\. URLs that match the patterns are included in the index\. URLs that don't match the patterns are excluded from the index\. If a URL matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the URL file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** Urls **   <a name="Kendra-Type-WebCrawlerConfiguration-Urls"></a>
Specifies the seed or starting point URLs of the websites or the sitemap URLs of the websites you want to crawl\.  
You can include website subdomains\. You can list up to 100 seed URLs and up to three sitemap URLs\.  
You can only crawl websites that use the secure communication protocol, Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive an error when crawling a website, it could be that the website is blocked from crawling\.  
 *When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own web pages, or web pages that you have authorization to index\.*   
Type: [Urls](API_Urls.md) object  
Required: Yes

## See Also<a name="API_WebCrawlerConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/WebCrawlerConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/WebCrawlerConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/WebCrawlerConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/WebCrawlerConfiguration) 