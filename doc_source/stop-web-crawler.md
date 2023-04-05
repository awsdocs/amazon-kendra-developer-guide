--------

--------

# Configuring the `robots.txt` file for Amazon Kendra Web Crawler<a name="stop-web-crawler"></a>

Amazon Kendra is an intelligent search service that AWS customers use to index and search documents of their choice\. In order to index documents on the web, customers may use Amazon Kendra Web Crawler, indicating which URL\(s\) should be indexed and other operational parameters\. Amazon Kendra customers are required to obtain authorization before indexing any particular website\.

Amazon Kendra Web Crawler respects standard robots\.txt directives like `Allow` and `Disallow`\. You can modify the `robot.txt` file of your website to control how Amazon Kendra Web Crawler crawls your website\.

## Configuring how Amazon Kendra Web Crawler accesses your website<a name="configure-web-crawler-website-access"></a>

You can control how the Amazon Kendra Web Crawler indexes your website using `Allow` and `Disallow` directives\. You can also control which web pages are indexed and which web pages are not crawled\.

**To allow Amazon Kendra Web Crawler to crawl all web pages except disallowed web pages, use the following directive:**

```
User-agent: amazon-kendra    # Amazon Kendra Web Crawler
Disallow: /credential-pages/ # disallow access to specific pages
```

**To allow Amazon Kendra Web Crawler to crawl only specific web pages, use the following directive:**

```
User-agent: amazon-kendra    # Amazon Kendra Web Crawler
Allow: /pages/ # allow access to specific pages
```

**To allow Amazon Kendra Web Crawler to crawl all website content and disallow crawling for any other robots, use the following directive:**

```
User-agent: amazon-kendra # Amazon Kendra Web Crawler
Allow: / # allow access to all pages
User-agent: * # any (other) robot
Disallow: / # disallow access to any pages
```

## Stopping Amazon Kendra Web Crawler from crawling your website<a name="stop-web-crawler-access"></a>

You can stop Amazon Kendra Web Crawler from indexing your website using the `Disallow` directive\. You can also control which web pages are crawled and which are not\.

**To stop Amazon Kendra Web Crawler from crawling the website, use the following directive:**

```
User-agent: amazon-kendra # Amazon Kendra Web Crawler
Disallow: / # disallow access to any pages
```

Amazon Kendra Web Crawler also supports the robots `noindex` and `nofollow` directives in meta tags in HTML pages\. These directives stop the web crawler from indexing a web page and stops following any links on the web page\. You put the meta tags in the section of the document to specify the rules of robots rules\.

For example, the below web page includes the directives robots `noindex` and `nofollow`:

```
            <html>
            <head>
                <meta name="robots" content="noindex, nofollow"/>
                ...
            </head>
            <body>...</body>
            </html>
```

If you have any questions or concerns regarding Amazon Kendra Web Crawler, you can reach out to the [AWS support team](https://aws.amazon.com/contact-us/?nc1=f_m)\.