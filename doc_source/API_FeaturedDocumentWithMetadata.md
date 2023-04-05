--------

--------

# FeaturedDocumentWithMetadata<a name="API_FeaturedDocumentWithMetadata"></a>

A featured document with its metadata information\. This document is displayed at the top of the search results page, placed above all other results for certain queries\. If there's an exact match of a query, then the document is featured in the search results\.

## Contents<a name="API_FeaturedDocumentWithMetadata_Contents"></a>

 ** Id **   <a name="Kendra-Type-FeaturedDocumentWithMetadata-Id"></a>
The identifier of the featured document with its metadata\. You can use the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API to search for specific documents with their document IDs included in the result items, or you can use the console\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** Title **   <a name="Kendra-Type-FeaturedDocumentWithMetadata-Title"></a>
The main title of the featured document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** URI **   <a name="Kendra-Type-FeaturedDocumentWithMetadata-URI"></a>
The source URI location of the featured document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: No

## See Also<a name="API_FeaturedDocumentWithMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FeaturedDocumentWithMetadata) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FeaturedDocumentWithMetadata) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FeaturedDocumentWithMetadata) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FeaturedDocumentWithMetadata) 