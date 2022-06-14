--------

--------

# How Amazon Kendra works<a name="how-it-works"></a>

Amazon Kendra provides the functionality to your search application\. It indexes your documents directly or from your third\-party document repository and intelligently serves relevant information to your users\. You can use Amazon Kendra to create an updatable index of documents of a variety of types, including plain text, HTML files, Microsoft Word documents, Microsoft PowerPoint presentations, and PDF files\.

Amazon Kendra integrates with other services\. For example, you can power [Amazon Lex chat bots](https://docs.aws.amazon.com/lexv2/latest/dg/faq-bot-kendra-search.html) with Amazon Kendra search to provide answers to users' questions\. You can use [Amazon S3 bucket](https://docs.aws.amazon.com/kendra/latest/dg/data-source-s3.html) as a data source for your Amazon Kendra index\. And you can set up [AWS Identity and Access Management](https://docs.aws.amazon.com/kendra/latest/dg/security-iam.html) to control access to Amazon Kendra resources\.

Amazon Kendra has the following components:
+ The *index*, which allows your documents to be searched\. You create the index from a source or repository of documents\.
+ A *source repository*, which contains the documents to index\.
+ A *data source* that syncs the documents in your source repository to an Amazon Kendra index\. You can automatically synchronize a data source with an Amazon Kendra index so that new, updated, and deleted files in the source repository are updated in the index\.
+ A *document addition API*, that adds documents directly to the index\.

You can use Amazon Kendra through the console or the API\. You can create, update, and delete indexes\. Deleting an index deletes all data sources and permanently deletes all of your document information from Amazon Kendra\.

**Topics**
+ [Index](hiw-index.md)
+ [Documents](hiw-documents.md)
+ [Data sources](hiw-data-source.md)
+ [Queries](hiw-query.md)
+ [Tags](tagging.md)