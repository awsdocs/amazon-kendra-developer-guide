--------

--------

# FeaturedResultsItem<a name="API_FeaturedResultsItem"></a>

A single featured result item\. A featured result is displayed at the top of the search results page, placed above all other results for certain queries\. If there's an exact match of a query, then certain documents are featured in the search results\.

## Contents<a name="API_FeaturedResultsItem_Contents"></a>

 ** AdditionalAttributes **   <a name="Kendra-Type-FeaturedResultsItem-AdditionalAttributes"></a>
One or more additional attributes associated with the featured result\.  
Type: Array of [AdditionalResultAttribute](API_AdditionalResultAttribute.md) objects  
Required: No

 ** DocumentAttributes **   <a name="Kendra-Type-FeaturedResultsItem-DocumentAttributes"></a>
An array of document attributes assigned to a featured document in the search results\. For example, the document author \(`_author`\) or the source URI \(`_source_uri`\) of the document\.  
Type: Array of [DocumentAttribute](API_DocumentAttribute.md) objects  
Required: No

 ** DocumentExcerpt **   <a name="Kendra-Type-FeaturedResultsItem-DocumentExcerpt"></a>
Provides text and information about where to highlight the text\.  
Type: [TextWithHighlights](API_TextWithHighlights.md) object  
Required: No

 ** DocumentId **   <a name="Kendra-Type-FeaturedResultsItem-DocumentId"></a>
The identifier of the featured document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** DocumentTitle **   <a name="Kendra-Type-FeaturedResultsItem-DocumentTitle"></a>
Provides text and information about where to highlight the text\.  
Type: [TextWithHighlights](API_TextWithHighlights.md) object  
Required: No

 ** DocumentURI **   <a name="Kendra-Type-FeaturedResultsItem-DocumentURI"></a>
The source URI location of the featured document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: No

 ** FeedbackToken **   <a name="Kendra-Type-FeaturedResultsItem-FeedbackToken"></a>
A token that identifies a particular featured result from a particular query\. Use this token to provide click\-through feedback for the result\. For more information, see [Submitting feedback](https://docs.aws.amazon.com/kendra/latest/dg/submitting-feedback.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*.\P{C}*$`   
Required: No

 ** Id **   <a name="Kendra-Type-FeaturedResultsItem-Id"></a>
The identifier of the featured result\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 73\.  
Required: No

 ** Type **   <a name="Kendra-Type-FeaturedResultsItem-Type"></a>
The type of document within the featured result response\. For example, a response could include a question\-answer type that's relevant to the query\.  
Type: String  
Valid Values:` DOCUMENT | QUESTION_ANSWER | ANSWER`   
Required: No

## See Also<a name="API_FeaturedResultsItem_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FeaturedResultsItem) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FeaturedResultsItem) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FeaturedResultsItem) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FeaturedResultsItem) 