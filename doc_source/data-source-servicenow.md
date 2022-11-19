--------

--------

# Using a ServiceNow data source<a name="data-source-servicenow"></a>

ServiceNow provides a cloud\-based service management system to create and manage organization\-level workflows, such as IT services, ticketing systems, and support\. If you are a ServiceNow user, you can use Amazon Kendra to index your ServiceNow catalogs and knowledge articles\. You can also configure Amazon Kendra to index specific service catalogs, knowledge articles, and attachments\.

You can connect Amazon Kendra to your ServiceNow data source using either the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) or the [ServiceNowConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ServiceNowConfiguration.html) API\.

For troubleshooting your Amazon Kendra ServiceNow data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-servicenow)
+ [Prerequisites](#prerequisites-servicenow)
+ [Connecting Amazon Kendra to your ServiceNow data source](#data-source-procedure-servicenow)
+ [Specifying documents to index with a query](servicenow-query.md)
+ [Learn more](#servicenow-learn-more)

## Supported features<a name="supported-features-servicenow"></a>
+ Field mappings
+ Inclusion/exclusion patterns: Service catalogs, knowledge articles, attachments

## Prerequisites<a name="prerequisites-servicenow"></a>

Before you can use Amazon Kendra to index your ServiceNow data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your ServiceNow data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have created a ServiceNow administrator account and have created a ServiceNow instance\.
+ In your ServiceNow instance, you have:
  + Copied the host of your ServiceNow instance URL\. For example, if the URL of the instance is *https://your\-domain\.service\-now\.com*, the format for the host URL you enter is *your\-domain\.service\-now\.com*\. You will need your ServiceNow instance URL to connect to Amazon Kendra\.
  + Configured basic authentication credentials to enable Amazon Kendra to connect to the ServiceNow instance using a user name and password\. You will need to store the following credentials in a AWS Secrets Manager secret to connect Amazon Kendra to your ServiceNow instance:
    + username
    + password
  + \(Optional\) Configured an OAuth 2\.0 credential token that can identify Amazon Kendra and generate a user name and password\. The user name and password must provide access to the ServiceNow knowledge base and service catalog\. You will need to store the following credentials in a AWS Secrets Manager secret to connect Amazon Kendra to your ServiceNow instance if you use OAuth 2\.0:
    + client id
    + client secret
    + username
    + password
  + You have added the following read permissions in your ServiceNow account to enable Amazon Kendra to index your ServiceNow knowledge base and service catalog:
    + kb\_category
    + kb\_knowledge
    + kb\_knowledge\_base
    + kb\_uc\_cannot\_read\_mtom
    + kb\_uc\_can\_read\_mtom
    + sc\_catalog
    + sc\_category
    + sc\_cat\_item
    + sys\_attachment
    + sys\_attachment\_doc
    + sys\_user\_role

    You can find more information on how to configure your ServiceNow instance on the [ServiceNow documentation](https://docs.servicenow.com/) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your ServiceNow data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your ServiceNow data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your ServiceNow data source<a name="data-source-procedure-servicenow"></a>

To connect Amazon Kendra to your ServiceNow data source, you must provide details of your ServiceNow credentials so that Amazon Kendra can access your data\. If you have not yet configured ServiceNow for Amazon Kendra see [Prerequisites](#prerequisites-servicenow)\.

### <a name="servicenow-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to ServiceNow** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **ServiceNow**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **ServiceNow host**—Enter the ServiceNow host URL\.

   1. **ServiceNow version**—Select your ServiceNow version\.

   1. Choose between **Basic authentication** and **Oauth 2\.0 authentication** based on your use case\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your ServiceNow authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-ServiceNow\-’ is automatically added to your secret name\.

      1. If using Basic Authentication—Enter the **Secret name** **Username**, and **Password** you generated and downloaded as a JSON file from your ServiceNow account\.

         If using OAuth2 Authentication—Enter the **Secret name** **Username**, **Password**, **Client ID**, and **Client Secret** you generated and downloaded as a JSON file from your ServiceNow account\.

      1. Choose **Save and add secret**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Include knowledge articles**—Choose to index knowledge articles\.

   1. **Type of knowledge articles**—Choose between **Include only public articles** and **Include articles based on ServiceNow filter query** based on your use case\. If you select **Include articles based on ServiceNow filter query**, you must enter a **Filter query** copied from your ServiceNow account\.

   1. **Include knowledge articles attachments**—Choose to index knowledge article attachments\. You can also select specific file types to index\.

   1. **Include catalog items**—Choose to index catalog items\.

   1. **Include catalog item attachments**—Choose to index catalog item attachments\. You can also select specific file types to index\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Knowledge articles** and **Service catalog** —Select from the Amazon Kendra generated default data source fields and additional suggested field mappings that you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ ServiceNowConfiguration API ]

**To connect Amazon Kendra to ServiceNow**

You must specify the following using [ServiceNowConfiguration API](https://docs.aws.amazon.com/kendra/latest/dg/API_ServiceNowConfiguration.html):
+ **Data source URL**—You must specify the ServiceNow URL\. The host endpoint should look like the following: *your\-domain\.service\-now\.com*\.
+ **Data source host instance**—You must specify the ServiceNow host instance version as either `LONDON` or `OTHERS`\.
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your ServiceNow account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```

  If you are using OAuth2 authentication, the secret is stored in a JSON structure with the following keys:

  ```
  {
      "username": "user name",
      "password": "password",
      "clientId": "client id",
      "clientSecret": "client secret"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for ServiceNow data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the ServiceNow connector and Amazon Kendra\. For more information, see [IAM roles for ServiceNow data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Field mappings**—You can choose to map your ServiceNow data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **Inclusion and exclusion filters**—You can specify whether to include ServiceNow catalogs and knowledge articles\. You can also specify regular expression patterns to include or exclude specific attachments of ServiceNow catalogs and knowledge articles\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+ **Indexing parameters**—You can also choose to specify whether to:
  + Index knowledge articles and service catalogs, or both of these If you choose to index knowledge articles and service catalog items, you must provide the name of the ServiceNow field that is mapped to the index document contents field in the Amazon Kendra index\.
  + Index attachments to knowledge articles and catalog items\.
  + Use a ServiceNow query that selects documents from one or more knowledge bases\. The knowledge bases can be public or private\. For more information, see [Specifying documents to index with a query](https://docs.aws.amazon.com/kendra/latest/dg/servicenow-query.html)\.

------

## Learn more<a name="servicenow-learn-more"></a>

To learn more about integrating Amazon Kendra with your ServiceNow data source, see:
+ [Getting started with Amazon Kendra ServiceNow Online connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-amazon-kendra-servicenow-online-connector/)