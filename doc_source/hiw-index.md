--------

--------

# Index<a name="hiw-index"></a>

An *index* provides search results for documents and frequently asked questions \(FAQ\) that it has indexed\. The way you add documents to the index depends on the type of document and where they are stored\.
+ If your documents are in a store, such as an S3 bucket or a Microsoft SharePoint site, you use a data source
+ You use the Amazon Kendra API to add documents
+ For FAQ questions and answers, which must be stored in an Amazon Simple Storage Service \(Amazon S3\) bucket, you upload them from the bucket

An index can contain documents that are indexed from a data source, documents that are added directly to the index, and FAQs\. You can create indexes with the Amazon Kendra console, the AWS CLI, or an AWS SDK\. For information about the types of documents that can be indexed, see [Types of documents](index-document-types.md)\.

For information about using a data source with an index, see [Data sources](hiw-data-source.md)\.

<<<<<<< HEAD
To add documents directly to an index, you call the [ BatchPutDocument ](API_BatchPutDocument.md) operation\. The documents are supplied as plain text, as a binary blob, or using a path to a document stored in an Amazon S3 bucket\. For an example, see [Adding documents from an Amazon S3 bucket](in-adding-plain-text.md)\.
=======
To add documents directly to an index, you call the [BatchPutDocument](API_BatchPutDocument.md) operation\. The documents are supplied as plain text, as a binary blob, or using a path to a document stored in an Amazon S3 bucket\. For an example, see [Adding documents from an Amazon S3 bucket](in-adding-plain-text.md)\.
>>>>>>> parent of 2b1c178 (updating tutorial)

## Index fields<a name="index-fields"></a>

An index contains fields that you map to the attributes of your document\. Attributes could include, for example, the document title, main body text, last updated date, and other attributes contained within the structure of your documents\. You can also create custom attributes such as figure title, or the business department the document is related to\. Fields, which you map to your document attributes, provide the schema for your index\. Amazon Kendra uses the fields to search your documents\. After you map your fields to your document attributes, you can use the information in the field for searching, for display, and to create facets of the search result\.

Amazon Kendra has 14 reserved fields, which you can map to your document attributes:
+ `_authors` – A list of one or more authors responsible for the content of the document\.
+ `_category` – A category that places a document in a specific group\.
+ `_created_at` – The date and time in ISO 8601 format that the document was created\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_data_source_id` – The identifier of the data source that contains the document\.
+ `_document_body` – The content of the document\.
+ `_document_id` – A unique identifier for the document\.
+ `_document_title` – The title of the document\.
+ `_excerpt_page_number` – The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_faq_id` – If this is an FAQ question and answer, a unique identifier for them\.
+ `_file_type` – The file type of the document, such as pdf or doc\.
+ `_last_updated_at` – The date and time in ISO 8601 format that the document was last updated\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_source_uri` – The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_version` – An identifier for the specific version of a document\.
+ `_view_count` – The number of times that the document has been viewed\.

You can also create custom fields, which you can use like the reserved fields for search and display, and to create facets\. 

There are four types of custom fields:
+ Date
+ Number
+ String
+ String list

<<<<<<< HEAD
You create a custom field using the console or by using the [ UpdateIndex ](API_UpdateIndex.md) operation\. After you create a custom field, you map it to a document attribute, just as you do with a reserved field\. If you added a document to the index with [ BatchPutDocument ](API_BatchPutDocument.md) operation, you map the attributes with the API\. For documents indexed from an Amazon S3 data source, you map the attributes using a metadata file that contains a JSON structure that describes the document attributes\. For documents indexed with a database or SharePoint Online data source, you map attributes with the console or the data source configuration\. For more information, see [Document attributes](hiw-document-attributes.md)\.
=======
You create a custom field using the console or by using the [UpdateIndex](API_UpdateIndex.md) operation\. After you create a custom field, you map it to a document attribute, just as you do with a reserved field\. If you added a document to the index with [BatchPutDocument](API_BatchPutDocument.md) operation, you map the attributes with the API\. For documents indexed from an Amazon S3 data source, you map the attributes using a metadata file that contains a JSON structure that describes the document attributes\. For documents indexed with a database or SharePoint Online data source, you map attributes with the console or the data source configuration\. For more information, see [Document attributes](hiw-document-attributes.md)\.
>>>>>>> parent of 2b1c178 (updating tutorial)

## Searching indexes<a name="index-searching"></a>

After you create an index, you can use it for search queries\. For more information, see [Searching indexes](searching.md)\.