--------

--------

# Microsoft Exchange<a name="data-source-exchange"></a>

Microsoft Exchange is an enterprise collaboration tool for messaging, meetings and file sharing\. If you are a Microsoft Exchange user, you can use Amazon Kendra to index your Microsoft Exchange data source\.

You can connect Amazon Kendra to your Microsoft Exchange data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\.

For troubleshooting your Amazon Kendra Microsoft Exchange data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

## Supported features<a name="supported-features-exchange"></a>
+ Field mappings
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)
+ Sync all documents/Sync only new, modified, or deleted documents

## Prerequisites<a name="prerequisites-exchange"></a>

Before you can use Amazon Kendra to index your Microsoft Exchange data source, make these changes in your Microsoft Exchange and AWS accounts\.

**In Microsoft Exchange, make sure you have:**
+ Created a Microsoft Exchange account in Office 365\.
+ Copied your Microsoft 365 tenant ID\. You can find your tenant ID in the **Properties** of your Azure Active Directory Portal\. See [Find your Microsoft 365 tenant ID](https://learn.microsoft.com/en-us/sharepoint/find-your-office-365-tenant-id) for more details\.
+ Configured an OAuth 2\.0 credential token containing a client ID and client secret\.
+ Added the following permissions for the connector application:
  + Calendars\.Read
  + Mail\.Read
  + Mail\.ReadBasic
  + Mail\.ReadBasic\.All
  + User\.Read\.All
  + Contacts\.Read
  + Directory\.Read\.All
  + Contacts\.Read
  + Notes\.Read\.All
+ Checked each document is unique in Microsoft Exchange and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Microsoft Exchange authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Microsoft Exchange data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-exchange"></a>

To connect Amazon Kendra to your Microsoft Exchange data source, you must provide the necessary details of your Microsoft Exchange data source so that Amazon Kendra can access your data\. If you have not yet configured Microsoft Exchange for Amazon Kendra see [Prerequisites](#prerequisites-exchange)\.

### <a name="exchange-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Microsoft Exchange** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **Microsoft Exchange connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Source**—Enter your Microsoft 365 tenant ID\. You can find your tenant ID in the Properties of your Azure Active Directory Portal\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Microsoft Exchange authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix 'AmazonKendra\-Microsoft Exchange 

         1. For **Client ID** and **Client secret**—Enter the authentication credential values you created in your Microsoft Exchange account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **Identity crawler**—Choose to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Sync contents**—Select contents to sync\.

   1. **Additional configuration**—You can optionally use these options to index certain content instead of syncing all the documents\.

   1. **Sync mode**—You can choose how you want to update your index when your data source content changes\.

      1. If you choose full sync, Amazon Kendra will sync all contents in all entities, regardless of the previous sync status\.

      1. If you choose new or modified content sync, Amazon Kendra will only sync new or modified content\.

      1.  If you choose new, modified or deleted content sync, Amazon Kendra will only sync new, modified or deleted content\.

1. On the **Set field mappings** page, enter the following information:

   1. **Default data source fields**—Select from the Amazon Kendra generated default data source fields you want to map to your index\.

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Microsoft Exchange**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **Data source**—You must specify the data source as `MSEXCHANGE`\.
+ **Tenant ID**—You can find your tenant ID in the Properties of your Azure Active Directory Portal\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your Microsoft Exchange account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "client Id": "client ID",
      "client Secret": "client Secret",
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Microsoft Exchange connector and Amazon Kendra\. For more information, see [IAM roles for Microsoft Exchange data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+ **Identity crawler**— When the identity crawler is activated, Amazon Kendra syncs identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.
+ 
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Microsoft Exchange data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="exchange-learn-more"></a>

To learn more about integrating Amazon Kendra with your Microsoft Exchange data source, see:
+ [Index your Microsoft Exchange content using the Exchange connector for Amazon Kendra](https://aws.amazon.com/blogs/machine-learning/index-your-microsoft-exchange-content-using-the-exchange-connector-for-amazon-kendra/)