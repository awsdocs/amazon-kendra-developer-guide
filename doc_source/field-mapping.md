--------

--------

# Mapping data source fields<a name="field-mapping"></a>

You can map document or content fields from your data source to fields in your index\. For example, if you have a field in your data source called "dept" that contains department information for a document, you can map it to an index field called "Department"\. That way, you can use the field when querying documents\. 

You can also map standard or reserved fields such as `_created_at`\. If your data source has a field called "creation\_date", you can map this to the equivalent Amazon Kendra reserved field called `_created_at`\. You can map fields for most data sources\.

You can create field mappings for the following data sources:
+ Confluence
+ Database
+ Google Workspace Drives
+ Microsoft Exchange
+ Microsoft OneDrive
+ Microsoft SharePoint
+ Microsoft Teams
+ Microsoft Yammer
+ Salesforce
+ ServiceNow
+ Amazon WorkDocs
+ Amazon FSx
+ Slack
+ Box
+ Quip
+ Jira
+ GitHub
+ Alfresco
+ Zendesk
+ Dropbox

If you store your documents in an S3 bucket, or S3 data source, you can provide custom attributes directly using metadata files\. For more information, see [Creating custom document fields](custom-attributes.md)\.

Mapping your data source fields to an index field is a three\-step process:

1. Create an index\. For more information, see [Creating an index](create-index.md)\.

1. Update the index to add custom fields\.

1. Create a data source that maps data source fields to the index fields\.

To update the index to add custom fields, use the console or the [UpdateIndex](API_UpdateIndex.md) API\. You can add a total of 500 custom fields to your index\.

In the console, you can choose to map a data source field to one of the reserved field names\. Or, you can choose to create a new index field that maps to the field\. For database data sources, if the name of the database column matches the name of a reserved field, the field and column are automatically mapped\.

With the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API, you add custom and reserved fields using the `DocumentMetadataConfigurationUpdates` parameter\.

The following JSON example uses `DocumentMetadataConfigurationUpdates` to add a field called "Department" to the index\.

```
"DocumentmetadataConfigurationUpdates": [
   {
       "Name": "Department",
       "Type": "STRING_VALUE"
   }
]
```

When you create the field, you have the option of setting how the field is used in searches\. You can choose from the following:
+ **Displayable**—Determines whether the field is returned in the query response\. The default is `true`\.
+ **Facetable**—Indicates that the field can be used to create facets\. The default is `false`\.
+ **Searchable**—Determines whether the field is used in the search\. The default is `true` for string fields and `false` for number and date fields\.
+ **Sortable**—Indicates that the field can be used to sort the response from a query\. Can only be set for date, number, and string fields\. Can't be set for string list fields\.

The following JSON example uses `DocumentMetadataConfigurationUpdates` to add a field called "Department" to the index and marks it as facetable\.

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