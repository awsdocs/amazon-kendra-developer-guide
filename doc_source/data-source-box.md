--------

--------

# Using a Box data source<a name="data-source-box"></a>

You can use your Box content platform as a data source for Amazon Kendra\. To use Box in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Box\.

When you connect to Box to index your documents, you specify the Box enterprise ID\. For example, *801234567*\. You can specify regular expression patterns to include or exclude specific files and folders within in your Box platform\. You also can specify whether to include web links, comments, and tasks with your files\.

You must create an index before you create the Box data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Box, you specify the connection and other information in the console or by using the [BoxConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_BoxConfiguration.html) object\. You can find the enterprise ID in the Box Developer Console settings or when you create an app in Box and download your authentication credentials\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Box platform\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Box data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Box platform\. See [Authentication](#box-authentication)\.

Amazon Kendra also crawls user and group information from the Box instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Box data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-box)\.

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of comments of your documents\. Each comment is indexed as a separate document\.
+ Whether Amazon Kendra should use the Box change log mechanism to determine if content must be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the content\. If your change log is large, it might take Amazon Kendra less time to scan content in Box than to process the change log\. If you are syncing your Box data source with your index for the first time, all content is scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any file, document, or folder that doesn't match the pattern is not indexed\. If you specify an inclusion and exclusion pattern, content that matches the exclusion pattern isn't indexed even if it matches the inclusion pattern\.
+ Field mappings that map your Box fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="box-authentication"></a>

The authentication credentials to access your Box platform must include the following:
+ client ID
+ client secret
+ public key ID
+ private key
+ passphrase

You create an app in the Box Developer Console to generate these credentials\. You store your Box credentials in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{ 
            "clientID" : "client-id",
            "clientSecret" : "client-secret",
            "publicKeyID" : "public-key-id",
            "privateKey" : "private-key",
            "passphrase" : "pass-phrase"          
}
```

**To create an app in Box**

1. Log in to [developer\.box\.com](https://developer.box.com/) desktop application\. You must be a user with administrative permissions or have your app approved by a user with administrative permissions\.

1. Select **My Apps** from the navigation menu, and then select **Create New App**\.

1. Choose **Server Authentication \(with JWT\)**\.

1. Enter a name for your app\. For example, *kendra\_box\_app*\. Then select **Create app**\.

1. In your created app in **My Apps**, select the **Configuration** tab\.

1. In the **App Access Level** section, choose **App \+ Enterprise Access**\.

1. In the **Application Scopes** section, choose the following permissions:
   + Write all files and folders stored in a Box
   + Manage users
   + Manage groups
   + Manage enterprise properties

1. In the **Advanced Features** section, choose **Make API calls using the as\-user header**\.

1. In the **Add and Manage Public Keys** section, select **Add a Public Key**\. You first must create two\-factor authentication\. You can do this by selecting **Settings** in the pop\-up window or by going to your account settings and creating two\-factor authentication\.

1. Select **Generate a Public/Private Keypair**, then select **Download as JSON**\.

1. Go to your downloads directory on your computer and open the config\.json file\. Copy the client ID, client secret, public key ID, private key, and passphrase\. You'll need this when you create the Secrets Manager secret for the Box data source\.