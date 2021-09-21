--------

--------

# DocumentRelevanceConfiguration<a name="API_DocumentRelevanceConfiguration"></a>

Overrides the document relevance properties of a custom index field\.

## Contents<a name="API_DocumentRelevanceConfiguration_Contents"></a>

 ** Name **   <a name="Kendra-Type-DocumentRelevanceConfiguration-Name"></a>
The name of the tuning configuration to override document relevance at the index level\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 30\.  
Required: Yes

 ** Relevance **   <a name="Kendra-Type-DocumentRelevanceConfiguration-Relevance"></a>
Provides information for manually tuning the relevance of a field in a search\. When a query includes terms that match the field, the results are given a boost in the response based on these tuning parameters\.  
Type: [ Relevance ](API_Relevance.md) object  
Required: Yes

## See Also<a name="API_DocumentRelevanceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DocumentRelevanceConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DocumentRelevanceConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DocumentRelevanceConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DocumentRelevanceConfiguration) 