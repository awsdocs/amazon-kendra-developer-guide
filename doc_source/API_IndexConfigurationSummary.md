--------

--------

# IndexConfigurationSummary<a name="API_IndexConfigurationSummary"></a>

A summary of information about an index\.

## Contents<a name="API_IndexConfigurationSummary_Contents"></a>

<<<<<<< HEAD
 ** CreatedAt **   <a name="Kendra-Type-IndexConfigurationSummary-CreatedAt"></a>
=======
 **CreatedAt**   <a name="Kendra-Type-IndexConfigurationSummary-CreatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Unix timestamp when the index was created\.  
Type: Timestamp  
Required: Yes

<<<<<<< HEAD
 ** Edition **   <a name="Kendra-Type-IndexConfigurationSummary-Edition"></a>
=======
 **Edition**   <a name="Kendra-Type-IndexConfigurationSummary-Edition"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Indicates whether the index is a enterprise edition index or a developer edition index\.   
Type: String  
Valid Values:` DEVELOPER_EDITION | ENTERPRISE_EDITION`   
Required: No

<<<<<<< HEAD
 ** Id **   <a name="Kendra-Type-IndexConfigurationSummary-Id"></a>
=======
 **Id**   <a name="Kendra-Type-IndexConfigurationSummary-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A unique identifier for the index\. Use this to identify the index when you are using operations such as `Query`, `DescribeIndex`, `UpdateIndex`, and `DeleteIndex`\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: No

<<<<<<< HEAD
 ** Name **   <a name="Kendra-Type-IndexConfigurationSummary-Name"></a>
=======
 **Name**   <a name="Kendra-Type-IndexConfigurationSummary-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name of the index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

<<<<<<< HEAD
 ** Status **   <a name="Kendra-Type-IndexConfigurationSummary-Status"></a>
=======
 **Status**   <a name="Kendra-Type-IndexConfigurationSummary-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The current status of the index\. When the status is `ACTIVE`, the index is ready to search\.  
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | FAILED | UPDATING | SYSTEM_UPDATING`   
Required: Yes

<<<<<<< HEAD
 ** UpdatedAt **   <a name="Kendra-Type-IndexConfigurationSummary-UpdatedAt"></a>
=======
 **UpdatedAt**   <a name="Kendra-Type-IndexConfigurationSummary-UpdatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Unix timestamp when the index was last updated by the `UpdateIndex` operation\.  
Type: Timestamp  
Required: Yes

## See Also<a name="API_IndexConfigurationSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/IndexConfigurationSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/IndexConfigurationSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/IndexConfigurationSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/IndexConfigurationSummary) 