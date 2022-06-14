--------

--------

# Creating custom document attributes<a name="custom-attributes"></a>

When the source of your data is an S3 bucket or data source, you can apply custom attributes to your documents using metadata files\. For example, you can create a custom attribute called "Department" with the values of "HR", "Sales", and "Manufacturing"\. You can apply these attributes to your documents so that you can limit the response to documents in the "HR" department, for example\.

You can create up to 500 custom attributes\.

For other data sources, you map fields in the external data source to the corresponding custom attributes in Amazon Kendra\. For more information, see [Mapping data source fields](field-mapping.md)\.

Before you can use a custom attribute, you must first create a field in the index\. Use the console or the [UpdateIndex](API_UpdateIndex.md) API to create the index fields\. The supported field types are date, long, string, and string list\. 

With the `UpdateIndex` API, you add custom fields using the `DocumentMetadataConfigurationUpdates` parameter\.

The following JSON example uses `DocumentMetadataConfigurationUpdates` to add a field called "Department" to the index\.

```
"DocumentmetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE"
   }
]
```

Amazon Kendra has 15 reserved attributes that you can use\. The attributes are the following:
+ `_authors` \(String list\) – A list of one or more authors that are responsible for the content of the document\.
+ `_category` \(String\) – A category that places a document in a specific group\.
+ `_created_at` \(ISO 8601 encoded string\) – The date and time that the document was created\.

  You can also include the time zone in the ISO 8601 date\-time format if required\. For example, 2012\-03\-25T12:30:10\+01:00 is the ISO 8601 date\-time format for March 25, 2012, at 12:30PM \(plus 10 seconds\) in the Central European Time time zone\.
+ `_data_source_id` \(String\) – The identifier of the data source that contains the document\.
+ `_document_body` \(String\) – The content of the document\.
+ `_document_id` \(String\) – A unique identifier for the document\.
+ `_document_title` \(String\) – The title of the document\.
+ `_excerpt_page_number` \(Long\) – The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_faq_id` \(String\) – If this is an FAQ question and answer, a unique identifier for them\.
+ `_file_type` \(String\) – The file type of the document, such as PDF or DOC\.
+ `_last_updated_at` \(ISO 8601 encoded string\) – The date and time that the document was last updated\.

  You can also include the time zone in the ISO 8601 date\-time format if required\. For example, 2012\-03\-25T12:30:10\+01:00 is the ISO 8601 date\-time format for March 25, 2012, at 12:30PM \(plus 10 seconds\) in the Central European Time time zone\.
+ `_source_uri` \(String\) – The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_version` \(String\) – An identifier for the specific version of a document\.
+ `_view_count` \(Long\) – The number of times that the document is viewed\.
+ `_language_code` \(String\) – The code for a language that applies to the document\. This defaults to English if you don't specify a language\. For more information about the supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.

After you created a custom attribute, you can use the attribute when you call the `Query` API\. You can use it for faceted search, use it to filter the response, and choose whether the attribute is returned in the response\. For more information, see [Filtering queries](filtering.md)\.

## Adding custom attributes with the BatchPutDocument API<a name="custom-attributes-batch"></a>

When you use the [BatchPutDocument](API_BatchPutDocument.md) API to add a document to your index, you specify custom attributes as part of `Attributes`\. You can add multiple attributes when you call the API\. You can create up to 500 custom attributes\. The following example is a customer attribute that adds "Department" to a document\.

```
"Attributes": 
    {
        "Department": "HR",
        "_category": "Vacation policy"
    }
```

## Adding custom attributes to an Amazon S3 data source<a name="custom-attributes-s3"></a>

When you use an S3 bucket as a data source for your index, you add metadata to the documents with companion metadata files\. You place the metadata JSON files in a directory structure that is parallel to your documents\. For more information, see [Amazon S3 document metadata](s3-metadata.md)\.

You specify custom attributes in the `Attributes` JSON structure\. You can create up to 500 custom attributes\. For example, the following example uses `Attributes` to define three custom attributes and one reserved attribute\.

```
"Attributes": {
        "brand": "Amazon Basics",
        "price": 1595,
        "_category": "sports",
        "subcategories": ["outdoors", "electronics"]
    }
```