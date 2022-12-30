--------

--------

# GitHub<a name="data-source-github"></a>

GitHub is a web\-based hosting service for software development providing code storage and management services with version control\. You can use Amazon Kendra to index your GitHub Enterprise Cloud \(SaaS\) and GitHub Enterprise Server \(On Prem\) repository files, issue and pull requests, issue and pull request comments, and issue and pull request comment attachments\. You can also choose to include or exclude certain files\.

You can connect Amazon Kendra to your GitHub data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [GitHubConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GitHubConfiguration.html) API\.

For troubleshooting your Amazon Kendra GitHub data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-github)
+ [Prerequisites](#prerequisites-github)
+ [Connection instructions](#data-source-procedure-github)
+ [Learn more](#github-learn-more)

## Supported features<a name="supported-features-github"></a>

Amazon Kendra GitHub data source connector supports the following features:
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-github"></a>

Before you can use Amazon Kendra to index your GitHub data source, make these changes in your GitHub and AWS accounts\.

**In GitHub, make sure you have:**
+ Created a GitHub user with administrative permissions to the GitHub organization\.
+ Created a personal access token for authentication credentials\.
+ **Recommended:**Created an OAuth token for authentication credentials\. Use OAuth token for better API throttle limits and connector performance\.
+ **Optional:** Installed a SSL certificate\.
+ Noted the GitHub host URL for the type of GitHub service that you use\. For example, the host URL for GitHub cloud could be *https://api\.github\.com* and the host URL for GitHub server could be *https://on\-prem\-host\-url/api/v3/*\.
+ Noted the GitHub organization name for your respositories from your GitHub settings\.
+ Added the following permissions:

  **For GitHub Enterprise Cloud \(SaaS\)**
  + repo:status
  + public\_repo
  + repo:invite
  + read:org
  + user:email
  + read:user

  **For GitHub Enterprise Server \(On Prem\)**
  + repo:status
  + public\_repo
  + repo:invite
  + read:org
  + user:email
  + read:user
  + site\_admin

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your GitHub authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your GitHub data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index id\.

## Connection instructions<a name="data-source-procedure-github"></a>

To connect Amazon Kendra to your GitHub data source you must provide details of your GitHub credentials so that Amazon Kendra can access your data\. If you have not yet configured GitHub for Amazon Kendra see [Prerequisites](#prerequisites-github)\.

### <a name="github-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to GitHub** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **GitHub**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **GitHub source**—Choose between **GitHub Enterprise Cloud** and **GitHub Enterprise Server**\.

   1. **GitHub host URL**—Enter your GitHub host name\.

   1. **GitHub organization name**—Enter your GitHub organization name\. You can find your organization information in your GitHub account\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your GitHub authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-GitHub\-’ is automatically added to your secret name\.

         1. For **GitHub token**—Enter the authentication credential values you generated and downloaded from your GitHub account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Select repositories to crawl**—The GitHub entities or content types you want to crawl\.

   1. **Change log**—Select to update your index instead of syncing all your files\.

   1. **Content types**—Select to file types you want to include\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Repository**, **Respository Commit**, **Issue Document**, **Issue Comment**, **Issue Attachment**, **Pull Request Comment**, **Pull Request Document**, **Pull Request Attachment**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to GitHub**

You must specify the following using the [GitHubConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GitHubConfiguration.html) API object:
+ **Data source type**—Specify the data source type as either `SAAS` or `ON_PREMISE`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your GitHub account\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "personalToken": "token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.
+ **IAM role**—Provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the GitHub connector and Amazon Kendra\. For more information, see [IAM roles for GitHub data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
**Note**  
If you use GitHub server, you must use an Amazon VPC to connect to your GitHub server\.
+  **Change log**—Whether Amazon Kendra should use the GitHub data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the GitHub data source than to process the change log\. If you are syncing your GitHub data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—Specify whether to include repository files, issue and pull requests, issue and pull request comments, and issue and pull request comment attachments\. You can also specify regular expression patterns to include or exclude \[repository files, issue and pull requests, issue and pull request comments, and issue and pull request comment attachments\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—Choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for GitHub data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—Choose to map your GitHub data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="github-learn-more"></a>

To learn more about integrating Amazon Kendra with your GitHub data source, see:
+ [Reimagine search on GitHub repositories with the power of the Amazon Kendra GitHub connector](https://aws.amazon.com/blogs/machine-learning/reimagine-search-on-github-repositories-with-the-power-of-the-amazon-kendra-github-connector/)