--------

--------

# Creating custom document attributes<a name="custom-attributes"></a>

When the source of your data is an S3 bucket or an Amazon S3 data source, you can apply custom attributes to your documents using metadata files\. For example, you could create a custom attribute called "Department" with values "HR", "Sales", and "Manufacturing"\. You can apply these attributes to your documents so that you can limit the response to documents in the "HR" department, for example\.

You can create up to 500 custom attributes\.

For other data sources, you map fields in the external data source to the corresponding custom attributes in Amazon Kendra\. For more information, see [Mapping data source fields](field-mapping.md)\.

Before you can use a custom attribute, you must first create a field in the index\. Use the console or the [ UpdateIndex ](API_UpdateIndex.md) operation to create the index fields\. The supported field types are date, long, string, and string list\. 

With the `UpdateIndex` operation, you add custom fields using the `DocumentMetadataConfigurationUpdates` parameter

The following JSON example is a `DocumentMetadataConfigurationUpdates` structure that adds a field called "Department" to the index\.

```
"DocumentmetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE"
   }
]
```

Amazon Kendra has 14 reserved attributes that you can use\. The attributes are:
+ `_authors` \(String list\) – A list of one or more authors responsible for the content of the document\.
+ `_category` \(String\) – A category that places a document in a specific group\.
+ `_created_at` \(ISO 8601 encoded string\) – The date and time that the document was created\.

  It is important for the time zone to be included in the ISO 8601 date\-time format\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_data_source_id` \(String\) – The identifier of the data source that contains the document\.
+ `_document_body` \(String\) – The content of the document\.
+ `_document_id` \(String\) – A unique identifier for the document\.
+ `_document_title` \(String\) – The title of the document\.
+ `_excerpt_page_number` \(Long\) – The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_faq_id` \(String\) – If this is an FAQ question and answer, a unique identifier for them\.
+ `_file_type` \(String\) – The file type of the document, such as pdf or doc\.
+ `_last_updated_at` \(ISO 8601 encoded string\) – The date and time that the document was last updated\.

  It is important for the time zone to be included in the ISO 8601 date\-time format\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_source_uri` \(String\) – The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_version` \(String\) – An identifier for the specific version of a document\.
+ `_view_count` \(Long\) – The number of times that the document has been viewed\.

After you have created a custom attribute, you can use the attribute when you call the `Query` operation\. You can use it for faceted search, use it to filter the response, and choose whether or not the attribute should be returned in the response\. For more information, see [Filtering queries](filtering.md)\.

## Adding custom attributes with the BatchPutDocument operation<a name="custom-attributes-batch"></a>

When you use the [ BatchPutDocument ](API_BatchPutDocument.md) operation to add a document to your index, you specify custom attributes as part of the `Attributes` structure\. You can add multiple attributes when you call the operation\. You can create up to 500 custom attributes\. The following example is a `Attributes` structure that adds "Department" and "\_category" attributes to a document\.

```
"Attributes": 
    {
        "Department": "HR",
        "_category": "Vacation policy"
    }
```

## Adding custom attributes to an Amazon S3 data source<a name="custom-attributes-s3"></a>

When you use an Amazon S3 bucket as a data source for your index, you add metadata to the documents with companion metadata files\. You place the metadata JSON files in a directory structure that is parallel to your documents\. For more information, see [S3 document metadata](s3-metadata.md)\.

You specify custom attributes in the `Attributes` JSON structure\. You can create up to 500 custom attributes\. For example, the following example is an `Attributes` structure that defines three custom attributes and one reserved attribute\.

```
"Attributes": {
        "brand": "Amazon Basics",
        "price": 1595,
        "_category": "sports",
        "subcategories": ["outdoors", "electronics"]
    }
```