--------

--------

# Slack<a name="data-source-slack"></a>

Slack is an enterprise communications app that lets users send messages and attachments through various public and private channels\. You can use Amazon Kendra to index your Slack public and private channels, bot and archive messages, files and attachments, direct and group messages\. You can also choose specific content to filter\.

You can connect Amazon Kendra to your Slack data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [SlackConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SlackConfiguration.html) API\.

For troubleshooting your Amazon Kendra Slack data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-slack)
+ [Prerequisites](#prerequisites-slack)
+ [Connection instructions](#data-source-procedure-slack)
+ [Learn more](#slack-learn-more)

## Supported features<a name="supported-features-slack"></a>

Amazon Kendra Slack data source connector supports the following features:
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-slack"></a>

Before you can use Amazon Kendra to index your Slack data source, make these changes in your Slack and AWS accounts\.

**In Slack, make sure you have:**
+ Created a Slack Bot User OAuth token or Slack User OAuth token\. You can choose either token to connect Amazon Kendra to your Slack data source\. See [Slack documentation on access tokens](https://api.slack.com/authentication/token-types) for more information\.
**Note**  
If you use the bot token as part of your Slack credentials, you cannot index direct messages and group messages and you must add the bot token to the channel you want to index\.
+ Noted your Slack workspace team ID from your Slack workspace main page URL\. For example, *https://app\.slack\.com/client/T0123456789/\.\.\. * where *T0123456789* is the team ID\.
+ Added the following \[Oauth scopes/ read\] permissions:
  + channels:history
  + channels:read
  + groups:history
  + groups:read
  + im:history
  + mpim:history
  + mpim:read
  + team:read
  + users\.profile:read
  + users:read
  + emoji:read
  + files:read
  + usergroups:read
+ Checked each document is unique in Slack and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Slack authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Slack data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-slack"></a>

To connect Amazon Kendra to your Slack data source, you must provide the necessary details of your Slack data source so that Amazon Kendra can access your data\. If you have not yet configured Slack for Amazon Kendra see [Prerequisites](#prerequisites-slack)\.

### <a name="slack-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Slack** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **Slack connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Slack workspace team ID**—The team ID of your Slack workspace\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Slack authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Slack\-’ is automatically added to your secret name\.

         1. For **Slack token**—Enter the authentication credential values you created in your Slack account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Select type of content to crawl**—The Slack entities or content types you want to crawl\.

   1. **Change log**—Select to update your index instead of syncing all your files\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. **Select crawl start date**—What date Amazon Kendra will start crawling your data from\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Slack field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Slack**

You must specify the following using [SlackConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SlackConfiguration.html) API:
+ **Slack workspace team ID**—The Slack team ID you copied from your Slack main page URL\.
+ **List of entities to index**—Whether Amazon Kendra should index your public and private channels, and your group and direct messages\.
+ **Crawl date**—The date to start crawling your data from your Slack workspace team\. The date must follow this format: yyyy\-mm\-dd\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your Slack account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "slackToken": "token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Slack connector and Amazon Kendra\. For more information, see [IAM roles for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+ **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` as part of the data source configuration\. See [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.
+  **Change log**—Whether Amazon Kendra should use the Slack data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Slack data source than to process the change log\. If you are syncing your Slack data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—Specify whether to include or exclude certain public and private channels, group and private messages, and bot and archived messages\. If you use a bot token as part of your Slack authentication credentials, you must add the bot token to the channel you want to index\. You cannot index direct messages and group messages using a bot token\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Slack data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------

## Learn more<a name="slack-learn-more"></a>

To learn more about integrating Amazon Kendra with your Slack data source, see:
+ [Unravel the knowledge in Slack workspaces with intelligent search using the Amazon Kendra Slack connector](https://aws.amazon.com/blogs/machine-learning/unravel-the-knowledge-in-slack-workspaces-with-intelligent-search-using-the-amazon-kendra-slack-connector/)