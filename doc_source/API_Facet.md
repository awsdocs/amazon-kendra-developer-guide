--------

--------

# Facet<a name="API_Facet"></a>

Information about a document attribute\. You can use document attributes as facets\.

For example, the document attribute or facet "Department" includes the values "HR", "Engineering", and "Accounting"\. You can display these values in the search results so that documents can be searched by department\.

You can display up to 10 facet values per facet for a query\. If you want to increase this limit, contact [Support](http://aws.amazon.com/contact-us/)\.

## Contents<a name="API_Facet_Contents"></a>

 ** DocumentAttributeKey **   <a name="Kendra-Type-Facet-DocumentAttributeKey"></a>
The unique key for the document attribute\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[a-zA-Z0-9_][a-zA-Z0-9_-]*`   
Required: No

 ** Facets **   <a name="Kendra-Type-Facet-Facets"></a>
An array of document attributes that are nested facets within a facet\.  
For example, the document attribute or facet "Department" includes a value called "Engineering"\. In addition, the document attribute or facet "SubDepartment" includes the values "Frontend" and "Backend" for documents assigned to "Engineering"\. You can display nested facets in the search results so that documents can be searched not only by department but also by a sub department within a department\. This helps your users further narrow their search\.  
You can only have one nested facet within a facet\. If you want to increase this limit, contact [Support](http://aws.amazon.com/contact-us/)\.  
Type: Array of [Facet](#API_Facet) objects  
Required: No

 ** MaxResults **   <a name="Kendra-Type-Facet-MaxResults"></a>
Maximum number of facet values per facet\. The default is 10\. You can use this to limit the number of facet values to less than 10\. If you want to increase the default, contact [Support](http://aws.amazon.com/contact-us/)\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 5000\.  
Required: No

## See Also<a name="API_Facet_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Facet) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Facet) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Facet) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Facet) 