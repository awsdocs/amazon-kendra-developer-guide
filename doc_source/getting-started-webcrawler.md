--------

--------

# Getting started with Amazon Kendra Web Crawler \(console\)<a name="getting-started-webcrawler"></a>

You can use the Amazon Kendra console to get started using the Amazon Kendra *Web Crawler*\. When you use the console, you specify the connection information you need to index the contents of the webpages crawled using the web crawler\. For more information, see [Using a web crawler data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-web-crawler.html)\.

If you want to use a web proxy server to connect to and crawl websites, you need to provide the website host name and port number\. Web proxy credentials \(stored in a secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\) are optional and you can use them to connect to a web proxy server that requires basic authentication\.

If you want to use basic authentication of user name and password to access and crawl websites, you need to provide the website host name, port number, and your secret in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) that stores your authentication credentials\.

The following procedure assumes that you created an index following step 1 of [Getting started with an S3 bucket \(Console\)](https://docs.aws.amazon.com/kendra/latest/dg/gs-console.html)\.

**To create Amazon Kendra Web Crawler as a data source connector \(console\)**

1. Sign into the AWS Management Console and then open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add the data source to\.

1. Choose **Add data sources**\.

1. From the list of data source connectors, choose **WebCrawler**\.

1. On the **Specify data source details** page, do the following:

   1. In the **Name data source** section, give your data source a name and optionally a description\. 

   1. \(Optional\) In the **Tags** section, add tags to categorize your data source\. 

   1. Choose **Next**\.

1. On the **Define access and security page**, do the following:

   1. In the **Source** section, do one of the following:
      + Choose **Source URLs** to enter the seed URLs of the website domains you want to crawl\. Enter the seed or starting point URL, and then choose **Add new URL**\. You can also add website subdomains\. You can add up to ten seed URLs\.
      + Choose **Source Sitemaps** to enter the website sitemap URLs you want to crawl\. A sitemap includes all relevant webpages or website domains you want to crawl\. Enter the sitemap URL, and then choose **Add new URL**\. You can add up to three sitemap URLs\. 
**Note**  
You can only crawl websites that use the secure communication protocol, Hypertext Transfer Protocol Secure \(HTTPS\)\. If you receive a validation exception error when trying to crawl a website, it could be due the website being blocked from crawling\.

   1. \(Optional\) In the **Web proxy** section, do the following:

      1. In **Host name** and **Port number**, enter the website host name and port number\. For example, the host name of https://a\.example\.com/page1\.html is "a\.example\.com" and the port is 443, the standard port for HTTPS\. 

      1. Under **Web proxy credentials**, to use web proxy credentials to connect to a web proxy server that requires basic authentication, choose AWS Secrets Manager secret\. For more information, see [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)

   1. \(Optional\) In the **Hosts with authentication** section, to connect to websites that require user authentication, choose **Add additional host with authentication**\.

   1. In the **IAM role** section, in **IAM role**, choose an existing role that grants Amazon Kendra permission to access the web crawler resources such as your index\. For more information about the required permissions, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\. 

   1. Choose **Next**\.

1. On the **Configure sync settings** page, do the following:

   1. If you selected **Source URLs** in step 6a, in **Crawl range**, do one of the following:
      + Keep **Crawl host domains only**\.
      + 
      + To include subdomains and other domains the webpages link to, choose **Crawl everything**\.

   1. In **Crawl depth**, set the depth to the number of levels in a website from the seed level that you want to crawl\. For example, if a website has three levels – index level or seed level in this example, sections level, and subsections level – and you are only interested in crawling information up to the sections level \(levels 0 to 1\), set your depth to **1**\.

   1. Choose **Advanced crawl settings** to set the maximum size \(in MB\) of a webpage to crawl, the maximum number of URLs on a single webpage to also crawl, and the maximum number of URLs crawled per website host per minute\.

   1. Choose **Additional configuration** to use regular expression patterns to include or exclude certain URLs to crawl\.

   1. In the ** Sync schedule** section, for **Frequency**, choose the frequency to sync your index with the web crawler data source\. You can sync hourly, daily, weekly, monthly, run on demand, or you can choose your own custom sync schedule\.

   1. Choose **Next**\.

1. On the **Review and Create** page, review the details of your web crawler data source\. To make changes, choose the **Edit** button next to the item that you want to change\. When you are done, choose **Add data source** to add the web crawler data source\.

After you choose **Add data source**, Amazon Kendra starts web crawling\. It can take several minutes to a few hours for the web crawling to complete, depending on the number and size of the webpages to crawl\. When it is finished, the status changes from **Creating** to **Active**\.

Amazon Kendra syncs the index with the web crawler in accordance with the sync schedule you set\. If you choose **Sync now** to start the sync process immediately, it can take several minutes to a few hours to synchronize, depending on the number and size of the documents\.

*When selecting websites to index, you must adhere to the [Amazon Acceptable Use Policy](https://aws.amazon.com/aup/) and all other Amazon terms\. Remember that you must only use Amazon Kendra Web Crawler to index your own webpages, or webpages that you have authorization to index\. To learn how to stop Amazon Kendra Web Crawler from indexing your website\(s\), please see [Stopping Amazon Kendra Web Crawler from indexing your website](https://docs.aws.amazon.com/kendra/latest/dg/stop-web-crawler.html)\.*