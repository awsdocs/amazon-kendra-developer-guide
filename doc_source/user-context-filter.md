--------

--------

# Filtering on user context<a name="user-context-filter"></a>

You can filter a user's search results based on the user or their group access to documents\. You can use a user token, user ID, or user attribute to filter documents\. Amazon Kendra can also map users to their groups\. You can choose to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\) as your identity store/source\.

User context filtering is a kind of personalized search with the benefit of controlling access to documents\. For example, not all teams that search the company portal for information should access top\-secret company documents, nor are these documents relevant to all users\. Only specific users or groups of teams given access to top\-secret documents should see these documents in their search results\.

When a document is indexed into Amazon Kendra, a corresponding Access Control List \(ACL\) is ingested for most documents\. The ACL specifies which user names and group names are allowed or denied access to the document\. Documents without an ACL are public documents\.

Amazon Kendra automatically extracts the user or group information associated with each document in most data sources\. For example, a document in Quip can include a 'share' list of select users or groups that are given access to the document\. If you use an S3 bucket as a data source, you provide a [JSON file](https://docs.aws.amazon.com/kendra/latest/dg/s3-acl.html) for your ACL and include the S3 path to this file as part of the data source configuration\. If you add documents directly to an index, you specify the ACL in the [Principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) object as part of the document object in the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API\.

You can use the [CreateAccessControlConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateAccessControlConfiguration.html) API to re\-configure your existing document level access control without indexing all of your documents again\. For example, your index contains top\-secret company documents that only certain employees or users should access\. One of these users leaves the company or switches to a team that should be blocked from accessing top\-secret documents\. The user still has access to top\-secret documents because the user had access when your documents were previously indexed\. You can create a specific access control configuration for the user with deny access\. You can later update the access control configuration to allow access in the case the user returns to the company and re\-joins the 'top\-secret' team\. You can re\-configure access control for your documents as circumstances change\.

To apply your access control configuration to certain documents, you call the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API with the `AccessControlConfigurationId` included in the [Document](https://docs.aws.amazon.com/kendra/latest/dg/API_Document.html) object\. If you use an S3 bucket as a data source, you update the `.metadata.json` with the `AccessControlConfigurationId` and synchronize your data source\. Amazon Kendra currently only supports access control configuration for S3 data sources and documents indexed using the `BatchPutDocument` API\.

## Filtering by user token<a name="context-filter-token"></a>

When you query an index, you can use a user token to filter search results based on the user or their group access to documents\. When you issue a query, Amazon Kendra extracts and validates the token, pulls and checks the user and group information, and runs the query\. All of the documents the user has access to, including public documents, are returned\. For more information, see [Token\-based user access control](https://docs.aws.amazon.com/kendra/latest/dg/create-index-access-control.html)\.

You provide the user token in the [UserContext](https://docs.aws.amazon.com/kendra/latest/dg/API_UserContext.html) object and pass this in the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API\.

The following shows how to include a user token\. 

```
response = kendra.query(
    QueryText = query,
    IndexId = index,
    UserToken = {
        Token = "token"
    })
```

You can map users to groups\. When you use user\-context filtering, it is not required to include all of the groups that a user belongs to when you issue the query\. With the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API, you can map users to their groups\. If you do not want to use the `PutPrincipalMapping` API, you must provide the user name and all the groups the user belongs to when you issue a query\. You can also fetch access levels of groups and users in your IAM Identity Center identity source by using the [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html) object\.

## Filtering by user ID<a name="context-filter-user-incl-datasources"></a>

When you query an index, you can use the user and group IDs to filter search results based on the user or their group access to documents\. When you issue a query, Amazon Kendra checks the user and group information and runs the query\. All of the documents relevant to the query that the user has access to, including public documents, are returned\.

You can also filter search results by data sources that users and groups have access to\. Specifying a data source is useful if a group is tied to multiple data sources, but you only want the group to access documents of a certain data source\. For example, the groups "Research", "Engineering", and "Sales and Marketing" are all tied to the company's documents stored in the data sources Confluence and Salesforce\. However, "Sales and Marketing" team only needs access to customer\-related documents stored in Salesforce\. So when sales and marketing users search for customer\-related documents, they can see documents from Salesforce in their results\. Users who do not work in sales and marketing do not see Salesforce documents in their search results\.

You provide the user, groups and data sources information in the [UserContext](https://docs.aws.amazon.com/kendra/latest/dg/API_UserContext.html) object and pass this in the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API\. The user ID, and the list of groups and data sources should match the name you specify in the [Principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) object to identify the user, groups, and data sources\. With the `Principal` object, you can add a user, group, or data source to either an allow list or a deny list for accessing a document\.

You are required to provide one of the following:
+ User and groups information, and \(optional\) data sources information\.
+ Only the user information if you map your users to groups and data sources using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API\. You can also fetch access levels of groups and users in your IAM Identity Center identity source by using the [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html) object\.

If this information is not included in the query, Amazon Kendra returns all documents\. If you provide this information, only documents with matching user IDs, groups, and data sources are returned\.

The following shows how to include user ID, groups, and data sources\.

```
response = kendra.query(
    QueryText = query,
    IndexId = index,
    UserId = {
        UserId = "user1"
    },
    Groups = {
        Groups = ["Sales and Marketing"]
    },
    DataSourceGroups = {
        DataSourceGroups = [{"DataSourceId" : "SalesforceCustomerDocsGroup", "GroupId": "Sales and Marketing"}]
    })
```

## Filtering by user attribute<a name="context-filter-attribute"></a>

When you query an index, you can use built\-in attributes `_user_id` and `_group_id` to filter search results based on the user and their group access to documents\. You can set up to 100 group identifiers\. When you issue a query, Amazon Kendra checks the user and group information and runs the query\. All documents relevant to the query that the user has access to, including public documents, are returned\.

You provide the user and groups attributes in the [AttributeFilter](https://docs.aws.amazon.com/kendra/latest/dg/API_AttributeFilter.html) object and pass this in the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API\.

The following example shows a request that filters the query response based on the user ID and the groups "HR" and "IT", which the user belongs to\. The query will return any document that has the user or the "HR" or "IT" groups in the allow list\. If the user or either group is in the deny list for a document, the document is not returned\.

```
response = kendra.query(
        QueryText = query,
        IndexId = index,
        AttributeFilter = {
            "OrAllFilters": [
                {
                    "EqualsTo": {
                        "Key": "_user_id",
                        "Value": {
                            "StringValue": "user1"
                        }
                     }
                },
                {
                    "EqualsTo": {
                        "Key": "_group_ids",
                        "Value": {
                            "StringListValue": ["HR", "IT"]
                        }
                    }
                }
            ]
        }
        )
```

You can also specify which data source a group can access in the `Principal` object\.

**Note**  
User context filtering isn't an authentication or authorization control for your content\. It doesn't do user authentication on the user and groups sent to the `Query` API\. It is up to your application to ensure that the user and group information sent to `Query` API is authenticated and authorized\.

There is an implementation of user context filtering for each data source\. The following section describes each implementation\. 

**Topics**
+ [Filtering by user token](#context-filter-token)
+ [Filtering by user ID](#context-filter-user-incl-datasources)
+ [Filtering by user attribute](#context-filter-attribute)
+ [User context filtering for documents added directly to an index](#context-filter-batch)
+ [User context filtering for frequently asked questions](#context-filter-faq)
+ [User context filtering for database data sources](#context-filter-jdbc)
+ [User context filtering for Confluence data sources](#context-filter-confluence)
+ [User context filtering for Google Drive data sources](#context-filter-google)
+ [User context filtering for Microsoft OneDrive data sources](#context-filter-onedrive)
+ [User context filtering for Amazon S3 data sources](#context-filter-s3)
+ [User context filtering for Salesforce data sources](#context-filter-salesforce)
+ [User context filtering for ServiceNow data sources](#context-filter-servicenow)
+ [User context filtering for Microsoft SharePoint data sources](#context-filter-sharepoint-online)
+ [User context filtering for Amazon WorkDocs data sources](#context-filter-workdocs)
+ [User context filtering for Amazon FSx data sources](#context-filter-fsx)
+ [User context filtering for Slack data sources](#context-filter-slack)
+ [User context filtering for Box data sources](#context-filter-box)
+ [User context filtering for Quip data sources](#context-filter-quip)
+ [User context filtering for Jira data sources](#context-filter-jira)
+ [User context filtering for GitHub data sources](#context-filter-github)
+ [User context filtering for Alfresco data sources](#context-filter-alfresco)
+ [User context filtering for Zendesk data sources](#context-filter-zendesk)
+ [User context filtering for Dropbox data sources](#context-filter-dropbox)

## User context filtering for documents added directly to an index<a name="context-filter-batch"></a>

When you add documents directly to an index using the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API, Amazon Kendra gets user and group information from the `AccessControlList` field of the document\. You provide an Access Control List \(ACL\) for your documents and the ACL is ingested with your documents\.

You specify the ACL in the [Principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) object as part of the [Document](https://docs.aws.amazon.com/kendra/latest/dg/API_Document.html) object in the `BatchPutDocument` API\. You provide the following information:
+ The access that the user or group should have\. You can say `ALLOW` or `DENY`\.
+ The type of entity\. You can say `USER` or `GROUP`\.
+ The name of the user or group\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for frequently asked questions<a name="context-filter-faq"></a>

When you [add a FAQ](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateFaq.html) to an index, Amazon Kendra gets user and group information from the `AccessControlList` object/field of the FAQ JSON file\. You can also use a FAQ CSV file with custom fields or attributes for access control\.

You provide the following information:
+ The access that the user or group should have\. You can say `ALLOW` or `DENY`\.
+ The type of entity\. You can say `USER` or `GROUP`\.
+ The name of the user or group\.

For more information, see [FAQ files](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html)\.

## User context filtering for database data sources<a name="context-filter-jdbc"></a>

When you use a database data source, such as Amazon Aurora PostgreSQL, Amazon Kendra gets user and group information from a column in the source table\. You specify this column in the [AclConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AclConfiguration.html) object as part of the [DatabaseConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_DatabaseConfiguration.html) object in the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\.

A database data source has the following limitations:
+ You can only specify an allow list for a database data source\. You can't specify a deny list\. 
+ You can only specify groups\. You can't specify individual users for the allow list\.
+ The database column should be string containing a semicolon delimited list of groups\.

## User context filtering for Confluence data sources<a name="context-filter-confluence"></a>

When you use a Confluence data source, Amazon Kendra gets user and group information from the Confluence instance\.

You configure user and group access to spaces using the space permissions page\. For pages and blogs, you use the restrictions page\. For more information about space permissions, see [ Space Permissions Overview ](https://confluence.atlassian.com/doc/space-permissions-overview-139521.html) on the Confluence Support website\. For more information about page and blog restrictions, see [ Page Restrictions ](https://confluence.atlassian.com/doc/page-restrictions-139414.html) on the Confluence Support website\.

The Confluence group and user names are mapped as follows:
+ `_group_ids`—Group names are present on spaces, pages, and blogs where there are restrictions\. They are mapped from the name of the group in Confluence\. Group names are always lower case\.
+ `_user_id`—User names are present on the space, page, or blog where there are restrictions\. They are mapped depending on the type of Confluence instance that you are using\.
  + Server—The `_user_id` is the username\. The username is always lower case\.
  + Cloud—The `_user_id` is the account ID of the user\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Google Drive data sources<a name="context-filter-google"></a>

A Google Workspace Drive data source returns user and group information for Google Drive users and groups\. Group and domain membership are mapped to the `_group_ids` index field\. The Google Drive user name is mapped to the `_user_id` field\.

When you provide one or more user email addresses in the `Query` API, only documents that have been shared with those email addresses are returned\. The following `AttributeFilter` parameter only returns documents shared with "martha@example\.com"\.

```
"AttributeFilter": {
                "EqualsTo":{
                   "Key": "_user_id", 
                   "Value": {
                       "StringValue": "martha@example.com"
                   }
               }
           }
```

If you provide one or more group email addresses in the query, only documents shared with the groups are returned\. The following `AttributeFilter` parameter only returns documents shared with the "hr@example\.com" group\.

```
"AttributeFilter": {
                "EqualsTo":{
                   "Key": "_group_ids", 
                   "Value": {
                       "StringListValue": ["hr@example.com"]
                   }
               }
           }
```

If you provide the domain in the query, all documents shared with the domain are returned\. The following `AttributeFilter` parameter returns documents shared with the "example\.com" domain\.

```
"AttributeFilter": {
                "EqualsTo":{
                   "Key": "_group_ids", 
                   "Value": {
                       "StringListValue": ["example.com"]
                   }
               }
           }
```

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Microsoft OneDrive data sources<a name="context-filter-onedrive"></a>

Amazon Kendra retrieves user and group information from Microsoft OneDrive when it indexes the documents on the site\. The user and group information is taken from the underlying Microsoft SharePoint site that hosts OneDrive\.

When you use a OneDrive user or group for user context filtering, calculate the ID as follows:

1. Get the site name\. For example, `https://host.onmicrosoft.com/sites/siteName.`

1. Take the MD5 hash of the site name\. For example, `430a6b90503eef95c89295c8999c7981`\.

1. Create the user email or group ID by concatenating the MD5 hash with a vertical bar \(\|\) and the ID\. For example, if a group name is "site owners", the group ID would be:

   `"430a6b90503eef95c89295c8999c7981|site owners"`

   For the user name "someone@host\.onmicrosoft\.com," the user ID would be the following:

   `"430a6b90503eef95c89295c8999c7981|someone@host.onmicrosoft.com"`

Send the user or group ID to Amazon Kendra as the `_user_id` or `_group_ids` attribute when you call the [Query](API_Query.md) API\. For example, the AWS CLI command that uses a group to filter the query response looks like this:

```
aws kendra  query \
                --index-id index ID  
                --query-text "query text" 
                --attribute-filter '{
                   "EqualsTo":{
                     "Key": "_group_ids", 
                     "Value": {"StringValue": "430a6b90503eef95c89295c8999c7981|site owners"}
                  }}'
```

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Amazon S3 data sources<a name="context-filter-s3"></a>

You add user context filtering to a document in an Amazon S3 data source using a metadata file associated with the document\. You add the information to the `AccessControlList` field in the JSON document\. For more information about adding metadata to the documents indexed from an Amazon S3 data source, see [Amazon S3 document metadata](s3-metadata.md)\.

You provide three pieces of information:
+ The access that the entity should have\. You can say `ALLOW` or `DENY`\.
+ The type of entity\. You can say `USER` or `GROUP`\.
+ The name of the entity\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Salesforce data sources<a name="context-filter-salesforce"></a>

A Salesforce data source returns user and group information from Salesforce access control list \(ACL\) entities\. You can apply user context filtering to Salesforce standard objects and chatter feeds\. User context filtering is not available for Salesforce knowledge articles\.

For standard objects, the `_user_id` and `_group_ids` are used as follows:
+ `_user_id`—The user name of the Salesforce user\.
+ `_group_ids`—
  + Name of the Salesforce `Profile`
  + Name of the Salesforce `Group`
  + Name of the Salesforce `UserRole`
  + Name of the Salesforce `PermissionSet`

For chatter feeds, the `_user_id` and `_group_ids` are used as follows:
+ `_user_id`—The user name of the Salesforce user\. Only available if the item is posted in the user's feed\.
+ `_group_ids`—Group IDs are used as follows\. Only available if the feed item is posted in a chatter or collaboration group\.
  + The name of the chatter or collaboration group\.
  + If the group is public, `PUBLIC:ALL`\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for ServiceNow data sources<a name="context-filter-servicenow"></a>

User context filtering isn't currently supported for ServiceNow\.

## User context filtering for Microsoft SharePoint data sources<a name="context-filter-sharepoint-online"></a>

Amazon Kendra retrieves user and group information from Microsoft SharePoint when it indexes the documents on the site\. To filter your documents, provide user and group information when you call the `Query` API\. 

To filter using a user name, use the user's email address\. For example, johnstiles@example\.com\.

When you use a SharePoint group for user context filtering, calculate the group ID as follows:

1. Get the site name\. For example, `https://host.onmicrosoft.com/sites/siteName.`

1. Take the SHA256 hash of the site name\. For example, `430a6b90503eef95c89295c8999c7981`\.

1. Create the group ID by concatenating the SHA256 hash with a vertical bar \(\|\) and the group name\. For example, if the group name is "site owners", the group ID would be:

   `"430a6b90503eef95c89295c8999c7981|site owners"`

Send the group ID to Amazon Kendra as the `_group_ids` attribute when you call the [Query](API_Query.md) API\. For example, the AWS CLI command looks like this:

```
aws kendra  query \
                --index-id index ID  
                --query-text "query text" 
                --attribute-filter '{
                   "EqualsTo":{
                     "Key": "_group_ids", 
                     "Value": {"StringValue": "430a6b90503eef95c89295c8999c7981|site owners"}
                  }}'
```

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Amazon WorkDocs data sources<a name="context-filter-workdocs"></a>

When you use an Amazon WorkDocs data source, Amazon Kendra gets user and group information from the Amazon WorkDocs instance\.

The Amazon WorkDocs group and user IDs are mapped as follows:
+ `_group_ids`—Group IDs exist in Amazon WorkDocs on files where there are set access permissions\. They are mapped from the names of the groups in Amazon WorkDocs\.
+ `_user_id`—User IDs exist in Amazon WorkDocs on files where there are set access permissions\. They are mapped from the user names in Amazon WorkDocs\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Amazon FSx data sources<a name="context-filter-fsx"></a>

When you use an Amazon FSx data source, Amazon Kendra gets user and group information from the directory service of the Amazon FSx instance\.

The Amazon FSx group and user IDs are mapped as follows:
+ `_group_ids`—Group IDs exist in Amazon FSx on files where there are set access permissions\. They are mapped from the system group names in the directory service of Amazon FSx\.
+ `_user_id`—User IDs exist Amazon FSx on files where there are set access permissions\. They are mapped from the system user names in the directory service of Amazon FSx\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Slack data sources<a name="context-filter-slack"></a>

When you use a Slack data source, Amazon Kendra gets the user information from the Slack instance\.

The Slack user IDs are mapped as follows:
+ `_user_id`—User IDs exist in Slack on messages and channels where there are set access permissions\. They are mapped from the user emails as the IDs in Slack\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Box data sources<a name="context-filter-box"></a>

When you use a Box data source, Amazon Kendra gets user and group information from the Box instance\.

The Box group and user IDs are mapped as follows:
+ `_group_ids`—Group IDs exist in Box on files where there are set access permissions\. They are mapped from the names of the groups in Box\.
+ `_user_id`—User IDs exist in Box on files where there are set access permissions\. They are mapped from the user emails as the user IDs in Box\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Quip data sources<a name="context-filter-quip"></a>

When you use a Quip data source, Amazon Kendra gets the user information from the Quip instance\.

The Quip user IDs are mapped as follows:
+ `_user_id`—User IDs exist in Quip on files where there are set access permissions\. They are mapped from the user emails as the IDs in Quip\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Jira data sources<a name="context-filter-jira"></a>

When you use a Jira data source, Amazon Kendra gets user and group information from the Jira instance\.

The Jira user IDs are mapped as follows:
+ `_user_id`—User IDs exist in Jira on files where there are set access permissions\. They are mapped from the user emails as the user IDs in Jira\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for GitHub data sources<a name="context-filter-github"></a>

When you use a GitHub data source, Amazon Kendra gets user information from the GitHub instance\.

The GitHub user IDs are mapped as follows:
+ `_user_id`—User IDs exist in GitHub on files where there are set access permissions\. They are mapped from the user emails as the IDs in GitHub\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Alfresco data sources<a name="context-filter-alfresco"></a>

When you use an Alfresco data source, Amazon Kendra gets the user and group information from the Alfresco instance\.

The group and user IDs are mapped as follows:
+ `_group_ids`—Group IDs exist in Alfresco on files where there are set access permissions\. They are mapped from the system names of the groups \(not display names\) in Alfresco\.
+ `_user_id`—User IDs exist in Alfresco on files where there are set access permissions\. They are mapped from the user emails as the IDs in Alfresco\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Zendesk data sources<a name="context-filter-zendesk"></a>

When you use an Zendesk data source, Amazon Kendra gets the user and group information from the Zendesk instance\.

The group and user IDs are mapped as follows:
+ `_group_ids`—Group IDs exist in Zendesk tickets and articles where there are set access permissions\. They are mapped from the names of the groups in Zendesk\.
+ `_user_id`—Group IDs exist in Zendesk tickets and articles where there are set access permissions\. They are mapped from the user emails as the IDs in Zendesk\.

You can add up to 200 entries in the `AccessControlList` field\.

## User context filtering for Dropbox data sources<a name="context-filter-dropbox"></a>

When you use a Dropbox data source, Amazon Kendra gets the user and group information from the Dropbox instance\.

The group and user IDs are mapped as follows:
+ `_group_ids` – Group IDs exist in Dropbox on files where there are set access permissions\. They are mapped from the names of the groups in Dropbox\.
+ `_user_id` – User IDs exist in Dropbox on files where there are set access permissions\. They are mapped from the user emails as the IDs in Dropbox\.

You can add up to 200 entries in the `AccessControlList` field\.