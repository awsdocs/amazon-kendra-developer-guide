--------

--------

# Tag<a name="API_Ranking_Tag"></a>

A key\-value pair that identifies or categorizes a rescore execution plan\. A rescore execution plan is an Amazon Kendra Intelligent Ranking resource used for provisioning the `Rescore` API\. You can also use a tag to help control access to a rescore execution plan\. A tag key and value can consist of Unicode letters, digits, white space, and any of the following symbols: \_ \. : / = \+ \- @\.

## Contents<a name="API_Ranking_Tag_Contents"></a>

 ** Key **   <a name="Kendra-Type-Ranking_Tag-Key"></a>
The key for the tag\. Keys are not case sensitive and must be unique\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Required: Yes

 ** Value **   <a name="Kendra-Type-Ranking_Tag-Value"></a>
The value associated with the tag\. The value can be an empty string but it can't be null\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 256\.  
Required: Yes

## See Also<a name="API_Ranking_Tag_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/Tag) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/Tag) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/Tag) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/Tag) 