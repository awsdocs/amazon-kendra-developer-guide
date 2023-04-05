--------

--------

# Google Drive connector v1\.0<a name="data-source-v1-google-drive"></a>

Google Drive is a cloud\-based file storage service\. You can use Amazon Kendra to index documents and comments stored in shared drives, My Drives, and Shared with me folders in your Google Drive data source\. You can index Google Workspace documents, as well as documents listed in [Types of documentation](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\. You can also use inclusion and exclusion filters to index content by file name, file type, and file path\.

**Note**  
Support for Google Drive connector v1\.0 / GoogleDriveConfiguration API is scheduled to end by June 2023\. We recommend using Google Drive connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Google Drive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v1-google-drive)
+ [Prerequisites](#prerequisites-v1-google-drive)
+ [Connection instructions](#data-source-v1-procedure-google-drive)
+ [Learn more](#google-drive-learn-more)

## Supported features<a name="supported-features-v1-google-drive"></a>
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-v1-google-drive"></a>

Before you can use Amazon Kendra to index your Google Drive data source, make these changes in your Google Drive and AWS accounts\.

**In Google Drive, make sure you have:**
+ **Either** been granted access by a super admin role **or** are a user with administrative privileges\. You do not need a super admin role for yourself if you have been granted access by a super admin role\.
+ Created a service account with **Enable G Suite Domain\-wide Delegation** activated and a JSON key as private key using the account\.
+ Copied your user account email and your service account email\. When you connect to Amazon Kendra you enter your user account email as admin account email and your service account email as client email in your Secrets Manager secret\.
+ Added Admin SDK API and Google Drive API in your account\.
+ Added \(or asked a user with a super admin role to add\) the following permissions to your service account using a super admin role:
  + https://www\.googleapis\.com/auth/drive\.readonly
  + https://www\.googleapis\.com/auth/drive\.metadata\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.user\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.group\.readonly
+ Checked each document is unique in Google Drive and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Google Drive authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Google Drive data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-v1-procedure-google-drive"></a>

To connect Amazon Kendra to your Google Drive data source, you must provide the necessary details of your Google Drive data source so that Amazon Kendra can access your data\. If you have not yet configured Google Drive for Amazon Kendra see [Prerequisites](#prerequisites-v1-google-drive)\.

### <a name="google-drive-v1-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Google Drive** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **Google Drive V1 Connector **, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. For **Type of authentication**—Choose between **Existing** and **New**\. If you choose to use an existing secret, use **Select secret** to choose your secret\.

   1. If you choose to create a new secret an AWS Secrets Manager secret option opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

        1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Google Drive\-’ is automatically added to your secret name\.

        1. For **Admin account email**, **Client email**, and **Private key**—Enter the authentication credential values you generated and downloaded from your Google Drive account\. 

        1. Choose **Save authentication**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Exclude user accounts**—The Google Drive users you want to exclude from the index\. You can add up to 100 user accounts\.

   1. **Exclude shared drives**—The Google Drive shared drives you want to exclude from your index\. You can add up to 100 shared drives\.

   1. **Exclude file types drives**—The Google Drive file types you want to exclude from your index\. You can also choose to edit MIME type selections\.

   1. **Additional configurations**—Regular expression patterns to include or exclude certain content\. You can add up to 100 patterns\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **GoogleDrive field name** and **Additional suggested field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Google Drive**

You must specify the following using the [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) API:
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your Google Drive account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "clientAccount": "service account email",
      "adminAccount": "user account email",
      "privateKey": "private key"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Google Drive connector and Amazon Kendra\. For more information, see [IAM roles for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—By default Amazon Kendra indexes all documents in Google Drive\. You can specify whether to include or exclude certain content in shared drives, user accounts, document MIME types, and files\. If you choose to exclude user accounts, none of the files in the My Drive owned by the account are indexed\. Files shared with the user are indexed unless the owner of the file is also excluded\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Google Drive data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------

## Learn more<a name="google-drive-learn-more"></a>

To learn more about integrating Amazon Kendra with your Google Drive data source, see:
+ [Getting started with the Amazon Kendra Google Drive connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-the-amazon-kendra-google-drive-connector/)