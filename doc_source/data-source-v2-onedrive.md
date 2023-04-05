--------

--------

# Microsoft OneDrive connector v2\.0<a name="data-source-v2-onedrive"></a>

Microsoft OneDrive is cloud\-based storage service that you can use to store, share, and host your content\. You can use Amazon Kendra to index your OneDrive data source\.

You can connect Amazon Kendra to your OneDrive data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/OneDriveConfiguration.html) API\. 



**Note**  
Support for OneDrive Connector v1\.0 / OneDriveConfiguration API is scheduled to end by June 2023\. We recommend using OneDrive Connector v2\.0 / TemplateConfiguration API\. Version 2\.0 provides additional ACLs and identity crawler functionality\.

For troubleshooting your Amazon Kendra OneDrive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v2-onedrive)
+ [Prerequisites](#prerequisites-v2-onedrive)
+ [Connection instructions](#data-source-procedure-v2-onedrive)

## Supported features<a name="supported-features-v2-onedrive"></a>

Amazon Kendra OneDrive data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-v2-onedrive"></a>

Before you can use Amazon Kendra to index your OneDrive data source, make these changes in your OneDrive and AWS accounts\.

**In your Azure Active Directory \(AD\), make sure you have:**
+ Created an Azure Active Directory \(AD\) application\.
+ Used the AD application ID to register a secret key for the application on the AD site\. The secret key must contain the application ID and a secret key\.
+ Copied the AD domain of the organization\.
+ Added the following permissions to your AD application on the Microsoft Graph option:
  + Read files in all site collections \(File\.Read\.All\)
  + Read all users' full profiles\(User\.Read\.All\)
  + Read all groups \(Group\.Read\.All\)
  + Read all notes \(Notes\.Read\.All\)

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your OneDrive authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your OneDrive data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index id\.

## Connection instructions<a name="data-source-procedure-v2-onedrive"></a>

To connect Amazon Kendra to your OneDrive data source you must provide details of your OneDrive credentials so that Amazon Kendra can access your data\. If you have not yet configured OneDrive for Amazon Kendra, see [Prerequisites](#prerequisites-v2-onedrive)\.

### <a name="onedrive-v2-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to OneDrive** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **OneDrive connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **OneDrive tenant ID**—Enter the OneDrive tenant ID without the protocol\.

   1. **Type of authentication**—Choose between **New** and **Existing**\.

   1. 

      1. If you choose **Existing**, select an existing secret for **Select secret**\.

      1. If you choose **New**, enter following information in the **New AWS Secrets Manager secret** section:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-OneDrive\-’ is automatically added to your secret name\.

         1. For **Client ID** and **Client Secret**—Enter the client ID and client secret and then select **Save authentication**\. 

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information: 

1. 

   1. For **Sync scope**—Choose which users' OneDrive data to index\. You can add a maximum of 10 users manually\.

   1. For **Additional configurations**—Add regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync mode**, choose how you want to update your index when your data source content changes\. **Full sync** indexes all contents, regardless of the previous sync status\. **New, modified or deleted documents sync** only syncs the new, modified, or deleted documents\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Default data source fields** and **Additional suggested field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to OneDrive**

You must specify the following using the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/OneDriveConfiguration.html) API:
+ **Tenant ID**—Tenant ID is used to connect to Microsoft OneDrive\.
+ **OneDrive Users**—Specify the list of user accounts whose documents should be indexed\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your OneDrive account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "client Id": "client ID",
      "clientSecret": "client Secret"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the OneDrive connector and Amazon Kendra\. For more information, see [IAM roles for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—Specify whether to include certain documents\. You can also specify regular expression patterns to include or exclude documents to be indexed\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—Choose to map your OneDrive data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------