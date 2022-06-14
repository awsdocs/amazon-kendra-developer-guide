--------

--------

# Using a GitHub data source<a name="data-source-github"></a>

You can use your GitHub repository or repositories as a data source for Amazon Kendra\. To use GitHub in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add GitHub\.

When you connect to GitHub to index your documents, you specify whether you use GitHub Enterprise Cloud \(SaaS\) or GitHub Enterprise Server \(on premises\)\. You provide the GitHub host URL for your type of GitHub service that you use\. For example, the host URL for GitHub cloud could be *https://api\.github\.com* and the host URL for GitHub server could be *https://on\-prem\-host\-url/api/v3/*\. 

You also provide the organization name for the repositories\. You can find your organization name by logging into GitHub desktop and selecting **Your organizations** under your profile picture dropdown\. If you use GitHub server, you must use an Amazon Virtual Private Cloud \(VPC\) to connect to your GitHub server\. You can specify regular expression patterns to include or exclude specific files within in your GitHub repositories\. You can specify which repositories you want to index\. You can choose whether to only index the files in the repositories, or also include issues and pull requests, and their comments and comment attachments\.

You must create an index before you create the GitHub data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to GitHub, you specify the connection and other information in the console or by using the [GitHubConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GitHubConfiguration.html) object\. You provide the GitHub host URL or API endpoint URL and the GitHub organization name associated with the repositories that you want to index\.

Before you can index your documents or content from your GitHub repositories, you must be a GitHub user with administrative permissions to the organization in the GitHub enterprise account\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your GitHub organization\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for GitHub data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your GitHub organization\. See [Authentication](#github-authentication)\.

Amazon Kendra also crawls user information from the GitHub instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for GitHub data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-github)\.

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of comments of your GitHub content\. Each comment is indexed as a separate document\.
+ Whether Amazon Kendra should use the GitHub change log mechanism to determine if content needs to be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the files\. However, if your change log is large, it may take Amazon Kendra less time to scan the files in the GitHub repositories than to process the change log\. If you are syncing your GitHub data source with your index for the first time, all files are scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any repository file with a file name or file type that does not match the pattern is not indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your GitHub fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="github-authentication"></a>

The authentication credentials to access your GitHub organization must include your GitHub access token\. You create the token in GitHub\. You store your GitHub credentials in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{ 
        "githubToken": token
}
```

**To create a token in GitHub**

1. Log in to the GitHub desktop application\. You must have administrative permissions to the organization in the GitHub enterprise account\.

1. Select your profile picture dropdown at the top of the page, then select **Your organizations**\.

1. Select **Settings** next to your organization name, then select **Developer settings**\.

1. In the **OAuth Apps** section, select **Personal access tokens** and then **Generate new token**\. 

1. Enter a name for your token\. For example, *kendra\_github\_token*\.

1. Set the expiration of your token\.

1. If you use GitHub Enterprise Cloud \(SaaS\), choose the following permissions:
   + repo:status
   + public\_repo
   + repo:invite
   + read:org
   + user:email
   + read:user

   If you use GitHub Enterprise Server \(on premises\), choose the following permissions:
   + repo:status
   + public\_repo
   + repo:invite
   + read:org
   + user:email
   + read:user
   + site\_admin

1. Select **Generate token**\.

1. Copy the token\. You'll need this when you create the Secrets Manager secret for the GitHub data source\.