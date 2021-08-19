--------

--------

# Getting started with an Amazon WorkDocs data source \(Console\)<a name="getting-started-workdocs"></a>

You can use the Amazon Kendra console to get started indexing an Amazon WorkDocs data source\. When you use the console, you specify the connection information you must index the contents of the Amazon WorkDocs data source\.

Amazon WorkDocs connector is available in Oregon, North Virginia, Sydney, Singapore and Ireland regions\.

Use the following procedure to create an Amazon WorkDocs data source\. The procedure assumes you created an index following step 1 of [Getting started with an S3 bucket \(Console\)](gs-console.md)\.

**To create an Amazon WorkDocs data source using the Amazon Kendra console**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add the data source to\.

1. Choose **Add data sources**\.

1. From the list of data source connectors, choose **Amazon WorkDocs**\.

1. On the **Specify data source details** page, do the following:

   1. In the **Name data source** section, give your data source a name and optionally a description\. 

   1. \(Optional\) In the **Tags** section, add tags to categorize your data source\.

   1. Choose **Next**\.

1. On the **Define access and security** page:

   1. In the **Source** section, do the following:
      + Choose the organization ID, which is the directory ID corresponding to your Amazon WorkDocs site\. To locate your organization ID, go to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) and select the **Active Directory** dropdown menu\. In your list of **Directories**, your Amazon WorkDocs site directory has an ID, which is the organization ID\. You can set up a new directory for your Amazon WorkDocs site in the AWS Directory Service console and enable the directory in the Amazon WorkDocs console\.
      + Choose an existing **IAM role** that grants Amazon Kendra permission to access your Amazon WorkDocs resources such as your index\. For more information about the required permissions, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page:

   1. \(Optional\) In the **Sync scope** section, do any of the following:
      + Select the checkbox **Crawl document comments** to include comments when syncing\. Each comment is indexed as a separate document\.
      + Select the checkbox **Use change logs** to sync based on identifying updated documents instead of scanning all documents\. If you are syncing your Amazon WorkDocs data source with your index for the first time, all documents are scanned\.
      + Select the **Advanced configuration** to use regular expression patterns to include or exclude files in your data source\.

   1. In the **Sync schedule** section, for **Frequency**, you can sync your index with your Amazon WorkDocs data source\. You can sync hourly, daily, weekly, monthly, run on demand, or you can choose your own custom sync schedule\.

   1. Choose **Next**\.

1. \(Optional\) On the **Set field mappings** page, check that your Amazon WorkDocs fields are mapped to Amazon Kendra index fields, such as the document ID, document authors, and more\. You can also add a custom field by selecting **Add field**\. The custom field name must exist in the metadata of your Amazon WorkDocs documents\. You can also add fields directly using the API\. Choose **Next**\.

1. On the **Review and Create** page, review the details of your Amazon WorkDocs data source\. To make changes, choose the **Edit** button next to the item that you want to change\. When you are done, choose **Add data source** to add your Amazon WorkDocs data source\.

After you choose **Add data source**, Amazon Kendra starts creating the data source\. It can take several minutes for the data source to be created\. When it is finished, the status of the data source changes from **Creating** to **Active**\.

Amazon Kendra syncs the index with Amazon WorkDocs based on the sync schedule you set\. If you choose **Sync now**, it still can take several minutes to a few hours to synchronize, depending on the number and size of documents\.