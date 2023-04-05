--------

--------

# Configuring Amazon Kendra to use a VPC<a name="vpc-configuration"></a>

Amazon Kendra can connect to your Amazon Virtual Private Cloud to index content stored in data sources or databases running in your private cloud\. When you create a data source connector or a database connector, you provide security group and subnet identifiers for the subnet that contains your data source or database\. Amazon Kendra uses this information to create an elastic network interface that it uses to securely communicate with your data source or database\.

If your data source or database isn't running on an Amazon VPC, you can connect your data source or database to your Amazon VPC using a Virtual Private Network \(VPN\)\. You get a default VPC when you create your Amazon account\. For information about setting up a VPN, see the [AWS VPN Documentation](https://docs.aws.amazon.com/vpn/)\.



To use a VPC, you must tell Amazon Kendra the identifier of the subnet that the database belongs to and the identifiers of any security groups that Amazon Kendra must use to access the subnet\. For example, if you're using the default port for a MySQL database, the security groups must allow Amazon Kendra to access port 3306 on the host that runs the database\.

Only use private subnets in the VPC configuration of your data source or database\. If your RDS instance is in a public subnet in your VPC, then you can't use that subnet directly to sync your data source or database\. Instead, create a private subnet that has outbound access to a NAT gateway in the public subnet\. When you configure the VPC for your data source or database, specify that private subnet\. For a database data source configured with a VPC, the subnets must be in one of the following Availability Zone IDs:
+ US West \(Oregon\)—usw2\-az1, usw2\-az2, usw2\-az3
+ US East \(N\. Virginia\)—use1\-az1, use1\-az2, use1\-az4
+ EU \(Ireland\)—euw1\-az1, uew1\-az2, euw1\-az3

The identifiers for subnets and security groups are configured in the Amazon VPC control panel\. To see the identifiers, open the Amazon VPC console as follows:

**To view subnet identifiers**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. From the navigation pane, choose **Subnets**\.

1. From the subnet list, choose the subnet that contains your database server\.

1. From the description tab, make a note of the identifier in the **Subnet ID** field\.

**To view security group identifiers**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. From the navigation pane, choose **Security Groups**\.

1. From the security group list, choose the group that you want the identifier for\.

1. From the description tab, make a note of the identifier in the **Group ID** field\.

If Amazon Kendra must route the connection between two or more subnets, you can provide multiple subnets\. For example, if the subnet that contains your database server is out of IP addresses, Amazon Kendra can connect to a subnet with free IP addresses and route the connection to the first subnet\. If you list multiple subnets, the subnets must be able to communicate with each other\. Each subnet must be associated with a route table that provides outbound internet access using a network address translator \(NAT\) device\. 

You can also provide multiple security groups\. The combined effect of the security groups must allow Amazon Kendra to access the data source or database server that you have specified in the connection configuration\.

## Connecting to a database in a VPC<a name="vpc-example"></a>

The following example shows how to connect a MySQL database running in a VPC\. The example assumes that you're starting with your default VPC and that you need to create a MySQL database\. If you already have a VPC, make sure that it's configured as shown\. If you have a MySQL database, you can use that instead of creating a new one\.

**Topics**
+ [Step 1: Configure a VPC](#vpc-create-vpc)
+ [Step 2: Configure security](#vpc-create-database)
+ [Step 3: Create a database](#vpc-create-database)
+ [Step 4: Create a database data source connector](#vpc-connect)

### Step 1: Configure a VPC<a name="vpc-create-vpc"></a>

Configure your VPC so that you have a private subnet and a security group for Amazon Kendra to access a MySQL database running in the subnet\. The subnets provided in the VPC configuration must be in either US West \(Oregon\), US East \(N\. Virginia\), EU \(Ireland\)\.

**To configure a VPC**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. From the navigation pane, choose **Route tables**, then choose **Create route table**\.

1. For the **Name tag** field, enter **Private subnet route table**\. In the **VPC field**, choose your VPC, and then choose **Create**\. Choose **Close** to return to the list of route tables\.

1. From the navigation pane, choose **NAT Gateways** then choose **Create NAT Gateway**\.

1. In the **Subnet** field, choose the subnet that's the public subnet and note the subnet ID\.

1. If you don't have an Elastic IP address, choose **Create New EIP**, choose **Create a NAT Gateway**, and then choose **Close**\.

1. From the navigation pane, choose **Route Tables**\.

1. From the route table list, choose the **Private subnet route table** that you created in step 3\. From **Actions**, choose **Edit Routes**\. 

1. Choose **Add route**\. Add the destination 0\.0\.0\.0/0 to allow all outgoing traffic to the internet\. For **Target**, choose **NAT Gateway**, and then choose the gateway that you created in step 4\. Choose **Save routes**, and then choose **Close**\.

1. From **Actions**, choose **Edit subnet associations\.**

1. Choose the subnets that you want to be private\. Don't choose the subnet with the NAT gateway that you noted previously\.

### Step 2: Configure security<a name="vpc-create-database"></a>

Next, configure security groups for your database\.

**To create security groups**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. From the description of your VPC, note the IPv4 CIDR\.

1. From the navigation pane, choose **Security Groups** and then choose **Create security group**\.

1. In **Security group name** enter **DataSourceInboundSecurityGroup**\. Provide a description, then choose your VPC from the list\. Choose **Create** and then choose **Close**\.

1. Choose the **Inbound** tab\.

1. Choose **Edit rules**, and then choose **Add Rule**

1. For a database, enter the port number for the **Port Range**\. For example, for MySQL it's **3306**, and, for HTTPS, it's **443**\. For the **Source**, type the Classless Inter\-Domain Routing \(CIDR\) of your VPC\. Choose **Save rules** and then choose **Close**\.

The security group allows anyone within the VPC to connect to the database, and it allows outbound connections to the internet\.

### Step 3: Create a database<a name="vpc-create-database"></a>

Create a database to hold your documents, or you can use your existing database\. See [Using a database data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-database.html) for a list of databases that Amazon Kendra supports\.

For instructions on how to create a MySQL database, see [Getting Starting with a MySQL database data source \(console\) using Amazon RDS](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-mysql.html)\.

### Step 4: Create a database data source connector<a name="vpc-connect"></a>

After you configured your VPC and created your database, you can create a data source connector for the database\. See [Using a database data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-database.html)\.

Make sure that you configure your VPC, the private subnets that you created in your VPC, and the security group that you created in your VPC for your database\.

For instructions on how to create a data source for a MySQL database, see [Getting Starting with a MySQL database data source \(console\) using Amazon RDS](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-mysql.html)\.