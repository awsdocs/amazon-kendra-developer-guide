--------

--------

# Google Drive connector v2\.0<a name="data-source-v2-google-drive"></a>

Google Drive is a cloud\-based file storage service\. You can use Amazon Kendra to index documents and comments stored in shared drives, My Drives, and Shared with me folders in your Google Drive data source\. You can index Google Workspace documents, as well as documents listed in [Types of documentation](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\. You can also use inclusion and exclusion filters to index content by file name, file type, and file path\.

**Note**  
Support for Google Drive connector v1\.0 / GoogleDriveConfiguration API is scheduled to end by June 2023\. We recommend using Google Drive connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Google Drive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v2-google-drive)
+ [Prerequisites](#prerequisites-v2-google-drive)
+ [Connection instructions](#data-source-procedure-v2-google-drive)
+ [Notes](#google-drive-notes)

## Supported features<a name="supported-features-v2-google-drive"></a>
+ Field mappings
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Sync all documents/ Sync only new, modified, or deleted documents
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-v2-google-drive"></a>

Before you can use Amazon Kendra to index your Google Drive data source, make these changes in your Google Drive and AWS accounts\.

**In Google Drive, make sure you have:**
+ **Either** been granted access by a super admin role **or** are a user with administrative privileges\. You do not need a super admin role for yourself if you have been granted access by a super admin role\.
+ Created a service account with **Enable G Suite Domain\-wide Delegation** activated and generated a JSON private key using the account\.
+ Added Admin SDK API and Google Drive API in your user account\.
+ Configured Google Drive Service Account connection credentials containing your admin account email, client email \(service account email\), and private key\. See [Google Cloud documentation on creating and deleting service account keys](https://cloud.google.com/iam/docs/keys-create-delete)\.
+ **Optional:** Configured an OAuth 2\.0 credential token that can identify Amazon Kendra and generate a OAuth client id, a client secret, and a refresh token as connection credentials\. See [Google documentation on using OAuth 2\.0 to access APIs](https://developers.google.com/identity/protocols/oauth2)\.
+ Added \(or asked a user with a super admin role to add\) the following OAuth scopes to your service account using a super admin role:
  + https://www\.googleapis\.com/auth/drive
  + https://www\.googleapis\.com/auth/drive\.file
  + https://www\.googleapis\.com/auth/drive\.readonly
  + https://www\.googleapis\.com/auth/cloud\-platform
  + https://www\.googleapis\.com/auth/forms\.body\.readonly
  + https://www\.googleapis\.com/auth/drive\.metadata\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.user\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.group\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.user\.alias\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.userschema\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.group\.member\.readonly
+ Checked each document is unique in Google Drive and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Google Drive authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Google Drive data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-v2-google-drive"></a>

To connect Amazon Kendra to your Google Drive data source, you must provide the necessary details of your Google Drive data source so that Amazon Kendra can access your data\. If you have not yet configured Google Drive for Amazon Kendra see [Prerequisites](#prerequisites-v2-google-drive)\.

### <a name="google-drive-v2-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Google Drive** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index that you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **Google Drive V2**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. For **Authentication**—Choose between **Google service account** and **OAuth 2\.0 authentication** based on your use case\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Google Drive authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. If you chose **Google service account**, enter the **Secret Name**, **Admin account email**, **Client email**, and **Private Key** that you created in your service account and choose **Save and add secret**\.

      1. If you chose **OAuth 2\.0 authentication**, enter the details of **Secret Name**, **Client ID**, **Client secret** and **Refresh token** that you created in your service account and choose **Save and add secret**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. \(For Google service account authentication users only\) **Identity crawler**—Choose to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Sync contents**—Select to index **Comments**\. Files are crawled by default\.

   1. In **Additional configuration \- optional** enter the following optional information:

      1. **User email**—Add user emails you want to include or exclude\.

      1. **Shared drives**—Add the shared drive names you want to include or exclude\.

      1. **Mime types**—Add MIME types you want to include or exclude\.

      1. **Attachment regex patterns**—Add regular expression patterns to include or exclude certain attachments for all supported entities\. You can add up to 100 patterns\.

   1. For **Sync mode**, choose how you want to update your index when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.
      + **Full sync**—Sync all content regardless of the previous sync status\.
      + **New or modified documents sync**—Sync only new and modified documents\.
      + **New, modified, or deleted documents sync**—Sync only new, modified, and deleted documents\.
**Important**  
Google Drive API does not support retrieving comments from a permanently deleted file\. Comments from trashed files are retrievable\. When a file is trashed, the connector will delete comments from the Amazon Kendra index\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Files**—Select from the Amazon Kendra generated default data source fields you want to map to your index\.

   1. For **Comments**—Select from the Amazon Kendra generated default data source fields you want to map to your index\.
**Note**  
Google Drive API does not support creating custom fields\. Custom field mapping is not available for the Google Drive connector\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Google Drive**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **Data source**—Specify the data source as `GOOGLEDRIVEV2`\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Google Drive account\. If you use Google service account authentication, the secret is stored in a JSON structure with the following keys: 

  ```
  {
      "clientEmail": "service account email",
      "adminAccountEmail": "user account email",
      "privateKey": "private key"
  }
  ```

  If you use OAuth 2\.0 authentication, the secret is stored in a JSON structure with the following keys:

  ```
  {
      "clientID": "OAuth Client ID",
      "clientSecret": "client secret",
      "refreshToken": "refresh token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Google Drive connector and Amazon Kendra\. For more information, see [IAM roles for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+ **Sync mode**—Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between:
  + `FORCED_FULL_CRAWL` to crawl and sync all content to your index
  + `FULL_CRAWL` to crawl all content and sync only new, modified, or deleted content
  + `CHANGE_LOG` to crawl and sync only new, modified, and deleted content
**Important**  
Google Drive API does not support retrieving comments from a permanently deleted file\. Comments from trashed files are retrievable\. When a file is trashed, the connector will delete comments from the Amazon Kendra index\.
+  **Enable identity crawler**—You must specify whether to activate identity crawler\. If identity crawler is deactivated, you must upload the principal information using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API\.
+  **Inclusion and exclusion filters**—You can specify whether to include or exclude certain user accounts, shared drives, MIME types, and files\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—You can only built\-in index fields for the Amazon Kendra Google Drive connector\. Custom field mapping is not available for the Google Drive connector because of API limitations\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

For a list of other important JSON keys to configure, see [Google Drive template schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html#ds-google-drive-schema)\.

------

## Notes<a name="google-drive-notes"></a>
+ Custom field mapping is not available for Google Drive connector as the Google Drive UI does not support creating custom fields\.
+ Google Drive API does not support retrieving comments from a permamently deleted file\. Comments are retrievable, however, for trashed files\. When a file is trashed, the Amazon Kendra connector will delete comments from the Amazon Kendra index\.
+ Google Drive API does not return comments present in a \.docx file\.