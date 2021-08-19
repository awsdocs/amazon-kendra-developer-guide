--------

--------

# Stopping Amazon Kendra web crawler from indexing your website<a name="stop-web-crawler"></a>

Amazon Kendra is an intelligent search service that AWS customers may use to index and search documents of their choice\. In order to index documents on the web, customers may use the Amazon Kendra web crawler, indicating which URL\(s\) should be indexed and other operational parameters\. Amazon Kendra customers are required to obtain authorization before indexing any particular website\.

You can stop the Amazon Kendra web crawler from indexing your website using the `Disallow` directive, as shown below\. You can also control which webpages are indexed and which webpages are not crawled\.

The Amazon Kendra web crawler respects standard robots\.txt directives like `Allow` and `Disallow`\. Each Amazon Kendra customer using the web crawler has a unique user agent or customer ID\. You can identify the user agent or customer ID that you would like to control and configure it in the robots\.txt directives\.

For example, the below directives stop an Amazon Kendra customer from being able to index a directory of your webpages under `/do-not-crawl/`, but allow indexing a sub\-directory `/do-not-crawl/except-this/`:

```
User-agent: amazon-kendra-customer-id-[id] # Amazon customer's user agent/ID
Disallow: /do-not-crawl/ # disallow this directory
Allow: /do-not-crawl/except-this/ # allow this subdirectory

User-agent: * # any robot
Disallow: /not-allowed/ # disallow this directory

User-agent: amazon-kendra-web-crawler-* # all customers of Amazon Kendra's web crawler
Disallow: /confidential/ # disallow this directory
```

The Amazon Kendra web crawler also supports the robots `noindex` and `nofollow` directives in meta tags in HTML pages\. These directives stop the web crawler from indexing a webpage and stops following any links on the webpage\. You put the meta tags in the section of the document to specify the rules of robots rules\.

For example, the below webpage includes the directives robots `noindex` and `nofollow`:

```
            <html>
            <head>
                <meta name="robots" content="noindex, nofollow"/>
                ...
            </head>
            <body>...</body>
            </html>
```

If you have any questions or concerns regarding the Amazon Kendra web crawler, you can reach out to the [AWS support team](https://aws.amazon.com/contact-us/?nc1=f_m)\.