--------

--------

# Document attributes<a name="hiw-document-attributes"></a>

A document has attributes associated with it\. Attributes of a document are the properties of a document or what is contained within the structure of a document\. For example, each of your documents might contain title, body text, and author\. You can also add your own custom attributes of your documents\. Custom attributes are attributes that you specify for your own needs\. For example, if your index searches tax documents, you might specify a custom attribute for the type of tax document such as W\-2, 1099, and so on\.

Before you can use a document attribute in a query, it must be mapped to an index field\. For example, the title attribute can be mapped to the field `_document_title`\. For more information, see [Mapping fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. To add a new attribute, you must create an index field to map the attribute to\. You create index fields using the console or by using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\.

You can use document attributes to filter responses and to make faceted search suggestions\. For example, you can filter a response to only return a specific version of a document, or you can filter searches to only return 1099 type of tax documents that match the search term\. For more information, see [Filtering queries](https://docs.aws.amazon.com/kendra/latest/dg/filtering.html)\.

You can also use document attributes to manually tune the query response\. For example, you can choose to increase the importance of the title field to increase the weight that Amazon Kendra assigns to the field when determining which documents to return in the response\. For more information, see [Tuning search relevance](https://docs.aws.amazon.com/kendra/latest/dg/tuning.html)\.

If you are adding a document directly to an index, you specify the attributes in the [Document](https://docs.aws.amazon.com/kendra/latest/dg/API_Document.html) input parameter to the [BatchPutDocument](API_BatchPutDocument.md) API\. You specify the custom attribute values in a [DocumentAttribute](API_DocumentAttribute.md) object array\. If you are using a data source, the method that you use to add the document attributes depends on the data source\. For more information, see [Creating custom document attributes](custom-attributes.md)\.