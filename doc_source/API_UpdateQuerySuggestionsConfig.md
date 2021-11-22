--------

--------

# UpdateQuerySuggestionsConfig<a name="API_UpdateQuerySuggestionsConfig"></a>

Updates the settings of query suggestions for an index\.

Amazon Kendra supports partial updates, so you only need to provide the fields you want to update\.

If an update is currently processing \(i\.e\. 'happening'\), you need to wait for the update to finish before making another update\.

Updates to query suggestions settings might not take effect right away\. The time for your updated settings to take effect depends on the updates made and the number of search queries in your index\.

You can still enable/disable query suggestions at any time\.

 `UpdateQuerySuggestionsConfig` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_UpdateQuerySuggestionsConfig_RequestSyntax"></a>

```
{
   "IncludeQueriesWithoutUserInformation": boolean,
   "IndexId": "string",
   "MinimumNumberOfQueryingUsers": number,
   "MinimumQueryCount": number,
   "Mode": "string",
   "QueryLogLookBackWindowInDays": number
}
```

## Request Parameters<a name="API_UpdateQuerySuggestionsConfig_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ IncludeQueriesWithoutUserInformation ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-IncludeQueriesWithoutUserInformation"></a>
 `TRUE` to include queries without user information \(i\.e\. all queries, irrespective of the user\), otherwise `FALSE` to only include queries with user information\.  
If you pass user information to Amazon Kendra along with the queries, you can set this flag to `FALSE` and instruct Amazon Kendra to only consider queries with user information\.  
If you set to `FALSE`, Amazon Kendra only considers queries searched at least `MinimumQueryCount` times across `MinimumNumberOfQueryingUsers` unique users for suggestions\.  
If you set to `TRUE`, Amazon Kendra ignores all user information and learns from all queries\.  
Type: Boolean  
Required: No

 ** [ IndexId ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-IndexId"></a>
The identifier of the index you want to update query suggestions settings for\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ MinimumNumberOfQueryingUsers ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-MinimumNumberOfQueryingUsers"></a>
The minimum number of unique users who must search a query in order for the query to be eligible to suggest to your users\.  
Increasing this number might decrease the number of suggestions\. However, this ensures a query is searched by many users and is truly popular to suggest to users\.  
How you tune this setting depends on your specific needs\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 10000\.  
Required: No

 ** [ MinimumQueryCount ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-MinimumQueryCount"></a>
The the minimum number of times a query must be searched in order to be eligible to suggest to your users\.  
Decreasing this number increases the number of suggestions\. However, this affects the quality of suggestions as it sets a low bar for a query to be considered popular to suggest to users\.  
How you tune this setting depends on your specific needs\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 10000\.  
Required: No

 ** [ Mode ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-Mode"></a>
Set the mode to `ENABLED` or `LEARN_ONLY`\.  
By default, Amazon Kendra enables query suggestions\. `LEARN_ONLY` mode allows you to turn off query suggestions\. You can to update this at any time\.  
In `LEARN_ONLY` mode, Amazon Kendra continues to learn from new queries to keep suggestions up to date for when you are ready to switch to ENABLED mode again\.  
Type: String  
Valid Values:` ENABLED | LEARN_ONLY`   
Required: No

 ** [ QueryLogLookBackWindowInDays ](#API_UpdateQuerySuggestionsConfig_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsConfig-request-QueryLogLookBackWindowInDays"></a>
How recent your queries are in your query log time window\.  
The time window is the number of days from current day to past days\.  
By default, Amazon Kendra sets this to 180\.  
Type: Integer  
Required: No

## Response Elements<a name="API_UpdateQuerySuggestionsConfig_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateQuerySuggestionsConfig_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** ConflictException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
  
HTTP Status Code: 400

## See Also<a name="API_UpdateQuerySuggestionsConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateQuerySuggestionsConfig) 