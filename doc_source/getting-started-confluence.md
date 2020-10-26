--------

--------

# Getting started with a Confluence data source \(Console\)<a name="getting-started-confluence"></a>

You can use the Amazon Kendra console to get started using a Confluence data store\. When you use the console you specify the connection information you need to index the contents of a Confluence instance\. For more information, see [Using a Confluence data source](data-source-confluence.md)\.

Use the following procedure to create a basic Confluence data source using the default configuration\. The procedure assumes you created an index following the steps in step 1 of [Getting started with an S3 bucket \(Console\)](gs-console.md)\.

**To create a Confluence data source using the Amazon Kendra console**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add the data source to\.

1. Choose **Add data sources**\.

1. From the list of data source connectors, choose **Confluence**\.

1. On **Specify data source details**, give your data source a name and optionally a description\. Leave the **Tags** field blank\. Choose **Next** to continue\.

1. On **Define access and security**, in **Set source**, enter the URL of your Confluence server\.

1. In **Set authentication**, perform the following steps:

   1. For the **Type of authentication**, choose **New**\.

   1. In **Secret name**, enter a name for the AWS Secrets Manager secret that will contain your user credentials\.

   1. In **User name**, enter the Confluence account that Amazon Kendra uses to connect to the Confluence server\. The account should have administrator permissions\.

   1. In **Password**, enter the password for the Confluence account\.

   1. Choose **Save authentication** to save the Secrets Manager secret\.

1. In **Virtual Private Cloud \(VPC\)** choose **No VPC**\.

1. In **IAM role** choose **Create a new role\.** Enter a name for the role in the **Role name** field\. Choose **Next** to continue\.

1. Choose **Next** to continue\.

1. On **Set sync scope**, leave the defaults\.

1. In **Frequency**, choose **Run on demand** and then choose **Next**\.

1. In **Set field mappings \- optional**, leave the defaults and choose **Next**\.

1. On **Review and create**, review the settings for the data source\. Use the **Edit** buttons to make any changes that you need to make\. When you are satisfied with the settings, choose **Create** to create your Confluence data source\.

After you choose **Create**, Amazon Kendra starts creating the data source\. It can take several minutes for the data source to be created\. When it is finished, the status changes from **Creating** to **Active**\.

After creating the index, you need to sync the Amazon Kendra index with the data source\. Choose **Sync now** to start the sync process\. It can take several minutes to several hours to synchronize the data source, depending on the number and size of the documents\.