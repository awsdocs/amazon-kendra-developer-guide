--------

--------

# Getting started with an AWS Single Sign\-On identity source \(console\)<a name="getting-started-aws-sso"></a>

An AWS Single Sign\-On identity source contains information on access levels of groups and users\. This is useful for setting up user context filtering, where Amazon Kendra filters search results for different users based on their group's access to documents\.

To create an AWS SSO identity source, you must enable AWS SSO and create an organization\. When you enable AWS SSO and create an organization for the first time, it automatically creates AWS SSO identity store as the default identity source\. You can change to Active Directory \(Amazon managed or self\-managed\) or an external identity provider as your identity source\. You must follow the correct guidance for this – see [Changing your AWS SSO identity source](https://docs.aws.amazon.com/kendra/latest/dg/changing-aws-sso-source.html)\. You can have only one identity source per organization\.

In order for your groups in AWS SSO to be assigned different levels of access to documents, you need to include your groups in your Access Control List when you ingest documents into your index\. This allows your groups to search for documents in Amazon Kendra in accordance with their level of access\. When you issue a query, the user ID needs to be an exact match of the user name in AWS SSO\. 

You must also grant the required permissions to use AWS SSO with Amazon Kendra\. For more information, see [IAM roles for AWS Single Sign\-On](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-aws-sso)\.

**To set up an AWS SSO identity source**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Enable AWS SSO**, and then choose **Create AWS organization**\.

   AWS SSO identity store is created by default, and an email is sent to you to verify the email address associated with the organization\.

1. To add a group to your AWS organization, in the navigation pane, choose **Groups**\.

1. On the **Groups page**, choose **Create group** and enter a group name and description in the dialog box\. Choose **Create**\.

1. To add a user to your AWS SSO organization, in the navigation pane, choose **Users**\.

1. On the **Users** page, choose **Add user**\. Under **User details**, specify all required fields\. For **Password**, choose **Send an email to the user**\. Choose **Next**\.

1. To add a user to a group, choose **Groups** and select a group\.

1. On the **Details** page, under **Group members**, choose **Add user**\.

1. On the **Add users to group** page, select the user you want to add as a member of the group\. You can select multiple users to add to a group\.

1. To sync your list of users and groups with AWS SSO, change your identity source to Active Directory or External identity provider\.

   AWS SSO identity store is the default identity source and requires you to manually add your users and groups using this source if you do not have your own list managed by a provider\. To change your identity source, you must follow the correct guidance for this – see [Changing your AWS SSO identity source](https://docs.aws.amazon.com/kendra/latest/dg/changing-aws-sso-source.html)\.

**Note**  
If using Active Directory or an external identity provider as your identity source, you must map the email addresses of your users to AWS SSO user names when you specify the System for Cross\-domain Identity Management \(SCIM\) protocol\. For more information, see the [AWS SSO guide on SCIM for configuring AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/scim-profile-saml.html)\.

Once you have set up your AWS SSO identity source, you can enable this in the console when you create or edit your index\. Go to **User access control** in your index settings and edit your settings to enable fetching user\-group information from AWS SSO\. You can also enable AWS SSO using the [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html) object\. You provide the `UserGroupResolutionMode` as `AWS_SSO` and create an IAM role that gives permission to call `sso:ListDirectoryAssociations`, `sso-directory:SearchUsers`, `sso-directory:ListGroupsForUser`, `sso-directory:DescribeGroups`\.

**Warning**  
Amazon Kendra currently does not support using `UserGroupResolutionConfiguration` with an AWS organization member account for your AWS SSO identify source\. You must create your index in the management account for the organization in order to use `UserGroupResolutionConfiguration`\.

The following is an overview of how to set up a data source with `UserGroupResolutionConfiguration` and user access control to filter search results on user context\. This assumes you have already created an index and an IAM role that can run Amazon Kendra APIs for indexes\. You create an index and provide the IAM role using the [CreateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateIndex.html) API\.

**Setting up a data source with `UserGroupResolutionConfiguration` and user context filtering**

1. Create an [IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-aws-sso) that gives permission to access your AWS SSO identity source\.

1. Configure [https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html) by setting the mode to `AWS_SSO` and call [UpdateIndex](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html) to update your index to use AWS SSO\.

1. If you want to use token\-based user access control to filter search results on user context, set [UserContextPolicy](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateIndex.html#Kendra-UpdateIndex-request-UserContextPolicy) to `USER_TOKEN` when you call `UpdateIndex`\. Otherwise, Amazon Kendra crawls the Access Control List for each of your documents for most data source connectors\. You can also filter search results on user context in the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API by providing user and group information in `UserContext`\. You can also map users to their groups using [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) so that you only need to provide the user ID when you issue the query\.

1. Create an [IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) that gives permission to access your data source\.

1. [Configure](https://docs.aws.amazon.com/kendra/latest/dg/API_DataSourceConfiguration.html) your data source\. You must provide the required connection information to connect to your data source\.

1. Create a data source using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. Provide the `DataSourceConfiguration` object, the ID of your index, the IAM role for your data source, the data source type, and give your data source a name\. You can also update your data source\.