--------

--------

# Mapping data source fields<a name="field-mapping"></a>

When the source of your data is a data source other than Amazon Simple Storage Service \(Amazon S3\), you can map data source fields to fields in your index\. For example, if you have a field that contains department information for a document, you can map it to an index field called "Department" so that you can use the field in queries\.

You can create field mappings for the following data sources:
+ Confluence
+ Database
+ Google Workspace Drives
+ Microsoft OneDrive
+ Microsoft SharePoint
+ Salesforce
+ ServiceNow

If you store your documents in an S3 bucket, or if you use an Amazon S3 data source, you can provide custom attributes directly using metadata files\. For more information, see [Creating custom document attributes](custom-attributes.md)\.

Mapping your data source fields to an index field is a three\-step process:

1. Create an index\. For more information, see [Creating an index](create-index.md)\.

1. Update the index to add custom fields\.

1. Create a data source that maps data source fields to the index fields\.

To update the index to add custom fields, use the console or the [ UpdateIndex ](API_UpdateIndex.md) operation\. You can add a total of 500 custom fields to your index\.

When you are using the console, you can choose to map a data source field to one of the seven reserved field names, or you can choose to create a new index field that maps to the field\. For database data sources, if the name of the database column matches the name of a reserved field, the field and column are automatically mapped\.

With the API, you add custom and reserved fields using the `DocumentMetadataConfigurationUpdates` parameter\. 

The following JSON example is a `DocumentMetadataConfigurationUpdates` structure that adds a field called "Department" to the index\.

```
"DocumentmetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE"
   }
]
```

When you create the field, you have the option of setting how the field should be used in searches\. You can choose from the following:
+ **Displayable** – Determines whether the field is returned in the query response\. The default is `true`\.
+ **Facetable** – Indicates that the field can be used to create facets\. The default is `false`\.
+ **Searchable** – Determines whether the field is used in the search\. The default is `true` for string fields and `false` for number and date fields\.
+ **Sortable** – Indicates that the field can be used to sort the response from a query\. Can only be set for date, number, and string fields\. Can't be set for string list fields\.

The following JSON example is a `DocumentMetadataConfigurationUpdates` structure that adds a field called "Department" to the index and marks it as facetable\.

```
"DocumentMetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE",
       "Search": {
           "Facetable": true
       }
   }
]
```

Amazon Kendra has 14 reserved fields that you can map to data source fields\. You must provide values for these fields\. The fields are:
+ `_authors` \(String list\) – A list of one or more authors responsible for the content of the document\.
+ `_category` \(String\) – A category that places a document in a specific group\.
+ `_created_at` \(ISO 8601 encoded string\) – The date and time in ISO 8601 format that the document was created\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_data_source_id` \(String\) – The identifier of the data source that contains the document\.
+ `_document_body` \(String\) – The content of the document\.
+ `_document_id` \(String\) – A unique identifier for the document\.
+ `_document_title` \(String\) – The title of the document\.
+ `_excerpt_page_number` \(Long\) – The page number in a PDF file where the document excerpt appears\. If your index was created before September 8, 2020, you must re\-index your documents before you can use this attribute\.
+ `_faq_id` \(String\) – If this is an FAQ question and answer, a unique identifier for them\.
+ `_file_type` \(String\) – The file type of the document, such as pdf or doc\.
+ `_last_updated_at` \(ISO 8601 encoded string\) – The date and time in ISO 8601 format that the document was last updated\. For example, 20120325T123010\+01:00 is the ISO 8601 date\-time format for March 25th 2012 at 12:30PM \(plus 10 seconds\) in Central European Time\.
+ `_source_uri` \(String\) – The URI where the document is available\. For example, the URI of the document on a company website\.
+ `_version` \(String\) – An identifier for the specific version of a document\.
+ `_view_count` \(Long\) – The number of times that the document has been viewed\.

After you have created the index fields, you can map the data source fields to the index fields\. If you are using the console, you can create index fields and map data source fields using the **Custom field mappings** editor\. If you are using the API, you can add field mappings using the [ CreateDataSource ](API_CreateDataSource.md) or [ UpdateDataSource ](API_UpdateDataSource.md) operations\.