--------

--------

# Using a Zendesk data source<a name="data-source-zendesk"></a>

You can use your Zendesk Suite as a data source for Amazon Kendra\. The Zendesk data source can index the support ticketing system, help center articles, and Guide community forums in your Zendesk Suite\. 

For troubleshooting your Amazon Kendra Zendesk data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create the Zendesk data source\. For more information, see [ Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\. To use Zendesk in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index, and then select **Data sources** from the navigation menu to add Zendesk\. To use the Zendesk data source, you must specify the host URL of your Zendesk Suite\. For example, *https://yoursubdomain\.zendesk\.com*\.

With Amazon Kendra, you can specify the following items in your Zendesk Suite:
+ Regular expression patterns to include or exclude specific files\.
+ Whether to index support tickets, ticket comments, and/or ticket comment attachments\. You can filter by **Organization name** if you want to index tickets that are only within a specific organization\.
+ Whether to index help center articles, article attachments, and article comments\.
+ Whether to index Guide community topics, posts, or post comments\. You can choose to set a crawl date for when you want start crawling data from Zendesk\.

Amazon Kendra requires authentication credentials to access your Zendesk Suite\. See [Authentication](#zendesk-authentication)\.

You also must provide the Amazon Resource Name \(ARN\) of an AWS Identity and Access Management role to grant access to your Zendesk Suite\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Zendesk data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\. 

To connect to Zendesk, you specify the connection and other information in the console or by using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You include a JSON that contains the data source schema as part of the template configuration\. You provide the host URL as a part of the connection configuration or repository endpoint details\. You must also specify the type of data source as `ZENDESK` and a secret for your authentication credentials as part of the repository configuration details\. You then specify `TEMPLATE` as the **Type** when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. To view the template schema, see [Data source schemas](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)\.

Amazon Kendra also crawls user, user segment, and group information from the Zendesk instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Zendesk data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-zendesk)\.

You also can add the following optional information:
+ Whether Amazon Kendra should use the Zendesk change log mechanism to determine if a document was added, modified, updated, or deleted in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might be faster to scan the documents in Zendesk\. If you are syncing your Zendesk data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any attachment with a file type that doesn't match the pattern will not be indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Zendesk fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="zendesk-authentication"></a>

The authentication credentials to access your Zendesk Suite must include your Zendesk client secret, user name, and password\. You create the client secret in your Zendesk account\.

You store your Zendesk credentials as a secret in AWS Secrets Manager\. The credentials are your Zendesk client secret, user name, and password\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. You can also store the credentials in an existing secret in Secrets Manager\. If you are using the API to create your data source, you must provide the ARN of an existing secret\.

The credentials are stored as a JSON string in Secrets Manager\.

```
{
"hostUrl" : "https://yoursubdomain.zendesk.com",
"clientId" : "kendra",
"clientSecret" : "Zendesk client secret",
"userName" : "Zendesk user name",
"password" : "Zendesk password"
}
```

**To create a client\_secret in Zendesk**

1. Log in at *https://yoursubdomain\.zendesk\.com*\.

1. Navigate to the **Admin Center**\.

1. Select **Channels**, then select **API**\.

1. Agree to the terms and conditions\.

1. Navigate to the **OAuth Clients** tab and then select **Add Oauth Client**\.

1. Enter a **Client Name** and **Unique Identifier**\. 

1. Select **Save**\. Refresh the page to see the generated **client\_secret\.** Copy and store the **client\_secret** for reference\. You'll need it when you create a secret in Secrets Manager\.

**Note**  
For security reasons, the **client\_secret** is displayed fully only once\. Once you save, you will only be able to view the first nine characters\. If necessary, regenerate a new **client\_secret**\.
Store the Zendesk **client\_secret** securely, as you would for any password\.