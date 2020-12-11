--------

--------

# Getting started with a Google Workspace Drive data source \(Console\)<a name="getting-started-google"></a>

You can use the Amazon Kendra console to index a Google Workspace Drive\. Using the console, you can specify all of the connection information that you need to index the contents of a Google Drive\. For more information, see [Using a Google Workspace Drive data source](data-source-google-drive.md)\.

Use the following procedure to create a basic Google Drive data source using the default configuration\. The procedure assumes that you have already created an index following the steps in step 1 of [Getting started with an S3 bucket \(Console\)](gs-console.md)\.

Before you can create a Google Drive data source, you must create a service account that Amazon Kendra uses to connect to your Google Drive\. 

**Step 1: To create a Google Drive service account**

1. Log into the [ Google Cloud Platform console](https://console.cloud.google.com/) with an account that has administrator privilege\.

1. From the top menu, choose your project\.

1. From the top\-left menu, choose **IAM & Admin / Service Accounts**\.

1. From the top menu, choose **CREATE SERVICE ACCOUNT**\.

1. Enter a service account name and description\. The service account ID, an email address, is generated automatically\. Choose **Create**\.

1. Skip steps 2 and 3 on the page\. Choose **Done** to continue\.

**Step 2: Configure the service account\.**

Begin this procedure immediately after you finish step 1\.

1. On the service account page, choose **SHOW DOMAIN\-WIDE DELEGATION** to view the available options\.

1. Choose **Enable G Suite Domain\-wide Delegation**\. 

1. On the service account page, choose the three vertical dots under **Actions** and choose **Edit** to configure the service account\.

1. Choose **CREATE KEY**, set the **Key Type ** to **JSON**\. Choose **Create**\.

1. Choose **CLOSE**\. A JSON file containing the client email address and private key for the service account is saved on your computer\.

1. Choose the service account and copy the unique ID of the account\. You'll need this in Step 3: Enable API scopes\.

1. From the top\-left menu, choose **APIs & Services / Library**\.

1. Search for **Admin SDK** and then choose it\.

1. Choose **Enable**\.

1. Search for **Google Drive API** and then choose it\.

1. Choose **Enable**\.

**Step 3: Enable Google API scopes**

1. [Log in](https://admin.google.com/) to a Google account that has administrator privileges\.

1. From the top\-left menu, choose **Security** and then choose **Settings**\.

1. Scroll down and choose **API controls**\.

1. Choose **MANAGE DOMAIN\-WIDE DELEGATION** in the **Domain\-wide delegation** section of the page\.

1. Choose **Add New**\. Paste the service account unique ID from step 2 in **Client ID**\.

1. Add the following read\-only scopes to **OAuth scopes**, and then choose **Authorize**\.

   ```
   https://www.googleapis.com/auth/drive.readonly,
   https://www.googleapis.com/auth/drive.metadata.readonly,
   https://www.googleapis.com/auth/admin.directory.user.readonly,
   https://www.googleapis.com/auth/admin.directory.group.readonly
   ```

Once you have created a service account and configured it to use the Google API, you can create a Google Drive data source\.

**Step 4: To create a Google Drive data source using the Amazon Kendra console**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add the data source to\.

1. Choose **Add data sources**\. 

1. From the list of data source connectors, choose **Google Drive**\. 

1. On the **Name and description** page, give your data source a name and optionally a description\. Leave the **Tags** field blank\. Choose **Next** to continue\.

1. Under **Type of authentication**, choose **New**\. Enter the following information:
   + **Secret name** – the name of the Secrets Manager secret that holds the authentication information\.
   + **Admin account email** – The email of the administrator that created the service account\.
   + **Client email** – The service account email address\. You can find this address in `client_email` field of the JSON file you downloaded in step 1\.
   + **Private key** – The private key from the JSON file that you downloaded in step 1\.

   Choose **Save authentication** to create a new Secrets Manager secret\.

1. Under **Define access and security** choose **Create a new role \(Recommended\)** to create an IAM role for your data source\.

1. Under **Role name** enter a name for the IAM role\.

1. Choose **Next**\.

1. On the **Configure sync settings** page, don't change the **Set sync scope** or **Additional configuration** sections\. In the **Sync run schedule** section, choose **Run on demand** for the frequency\.

1. Choose **Next**\.

1. On the **Data source fields** page, leave the defaults\.

1. Choose **Next**\.

1. On the **Review and create** page, review the settings for your data source\. Once you are satisfied, choose **Create**\.

After you choose **Create**, Amazon Kendra returns you to the list of data sources and starts creating the data source\. It can take several minutes for the data source to be created\. When it is finished, the console displays a banner and the status of the data source changes from **Creating** to **Active**\.

After creating the data source, you need to sync the Amazon Kendra index with the data source\. Choose **Sync now** to start the sync process\. It can take several minutes to several hours to synchronize the data source, depending on the number and size of the documents\.