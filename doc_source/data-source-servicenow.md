--------

--------

# Using a ServiceNow data source<a name="data-source-servicenow"></a>

Amazon Kendra can connect to your ServiceNow instance to index your knowledge bases and a service catalog\. For a walkthrough of creating a ServiceNow data source, see [Getting started with a ServiceNow data source \(Console\)](getting-started-servicenow.md)\.

When you use Amazon Kendra to index a ServiceNow instance, you can choose to index public knowledge bases and public service catalogs, or you can use a query to index specific knowledge bases, including private ones\. You can connect to a ServiceNow instance using basic authentication and a ServiceNow administrative user, or you can use an OAuth 2\.0 token and a user with read permission on instance tables\.

For public knowledge bases in your ServiceNow instance, Amazon Kendra indexes only public articles\. A public knowledge base must have the public role under **Can Read**, and **Cannot Read** must be null or not set\.

## Authentication<a name="servicenow-authentication"></a>

There are two forms of authentication that you can use with ServiceNow\. The first, basic authentication, enables Amazon Kendra to connect to the ServiceNow instance using a user name and password\. The user must have administrative permissions to the ServiceNow instance\.

The second, OAuth, uses a token that follows the OAuth 2\.0 authentication specification to identify Amazon Kendra and a user name and password\. The user name and password must provide access to the ServiceNow knowledge base and service catalog\.

### Basic authentication<a name="servicenow-auth-basic"></a>

When you use basic authentication, you provide the user name and password of an administrative user of your ServiceNow instance\. Amazon Kendra uses these credentials to connect to ServiceNow\.

The user name and password for the ServiceNow instance must be stored in an AWS Secrets Manager secret\. If you use the Amazon Kendra console, you can enter the ServiceNow credentials there to create a new secret, or you can choose an existing secret\. If you use the Amazon Kendra API, you must provide the Amazon Resource Name \(ARN\) of an existing secret that contains your ServiceNow user name and password\.

The secret must contain the username and password of the ServiceNow account that you want Amazon Kendra to use to access ServiceNow\. The following is the minimum JSON structure that must be stored in the secret\.

```
{
    "username": "user-name",
    "password": "password"
}
```

