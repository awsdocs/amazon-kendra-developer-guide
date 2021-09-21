--------

--------

# FaqSummary<a name="API_FaqSummary"></a>

Provides information about a frequently asked questions and answer contained in an index\.

## Contents<a name="API_FaqSummary_Contents"></a>

<<<<<<< HEAD
 ** CreatedAt **   <a name="Kendra-Type-FaqSummary-CreatedAt"></a>
=======
 **CreatedAt**   <a name="Kendra-Type-FaqSummary-CreatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The UNIX datetime that the FAQ was added to the index\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** FileFormat **   <a name="Kendra-Type-FaqSummary-FileFormat"></a>
=======
 **FileFormat**   <a name="Kendra-Type-FaqSummary-FileFormat"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The file type used to create the FAQ\.   
Type: String  
Valid Values:` CSV | CSV_WITH_HEADER | JSON`   
Required: No

<<<<<<< HEAD
 ** Id **   <a name="Kendra-Type-FaqSummary-Id"></a>
=======
 **Id**   <a name="Kendra-Type-FaqSummary-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

<<<<<<< HEAD
 ** Name **   <a name="Kendra-Type-FaqSummary-Name"></a>
=======
 **Name**   <a name="Kendra-Type-FaqSummary-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name that you assigned the FAQ when you created or updated the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

<<<<<<< HEAD
 ** Status **   <a name="Kendra-Type-FaqSummary-Status"></a>
=======
 **Status**   <a name="Kendra-Type-FaqSummary-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The current status of the FAQ\. When the status is `ACTIVE` the FAQ is ready for use\.  
Type: String  
Valid Values:` CREATING | UPDATING | ACTIVE | DELETING | FAILED`   
Required: No

<<<<<<< HEAD
 ** UpdatedAt **   <a name="Kendra-Type-FaqSummary-UpdatedAt"></a>
=======
 **UpdatedAt**   <a name="Kendra-Type-FaqSummary-UpdatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The UNIX datetime that the FAQ was last updated\.  
Type: Timestamp  
Required: No

## See Also<a name="API_FaqSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FaqSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FaqSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FaqSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FaqSummary) 