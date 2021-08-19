--------

--------

# Adding documents directly to an index<a name="in-adding-documents"></a>

You can add documents directly to an index using the [BatchPutDocument](API_BatchPutDocument.md) operation\. You can't add documents directly using the console\. When you are using the console, you use a data source to add documents\.

You can add only the following types of documents with the `BatchPutDocuments` operation\.
+ Plain text
+ HTML
+ PDF
+ Microsoft PowerPoint
+ Microsoft Word

Documents can be added from an Amazon S3 bucket or supplied as binary data\.

Adding documents to an index is an asynchronous operation\. After you call the `BatchPutDocument` operation, you use the [BatchGetDocumentStatus](API_BatchGetDocumentStatus.md) operation to monitor the progress of indexing your documents\. When you call the `BatchGetDocumentStatus` operation with a list of document IDs, it returns the status of the document\. When the status of the document is `INDEXED` or `FAILED`, processing of the document is complete\. When the status is `FAILED`, the `BatchGetDocumentStatus` operation returns the reason that the document couldn't be indexed\.

 The following examples show how to add documents directly to an index\.

**Topics**
+ [Adding documents with the API](in-adding-binary-doc.md)
+ [Adding documents from an Amazon S3 bucket](in-adding-plain-text.md)