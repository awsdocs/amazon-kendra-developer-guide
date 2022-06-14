--------

--------

# UserContext<a name="API_UserContext"></a>

Provides information about the user context for an Amazon Kendra index\.

This is used for filtering search results for different users based on their access to documents\.

You provide one of the following:
+ User token
+ User ID, the groups the user belongs to, and any data sources the groups can access\.

If you provide both, an exception is thrown\.

## Contents<a name="API_UserContext_Contents"></a>

 ** DataSourceGroups **   <a name="Kendra-Type-UserContext-DataSourceGroups"></a>
The list of data source groups you want to filter search results based on groups' access to documents in that data source\.  
Type: Array of [DataSourceGroup](API_DataSourceGroup.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 2048 items\.  
Required: No

 ** Groups **   <a name="Kendra-Type-UserContext-Groups"></a>
The list of groups you want to filter search results based on the groups' access to documents\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 2048 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^\P{C}*$`   
Required: No

 ** Token **   <a name="Kendra-Type-UserContext-Token"></a>
The user context token for filtering search results for a user\. It must be a JWT or a JSON token\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** UserId **   <a name="Kendra-Type-UserContext-UserId"></a>
The identifier of the user you want to filter search results based on their access to documents\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^\P{C}*$`   
Required: No

## See Also<a name="API_UserContext_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UserContext) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UserContext) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UserContext) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UserContext) 