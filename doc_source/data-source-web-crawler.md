--------

--------

# Using a web crawler data source<a name="data-source-web-crawler"></a>

You can use Amazon Kendra *Web Crawler* to crawl and index webpages\. To use Web Crawler in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Web Crawler\.

For troubleshooting your Amazon Kendra web crawler data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create your data source using the web crawler\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

When you use the web crawler to crawl webpages and index them as your documents, you specify the websites you want to crawl and index\. You provide either the seed or starting point URLs or the sitemap URLs\. You can only crawl websites that use the secure communication protocol, Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive an error when crawling a website, it could be that the website is blocked from crawling\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role with the required permissions\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for web crawler data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

To use the web crawler, you specify the configuration and other information in the console or by using the [WebCrawlerConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WebCrawlerConfiguration.html) object\. You provide the seed or sitemap URLs of the website or websites you want to index\.

You use the [SeedUrlConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SeedUrlConfiguration.html) object to provide a list of seed URLs and choose whether to crawl only website host names, or include subdomains, or include subdomains and other domains the webpages link to\. You use the [SiteMapsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SiteMapsConfiguration.html) object to provide a list of sitemap URLs\.

You also can add the following optional information:
+ The 'depth' or number of levels in a website from the seed level to crawl\. For example, if a website has 3 levels—index level \(the seed level in this example\), sections level, and subsections level—and you are only interested in crawling information from the index level to the sections level \(levels 0 to 1\), you can set your depth to 1\.
+ The maximum number of URLs on a single webpage to crawl\.
+ The maximum size in MB of a webpage to crawl\.
+ The maximum number of URLs crawled per website host per minute\.
+ Regular expression patterns to include or exclude certain URLs to crawl\.
+ The web proxy information to connect to and crawl internal websites\.
+ The authentication information to access and crawl websites that require user authentication\.

You can extract HTML meta tags as fields using the *Custom Document Enrichment* tool\. For more information, see [Customizing document metadata during the ingestion process](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\. For an example of extracting HTML meta tags, see [CDE examples](https://github.com/aws-samples/amazon-kendra-cde-examples)\.

*When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\. To learn how to stop Amazon Kendra Web Crawler from indexing your website\(s\), please see [Stopping Amazon Kendra Web Crawler from indexing your website](https://docs.aws.amazon.com/kendra/latest/dg/stop-web-crawler.html)\.*

## Website authentication<a name="website-user-auth"></a>

Some websites you want to crawl require authentication to access the websites\.

If a website requires basic authentication, you provide the host name of the website, the port number, and a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) that stores your basic authentication credentials of your user name and password\.

If you use the Amazon Kendra console, you can choose an existing secret\. If you use the Amazon Kendra API, you must provide the Amazon Resource Name \(ARN\) of an existing secret that contains your user name and password\. You can create a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.

The secret must contain the user name and password of the website that you want to crawl\.

The following is the minimum JSON structure that must be stored in the secret\.

```
{
    "username": "user name",
    "password": "password"
}
```

You use the [AuthenticationConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AuthenticationConfiguration.html) object to provide the website host name, website port number, and the secret that stores your authentication credentials\.

## Web proxy<a name="web-proxy-web-crawler"></a>

You can use a web proxy to connect to internal websites you want to crawl\. Amazon Kendra supports connecting to web proxy servers that are backed by basic authentication or you can connect with no authentication\. You provide the host name of the website and the port number\.

You can provide web proxy credentials using a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\. You use the [ProxyConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ProxyConfiguration.html) object to provide the website host name and port number, and optionally the secret that stores your web proxy credentials\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.