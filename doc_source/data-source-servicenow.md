--------

--------

# Using a ServiceNow data source<a name="data-source-servicenow"></a>

You can use your ServiceNow instance as a data source for Amazon Kendra\. To use ServiceNow in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add ServiceNow\.

For troubleshooting your Amazon Kendra ServiceNow data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create the ServiceNow data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

Before you can index your documents from your ServiceNow instance, you must use a user name and password with administrative permissions for the ServiceNow instance\.

When you connect to ServiceNow to index your documents, you specify the host of your ServiceNow instance URL\. For example, if the URL of the instance is *https://your\-domain\.service\-now\.com*, the host is *your\-domain\.service\-now\.com*\. You also specify the instance version that the ServiceNow host is running—whether the host is running the `LONDON` instance version or `OTHERS`\. You can specify regular expression patterns to include or exclude specific attachments of ServiceNow catalogs and knowledge articles\.

To connect to ServiceNow, you specify the connection and other information in the console or by using the [ServiceNowConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ServiceNowConfiguration.html) object\. You provide the ServiceNow host and instance version for the host\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your ServiceNow instance\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for ServiceNow data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your ServiceNow instance\. See [Authentication](#servicenow-authentication)\.

Amazon Kendra currently doesn't support user context filtering for ServiceNow data sources\. User context filtering limits search results to users based on their authorized access to documents\.

You also can add the following optional information:
+ Whether to index knowledge articles and service catalogs, or both of these\. You must also provide the name of the ServiceNow field that contains the document body\.
+ Whether to index attachments to knowledge articles and catalog items\.
+ Whether to use a ServiceNow query that selects documents from one or more knowledge bases\. The knowledge bases can be public or private\. For more information, see [Specifying documents to index with a query](https://docs.aws.amazon.com/kendra/latest/dg/servicenow-query.html)\.
+ Inclusion or exclusion patterns: If you specify an inclusion pattern, only content that matches the inclusion pattern is indexed\. Any attachment of catalogs or knowledge articles with a name or type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, attachments that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your ServiceNow catalog and knowledge article fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="servicenow-authentication"></a>

There are two types of authentication that you can use with ServiceNow\. The first, basic authentication, enables Amazon Kendra to connect to the ServiceNow instance using a user name and password\. The user must have administrative permissions to the ServiceNow instance\.

The second, OAuth, uses the OAuth 2\.0 authentication specification to identify Amazon Kendra and a user name and password\. The user name and password must provide access to the ServiceNow knowledge base and service catalog\.

It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.

### Basic authentication<a name="servicenow-auth-basic"></a>

When you use basic authentication, you provide the user name and password of an administrative user of your ServiceNow instance\. Amazon Kendra uses these credentials to connect to ServiceNow\.

You store your user name and password in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The basic credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user name",
    "password": "password"
}
```

### OAuth authentication<a name="servicenow-auth-oauth"></a>

When you use OAuth authentication to connect to ServiceNow, you provide the client ID and secret that identifies Amazon Kendra to ServiceNow\. You also provide a user name and password that is used to access the knowledge bases and service catalog\.

You store your client ID, client secret, user name, and password in an AWS Secrets Manager secret\. You generate the client ID and client secret in ServiceNow\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The OAuth credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user name",
    "password": "password",
    "clientId": "client id",
    "clientSecret": "client secret"
}
```

#### Generating the client ID and secret<a name="oauth-token"></a>

You generate the OAuth client ID and secret using the ServiceNow console and then copy them to the Amazon Kendra console\. Create the client ID and secret using the following procedure\.

**To create a ServiceNow client ID and secret**

1. Log in to the ServiceNow console\.

1. From the left menu, choose **System OAuth** and then choose **Application Registry**\.

1. Choose **New** to create a new registry\.

1. For the type of OAuth application, choose **Create an OAuth application endpoint for external clients**\.

1. Enter a name\.

1. You can enter your own client secret, or you can have ServiceNow generate one for you\. Leave the defaults for the other fields\.

1. Choose **Submit** to create the registry containing the OAuth client secret and ID\.

1. After the registry is created, choose it from the list of registries\.

1. Copy the client secret and ID\. You'll need them when you create the ServiceNow data source\.

#### Table permissions<a name="oauth-tables"></a>

When you use OAuth authentication, you provide a user name and password\. Amazon Kendra sends the user name and password to ServiceNow\. ServiceNow uses them to determine the access that Amazon Kendra has to the ServiceNow instance\. To index a knowledge base and service catalog, the user must have read permission on the following tables\.
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