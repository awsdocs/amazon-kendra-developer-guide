--------

--------

# Adding documents directly to an index<a name="in-adding-documents"></a>

You can add documents directly to an index using the [BatchPutDocument](API_BatchPutDocument.md) API\. You can't add documents directly using the console\. When you're using the console, you use a data source to add documents\.

You can add only the following types of documents with the `BatchPutDocuments` API\.
+ Plain text
+ HTML
+ PDF
+ Microsoft PowerPoint
+ Microsoft Word

Documents can be added from an S3 bucket or supplied as binary data\.

Adding documents to an index is an asynchronous operation\. After you call the `BatchPutDocument` API, you use the [BatchGetDocumentStatus](API_BatchGetDocumentStatus.md) API to monitor the progress of indexing your documents\. When you call the `BatchGetDocumentStatus` API with a list of document IDs, it returns the status of the document\. When the status of the document is `INDEXED` or `FAILED`, processing of the document is complete\. When the status is `FAILED`, the `BatchGetDocumentStatus` API returns the reason that the document couldn't be indexed\.

If you want to alter your document metadata or attributes and content during the document ingestion process, see [Amazon Kendra Custom Document Enrichment](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\.

If you want to use a custom data source, each document you submit using the `BatchPutDocument` API requires a data source ID and execution ID as attributes\. For more information, see [Required attributes for custom data sources](https://docs.aws.amazon.com/kendra/latest/dg/data-source-custom.html#custom-required-attributes)\.

Note, each document ID must be unique per index\. You cannot create a data source to index your documents with their unique IDs and then use the `BatchPutDocument` API to index the same documents, or vice versa\. You can delete a data source and then use the `BatchPutDocument` API to index the same documents, or vice versa\.

The following examples show how to add documents directly to an index\.

**Topics**
+ [Adding documents with the API](in-adding-binary-doc.md)
+ [Adding documents from an S3 bucket](in-adding-plain-text.md)