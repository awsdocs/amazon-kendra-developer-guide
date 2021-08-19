--------

--------

# Getting started with a Microsoft SharePoint data source \(Console\)<a name="getting-started-sharepoint"></a>

You can use the Amazon Kendra console to get started indexing a Microsoft SharePoint data source\. When you use the console you specify the connection information you need to index the contents of the SharePoint data source\.

Use the following procedure to create a basic SharePoint data source using the default configuration\. The procedure assumes you created an index following step 1 of [Getting started with an S3 bucket \(Console\)](gs-console.md)\.

**To create a SharePoint data source using the Amazon Kendra console**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add the data source to\.

1. Choose **Add data sources**\.

1. From the list of data source connectors, choose **SharePoint**\.

1. On the **Specify data source details** page, do the following:

   1. In the **Name data source** section, give your data source a name and optionally a description\. 

   1. \(Optional\) In the **Tags** section, add tags to categorize your data source\. 

   1. Choose **Next**\.

1. On the **Define access and security** page, do the following:

   1. In the **Source** section, do one of the following:
      + Choose **SharePoint Online** to connect to your SharePoint cloud account and add the URLs of your SharePoint data repository to index\.
      + Choose **SharePoint Server** to connect to your SharePoint hosted on your own server and choose your SharePoint version\. Then add the URLs of your SharePoint data repository to index\. \(Optional\) If using your own private certificate authority, you need to provide the SSL certificate location and the certificate needs to be in X\.509 standard format\. Amazon Kendra supports most public certificate authorities\. You also need to provide permission to access the Amazon S3 bucket that contains the SSL certificate used to communicate with the SharePoint site\.

   1. In the **Authentication** section, do the following:
      + If you chose **SharePoint Online** as your source, you can select the **AWS Secrets Manager secret** dropdown to create a secret and enter your SharePoint credentials, or choose an existing secret\. Your secret must contain your SharePoint user name and password, and a name for your secret\. For more information on a secret that stores your authentication credentials, see [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)\.
      + If you chose **SharePoint Server** as your source, you can select the **AWS Secrets Manager secret** dropdown to create a secret and enter your SharePoint credentials, or choose an existing secret\. In addition to your SharePoint user name and password, and a name for your secret, your secret must include the server domain name\. The server domain name is the NetBIOS name in your active directory provider\.

        If you want to filter on user context and you need to convert access control list \(ACL\) to email format, you choose whether to provide the LDAP server URL and LDAP search base, or manually enter the email domain\. You can choose to keep ACL as `sAMAccountName` if you do not want to provide an email domain\. `sAMAccountName` is the server domain name and the user name\. For more information on LDAP server URL and LDAP search base, and manual email domain override of these, see [Using a SharePoint data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-sharepoint.html)\.

   1. \(Optional\) If you chose **SharePoint Server**, in the **VPC and security group** section, do the following:
      + If you want Amazon Kendra to connect to your Amazon virtual private cloud \(VPC\) to index documents stored in SharePoint running in your private cloud, choose a **Virtual Private Cloud \(VPC\)**\. You need to provide the required permissions for VPC \- see [IAM role for VPC](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-vpc)\. To configure Amazon Kendra to use a VPC, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.

   1. In the **IAM role** section, in **IAM role**, choose an existing role that grants permission to your SharePoint and other resources\. For more information about the required permissions, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, do the following:

   1. \(Optional\) In the **Sync scope** section, do one of the following:
      + Choose **Use change logs** to sync based on identifying updated documents instead of scanning all documents\.
      + Choose **Crawl document attachments** to include attachments when syncing\.
      + Choose **Use local group mappings** if your SharePoint server is not in sync with your local active directory provider and you want to filter your documents\. You need to provide a hash of each site name when you query the index\.

   1. Choose **Additional configuration** to use regular expression patterns to include or exclude certain files to index\.

   1. In the ** Sync schedule** section, for **Frequency**, choose the frequency to sync your index with your SharePoint data source\. You can sync hourly, daily, weekly, monthly, run on demand, or you can choose your own custom sync schedule\.

   1. Choose **Next**\.

1. \(Optional\) On the **Set field mappings** page, check your SharePoint fields are mapped to Amazon Kendra index fields, such as the document ID, document title, and more\. You can also add a custom field by selecting **Add field** or you can add fields directly using the API\. Choose **Next**\.

1. On the **Review and Create** page, review the details of your SharePoint data source\. To make changes, choose the **Edit** button next to the item that you want to change\. When you are done, choose **Add data source** to add your SharePoint data source\.

After you choose **Create**, Amazon Kendra starts creating the data source\. It can take several minutes for the data source to be created\. When it is finished, the status of the data source changes from **Creating** to **Active**\.

Amazon Kendra syncs the index with SharePoint in accordance with the sync schedule you set\. If you choose **Sync now** to start the sync process immediately, it can take several minutes to a few hours to synchronize, depending on the number and size of the documents\.