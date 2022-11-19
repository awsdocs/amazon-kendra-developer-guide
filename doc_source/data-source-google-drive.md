--------

--------

# Using a Google Drive data source<a name="data-source-google-drive"></a>

Google Drive is a cloud\-based file storage service\. If you are a Google Drive user, you can use Amazon Kendra to index documents stored in shared drives and user My Drives in your Google Drive data source\. You can index both Google Workspace documents as well as documents listed in [Types of documentation](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\.

Amazon Kendra supports the following both Google Docs and Google Slides in Google Workspace Drive\.

You can connect Amazon Kendra to your Google Drive data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) API\.

For troubleshooting your Amazon Kendra Google Drive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-google-drive)
+ [Prerequisites](#prerequisites-google-drive)
+ [Connecting Amazon Kendra to your Google Drive data source](#data-source-procedure-google-drive)
+ [Learn more](#google-drive-learn-more)

## Supported features<a name="supported-features-google-drive"></a>
+ Field mappings
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-google-drive"></a>

Before you can use Amazon Kendra to index your Google Drive data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your Google Drive data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You are a user who either has administrative privileges or has been granted access by a super admin role\.
**Note**  
As long as you have been authorized access by a super admin role, you do not need a super admin role yourself for connecting Amazon Kendra to your account\. 
+ You have created a service account with a JSON key as Private Key using your user account\. You do this in the [Google Cloud Console](https://console.cloud.google.com/)\.
+ You have copied your user account email and your service account email \. When you connect to Amazon Kendra you enter your user account email as Admin account email and your service account email as client email in your Secrets Manager secret\.
+ You have enabled Admin SDK API and Google Drive API in your user account\. You do this in the [Google Cloud Console](https://console.cloud.google.com/)\.
+ You have used a super admin role or asked a user with a super admin role to add the following read only permissions to the service account you have created\.

  Added the following permissions to your Google Drive using a super admin role:
  + https://www\.googleapis\.com/auth/drive\.readonly
  + https://www\.googleapis\.com/auth/drive\.metadata\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.user\.readonly
  + https://www\.googleapis\.com/auth/admin\.directory\.group\.readonly

  You can find more information on how to configure your Google Drive account on the [Google Cloud documentation](https://cloud.google.com/docs) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your Google Drive data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your Google Drive data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Google Drive data source<a name="data-source-procedure-google-drive"></a>

To connect Amazon Kendra to your Google Drive data source you must provide details of your Google Drive credentials so that Amazon Kendra can access your data\. If you have not yet configured Google Drive for Amazon Kendra see [Prerequisites](#prerequisites-google-drive)\.

### <a name="google-drive-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Google Drive** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Google Drive**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

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

   1. **Exclude user accounts**—The Google Drive users you want to exclude from the index\. You can add upto 100 user accounts\.

   1. **Exclude shared drives**—The Google Drive shared drives you want to exclude from your index\. You can add upto 100 shared drives\.

   1. **Exclude file types drives**—The Google Drive file types you want to exclude from your index\. You can also choose to edit MIME type selections\.

   1. **Additional configurations**—Regular expression patterns to include or exclude certain folders and files\. You can add up to 100 patterns\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **GoogleDrive field name** and **Additional suggested field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ GoogleDriveConfiguration API ]

**To connect Amazon Kendra to Google Drive**

You must specify the following using the [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) API:
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Google Drive account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "clientAccount": "service account email",
      "adminAccount": "user account email",
      "privateKey": "private key"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Google Drive connector and Amazon Kendra\. For more information, see [IAM roles for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—By default Amazon Kendra indexes all documents in Google Drive\. You can specify whether to include content in shared drives, user accounts, document MIME types and paths\. You can also specify regular expression patterns to include or exclude files\. If you choose to exclude user accounts, none of the files in the My Drive owned by the account are indexed\. Files shared with the user are indexed unless the owner of the file is also excluded\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your Google Drive data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="google-drive-learn-more"></a>

To learn more about integrating Amazon Kendra with your Google Drive data source, see:
+ [Getting started with the Amazon Kendra Google Drive connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-the-amazon-kendra-google-drive-connector/)