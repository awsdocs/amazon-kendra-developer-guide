--------

--------

# Getting started with the Amazon Kendra console<a name="gs-console"></a>

The following procedures show how to create and test an Amazon Kendra index by using the AWS console\. In the procedures you create an index and a data source for an index\. Finally, you test your index by making a search request\. 

**Step 1: To create an index \(console\)**

1. Sign in to the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.

1. Select **Create index** in the **Indexes** section\.

1. In the **Specify index details** page, give your index a name and a description\.

1. In **IAM role**, choose **Create a new role** and then give the role a name\. The IAM role will have the prefix "AmazonKendra\-"\.

1. Leave all of the other fields at their defaults\. Choose **Next**\.

1. In the **Configure user access control** page, choose **Next**\.

1. In the **Provisioning details** page, choose **Developer edition**\.

1. Choose **Create** to create your index\.

1. Wait for your index to be created\. Amazon Kendra provisions the hardware for your index\. This operation can take some time\.<a name="gs-data-source"></a>

**Step 2: To add a data source to an index \(console\)**

1. View the available [data sources](https://docs.aws.amazon.com/kendra/latest/dg/data-source.html) to connect Amazon Kendra to and index your documents\.

1. In the navigation pane, select **Data sources** and then select **Add data source** for your chosen data source\.

1. Follow the steps to configure the data source\.<a name="gs-search"></a>

**Step 3: To search an index \(console\)**

1. In the navigation pane, choose **Search console**\.

1. Enter a search term that's appropriate for your index\. The **top results** and **top document** results are shown\.