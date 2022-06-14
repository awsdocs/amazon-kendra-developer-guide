--------

--------

# DataSourceGroup<a name="API_DataSourceGroup"></a>

Data source information for user context filtering\.

## Contents<a name="API_DataSourceGroup_Contents"></a>

 ** DataSourceId **   <a name="Kendra-Type-DataSourceGroup-DataSourceId"></a>
The identifier of the data source group you want to add to your list of data source groups\. This is for filtering search results based on the groups' access to documents in that data source\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** GroupId **   <a name="Kendra-Type-DataSourceGroup-GroupId"></a>
The identifier of the group you want to add to your list of groups\. This is for filtering search results based on the groups' access to documents\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^\P{C}*$`   
Required: Yes

## See Also<a name="API_DataSourceGroup_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DataSourceGroup) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DataSourceGroup) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DataSourceGroup) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DataSourceGroup) 