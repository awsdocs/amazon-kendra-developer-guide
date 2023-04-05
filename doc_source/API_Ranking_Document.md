--------

--------

# Document<a name="API_Ranking_Document"></a>

Information about a document from a search service such as OpenSearch \(self managed\)\. Amazon Kendra Intelligent Ranking uses this information to rank and score on\.

## Contents<a name="API_Ranking_Document_Contents"></a>

 ** Body **   <a name="Kendra-Type-Ranking_Document-Body"></a>
The body text of the search service's document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

 ** GroupId **   <a name="Kendra-Type-Ranking_Document-GroupId"></a>
The optional group identifier of the document from the search service\. Documents with the same group identifier are grouped together and processed as one document within the service\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** Id **   <a name="Kendra-Type-Ranking_Document-Id"></a>
The identifier of the document from the search service\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: Yes

 ** OriginalScore **   <a name="Kendra-Type-Ranking_Document-OriginalScore"></a>
The original document score or rank from the search service\. Amazon Kendra Intelligent Ranking gives the document a new score or rank based on its intelligent search algorithms\.  
Type: Float  
Valid Range: Minimum value of \-100000\. Maximum value of 100000\.  
Required: Yes

 ** Title **   <a name="Kendra-Type-Ranking_Document-Title"></a>
The title of the search service's document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Required: No

 ** TokenizedBody **   <a name="Kendra-Type-Ranking_Document-TokenizedBody"></a>
The body text of the search service's document represented as a list of tokens or words\. You must choose to provide `Body` or `TokenizedBody`\. You cannot provide both\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** TokenizedTitle **   <a name="Kendra-Type-Ranking_Document-TokenizedTitle"></a>
The title of the search service's document represented as a list of tokens or words\. You must choose to provide `Title` or `TokenizedTitle`\. You cannot provide both\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_Ranking_Document_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/Document) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/Document) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/Document) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/Document) 