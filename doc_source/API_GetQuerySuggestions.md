--------

--------

# GetQuerySuggestions<a name="API_GetQuerySuggestions"></a>

Fetches the queries that are suggested to your users\.

## Request Syntax<a name="API_GetQuerySuggestions_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxSuggestionsCount": number,
   "QueryText": "string"
}
```

## Request Parameters<a name="API_GetQuerySuggestions_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ IndexId ](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-IndexId"></a>
=======
 ** [IndexId](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index you want to get query suggestions from\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ MaxSuggestionsCount ](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-MaxSuggestionsCount"></a>
=======
 ** [MaxSuggestionsCount](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-MaxSuggestionsCount"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The maximum number of query suggestions you want to show to your users\.  
Type: Integer  
Required: No

<<<<<<< HEAD
 ** [ QueryText ](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-QueryText"></a>
=======
 ** [QueryText](#API_GetQuerySuggestions_RequestSyntax) **   <a name="Kendra-GetQuerySuggestions-request-QueryText"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The text of a user's query to generate query suggestions\.  
A query is suggested if the query prefix matches what a user starts to type as their query\.  
Amazon Kendra does not show any suggestions if a user types fewer than two characters or more than 60 characters\. A query must also have at least one search result and contain at least one word of more than four characters\.  
Type: String  
Pattern: `^\P{C}*$`   
Required: Yes

## Response Syntax<a name="API_GetQuerySuggestions_ResponseSyntax"></a>

```
{
   "QuerySuggestionsId": "string",
   "Suggestions": [ 
      { 
         "Id": "string",
         "Value": { 
            "Text": { 
               "Highlights": [ 
                  { 
                     "BeginOffset": number,
                     "EndOffset": number
                  }
               ],
               "Text": "string"
            }
         }
      }
   ]
}
```

## Response Elements<a name="API_GetQuerySuggestions_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ QuerySuggestionsId ](#API_GetQuerySuggestions_ResponseSyntax) **   <a name="Kendra-GetQuerySuggestions-response-QuerySuggestionsId"></a>
=======
 ** [QuerySuggestionsId](#API_GetQuerySuggestions_ResponseSyntax) **   <a name="Kendra-GetQuerySuggestions-response-QuerySuggestionsId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier for a list of query suggestions for an index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.

<<<<<<< HEAD
 ** [ Suggestions ](#API_GetQuerySuggestions_ResponseSyntax) **   <a name="Kendra-GetQuerySuggestions-response-Suggestions"></a>
A list of query suggestions for an index\.  
Type: Array of [ Suggestion ](API_Suggestion.md) objects
=======
 ** [Suggestions](#API_GetQuerySuggestions_ResponseSyntax) **   <a name="Kendra-GetQuerySuggestions-response-Suggestions"></a>
A list of query suggestions for an index\.  
Type: Array of [Suggestion](API_Suggestion.md) objects
>>>>>>> parent of 2b1c178 (updating tutorial)

## Errors<a name="API_GetQuerySuggestions_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

<<<<<<< HEAD
 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** ConflictException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ServiceQuotaExceededException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
=======
 **AccessDeniedException**   
  
HTTP Status Code: 400

 **ConflictException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ServiceQuotaExceededException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_GetQuerySuggestions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/GetQuerySuggestions) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GetQuerySuggestions) 