--------

--------

# ListGroupsOlderThanOrderingId<a name="API_ListGroupsOlderThanOrderingId"></a>

Provides a list of groups that are mapped to users before a given ordering or timestamp identifier\.

## Request Syntax<a name="API_ListGroupsOlderThanOrderingId_RequestSyntax"></a>

```
{
   "DataSourceId": "string",
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string",
   "OrderingId": number
}
```

## Request Parameters<a name="API_ListGroupsOlderThanOrderingId_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ DataSourceId ](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-DataSourceId"></a>
=======
 ** [DataSourceId](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-DataSourceId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the data source for getting a list of groups mapped to users before a given ordering timestamp identifier\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

<<<<<<< HEAD
 ** [ IndexId ](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-IndexId"></a>
=======
 ** [IndexId](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index for getting a list of groups mapped to users before a given ordering or timestamp identifier\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ MaxResults ](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-MaxResults"></a>
=======
 ** [MaxResults](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-MaxResults"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
 The maximum number of returned groups that are mapped to users before a given ordering or timestamp identifier\.   
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 10\.  
Required: No

<<<<<<< HEAD
 ** [ NextToken ](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-NextToken"></a>
=======
 ** [NextToken](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-NextToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
 If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of groups that are mapped to users before a given ordering or timestamp identifier\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

<<<<<<< HEAD
 ** [ OrderingId ](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-OrderingId"></a>
=======
 ** [OrderingId](#API_ListGroupsOlderThanOrderingId_RequestSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-request-OrderingId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The timestamp identifier used for the latest `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 32535158400000\.  
Required: Yes

## Response Syntax<a name="API_ListGroupsOlderThanOrderingId_ResponseSyntax"></a>

```
{
   "GroupsSummaries": [ 
      { 
         "GroupId": "string",
         "OrderingId": number
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListGroupsOlderThanOrderingId_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ GroupsSummaries ](#API_ListGroupsOlderThanOrderingId_ResponseSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-response-GroupsSummaries"></a>
 Summary information for list of groups that are mapped to users before a given ordering or timestamp identifier\.   
Type: Array of [ GroupSummary ](API_GroupSummary.md) objects

 ** [ NextToken ](#API_ListGroupsOlderThanOrderingId_ResponseSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-response-NextToken"></a>
=======
 ** [GroupsSummaries](#API_ListGroupsOlderThanOrderingId_ResponseSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-response-GroupsSummaries"></a>
 Summary information for list of groups that are mapped to users before a given ordering or timestamp identifier\.   
Type: Array of [GroupSummary](API_GroupSummary.md) objects

 ** [NextToken](#API_ListGroupsOlderThanOrderingId_ResponseSyntax) **   <a name="Kendra-ListGroupsOlderThanOrderingId-response-NextToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
 If the response is truncated, Amazon Kendra returns this token that you can use in the subsequent request to retrieve the next set of groups that are mapped to users before a given ordering or timestamp identifier\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

## Errors<a name="API_ListGroupsOlderThanOrderingId_Errors"></a>

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

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_ListGroupsOlderThanOrderingId_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListGroupsOlderThanOrderingId) 