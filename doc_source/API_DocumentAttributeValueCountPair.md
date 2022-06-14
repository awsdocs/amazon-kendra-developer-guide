--------

--------

# DocumentAttributeValueCountPair<a name="API_DocumentAttributeValueCountPair"></a>

Provides the count of documents that match a particular attribute when doing a faceted search\.

## Contents<a name="API_DocumentAttributeValueCountPair_Contents"></a>

 ** Count **   <a name="Kendra-Type-DocumentAttributeValueCountPair-Count"></a>
The number of documents in the response that have the attribute value for the key\.  
Type: Integer  
Required: No

 ** DocumentAttributeValue **   <a name="Kendra-Type-DocumentAttributeValueCountPair-DocumentAttributeValue"></a>
The value of the attribute\. For example, "HR"\.  
Type: [DocumentAttributeValue](API_DocumentAttributeValue.md) object  
Required: No

 ** FacetResults **   <a name="Kendra-Type-DocumentAttributeValueCountPair-FacetResults"></a>
Contains the results of a document attribute that is a nested facet\. A `FacetResult` contains the counts for each facet nested within a facet\.  
For example, the document attribute or facet "Department" includes a value called "Engineering"\. In addition, the document attribute or facet "SubDepartment" includes the values "Frontend" and "Backend" for documents assigned to "Engineering"\. You can display nested facets in the search results so that documents can be searched not only by department but also by a sub department within a department\. The counts for documents that belong to "Frontend" and "Backend" within "Engineering" are returned for a query\.  
Type: Array of [FacetResult](API_FacetResult.md) objects  
Required: No

## See Also<a name="API_DocumentAttributeValueCountPair_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DocumentAttributeValueCountPair) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DocumentAttributeValueCountPair) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DocumentAttributeValueCountPair) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DocumentAttributeValueCountPair) 