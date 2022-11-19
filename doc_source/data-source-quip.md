--------

--------

# Using a Quip data source<a name="data-source-quip"></a>

Quip is a collaborative productivity software that offers real time document\-authoring capabilities\. If you are a Quip user, you can use Amazon Kendra to index your Quip folders, files, file comments, chatrooms, and attachments\.

You can connect Amazon Kendra to your Quip data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [QuipConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_QuipConfiguration.html) API\.

For troubleshooting your Amazon Kendra Quip data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-quip)
+ [Prerequisites](#prerequisites-quip)
+ [Connecting Amazon Kendra to your Quip data source](#data-source-procedure-quip)
+ [Learn more](#quip-learn-more)

## Supported features<a name="supported-features-quip"></a>
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-quip"></a>

Before you can use Amazon Kendra to index your Quip data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your Quip data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have a Quip administrative account in which you have created Quip authentication credentials that include a personal access token\.
+ You have copied your Quip site domain\. For example, *https://quip\-company\.quipdomain\.com/browse* where *quipdomain* is the domain\.

  You can find more information on how to configure your Quip account on the [Quip Developer Documentation](https://quip.com/dev) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your Quip data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your Quip data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Quip data source<a name="data-source-procedure-quip"></a>

To connect Amazon Kendra to your Quip data source you must provide details of your Quip credentials so that Amazon Kendra can access your data\. If you have not yet configured Quip for Amazon Kendra see [Prerequisites](#prerequisites-quip)\.

### <a name="quip-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Quip** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Quip**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Quip domain name**—Enter the Quip you copied from your Quip account\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Quip authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Quip\-’ is automatically added to your secret name\.

         1. **Quip token**—Enter the Quip personal access token you generated and downloaded from your Quip account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Add Quip folder IDs to crawl**—The Quip folder IDs you want to crawl\.

   1. **Additional configuration \(content types\)**—Enter the content types you want to crawl\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Threads**, and **Messages**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ QuipConfiguration API ]

**To connect Amazon Kendra to Quip**

You must specify the following using [QuipConfiguration ](https://docs.aws.amazon.com/kendra/latest/dg/API_QuipConfiguration.html) API:
+ **Quip site domain**—For example, *https://quip\-company\.quipdomain\.com/browse* where *quipdomain* is the domain\.
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Quip account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "accessToken": "token"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for Quip data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Quip connector and Amazon Kendra\. For more information, see [IAM roles for Quip data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—You can choose to specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Inclusion and exclusion filters**—You can specify whether to include files, comments, chatrooms, threads, messages, and assignments\. You can also specify regular expression patterns to include or exclude files, comments, chatrooms, threads, messages, and assignments\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Quip data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your Quip data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="quip-learn-more"></a>

To learn more about integrating Amazon Kendra with your Quip data source, see:
+ [Search for knowledge in Quip documents with intelligent search using the Quip connector for Amazon Kendra](https://aws.amazon.com/blogs/machine-learning/search-for-knowledge-in-quip-documents-with-intelligent-search-using-the-quip-connector-for-amazon-kendra/)