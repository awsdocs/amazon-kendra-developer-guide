--------

--------

# Amazon WorkDocs<a name="data-source-workdocs"></a>

Amazon WorkDocs is a secure content collaboration service for creating, editing, storing, and sharing content\. You can use Amazon Kendra to index your Amazon WorkDocs data source\.

You can connect Amazon Kendra to your Amazon WorkDocs data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [WorkDocsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WorkDocsConfiguration.html) API\.

Amazon WorkDocs is available in Oregon, North Virginia, Sydney, Singapore, and Ireland regions\.

For troubleshooting your Amazon Kendra WorkDocs data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-workdocs)
+ [Prerequisites](#prerequisites-workdocs)
+ [Connection instructions](#data-source-procedure-workdocs)
+ [Learn more](#workdocs-learn-more)

## Supported features<a name="supported-features-workdocs"></a>

Amazon Kendra WorkDocs data source connector supports the following features:
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-workdocs"></a>

Before you can use Amazon Kendra to index your WorkDocs data source, make these changes in your WorkDocs and AWS accounts\.

**In WorkDocs, make sure you have:**
+ Noted the Amazon WorkDocs directory ID \(organization ID\) for your Amazon WorkDocs repository\.
+ Checked each document is unique in WorkDocs and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.

If you don’t have an existing IAM role, you can use the console to create a new IAM role when you connect your WorkDocs data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and an index ID\.

## Connection instructions<a name="data-source-procedure-workdocs"></a>

To connect Amazon Kendra to your WorkDocs data source, you must provide the necessary details of your WorkDocs data source so that Amazon Kendra can access your data\. If you have not yet configured WorkDocs for Amazon Kendra see [Prerequisites](#prerequisites-workdocs)\.

### <a name="workdocs-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Amazon WorkDocs** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **WorkDocs connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Organization ID specific to your Amazon WorkDocs site**—Select the ID of the Amazon WorkDocs site you want to index\. You must already have created a site\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Crawl document comments**—The Amazon WorkDocs entities or content types you want to crawl\.

   1. **Use change logs**—Select to update your index instead of syncing all your files\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync run schedule** for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Default data source fields**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Amazon WorkDocs**

You must specify the following using the [WorkDocsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WorkDocsConfiguration.html) API:
+ **Amazon WorkDocs directory ID**—Specify the organization ID of your Amazon WorkDocs directory\. You can find the organization ID in the AWS Directory Service by going to **Active Directory** and then **Directories**\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access the WorkDocs dirtectory and to call the required public APIs for the WorkDocs connector and Amazon Kendra\. For more information, see [IAM roles for WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Change log**—Whether Amazon Kendra should use the WorkDocs data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the WorkDocs data source than to process the change log\. If you are syncing your WorkDocs data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—Specify whether to include or exclude certain documents and document comments\. Each comment is indexed as a separate document\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your WorkDocs data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------

## Learn more<a name="workdocs-learn-more"></a>

To learn more about integrating Amazon Kendra with your WorkDocs data source, see:
+ [Get started with the Amazon Kendra Amazon WorkDocs connector](https://aws.amazon.com/blogs/machine-learning/get-started-with-the-amazon-kendra-amazon-workdocs-connector/)