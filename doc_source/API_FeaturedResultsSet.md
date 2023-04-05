--------

--------

# FeaturedResultsSet<a name="API_FeaturedResultsSet"></a>

A set of featured results that are displayed at the top of your search results\. Featured results are placed above all other results for certain queries\. If there's an exact match of a query, then one or more specific documents are featured in the search results\.

## Contents<a name="API_FeaturedResultsSet_Contents"></a>

 ** CreationTimestamp **   <a name="Kendra-Type-FeaturedResultsSet-CreationTimestamp"></a>
The Unix timestamp when the set of featured results was created\.  
Type: Long  
Required: No

 ** Description **   <a name="Kendra-Type-FeaturedResultsSet-Description"></a>
The description for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** FeaturedDocuments **   <a name="Kendra-Type-FeaturedResultsSet-FeaturedDocuments"></a>
The list of document IDs for the documents you want to feature at the top of the search results page\. You can use the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API to search for specific documents with their document IDs included in the result items, or you can use the console\.  
You can add up to four featured documents\. You can request to increase this limit by contacting [Support](http://aws.amazon.com/contact-us/)\.  
Specific queries are mapped to specific documents for featuring in the results\. If a query contains an exact match, then one or more specific documents are featured in the results\. The exact match applies to the full query\. For example, if you only specify 'Kendra', queries such as 'How does kendra semantically rank results?' will not render the featured results\. Featured results are designed for specific queries, rather than queries that are too broad in scope\.  
Type: Array of [FeaturedDocument](API_FeaturedDocument.md) objects  
Required: No

 ** FeaturedResultsSetId **   <a name="Kendra-Type-FeaturedResultsSet-FeaturedResultsSetId"></a>
The identifier of the set of featured results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*`   
Required: No

 ** FeaturedResultsSetName **   <a name="Kendra-Type-FeaturedResultsSet-FeaturedResultsSetName"></a>
The name for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][ a-zA-Z0-9_-]*`   
Required: No

 ** LastUpdatedTimestamp **   <a name="Kendra-Type-FeaturedResultsSet-LastUpdatedTimestamp"></a>
The Unix timestamp when the set of featured results was last updated\.  
Type: Long  
Required: No

 ** QueryTexts **   <a name="Kendra-Type-FeaturedResultsSet-QueryTexts"></a>
The list of queries for featuring results\.  
Specific queries are mapped to specific documents for featuring in the results\. If a query contains an exact match, then one or more specific documents are featured in the results\. The exact match applies to the full query\. For example, if you only specify 'Kendra', queries such as 'How does kendra semantically rank results?' will not render the featured results\. Featured results are designed for specific queries, rather than queries that are too broad in scope\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 49 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Required: No

 ** Status **   <a name="Kendra-Type-FeaturedResultsSet-Status"></a>
The current status of the set of featured results\. When the value is `ACTIVE`, featured results are ready for use\. You can still configure your settings before setting the status to `ACTIVE`\. You can set the status to `ACTIVE` or `INACTIVE` using the [UpdateFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateFeaturedResultsSet.html) API\. The queries you specify for featured results must be unique per featured results set for each index, whether the status is `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

## See Also<a name="API_FeaturedResultsSet_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FeaturedResultsSet) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FeaturedResultsSet) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FeaturedResultsSet) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FeaturedResultsSet) 