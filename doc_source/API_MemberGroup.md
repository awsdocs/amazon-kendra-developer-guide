--------

--------

# MemberGroup<a name="API_MemberGroup"></a>

The sub groups that belong to a group\.

## Contents<a name="API_MemberGroup_Contents"></a>

 ** DataSourceId **   <a name="Kendra-Type-MemberGroup-DataSourceId"></a>
The identifier of the data source for the sub group you want to map to a group\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** GroupId **   <a name="Kendra-Type-MemberGroup-GroupId"></a>
The identifier of the sub group you want to map to a group\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^\P{C}*$`   
Required: Yes

## See Also<a name="API_MemberGroup_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/MemberGroup) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/MemberGroup) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/MemberGroup) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/MemberGroup) 