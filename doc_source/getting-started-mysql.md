--------

--------

# Getting started with a MySQL database data source \(console\)<a name="getting-started-mysql"></a>

You can use the Amazon Kendra console to get started using a MySQL database as a data source\. When you use the console you specify the connection information you need to index the contents of a MySQL database\. For more information, see [Using a database data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-database.html)\.

You first need to create a MySQL database, then you can create a data source for the database\.

Use the following procedure to create a basic MySQL database\. The procedure assumes that you have already created an index following step 1 of [Getting started with the Amazon Kendra console](gs-console.md)\.

**To create a MySQL database**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. From the navigation pane, choose **Subnet groups** and then choose **Create DB Subnet Group**\.

1. Name the group and choose your Virtual Private Cloud \(VPC\)\. For more information on configuring a VPC, see [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.

1. Add your VPC's private subnets\. Your private subnets are the ones that are not connected to your NAT\. Choose **Create**\.

1. From the navigation pane, choose **Databases** and then choose **Create database\.**

1. Use the following parameters to create the database\. Leave all of the other parameters at their defaults\.
   + **Engine options** – MySQL
   + **Templates** – Free tier
   + **Credential Settings** – Enter and confirm a password
   + Under **Connectivity**, choose **Additional connectivity configuration**\. Make the following choices\.
     + **Subnet group** – Choose the subnet group that you created in step 4\.
     + **VPC security group** – Choose the group that contains both inbound and outbound rules that you created in your VPC\. For example, **DataSourceSecurityGroup**\. For more information on configuring a VPC, see [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.
   + Under **Additional configuration**, set the **Initial database name** to **content**\.

1. Choose **Create database**\.

1. From the list of databases, choose your new database\. Make a note of the database endpoint\.

1. After you create your database, you must create a table to hold your documents\. Creating a table is outside the scope of these instructions\. When you create your table, note the following:
   + Database name – **content**
   + Table name – **documents**
   + Columns – **ID**, **Title**, **Body**, and **LastUpdate**\. You can include additional columns if you want\.

Now that you have created your MySQL database, you can create a data source for the database\.

**To create a MySQL data source**

1. Sign in to the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the navigation pane, choose **Indexes** and then choose your index\.

1. Choose **Add data sources** and then choose **Amazon RDS**\.

1. Type a name and description for the data source and then choose **Next**\.

1. Choose **MySQL**\.

1. Under **Connection access**, enter the following information:
   + **Endpoint** – The endpoint of the database that you created earlier\.
   + **Port** – The port number for the database\. For MySQL, the default is 3306\.
   + **Type of authentication** – Choose **New**\.
   + **New secret container name** – A name for the Secrets Manager container for the database credentials\.
   + **Username** – The name of a user with administrative access to the database\.
   + **Password** – The password for the user, and then choose **Save authentication**\.
   + **Database name** – **content**\.
   + **Table name** – **documents**\.
   + **IAM role** – Choose **Create a new role**, and then type a name for the role\.

1. In **Column configuration** enter the following:
   + **Document ID column name** – **ID**
   + **Document title column name** – **Title**
   + **Document data column name** – **Body**

1. In **Column change detection** enter the following:
   + **Change detecting columns** – **LastUpdate**

1. In **Configure VPC & security group** provide the following:
   + In **Virtual Private Cloud \(VPC\)**, choose your VPC\.
   + In **Subnets**, choose the private subnets that you created in your VPC\.
   + In **VPC security groups**, choose the security group that contains both inbound and outbound rules that you created in your VPC for MySQL databases\. For example, **DataSourceSecurityGroup**\.

1. In **Set sync run schedule**, choose **Run on demand** and then choose **Next**\.

1. In **Data source field mapping**, choose **Next**\.

1. Review the configuration of your data source to make sure that it is correct\. When you're satisfied that everything is correct, choose **Create**\.