--------

--------

# Index<a name="hiw-index"></a>

An index holds the contents of your documents and is structured in a way to make the documents searchable\. The way you add documents to the index depends on how you store your documents\.
+ If you store your documents in some kind of repository, such as an Amazon S3 bucket or a Microsoft SharePoint site, you use a [data source connector](https://docs.aws.amazon.com/kendra/latest/dg/data-source.html) to index your documents from your repository\.
+ If you don't store your documents in a repository, you use the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API to directly index your documents\. 
+ For FAQ questions and answers, which must be stored in an Amazon Kendra \(Amazon S3\) bucket, you upload them from the bucket

You can create indexes with the Amazon Kendra console, the AWS CLI, or an AWS SDK\. For information about the types of documents that can be indexed, see [Types of documents](index-document-types.md)\.

## Using Amazon Kendra built\-in document fields<a name="index-reserved-fields"></a>

Amazon Kendra has the following reserved or built\-in document fields that you can use:
+ `_authors`—A list of one or more authors responsible for the content of the document\.
+ `_category`—A category that places a document in a specific group\.
+ `_created_at`—The date and time in ISO 8601 format that the document was created\. For example, 2012\-03\-25T12:30:10\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_data_source_id`—The identifier of the data source that contains the document\.
+ `_document_body`—The content of the document\.
+ `_document_id`—A unique identifier for the document\.
+ `_document_title`—The title of the document\.
+ `_excerpt_page_number`—The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_faq_id`—If this is an FAQ question and answer, a unique identifier for them\.
+ `_file_type`—The file type of the document, such as pdf or doc\.
+ `_last_updated_at`—The date and time in ISO 8601 format that the document was last updated\. For example, 2012\-03\-25T12:30:10\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_source_uri`—The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_version`—An identifier for the specific version of a document\.
+ `_view_count`—The number of times that the document has been viewed\.
+ `_language_code` \(String\)—The code for a language that applies to the document\. This defaults to English if you do not specify a language\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.

You can also create custom fields, which you can use like the reserved fields for search and display, and to create facets\. 

There are four types of custom fields:
+ Date
+ Number
+ String
+ String list

You create a custom field using the console or by using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. After you create a custom field, you map it to a document attribute, just as you do with a reserved field\. If you added a document to the index with [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API, you map the attributes with the API\. For documents indexed from an Amazon S3 data source, you map the attributes using a metadata file that contains a JSON structure that describes the document attributes\. For documents indexed with a database or a data source that allows field mapping, you map attributes with the console or the data source configuration\. For more information, see [Searching indexes](https://docs.aws.amazon.com/kendra/latest/dg/searching.html)\.

## Searching indexes<a name="index-searching"></a>

After you create an index, you can start searching your documents\. For more information, see [Searching indexes](https://docs.aws.amazon.com/kendra/latest/dg/searching.html)\.