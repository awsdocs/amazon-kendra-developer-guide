--------

--------

# Using an Atlassian Confluence data source<a name="data-source-confluence"></a>

You can use your Atlassian Confluence as a data source for Amazon Kendra\. To use Confluence in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Confluence\.

Amazon Kendra supports Atlassian Confluence cloud and Atlassian Confluence server instance\.

When you connect to Confluence to index your documents, you specify the URL of your Confluence instance\. You can specify regular expression patterns to include or exclude specific blog posts, pages, spaces, or attachments in your Confluence\. Amazon Kendra indexes blogs, pages, and regular spaces by default\. If you choose to index attachments, only attachments to the indexed pages and blogs are indexed\.

You must create an index before you create the Confluence data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Confluence, you specify the connection and other information in the console or by using the [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) object\. You provide the URL of your Confluence instance you want to index\.

Before you can index your content from your Confluence, you must create an account with administrative permissions\. The account must grant Amazon Kendra permission to view all of the content within your Confluence instance\. You can grant the account these permissions by making it a member of the `confluence-administrators` group\. You must specify the version of Confluence you use when configuring Confluence, whether you use Confluence cloud or Confluence server\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your AWS Secrets Manager secret, which stores your Confluence authentication credentials, and the AWS Key Management Service key used to decrypt it\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Atlassian Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Confluence\. You store your Confluence credentials in an AWS Secrets Manager secret\. The credentials are user name and password of your Confluence account\. If you use Confluence cloud, you use a generated API token as the password\. For more information, see [API tokens](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) on the Atlassian website\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user-name",
    "password": "password or API token"
}
```

Amazon Kendra also crawls user information from the Confluence instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-confluence)\.

You also can add the following optional information:
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Page field mappings that map your Confluence fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Indexing spaces<a name="confluence-spaces"></a>

Amazon Kendra includes information from a space in the index\. A space may be included in the results of a query based on this information\. The Confluence account used for the data source must have permission to access the space in order to index it\.

By default, Amazon Kendra doesn't index Confluence archive and personal spaces\. You can choose to index them when you create the data source\. If you don't want Amazon Kendra to index a space, mark it private in Confluence\.

You can restrict access to the contents of a space by specifying view permissions\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

If you use the Amazon Kendra console to create a Confluence data source, Amazon Kendra creates index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. To map the Confluence fields to Amazon Kendra index fields, see the following table\.


| Confluence field | Suggested Amazon Kendra field | 
| --- | --- | 
| DISPLAY\_URL | \_source\_uri | 
| ITEM\_TYPE | \_category | 
| SPACE\_KEY | cf\_space\_key | 
| URL | cf\_url | 

## Indexing pages<a name="confluence-page"></a>

Amazon Kendra indexes all pages, including nested pages, in a space unless they are filtered out by an inclusion or exclusion pattern\.

To index pages, you must use a Confluence account that has access to the pages\. Access to pages in Confluence can be through nested group permissions\. To access a page, you must belong to the group or sub group that has permission to access the page\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

If you use the console to create a Confluence data source, Amazon Kendra creates the index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. To map the Confluence fields to Amazon Kendra index fields, see the following table\.


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

To index blogs, you must use a Confluence account that has access to the blogs and the spaces that contain the blogs\. Access to blogs in Confluence can be through nested group permissions\. To access a blog, you must belong to the group or sub group that has permission to access the blog and its space\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

If you use the console to index a Confluence data source, Amazon Kendra creates the index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. To map the Confluence data source fields to Amazon Kendra index fields, see the following table\. 


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

To index attachments, you must use a Confluence account that has access to the blogs or pages of the attachments and their spaces\. Access to blogs in Confluence can be through nested group permissions\. To access an, you must belong to the group or sub group that has permission to access the blogs or pages of the attachments and their spaces\. If a query includes user information, Amazon Kendra reads these permissions and uses them for user context filtering\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

If you use the console, Amazon Kendra creates index fields for you when you specify a field mapping\. If you use the API, you must first create the index field using the [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) API\. To map the Confluence fields to Amazon Kendra fields, see the following table\.


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