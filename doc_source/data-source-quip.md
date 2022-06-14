--------

--------

# Using a Quip data source<a name="data-source-quip"></a>

You can use your Quip file system as a data source for Amazon Kendra\. To use Quip in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Quip\.

When you connect to Quip to index your documents, you specify the Quip site domain\. You can specify regular expression patterns to include or exclude specific documents in your Quip\.

You must create an index before you create the Quip data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Quip, you specify the connection and other information in the console or by using the [QuipConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_QuipConfiguration.html) object\. You provide the Quip site domain for the Quip content you want to index\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Quip domain\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Quip data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Quip\. See [Authentication](https://docs.aws.amazon.com/kendra/latest/dg/data-source-quip.html#quip-authentication)\.

Amazon Kendra also crawls user and group information from the Quip instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Quip data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-quip)\.

You also can add the following optional information:
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Quip fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="quip-authentication"></a>

The authentication credentials to access your Quip data source must include your Quip token\. You create the token in Quip\. You store your Quip credentials in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{ 
        "accessToken" : "token"
}
```

**To create a personal access token in Quip**

1. Open https://\[subdomain\.domain\]/dev/token URL on a web browser \(must be logged in before this step\)\. For example, *https://service\-serviceteam\-quip\-company\.com/dev/token*

1. Select your organization name from the dropdown at the top of the side menu, then select **Get Personal Access Token**\.

1. Copy the token\. You’ll need this when you create the Secrets Manager secret in the Quip data source\.