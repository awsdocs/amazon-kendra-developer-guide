--------

--------

# ListExperiences<a name="API_ListExperiences"></a>

Lists one or more Amazon Kendra experiences\. You can create an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Request Syntax<a name="API_ListExperiences_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListExperiences_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ IndexId ](#API_ListExperiences_RequestSyntax) **   <a name="Kendra-ListExperiences-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ MaxResults ](#API_ListExperiences_RequestSyntax) **   <a name="Kendra-ListExperiences-request-MaxResults"></a>
The maximum number of returned Amazon Kendra experiences\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [ NextToken ](#API_ListExperiences_RequestSyntax) **   <a name="Kendra-ListExperiences-request-NextToken"></a>
If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of Amazon Kendra experiences\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListExperiences_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "SummaryItems": [ 
      { 
         "CreatedAt": number,
         "Endpoints": [ 
            { 
               "Endpoint": "string",
               "EndpointType": "string"
            }
         ],
         "Id": "string",
         "Name": "string",
         "Status": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListExperiences_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ NextToken ](#API_ListExperiences_ResponseSyntax) **   <a name="Kendra-ListExperiences-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns this token, which you can use in a later request to retrieve the next set of Amazon Kendra experiences\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

 ** [ SummaryItems ](#API_ListExperiences_ResponseSyntax) **   <a name="Kendra-ListExperiences-response-SummaryItems"></a>
An array of summary information for one or more Amazon Kendra experiences\.  
Type: Array of [ ExperiencesSummary ](API_ExperiencesSummary.md) objects

## Errors<a name="API_ListExperiences_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
  
HTTP Status Code: 400

## See Also<a name="API_ListExperiences_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListExperiences) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListExperiences) 