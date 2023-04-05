--------

--------

# Creating custom document fields<a name="custom-attributes"></a>

You can apply custom attributes or metadata fields relevant to your particular documents\. For example, you can create a custom field or attribute called "Department" with the values of "HR", "Sales", and "Manufacturing"\. You can use these fields or attributes to limit the response \(the search results\) to documents in the "HR" department, for example\.

You can create up to 500 custom fields or attributes\.

For most data sources, you map fields in the external data source to the corresponding fields in Amazon Kendra\. For more information, see [Mapping data source fields](field-mapping.md)\. For S3 data sources, you can apply custom fields or attributes using metadata files\.

Before you can use a custom field or attribute, you must first create the field in the index\. Use the console or the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API to create the index field\. You cannot change the field data type once you have created the field\.

You can also use Amazon Kendra's built\-in or reserved fields\.

With the `UpdateIndex` API, you add custom fields or attributes using the `DocumentMetadataConfigurationUpdates` parameter\.

The following JSON example uses `DocumentMetadataConfigurationUpdates` to add a field called "Department" to the index\.

```
"DocumentmetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE"
   }
]
```

## Using Amazon Kendra built\-in document fields<a name="index-reserved-fields"></a>

With the [UpdateIndex API](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html), you can create reserved or built\-in fields using `DocumentMetadataConfigurationUpdates` and specifying the reserved field name to map to your equivalent document attribute or document field\. You can also create custom fields this way\. If you use a data source connector, most include field mappings that map your data source document fields to Amazon Kendra index fields\. When you create a field, you can configure the `Search` object to set the field as displayable, facetable, searchable, and sortable\. You can configure the `Relevance` object to set the field's relevance boosting duration, freshness, importance, rank order, and importance values\. You cannot change the field type once you have created the field\.

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

For custom fields, you create these fields using `DocumentMetadataConfigurationUpdates` with the `UpdateIndex` API, just as you do when creating a reserved or built\-in field\. You must set the appropriate data type for your custom field\. You cannot change the field type once you have created the field\.

The following are the types you can set for custom fields:
+ Date
+ Number
+ String
+ String list

You create a custom field using the console or by using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. After you create a custom field, you map it to a document attribute, just as you do with a reserved field\. If you added a document to the index with [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API, you map the attributes with the API\. For documents indexed from an Amazon S3 data source, you map the attributes using a metadata file that contains a JSON structure that describes the document attributes\. For documents indexed with a database or a data source that allows field mapping, you map attributes with the console or the data source configuration\.

## Adding custom attributes or fields with the BatchPutDocument API<a name="custom-attributes-batch"></a>

When you use the [BatchPutDocument](API_BatchPutDocument.md) API to add a document to your index, you specify custom fields or attributes as part of `Attributes`\. You can add multiple fields or attributes when you call the API\. You can create up to 500 custom fields or attributes\. The following example is a custom field or attribute that adds "Department" to a document\.

```
"Attributes": 
    {
        "Department": "HR",
        "_category": "Vacation policy"
    }
```

## Adding custom attributes or fields to an Amazon S3 data source<a name="custom-attributes-s3"></a>

When you use an S3 bucket as a data source for your index, you add metadata to the documents with companion metadata files\. You place the metadata JSON files in a directory structure that is parallel to your documents\. For more information, see [Amazon S3 document metadata](s3-metadata.md)\.

You specify custom fields or attributes in the `Attributes` JSON structure\. You can create up to 500 custom fields or attributes\. For example, the following example uses `Attributes` to define three custom fields or attributes and one reserved field\.

```
"Attributes": {
        "brand": "Amazon Basics",
        "price": 1595,
        "_category": "sports",
        "subcategories": ["outdoors", "electronics"]
    }
```