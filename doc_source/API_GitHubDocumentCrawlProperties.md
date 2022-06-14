--------

--------

# GitHubDocumentCrawlProperties<a name="API_GitHubDocumentCrawlProperties"></a>

Provides the configuration information to include certain types of GitHub content\. You can configure to index repository files only, or also include issues and pull requests, comments, and comment attachments\.

## Contents<a name="API_GitHubDocumentCrawlProperties_Contents"></a>

 ** CrawlIssue **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlIssue"></a>
 `TRUE` to index all issues within a repository\.  
Type: Boolean  
Required: No

 ** CrawlIssueComment **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlIssueComment"></a>
 `TRUE` to index all comments on issues\.  
Type: Boolean  
Required: No

 ** CrawlIssueCommentAttachment **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlIssueCommentAttachment"></a>
 `TRUE` to include all comment attachments for issues\.  
Type: Boolean  
Required: No

 ** CrawlPullRequest **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlPullRequest"></a>
 `TRUE` to index all pull requests within a repository\.  
Type: Boolean  
Required: No

 ** CrawlPullRequestComment **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlPullRequestComment"></a>
 `TRUE` to index all comments on pull requests\.  
Type: Boolean  
Required: No

 ** CrawlPullRequestCommentAttachment **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlPullRequestCommentAttachment"></a>
 `TRUE` to include all comment attachments for pull requests\.  
Type: Boolean  
Required: No

 ** CrawlRepositoryDocuments **   <a name="Kendra-Type-GitHubDocumentCrawlProperties-CrawlRepositoryDocuments"></a>
 `TRUE` to index all files with a repository\.  
Type: Boolean  
Required: No

## See Also<a name="API_GitHubDocumentCrawlProperties_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GitHubDocumentCrawlProperties) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GitHubDocumentCrawlProperties) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GitHubDocumentCrawlProperties) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GitHubDocumentCrawlProperties) 