The secret can contain other information, but Amazon Kendra ignores it\. For more information, see [What is Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\.

When you create the ServiceNow data source, you specify an IAM role that grants Amazon Kendra permission to access resources required to index your ServiceNow instance\. The data source IAM role must have permission to access the secret and to use the AWS Key Management Service \(AWS KMS\) key to decrypt it\. For more information, see [IAM role for ServiceNow data sources](iam-roles.md#iam-roles-ds-sn)\.

### OAuth authentication<a name="servicenow-auth-oauth"></a>

When you use OAuth authentication to connect to ServiceNow, you provide the client ID and secret that identifies Amazon Kendra to ServiceNow\. You also provide a user name and password that is used to access the knowledge bases and service catalog\.

The client ID, client secret, user name, and password must be stored in an AWS Secrets Manager secret\. If you use the Amazon Kendra console, you can enter the ServiceNow credentials there to create an Secrets Manager secret, or you can choose an existing secret\. If you use the Amazon Kendra API, you must provide the Amazon Resource Name \(ARN\) of an existing Secrets Manager secret that contains your ServiceNow credentials\.

The secret must contain the user name, password, client ID and client secret for your ServiceNow instance\. The following is the minimum JSON structure that must be stored in the Secrets Manager secret\.

```
{
    "username": "user-name",
    "password": "password",
    "clientId": "client-id",
    "clientSecret": "client-secret"
}
```

The secret can contain other information, but Amazon Kendra ignores it\. For more information, see [What is Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\.

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

## Connecting to a ServiceNow instance<a name="servicenow-connection"></a>

You provide ServiceNow connection information in the Amazon Kendra console or by using an instance of the [ ServiceNowConfiguration ](API_ServiceNowConfiguration.md) data type\. You must provide the following information:
+ The ARN of the Secrets Manager secret that contains the credentials required to access the ServiceNow instance\.
+ The version of the ServiceNow instance\. For Amazon Kendra, this is `LONDON` for the London version and `OTHERS` for all other versions\.
+ The ServiceNow instance host\. For example, if the URL of the instance is `https://your-domain.service-now.com`, the host is `your-domain.service-now.com`\.
+ Whether to index knowledge articles, service catalogs, or both\. You must also provide the name of the ServiceNow field that contains the document body\.

You can optionally provide the following information:
+ A ServiceNow query that selects documents from one or more knowledge bases\. The knowledge bases can be public or private\. For more information, see [Specifying documents to index with a query](servicenow-query.md)\.
+ The name of the ServiceNow field that contains the document title\. This is typically the ServiceNow `title` field\. If you don't specify a document title field, Amazon Kendra uses the document ID as the title\.
+ Whether Amazon Kendra should index attachments to knowledge base or catalog items\. If you choose to index attachments, you can specify the file type of attachments to exclude from the index\.
+ Field mappings that map fields in your ServiceNow instance to fields in your Amazon Kendra index\. For more information, see [Mapping data source fields](field-mapping.md)\.
+ An inclusion pattern to specify the file type of document attachments to include in the index\. If you specify an inclusion pattern, any attachment that doesn't match the pattern isn't indexed\. If the pattern includes file types that Amazon Kendra does not support, those files won't be included\. For a list of supported file types, see [Types of documents](index-document-types.md)\.
+ An exclusion pattern to specify the file type of document attachments to exclude from the index\. If you specify an exclusion pattern, any attachment that doesn't match the pattern is indexed\. 

If you specify both an inclusion and an exclusion pattern, attachments that match the exclusion pattern won't be indexed even if they match the inclusion pattern\.

After you sync the data source for the first time, the inclusion and exclusion patterns can't be changed\.

You can map ServiceNow properties to Amazon Kendra index fields\. The following table shows the ServiceNow knowledge article properties that can be mapped and a suggested Amazon Kendra index field\. You can also create custom ServiceNow fields that you map to Amazon Kendra index fields\.


| ServiceNow field name | Suggested Amazon Kendra field name | 
| --- | --- | 
| content | \_document\_body | 
| displayUrl | sn\_display\_url | 
| first\_name | sn\_ka\_first\_name | 
| kb\_category | sn\_ka\_category | 
| kb\_catagory\_name | \_category | 
| kb\_knowledge\_base | sn\_ka\_knowledge\_base | 
| last\_name | sn\_ka\_last\_name | 
| number | sn\_kb\_number | 
| published | sn\_ka\_publish\_date | 
| repItemType | sn\_repItemType | 
| short\_description | \_document\_title | 
| sys\_created\_by | sn\_createdBy | 
| sys\_created\_on | \_created\_at | 
| sys\_id | sn\_sys\_id | 
| sys\_updated\_by | sn\_updatedBy | 
| sys\_updated\_on | \_last\_updated\_at | 
| url | sn\_url | 
| user\_name | sn\_ka\_user\_name | 
| valid\_to | sn\_ka\_valid\_to | 
| workflow\_state | sn\_ka\_workflow\_state | 

The following table shows the ServiceNow catalog properties that can be mapped and a suggested Amazon Kendra field\.


| ServiceNow field name | Suggested Amazon Kendra field name | 
| --- | --- | 
| category | sn\_sc\_category | 
| category\_full\_name | sn\_sc\_category\_full\_name | 
| category\_name | \_category | 
| description | \_document\_body | 
| displayUrl | sn\_display\_url | 
| repItemType | sn\_repItemType | 
| sc\_catalogs | sn\_sc\_catalogs | 
| sc\_catalogs\_name | sn\_sc\_catalogs\_name | 
| short\_description | \_document\_body | 
| sys\_created\_by | sn\_createdBy | 
| sys\_created\_on | \_created\_at | 
| sys\_id | sn\_sys\_id | 
| sys\_updated\_by | sn\_updatedBy | 
| sys\_updated\_on | \_last\_updated\_at | 
| title | \_document\_title | 
| url | sn\_url | 