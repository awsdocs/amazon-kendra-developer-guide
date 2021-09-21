--------

--------

# Using a web crawler data source<a name="data-source-web-crawler"></a>

You can use the Amazon Kendra web crawler to crawl and index webpages\. For a walk\-through of how to use the web crawler in the console, see [Getting started with Amazon Kendra web crawler \(Console\)](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-webcrawler.html)\.

You can use the web crawler to crawl webpages and index them as your documents\. For the websites you want to crawl and index, you provide either the seed or starting point URLs or the sitemap URLs\. You can only crawl websites that use the secure communication protocol, Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive an error when crawling a website, it could be that the website is blocked from crawling\.

You can configure the following crawl settings:
+ The range of websites to crawl: website host names only, or websites including subdomains, or websites including subdomains and others domains that the webpages link to\.
+ The *depth* or number of levels in a website from the seed level to crawl\. For example, if a website has 3 levels – index level or the seed level in this example, sections level, and subsections level – and you are only interested in crawling information from the index level to the sections level \(levels 0 to 1\), you can set your depth to 1\.
+ The maximum number of URLs on a single webpage that are crawled\.
+ The maximum size in MB of a webpage to crawl\.
+ The maximum number of URLs crawled per website host per minute\.
+ Regular expression patterns to include or exclude certain URLs to crawl\.
+ The web proxy information to connect to and crawl internal websites\.
+ The authentication information to access and crawl websites that require user authentication\.

You can configure the web crawler using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) operation\. You provide the web crawler configuration information in the [WebCrawlerConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WebCrawlerConfiguration.html) structure\.

You use the [SeedUrlConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SeedUrlConfiguration.html) structure to provide a list of seed URLs and choose whether to crawl only website host names, or include subdomains, or include subdomains and other domains the webpages link to\. You also use the [SiteMapsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SiteMapsConfiguration.html) structure to provide a list of sitemap URLs\.

*When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use the Amazon Kendra web crawler to index your own webpages, or webpages that you have authorization to index\. To learn how to stop the Amazon Kendra web crawler from indexing your website\(s\), please see [Stopping the Amazon Kendra web crawler from indexing your website](https://docs.aws.amazon.com/kendra/latest/dg/stop-web-crawler.html)\.*

## Website user authentication<a name="website-user-auth"></a>

Before connecting to the web crawler, you need to check if the websites you want to crawl require authentication to access the websites\. If a website requires basic authentication, you provide web crawler with the host name of the website, the port number, and a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) that stores your basic authentication credentials of your user name and password\.

If you use the Amazon Kendra console, you can choose an existing secret\. If you use the Amazon Kendra API, you must provide the Amazon Resource Name \(ARN\) of an existing secret that contains your user name and password\. You can create a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.

The secret must contain the user name and password of the website that you want to crawl\. The following is the minimum JSON structure that must be stored in the secret\.

```
{
    "username": "user-name",
    "password": "password"
}
```

The secret can contain other information, but Amazon Kendra ignores it\.

You use the [AuthenticationConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AuthenticationConfiguration.html) structure to provide the website host name, website port number, and the secret that stores your authentication credentials\.

## IAM role for web crawler<a name="iam-role-web-crawler"></a>

When you use the web crawler, you specify an IAM role that grants Amazon Kendra permission to access web crawler resources such as your index and secret\. The secret stores your credentials for websites or web proxy servers that require basic authentication\. The IAM role for the web crawler must have permission to access the secret and to use the AWS Key Management Service \(AWS KMS\) key to decrypt it\. The IAM role also needs access to your index so that it can add and update crawled webpages to the index\. For more information, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.

## Web proxy<a name="web-proxy-web-crawler"></a>

You can use a web proxy to connect to internal websites you want to crawl\. Amazon Kendra supports connecting to web proxy servers that are backed by basic authentication or you can connect with no authentication\. You provide the host name of the website and the port number\. You can also provide web proxy credentials using a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.

You use the [ProxyConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ProxyConfiguration.html) structure to provide the website host name and port number\. You can also provide the secret that stores your web proxy credentials\.