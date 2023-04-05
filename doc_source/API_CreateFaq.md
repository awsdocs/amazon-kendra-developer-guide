--------

--------

# CreateFaq<a name="API_CreateFaq"></a>

Creates a set of frequently ask questions \(FAQs\) using a specified FAQ file stored in an Amazon S3 bucket\.

Adding FAQs to an index is an asynchronous operation\.

For an example of adding an FAQ to an index using Python and Java SDKs, see [Using your FAQ file](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html#using-faq-file)\.

## Request Syntax<a name="API_CreateFaq_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Description": "string",
   "FileFormat": "string",
   "IndexId": "string",
   "LanguageCode": "string",
   "Name": "string",
   "RoleArn": "string",
   "S3Path": { 
      "Bucket": "string",
      "Key": "string"
   },
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateFaq_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ClientToken](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-ClientToken"></a>
A token that you provide to identify the request to create a FAQ\. Multiple calls to the `CreateFaqRequest` API with the same client token will create only one FAQ\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [Description](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Description"></a>
A description for the FAQ\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [FileFormat](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-FileFormat"></a>
The format of the FAQ input file\. You can choose between a basic CSV format, a CSV format that includes customs attributes in a header, and a JSON format that includes custom attributes\.  
The format must match the format of the file stored in the S3 bucket identified in the `S3Path` parameter\.  
For more information, see [Adding questions and answers](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html)\.  
Type: String  
Valid Values:` CSV | CSV_WITH_HEADER | JSON`   
Required: No

 ** [IndexId](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-IndexId"></a>
The identifier of the index for the FAQ\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [LanguageCode](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-LanguageCode"></a>
The code for a language\. This allows you to support a language for the FAQ document\. English is supported by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 10\.  
Pattern: `[a-zA-Z-]*`   
Required: No

 ** [Name](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Name"></a>
A name for the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [RoleArn](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-RoleArn"></a>
The Amazon Resource Name \(ARN\) of an IAM role with permission to access the S3 bucket that contains the FAQs\. For more information, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** [S3Path](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-S3Path"></a>
The path to the FAQ file in S3\.  
Type: [S3Path](API_S3Path.md) object  
Required: Yes

 ** [Tags](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Tags"></a>
A list of key\-value pairs that identify the FAQ\. You can use the tags to identify and organize your resources and to control access to resources\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateFaq_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateFaq_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Id](#API_CreateFaq_ResponseSyntax) **   <a name="Kendra-CreateFaq-response-Id"></a>
The identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

## Errors<a name="API_CreateFaq_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ServiceQuotaExceededException **   
You have exceeded the set limits for your Amazon Kendra service\. Please see [Quotas](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html) for more information, or contact [Support](http://aws.amazon.com/contact-us/) to inquire about an increase of limits\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_CreateFaq_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateFaq) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateFaq) 