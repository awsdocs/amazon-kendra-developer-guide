--------

--------

# Using a Confluence data source<a name="data-source-confluence"></a>

You can use Amazon Kendra to index blogs, pages, and attachments to either that are hosted on a Confluence cloud or Confluence server instance\. By default, Amazon Kendra indexes regular spaces, you can configure Amazon Kendra to index personal and archived spaces\. To exclude or include specific blogs, pages, and spaces from indexing, you use a list\. 

Amazon Kendra indexes pages and blogs by default\. You can restrict the pages and blogs that are crawled using inclusion and exclusion patterns\. When you use an inclusion pattern, only those pages and blogs that match the inclusion pattern are indexed\. If you specify an exclusion pattern, pages that match the pattern are not indexed\.

When you create the data source, you can use the console or the [CreateDataSource](API_CreateDataSource.md) operation to specify whether Amazon Kendra indexes the attachments to pages and blogs\. If you choose to index attachments, only attachments to the indexed pages and blogs are indexed\.

Before you can index the documents on a Confluence instance, you must create an account with administrative permission that Amazon Kendra can use to connect to the server\. The account must grant Amazon Kendra permission to view all of the content within your Confluence instance\. You can grant the account these permissions by making it a member of the `confluence-administrators` group\. 

You store the Confluence credentials in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The secret must contain the following information:
+ User name
+ Password or API token

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user-name",
    "password": "password or API token"
}
```

For Confluence cloud, you must generate an API token \. For more information, see [API tokens](https://confluence.atlassian.com/cloud/api-tokens-938839638.html) on the Atlassian website\.

The data source IAM role must have permission to access the secret and the AWS Key Management Service key used to decrypt it\. For more information see [IAM role for Confluence server data sources](iam-roles.md#iam-roles-ds-cnf)\.

You must create an index before you create the Confluence data source\. For more information, see [Creating an index](create-index.md)\. You provide the ID of the index when you create the data source\.

You specify connection and other information in the console or in an instance of the [ConfluenceConfiguration](API_ConfluenceConfiguration.md) data type\. You must provide the following information: 
+ Credentials to connect to the Confluence instance\.
+ The URL of the Confluence instance that contains your documents\.
+ The version of Confluence that you are using\.

## Indexing spaces<a name="confluence-spaces"></a>

Amazon Kendra includes information from a space in the index\. A space may be included in the results of a query based on this information\. The Confluence account used for the data source must have permission to access the space in order to index it\.

By default, Amazon Kendra doesn't index Confluence archive and personal spaces\. You can choose to index them when you create the data source\. If you don't want Amazon Kendra to index a space, mark it private in Confluence \.

You can restrict access to the contents of a space by specifying view permissions\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](user-context-filter.md)\.

If you use the Amazon Kendra console to create a Confluence data source, Amazon Kendra creates index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](API_UpdateIndex.md) operation\. To map the Confluence fields to Amazon Kendra index fields, see the following table\.


| Confluence field | Suggested Amazon Kendra field | 
| --- | --- | 
| DISPLAY\_URL | \_source\_uri | 
| ITEM\_TYPE | \_category | 
| SPACE\_KEY | cf\_space\_key | 
| URL | cf\_url | 

## Indexing pages<a name="confluence-page"></a>

Amazon Kendra indexes all pages, including nested pages, in a space unless they are filtered out by an inclusion or exclusion pattern\.

The Confluence security model uses nested permissions\. To have access to a page, the account that you use to connect to the Confluence instance\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](user-context-filter.md)\.

If you use the console to create a Confluence data source, Amazon Kendra creates the index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](API_UpdateIndex.md) operation\. To map the Confluence fields to Amazon Kendra index fields, see the following table\. 


| Confluence field | Suggested Amazon Kendra field | 
| --- | --- | 
| AUTHOR | cf\_author | 
| CONTENT\_STATUS | cf\_page\_content\_status | 
| CREATED\_DATE | \_created\_at | 
| DISPLAY\_URL | \_source\_uri | 
| ITEM\_TYPE | \_category | 
| LABELS | cf\_labels | 
| MODIFIED\_DATE | \_last\_updated\_at | 
| PARENT\_ID | cf\_parent\_id | 
| SPACE\_KEY | cf\_space\_key | 
| SPACE\_NAME | cf\_space\_name | 
| URL | cf\_url | 
| VERSION | cf\_version | 

## Blogs<a name="confluence-blogs"></a>

Amazon Kendra indexes all blogs in a space unless they are filtered from indexing by an inclusion or an exclusion pattern\. 

The Confluence security model uses nested permissions\. To index a blog, the user that you use to connect to the Confluence instance must have access to the blog and the space that contains it\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](user-context-filter.md)\.

If you use the console to index a Confluence data source, Amazon Kendra creates the index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](API_UpdateIndex.md) operation\. To map the Confluence data source fields to Amazon Kendra index fields, see the following table\. 


| Confluence field | Suggested Amazon Kendra field | 
| --- | --- | 
| AUTHOR | cf\_author | 
| DISPLAY\_URL | \_source\_uri | 
| ITEM\_TYPE | \_category | 
| LABELS | cf\_labels | 
| PUBLISH\_DATE | \_created\_at | 
| SPACE\_KEY | cf\_space\_key | 
| SPACE\_NAME | cf\_space\_name | 
| URL | cf\_url | 
| VERSION | cf\_version | 

## Attachments<a name="confluence-attachments"></a>

Confluence enables you to create attachments to pages and blog posts\. By default, attachments aren't indexed\. You can configure Amazon Kendra to include attachments in the index\. Amazon Kendra includes only attachments to indexed pages and blogs in the index\.

Amazon Kendra indexes only the following supported documents types:
+ Microsoft Word
+ Microsoft PowerPoint
+ HTML
+ PDF
+ Plain text

The Confluence security model uses nested permissions\. To index to an attachment, the account that you use to connect the Confluence instance must have access to the blog or page and the space that contains it\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](user-context-filter.md)\.

If you use the console, Amazon Kendra creates index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](API_UpdateIndex.md) operation\. To map the Confluence fields to Amazon Kendra fields, see the following table\. 


| Confluence field | Suggested Amazon Kendra field | 
| --- | --- | 
| AUTHOR | cf\_author | 
| CONTENT\_TYPE | cf\_attachment\_content\_type | 
| CREATED\_DATE | \_created\_at | 
| DISPLAY\_URL | \_source\_uri | 
| FILE\_SIZE | cf\_attachment\_file\_size | 
| ITEM\_TYPE | \_category | 
| LABELS | cf\_labels | 
| PARENT\_ID | cf\_parent\_id | 
| SPACE\_KEY | cf\_space\_key | 
| SPACE\_NAME | cf\_space\_name | 
| URL | cf\_url | 
| VERSION | cf\_version | 