--------

--------

# Using a Dropbox data source<a name="data-source-dropbox"></a>

You can use your Dropbox, including Dropbox Advanced for Dropbox Business, as a data source for Amazon Kendra\. To use Dropbox in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index, and then select **Data sources** from the navigation menu to add Dropbox\.

For troubleshooting your Amazon Kendra Dropbox data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

Create an index before you create the Dropbox data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

Before you can index your documents from your Dropbox, you must have administrative permissions for the Dropbox account\.

When you connect to Dropbox to index your documents, you specify the Dropbox app key, which you create in the Dropbox developer console\. The Dropbox app key information is used to connect to your Dropbox and is part of the secret that stores your authentication credentials\.

See [Authentication](#dropbox-authentication) for information on how to create a Dropbox app\.

You can specify regular expression patterns to include or exclude specific files in your Dropbox\. You can specify whether to index your files, Dropbox Paper and Dropbox Paper templates, and your stored shortcuts to webpages\.

To connect to Dropbox, specify the connection and other information in the console or use the [ TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You include a JSON that contains the data source schema as part of the template configuration\. You provide the Dropbox app key as part of your secret that stores your authentication credentials\. Also specify the type of data source as `DROPBOX`, the type of access token you want to use \(temporary or permanent\), and a secret for your authentication credentials as part of the repository configuration details\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. To view the template schema, see [Data source schemas](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Dropbox\. You provide the ARN of an IAM role using the [CreateDataSource API](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. For more information on permissions, see [IAM roles for Dropbox data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Dropbox\. See [Authentication](#dropbox-authentication)\.

Amazon Kendra also crawls user and group information from the Dropbox instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Dropbox data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

You also can add the following optional information:
+ Whether Amazon Kendra should use the Dropbox change log mechanism to determine if a document must be added, updated, or deleted in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in Dropbox than to process the change log\. If you are syncing your Dropbox data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion patterns: If you specify an inclusion pattern, only content that matches the inclusion pattern is indexed\. Any file that doesn’t match the inclusion pattern isn’t indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Dropbox fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="dropbox-authentication"></a>

The authentication credentials to access your Dropbox must include the following:
+ app key
+ app secret
+ acess token or refresh token

You create an app in the Dropbox Developer Portal to provide the required credentials\. You store your Dropbox credentials as a secret in AWS Secrets Manager\. It's recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. 

If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. You can also store the credentials in an existing secret in Secrets Manager\. If you are using the API to create your data source, you must provide the Amazon Resource Number \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in Secrets Manager\.

```
{
    "appKey": "Dropbox app key",
    "appSecret": "Dropbox app secret",
    "accesstoken": "temporary access token or refresh access token",
}
```

**Note**  
It's recommended that you create a Dropbox refresh access token that never expires, rather that relying on a one\-time acess token that expires after 4 hours\. You create an app and a refresh access token in the Dropbox developer console and provide your access token in your secret\. A refresh access token is permanent and never expires so that you can continue to sync your data source in the future\.

**To create an app in Dropbox**

1. Log in at [Dropbox Developer Portal](https://www.dropbox.com/developers)\. You must be a user with administrative permissions\.

1. Select **App console**, then go to **My apps** and select **Create app**\.

1. Check the radio button **Scoped access**, then check the option for full Dropbox permissions\.

1. In the **Name your app** field, enter a name for your app\. Your app name must follow the [Dropbox branding guidelines](https://www.dropbox.com/developers/reference/branding-guide) for Dropbox to approve the use of your Dropbox app\.

1. Select **Create app**\. You are directed to your app console main page\.

1. Select the **Permissions** tab and choose the following permissions:
   + files\.content\.read
   + files\.metadata\.read
   + sharing\.read
   + file\_requests\.read
   + groups\.read
   + team\_info\.read
   + team\_data\.content\.read

1. Select the **Settings** tab and copy the **App key** value\. You'll need this when you create the Secrets Manager secret for the Dropbox data source\.

1. In the **Settings** for **App secret**, select **Show** to reveal the secret\. Copy the secret\. You'll need this when you create the Secrets manager secret for the Dropbox data source\.

1. In **Settings** for **OAuth2**, select **Generate** under **Generate access token**\. Copy the access token\. You'll need this when you create the Secrets Manager secret for the Dropbox data source\. The token is for temporary use and expires after 4 hours\.

**To create a refresh token in Dropbox**

Generating an access token in your Dropbox app settings in the console provides a token for temporary use, which expires after 4 hours\. To use a more permanent access token that never expires, you must use an authorization code and request offline access\.

1. Open your browser window and enter the following URL using your app key that you copied from your app settings in the Dropbox app console: `https://www.dropbox.com/oauth2/authorize?token_access_type=offline&response_type=code&client_id= (https://www.dropbox.com/oauth2/authorize?token_access_type=offline&response_type=code&client_id=<App key>`\. The URL returns an authorization code\. Copy this code\.

1. In a terminal window, run the following curl command\. Use the authorization code that you copied earlier, plus your app key and secret that you copied from your settings in the Dropbox app console: `curl https://api.dropbox.com/oauth2/token -d code=<authorization code> -d grant_type=authorization_code -u <App key>:<App secret>`\.

   This returns a refresh token stored in a JSON string\. Copy this refresh toke to include in your JSON string in Secrets Manager\.

   ```
   {
       "appKey": "Dropbox app key",
       "appSecret": "Dropbox app secret",
       "accesstoken": "temporary access token or refresh access token",
   }
   ```

**Note**  
To regenerate your access token, run the following curl command\. Use the refresh token that you copied earlier plus your app key and secret that you copied from your settings in the Dropbox app console: `https://api.dropbox.com/oauth2/token -d grant_type=refresh_token -d refresh_token=<refresh token> -u <App key>:<App secret>`\.