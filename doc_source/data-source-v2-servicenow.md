--------

--------

# ServiceNow Connector v2\.0<a name="data-source-v2-servicenow"></a>

ServiceNow provides a cloud\-based service management system to create and manage organization\-level workflows, such as IT services, ticketing systems, and support\. You can use Amazon Kendra to index your ServiceNow catalogs, knowledge articles, and incidents\.

For troubleshooting your Amazon Kendra ServiceNow data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v2-servicenow)
+ [Prerequisites](#prerequisites-v2-servicenow)
+ [Connection instructions](#data-source-procedure-v2-servicenow)
+ [Learn more](#servicenow-learn-more)

## Supported features<a name="supported-features-v2-servicenow"></a>

Amazon Kendra ServiceNow data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Sync all documents/ Sync only new, modified, deleted documents
+ ServiceNow instance versions: Rome, Sandiego, Tokyo, Others
+ Inclusion/exclusion patterns: Service catalogs, knowledge articles, incidents, attachments

## Prerequisites<a name="prerequisites-v2-servicenow"></a>

Before you can use Amazon Kendra to index your ServiceNow data source, make these changes in your ServiceNow and AWS accounts\.

**In ServiceNow, make sure you have:**
+ Created a Personal or Enterprise Developer Instance and have a ServiceNow instance with an administrative role\.
+ Copied the host of your ServiceNow instance URL\. The format for the host URL you enter is *your\-domain\.service\-now\.com*\. You need your ServiceNow instance URL to connect to Amazon Kendra\.
+  Configured basic authentication credentials containing a user name and password to enable Amazon Kendra to connect to your ServiceNow instance\.
+ **Optional:** Configured an OAuth 2\.0 credential token that can identify Amazon Kendra and generate a user name, password, a client id, and a client secret\.

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your ServiceNow authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your ServiceNow data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index id\.

## Connection instructions<a name="data-source-procedure-v2-servicenow"></a>

To connect Amazon Kendra to your ServiceNow data source, you must provide details of your ServiceNow credentials so that Amazon Kendra can access your data\. If you have not yet configured ServiceNow for Amazon Kendra see [Prerequisites](#prerequisites-v2-servicenow)\.

### <a name="servicenow-v2-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to ServiceNow** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **ServiceNow Connector v2\.0**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **ServiceNow host**—Enter the ServiceNow host URL\. The format for the host URL you enter is *your\-domain\.service\-now\.com*\.

   1. **ServiceNow version**—Select your ServiceNow version\.

   1. Choose between **Basic authentication** and **Oauth 2\.0 authentication** based on your use case\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your ServiceNow authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. Enter the following information in the window:

      1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-ServiceNow\-’ is automatically added to your secret name\.

      1. If using Basic Authentication—Enter the **Secret name** **Username**, and **Password** you generated and downloaded as a JSON file from your ServiceNow account\.

         If using OAuth2\.0 Authentication—Enter the **Secret name** **Username**, **Password**, **Client ID**, and **Client Secret** you generated and downloaded as a JSON file from your ServiceNow account\.

      1. Choose **Save and add secret**\.

   1. \(Optional\) **Configure VPC and security group**—Select a VPC to use with your ServiceNow instance\.

   1. **Identity crawler**—Choose to enable Amazon Kendra identity crawler to sync identity information using principal store\. If you choose to turn identity crawler off, you must upload the principal information into the principal store using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. For **Knowledge articles**, choose from the following options :
      +  **Knowledge articles**—Choose to index knowledge articles\.
      + **Knowledge article attachments**—Choose to index knowledge article attachments\.
      + **Type of knowledge articles**—Choose between **Only public articles** and **Knowledge articles based on ServiceNow filter query** based on your use case\. If you select **Include articles based on ServiceNow filter query**, you must enter a **Filter query** copied from your ServiceNow account\. Example filter queries include: *workflow\_state=draft^EQ*, *kb\_knowledge\_base=dfc19531bf2021003f07e2c1ac0739ab^text ISNOTEMPTY^EQ*, *article\_type=text^active=true^EQ*\.
      + **Include articles based on Regex filter**—Specify a regex pattern to include specific articles\.

   1. For **Service catalog items**:
      +  **Service catalog items**—Choose to index service catalog items\.
      + **Service catalog item attachments**—Choose to index service catalog item attachments\.
      + **Active service catalog items**—Choose to index active service catalog items\.
      + **Inactive service catalog items**—Choose to index inactive service catalog items\.
      + **ServiceNow filter query**—Choose to include service catalog items based on a filter defined in your ServiceNow instance\. Example filter queries include: *workflow\_state=draft^EQ*, *kb\_knowledge\_base=dfc19531bf2021003f07e2c1ac0739ab^text ISNOTEMPTY^EQ*, *article\_type=text^active=true^EQ*\.
      + **Regex filter**—Specify a regex pattern to include specific catalog items\.

   1. For **Incidents**:
      +  **Incidents**—Choose to index service incidents\.
      + **Incident attachments**—Choose to index incident attachments\.
      + **Active incidents**—Choose to index active incidents\.
      + **Inactive incidents**—Choose to index inactive incidents\.
      + **Incident type**—Choose between **All incidents** **Open incidents**, **Open \- unassigned incidents** and **Resolved incidents** depending on your use case\.
      + **ServiceNow Filter query**—Choose to include incidents based on a filter defined in your ServiceNow instance\. Example filter queries include: *workflow\_state=draft^EQ*, *kb\_knowledge\_base=dfc19531bf2021003f07e2c1ac0739ab^text ISNOTEMPTY^EQ*, *article\_type=text^active=true^EQ*\.
      + **Regex filter**—Specify a regex pattern to include specific incidents\.

   1. For **Additional configuration**:
      + **ACL information**—Choose between **Service catalog ACL**, **Knowledge article ACL**, and **Incident ACL** based on your use case\. All access control lists are included by default\. Deselecting an access control list will make all files in that category public\.
      + **Regex patterns**—Add regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. For **Sync mode** choose how you want to update your index when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.
      + **Full sync**—Sync all content regardless of the previous sync status\.
      + **New, modified, and deleted content sync**—Only sync new, modified, and deleted content\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Knowledge articles**, **Service catalog**, **Attachments**, and **Incidents**—Select from the Amazon Kendra generated default data source fields that you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to ServiceNow**

You must specify the following using [TemplateConfiguration API](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html):
+ **Data source**—Specify the data source as `SERVICENOWV2`\. 
+ **Host URL**—Specify the ServiceNow host instance version\. For example, *your\-domain\.service\-now\.com*\.
+ **Auth type**—Specify the type of authentication, whether `basicAuth` or `OAuth2` for your ServiceNow instance\.
+ **ServiceNow instance version**—Specify the ServiceNow instance you are using, whether `Tokyo`, `Sandiego`, `Rome`, or `Others`\.
+ **Data source schema**—Include a JSON that contains the data source schema\. To view the template schema, see [Data source schemas](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+  **Sync mode**—Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose either `FORCED_FULL_CRAWL` to sync all content to your index or `FULL_CRAWL` to sync only new, modified, or deleted content\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your ServiceNow account\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.
+ \(Optional\): You can also configure OAuth2 token for connecting to Amazon Kendra\. The OAuth2 credentials are stored as a JSON string in the Secrets Manager secret\.

  ```
  {
      "username": "user name",
      "password": "password",
      "username": "client id",
      "password": "client-secret"
  }
  ```
+ **IAM role**—Provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the ServiceNow connector and Amazon Kendra\. For more information, see [IAM roles for ServiceNow data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Specific documents to index**—You can use a ServiceNow query to specify the documents you want from one or more knowledge bases, including private knowledge bases\. Access to the knowledge bases is determined by the user that you use to connect to the ServiceNow instance\. For more information, see [Specifying documents to index with a query](https://docs.aws.amazon.com/kendra/latest/dg/servicenow-query.html)\.
+  **Inclusion and exclusion filters**—You can specify whether to include knowledge articles, service catalogs, incidents and their attachments\. You can also specify regular expression patterns to include or exclude knowledge articles, service catalogs, incidents and their attachments\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+ **Enable identity crawler**—Specify whether to activate identity crawler\. If identity crawler is deactivated, you must upload the principal infromation into the principal store using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API\.
+  **Context filtering**—Choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for ServiceNow data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—Choose to map your ServiceNow data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

For a list of other important JSON keys to configure, see [ServiceNow template schema](ds-schemas.md#ds-servicenow-schema)\.

------

## Learn more<a name="servicenow-learn-more"></a>

To learn more about integrating Amazon Kendra with your ServiceNow data source, see:
+ [Getting started with Amazon Kendra ServiceNow Online connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-amazon-kendra-servicenow-online-connector/)