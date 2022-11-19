--------

--------

# Using an Amazon WorkDocs data source<a name="data-source-workdocs"></a>

Amazon WorkDocs is a secure content collaboration service for creating, editing, storing, and sharing content\. If you are a Amazon WorkDocs user, you can use Amazon Kendra to index your Amazon WorkDocs data source\.

You can connect Amazon Kendra to your Amazon WorkDocs data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [WorkDocsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WorkDocsConfiguration.html) API\.

Amazon WorkDocs is available in Oregon, North Virginia, Sydney, Singapore, and Ireland regions\.

For troubleshooting your Amazon Kendra WorkDocs data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-workdocs)
+ [Prerequisites](#prerequisites-workdocs)
+ [Connecting Amazon Kendra to your Amazon WorkDocs data source](#data-source-procedure-workdocs)
+ [Learn more](#workdocs-learn-more)

## Supported features<a name="supported-features-workdocs"></a>
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-workdocs"></a>

Before you can use Amazon Kendra to index your Amazon WorkDocs data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your WorkDocs data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have noted the Amazon WorkDocs directory ID \(organization ID\) for your Amazon WorkDocs repository\.

  You can find more information on how to configure your Amazon WorkDocs account on the [Amazon WorkDocs Documentation](/workdocs/latest/adminguide/what_is.html) page\.
+ \(Optional\) If you want to map attributes or custom index fields from your WorkDocs data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Amazon WorkDocs data source<a name="data-source-procedure-workdocs"></a>

To connect Amazon Kendra to your Amazon WorkDocs data source you must provide details of your Amazon WorkDocs credentials so that Amazon Kendra can access your data\. If you have not yet configured Amazon WorkDocs for Amazon Kendra see [Prerequisites](#prerequisites-workdocs)\.

### <a name="workdocs-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Amazon WorkDocs** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **WorkDocs**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

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

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Default data source fields**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ WorkDocsConfiguration API ]

**To connect Amazon Kendra to Amazon WorkDocs**

You must specify the following using the [WorkDocsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WorkDocsConfiguration.html) API:
+ **Amazon WorkDocs directory ID**—You must specify the organization ID of your Amazon WorkDocs directory\. You can find the organization ID in the AWS Directory Service by going to **Active Directory** and then **Directories**\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the WorkDocs connector and Amazon Kendra\. For more information, see [IAM roles for WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Change log**—Whether Amazon Kendra should use the WorkDocs data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the WorkDocs data source than to process the change log\. If you are syncing your WorkDocs data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—You can specify whether to include documents and document comments\. You can also specify regular expression patterns to include or exclude documents and document comments\. Each comment is indexed as a separate document\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your WorkDocs data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="workdocs-learn-more"></a>

To learn more about integrating Amazon Kendra with your WorkDocs data source, see:
+ [Get started with the Amazon Kendra Amazon WorkDocs connector](https://aws.amazon.com/blogs/machine-learning/get-started-with-the-amazon-kendra-amazon-workdocs-connector/)