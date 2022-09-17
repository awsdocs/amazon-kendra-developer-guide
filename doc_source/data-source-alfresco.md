--------

--------

# Using an Alfresco data source<a name="data-source-alfresco"></a>

You can use your Alfresco site as a data source for Amazon Kendra\. To use Alfresco in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Alfresco\.

**Note**  
Alfresco data source connector is currently in preview mode\. Basic authentication is currently supported\. If you would like to use Alfresco connector in production, contact [Support](http://aws.amazon.com/contact-us/)\.

For troubleshooting your Amazon Kendra Alfresco data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create the Alfresco data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

When you connect to Alfresco to index your documents, you specify the Alfresco site URL and Alfresco site ID\. You must also provide the Amazon Kendra path to your SSL certificate to connect to Alfresco\. You can specify regular expression patterns to include or exclude specific documents in your Alfresco site\. You can specify whether to index document libraries, wikis, blogs, comments on content, and shared files\.

To connect to Alfresco, you specify the connection and other information in the console or by using the [AlfrescoConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AlfrescoConfiguration.html) object\. You provide the URL and ID of the Alfresco site you want to index, as well as the SSL certificate stored in Amazon S3\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Alfresco files\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Alfresco data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Alfresco site\. You store your Alfresco credentials in an AWS Secrets Manager secret\. The credentials are user name and password of the Alfresco account\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user name",
    "password": "password"
}
```

Amazon Kendra also crawls user and group information from the Alfresco instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [ User context filtering for Alfresco data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-alfresco)\.

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of comments of Alfresco blogs and other content\. Each comment is indexed as a separate document\.
+ Inclusion or exclusion patterns: If you specify an inclusion pattern, only content that matches the inclusion pattern is indexed\. Any document with a file name or file type that doesn't match the pattern will not be indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Alfresco fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.