--------

--------

# FeaturedResultsSetSummary<a name="API_FeaturedResultsSetSummary"></a>

Summary information for a set of featured results\. Featured results are placed above all other results for certain queries\. If there's an exact match of a query, then one or more specific documents are featured in the search results\.

## Contents<a name="API_FeaturedResultsSetSummary_Contents"></a>

 ** CreationTimestamp **   <a name="Kendra-Type-FeaturedResultsSetSummary-CreationTimestamp"></a>
The Unix timestamp when the set of featured results was created\.  
Type: Long  
Required: No

 ** FeaturedResultsSetId **   <a name="Kendra-Type-FeaturedResultsSetSummary-FeaturedResultsSetId"></a>
The identifier of the set of featured results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*`   
Required: No

 ** FeaturedResultsSetName **   <a name="Kendra-Type-FeaturedResultsSetSummary-FeaturedResultsSetName"></a>
The name for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][ a-zA-Z0-9_-]*`   
Required: No

 ** LastUpdatedTimestamp **   <a name="Kendra-Type-FeaturedResultsSetSummary-LastUpdatedTimestamp"></a>
The Unix timestamp when the set of featured results was last updated\.  
Type: Long  
Required: No

 ** Status **   <a name="Kendra-Type-FeaturedResultsSetSummary-Status"></a>
The current status of the set of featured results\. When the value is `ACTIVE`, featured results are ready for use\. You can still configure your settings before setting the status to `ACTIVE`\. You can set the status to `ACTIVE` or `INACTIVE` using the [UpdateFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateFeaturedResultsSet.html) API\. The queries you specify for featured results must be unique per featured results set for each index, whether the status is `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

## See Also<a name="API_FeaturedResultsSetSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FeaturedResultsSetSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FeaturedResultsSetSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FeaturedResultsSetSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FeaturedResultsSetSummary) 