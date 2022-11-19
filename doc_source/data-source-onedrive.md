--------

--------

# Using a OneDrive data source<a name="data-source-onedrive"></a>

Microsoft OneDrive is cloud storage service that you can use to store, share, and host your content\. If you are a OneDrive user, you can use Amazon Kendra to index your OneDrive data source\.

You can connect Amazon Kendra to your OneDrive data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/OneDriveConfiguration.html) API\.

For troubleshooting your Amazon Kendra OneDrive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-onedrive)
+ [Prerequisites](#prerequisites-onedrive)
+ [Connecting Amazon Kendra to your OneDrive data source](#data-source-procedure-onedrive)

## Supported features<a name="supported-features-onedrive"></a>
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-onedrive"></a>

Before you can use Amazon Kendra to index your OneDrive data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your OneDrive data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have created an Azure Active Directory \(AD\) application and used the AD application ID to register a secret key for the application on the AD site\. The secret key must contain the following credentials:
  + application ID
  + secret key

  You need this information to connect to Amazon Kendra\.
+ You have copied the Azure Active Directory domain of the organization\. You need this information to connect to Amazon Kendra\.
+ You have added the following permissions to your Azure Active Directory application on the Microsoft Graph option:
  + Read files in all site collections \(File\.Read\.All\)
  + Read all users' full profile \(User\.Read\.All\)
  + Read directory data \(Directory\.Read\.All\)
  + Read all groups \(Group\.Read\.All\)
  + Read items in all site collections \(Site\.Read\.All\)

  You can find more information on how to configure your OneDrive account on the [Microsoft OneDrive Developer Documentation](https://learn.microsoft.com/en-us/onedrive/developer/?view=odsp-graph-online) page\.
+ You have copied the list of users whose documents must be indexed\. You can choose to provide a list of user names, or you can provide the user names in a file stored in an Amazon S3 bucket\. If you store the list of user names in an Amazon S3 bucket, the IAM policy for the data source must provide access to the bucket and access to the key that the bucket was encrypted with, if any\. After you create the data source, you can:
  + Modify the list of users\.
  + Change from a list of users to a list stored in an Amazon S3 bucket\.
  + Change the Amazon S3 bucket location of a list of users\. If you change the bucket location, you must also update the IAM role for the data source so that it has access to the bucket\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your OneDrive data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your OneDrive data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your OneDrive data source<a name="data-source-procedure-onedrive"></a>

To connect Amazon Kendra to your OneDrive data source you must provide details of your OneDrive credentials so that Amazon Kendra can access your data\. If you have not yet configured OneDrive for Amazon Kendra see [Prerequisites](#prerequisites-onedrive)\.

### <a name="onedrive-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to OneDrive** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **OneDrive**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **OneDrive tenant domain**—Enter the OneDrive tenant domain without the protocol\.

   1. **Type of authentication**—Choose between **New** and **Existing**\.

   1. 

      1. If you choose **Existing**, select an existing secret for **Select secret**\.

      1. If you choose **New**, enter following information in the **New AWS Secrets Manager secret** section:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-OneDrive\-’ is automatically added to your secret name\.

         1. For **Application ID** and **Application password**—Enter the authentication credential values you generated and downloaded from your OneDrive account and then choose **Save authentication**\. 

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. Choose between **List file** and **Names list** based on your use case\.

      1. If you choose **List file**, enter the following information:

         1.  **Select location**—Enter the path to your Amazon S3 bucket\. 

            **Add user list file to Amazon S3**—Select to add your user list files to your Amazon S3 bucket\. 

            **User local group mappings**—Select to use local group mapping to filter your content\.

      1. If you choose **Names list**, enter the following information:

         1.  **User name**—Enter up to 10 user drives to index\. To add more than 10 users, create a file that contains the names\.

            **Add another**—Choose to add more users\.

            **User local group mappings**—Select to use local group mapping to filter your content\.

   1. For **Additional configurations**— Add regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Default data source fields** and **Additional suggested field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ OneDriveConfiguration API ]

**To connect Amazon Kendra to OneDrive**

You must specify the following using the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/OneDriveConfiguration.html) API:
+ **Tenant Domain**—You must specify the Azure Active Directory domain of the organization\.
+ **OneDrive Users**—You must specify the list of user accounts whose documents should be indexed\.
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your OneDrive account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "username": "azure active directory application ID",
      "password": "secret key"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the OneDrive connector and Amazon Kendra\. For more information, see [IAM roles for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—You can specify whether to include certain documents\. You can also specify regular expression patterns to include or exclude documents to be indexed\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your OneDrive data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------