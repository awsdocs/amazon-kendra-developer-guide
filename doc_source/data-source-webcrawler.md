--------

--------

# Web crawler<a name="data-source-webcrawler"></a>

You can use Amazon Kendra Web Crawler to crawl and index webpages\. 

You can only crawl public facing websites and websites that use the secure communication protocol Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive an error when crawling a website, it could be that the website is blocked from crawling\. To crawl internal websites, you can set up a web proxy\. The web proxy must be public facing\.

*When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\. To learn how to stop Amazon Kendra Web Crawler from indexing your website\(s\), please see [Stopping Amazon Kendra Web Crawler from indexing your website](https://docs.aws.amazon.com/kendra/latest/dg/stop-web-crawler.html)\.*

You can connect Amazon Kendra to your Web crawler data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [WebCrawlerConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/WebCrawlerConfiguration.html) API\.

For troubleshooting your Amazon Kendra Web crawler data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-webcrawler)
+ [Prerequisites](#prerequisites-webcrawler)
+ [Connection instructions](#data-source-procedure-webcrawler)
+ [Learn more](#webcrawler-learn-more)
+ [Stopping Amazon Kendra Web Crawler from indexing your website](stop-web-crawler.md)

## Supported features<a name="supported-features-webcrawler"></a>

Amazon Kendra Web crawler data source connector supports the following features:
+ Web proxy
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-webcrawler"></a>

Before you can use Amazon Kendra to index your Web crawler data source, make these changes in your Web crawler and AWS accounts\.

**In your Web crawler data source, make sure you have:**
+ Copied the seed or sitemap URLs of the website you want to index\.
+ **For websites that require basic authentication to crawl**: Copied the host name of the website and the port number\.
+ **Optional:** Copied the host name of the website and the port number if you want to use a web proxy to connect to internal websites you want to crawl\. The web proxy must be public facing\. Amazon Kendra supports connecting to web proxy servers that are backed by basic authentication or you can connect with no authentication\.

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.

## Connection instructions<a name="data-source-procedure-webcrawler"></a>

To connect Amazon Kendra to your Web crawler data source you must provide details of your Web crawler credentials so that Amazon Kendra can access your data\. If you have not yet configured Web crawler for Amazon Kendra see [Prerequisites](#prerequisites-webcrawler)\.

### <a name="webcrawler-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Web crawler** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Web crawler**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. For **Source**, choose between **Source URLs** and **Source sitemaps** depending on your use case and enter the values for each\.
**Note**  
You can add up to 10 source URLs and 3 sitemaps\.  
If you want to crawl a sitemap, it is important to check if the base or root URL is the same base URL used for the URLs listed on your sitemap page\. For example, if your sitemap URL is *https://example\.com/sitemap\-page\.html*, the URLs listed on this sitemap page should also use the base URL "https://example\.com/"\.

   1. \(Optional\) For **Web proxy**— enter the following information:

      1. **Host name**—The host name where web proxy is required\.

      1. **Port number**—The port used by the host URL transport protocol\. The port number should be a numeric value between 0 and 65535\.

      1. For **Web proxy credentials**—Choose an existing secret or create a new secret to store your web crawler authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. 

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-WebCrawler\-’ is automatically added to your secret name\.

         1. For **User name** and **Password**—Enter the authentication credential values you generated and downloaded from your Web crawler account\. 

         1. Choose **Save**\.

   1. \(Optional\) **Hosts with authentication**—Select to add additional hosts with authentication\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Crawl range**—Choose the kind of web pages you want to crawl\.

   1. **Crawl depth**—Select number of levels from the seed URL that Amazon Kendra should crawl\.

   1. **Advanced crawl settings** and **Additional configuration**enter the following information:

      1. **Maximum file size**—The maximum web page or attachment size to crawl\. Minimum 0\.000001 MB \(1 byte\)\. Maximum 50 MB\.

      1. **Maximum links per page**—The maximum number of links crawled per page\. Links are crawled in order of appearance\. Minimum 1 link/page\. Maximum 1000 links/page\.

      1. **Maximum throttling**—The maximum number of URLs crawled per host name per minute\. Minimum 1 URLs/host name/minute\. Maximum 300 URLs/host name/minute\.

      1. **Regex patterns**—Add a pattern to include only certain URLs, or to exclude URLs, file types or specific files in your repository\. You can have a combined total of 100 patterns\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Web crawler**

You must specify the following the [WebCrawlerConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/Web crawlerConfiguration.html) API:
+ **Urls**—Specify the seed or starting point URLs of the websites or the sitemap URLs of the websites you want to crawl using [SeedUrlConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SeedUrlConfiguration.html) and [SiteMapsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SiteMapsConfiguration.html)\.

  If you want to crawl a sitemap, it is important to check if the base or root URL is the same base URL used for the URLs listed on your sitemap page\. For example, if your sitemap URL is *https://example\.com/sitemap\-page\.html*, the URLs listed on this sitemap page should also use the base URL "https://example\.com/"\.
+ **Secret Amazon Resource Name \(ARN\)**—If a website requires basic authentication, you provide the host name, port number and a secret that stores your basic authentication credentials of your user name and password\.You provide the ARN using the [AuthenticationConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AuthenticationConfiguration.html) API\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```

  You can provide web proxy credentials using a secret in AWS Secrets Manager secret\. You use the [ProxyConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ProxyConfiguration.html) API to provide the website host name and port number, and optionally the secret that stores your web proxy credentials\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

You can also add the following optional features:
+ The 'depth' or number of levels in a website from the seed level to crawl\. For example, if a website has 3 levels—index level \(the seed level in this example\), sections level, and subsections level—and you are only interested in crawling information from the index level to the sections level \(levels 0 to 1\), you can set your depth to 1\.
+ The maximum number of URLs on a single webpage to crawl\.
+ The maximum size in MB of a webpage to crawl\.
+ The maximum number of URLs crawled per website host per minute\.
+ The web proxy information to connect to and crawl internal websites\.
+ The authentication information to access and crawl websites that require user authentication\.
+ You can extract HTML meta tags as fields using the *Custom Document Enrichment* tool\. For more information, see [Customizing document metadata during the ingestion process](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\. For an example of extracting HTML meta tags, see [CDE examples](https://github.com/aws-samples/amazon-kendra-cde-examples)\.
+  **Inclusion and exclusion filters**—Specify whether to include certain URLs\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.

------

## Learn more<a name="webcrawler-learn-more"></a>

To learn more about integrating Amazon Kendra with your Web crawler data source, see:
+ [Reimagine knowledge discovery using Amazon Kendra’s Web Crawler](https://aws.amazon.com/blogs/machine-learning/reimagine-knowledge-discovery-using-amazon-kendras-web-crawler/)