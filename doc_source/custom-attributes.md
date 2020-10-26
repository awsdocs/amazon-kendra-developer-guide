--------

--------

# Creating custom document attributes<a name="custom-attributes"></a>

When the source of your data is an S3 bucket, you can apply custom attributes to your documents\. For example, you could create a custom attribute called "Department" with values "HR", "Sales", and "Manufacturing"\. You can apply these attributes to your documents so that you can limit the response to documents in the "HR" department, for example\.

For other data sources, you use field mapping for the same purpose\. For more information, see [Mapping data source fields](field-mapping.md)\.

Amazon Kendra has seven reserved attributes that you can use\. The attributes are:
+ `_category` \(String\) – A category that places a document in a specific group\.
+ `_created_at` \(ISO 8601 encoded string\) – The date and time that the document was created\.
+ `_excerpt_page_number` \(Long\) – The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_file_type` \(String\) – The file type of the document, such as pdf or doc\.
+ `_last_updated_at` \(ISO 8601 encoded string\) – The date and time that the document was last updated\.
+ `_source_uri` \(String\) – The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_view_count` \(Long\) – The number of times that the document has been viewed\.

After you have created a custom attribute, you can use the attribute when you call the `Query` operation\. You can use it for faceted search, use it to filter the response, and choose whether or not the attribute should be returned in the response\. For more information, see [Filtering queries](filtering.md)\.

## Adding custom attributes with the BatchPutDocument operation<a name="custom-attributes-batch"></a>

When you use the [BatchPutDocument](API_BatchPutDocument.md) operation to add a document to your index, you specify custom attributes as part of the `Attributes` structure\. You can add multiple attributes when you call the operation\. The following example is a `Attributes` structure that adds "Department" and "\_category" attributes to a document\.

```
"Attributes": 
    {
        "Department": "HR",
        "_category": "Vacation policy"
    }
```

## Adding custom attributes to an Amazon S3 data source<a name="custom-attributes-batch"></a>

When you use an Amazon S3 bucket as a data source for your index, you add metadata to the documents with companion metadata files\. You place the metadata JSON files in a directory structure that is parallel to your documents\. For more information, see [S3 document metadata](s3-metadata.md)\.

You specify custom attributes in the `Attributes` JSON structure\. You can add a list of attributes\. For example, the following example is an `Attributes` structure that defines three custom attributes and one reserved attribute\.

```
"Attributes": {
        "brand": "Amazon Basics",
        "price": 1595,
        "_category": "sports",
        "subcategories": ["outdoors", "electronics"]
    }
```