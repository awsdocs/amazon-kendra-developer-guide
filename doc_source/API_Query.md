--------

--------

# Query<a name="API_Query"></a>

Searches an active index\. Use this API to search your documents using query\. The `Query` operation enables to do faceted search and to filter results based on document attributes\.

It also enables you to provide user context that Amazon Kendra uses to enforce document access control in the search results\. 

Amazon Kendra searches your index for text content and question and answer \(FAQ\) content\. By default the response contains three types of results\.
+ Relevant passages
+ Matching FAQs
+ Relevant documents

You can specify that the query return only one type of result using the `QueryResultTypeConfig` parameter\.

## Request Syntax<a name="API_Query_RequestSyntax"></a>

```
{
   "[AttributeFilter](#Kendra-Query-request-AttributeFilter)": { 
      "[AndAllFilters](API_AttributeFilter.md#Kendra-Type-AttributeFilter-AndAllFilters)": [ 
         "[AttributeFilter](API_AttributeFilter.md)"
      ],
      "[ContainsAll](API_AttributeFilter.md#Kendra-Type-AttributeFilter-ContainsAll)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[ContainsAny](API_AttributeFilter.md#Kendra-Type-AttributeFilter-ContainsAny)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[EqualsTo](API_AttributeFilter.md#Kendra-Type-AttributeFilter-EqualsTo)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[GreaterThan](API_AttributeFilter.md#Kendra-Type-AttributeFilter-GreaterThan)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[GreaterThanOrEquals](API_AttributeFilter.md#Kendra-Type-AttributeFilter-GreaterThanOrEquals)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[LessThan](API_AttributeFilter.md#Kendra-Type-AttributeFilter-LessThan)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[LessThanOrEquals](API_AttributeFilter.md#Kendra-Type-AttributeFilter-LessThanOrEquals)": { 
         "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
         "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
            "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
            "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
            "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
            "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
         }
      },
      "[NotFilter](API_AttributeFilter.md#Kendra-Type-AttributeFilter-NotFilter)": "[AttributeFilter](API_AttributeFilter.md)",
      "[OrAllFilters](API_AttributeFilter.md#Kendra-Type-AttributeFilter-OrAllFilters)": [ 
         "[AttributeFilter](API_AttributeFilter.md)"
      ]
   },
   "[Facets](#Kendra-Query-request-Facets)": [ 
      { 
         "[DocumentAttributeKey](API_Facet.md#Kendra-Type-Facet-DocumentAttributeKey)": "string"
      }
   ],
   "[IndexId](#Kendra-Query-request-IndexId)": "string",
   "[PageNumber](#Kendra-Query-request-PageNumber)": number,
   "[PageSize](#Kendra-Query-request-PageSize)": number,
   "[QueryResultTypeFilter](#Kendra-Query-request-QueryResultTypeFilter)": "string",
   "[QueryText](#Kendra-Query-request-QueryText)": "string",
   "[RequestedDocumentAttributes](#Kendra-Query-request-RequestedDocumentAttributes)": [ "string" ]
}
```

## Request Parameters<a name="API_Query_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AttributeFilter](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-AttributeFilter"></a>
Enables filtered searches based on document attributes\. You can only provide one attribute filter; however, the `AndAllFilters`, `NotFilter`, and `OrAllFilters` parameters contain a list of other filters\.  
The `AttributeFilter` parameter enables you to create a set of filtering rules that a document must satisfy to be included in the query results\.  
Type: [AttributeFilter](API_AttributeFilter.md) object  
Required: No

 ** [Facets](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-Facets"></a>
An array of documents attributes\. Amazon Kendra returns a count for each attribute key specified\. You can use this information to help narrow the search for your user\.  
Type: Array of [Facet](API_Facet.md) objects  
Required: No

 ** [IndexId](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-IndexId"></a>
The unique identifier of the index to search\. The identifier is returned in the response from the [CreateIndex](API_CreateIndex.md) operation\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [PageNumber](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-PageNumber"></a>
Query results are returned in pages the size of the `PageSize` parameter\. By default, Amazon Kendra returns the first page of results\. Use this parameter to get result pages after the first one\.  
Type: Integer  
Required: No

 ** [PageSize](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-PageSize"></a>
Sets the number of results that are returned in each page of results\. The default page size is 10\. The maximum number of results returned is 100\. If you ask for more than 100 results, only 100 are returned\.  
Type: Integer  
Required: No

 ** [QueryResultTypeFilter](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-QueryResultTypeFilter"></a>
Sets the type of query\. Only results for the specified query type are returned\.  
Type: String  
Valid Values:` DOCUMENT | QUESTION_ANSWER | ANSWER`   
Required: No

 ** [QueryText](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-QueryText"></a>
The text to search for\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: Yes

 ** [RequestedDocumentAttributes](#API_Query_RequestSyntax) **   <a name="Kendra-Query-request-RequestedDocumentAttributes"></a>
An array of document attributes to include in the response\. No other document attributes are included in the response\. By default all document attributes are included in the response\.   
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[a-zA-Z0-9_][a-zA-Z0-9_-]*`   
Required: No

## Response Syntax<a name="API_Query_ResponseSyntax"></a>

```
{
   "[FacetResults](#Kendra-Query-response-FacetResults)": [ 
      { 
         "[DocumentAttributeKey](API_FacetResult.md#Kendra-Type-FacetResult-DocumentAttributeKey)": "string",
         "[DocumentAttributeValueCountPairs](API_FacetResult.md#Kendra-Type-FacetResult-DocumentAttributeValueCountPairs)": [ 
            { 
               "[Count](API_DocumentAttributeValueCountPair.md#Kendra-Type-DocumentAttributeValueCountPair-Count)": number,
               "[DocumentAttributeValue](API_DocumentAttributeValueCountPair.md#Kendra-Type-DocumentAttributeValueCountPair-DocumentAttributeValue)": { 
                  "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
                  "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
                  "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
                  "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
               }
            }
         ]
      }
   ],
   "[QueryId](#Kendra-Query-response-QueryId)": "string",
   "[ResultItems](#Kendra-Query-response-ResultItems)": [ 
      { 
         "[AdditionalAttributes](API_QueryResultItem.md#Kendra-Type-QueryResultItem-AdditionalAttributes)": [ 
            { 
               "[Key](API_AdditionalResultAttribute.md#Kendra-Type-AdditionalResultAttribute-Key)": "string",
               "[Value](API_AdditionalResultAttribute.md#Kendra-Type-AdditionalResultAttribute-Value)": { 
                  "[TextWithHighlightsValue](API_AdditionalResultAttributeValue.md#Kendra-Type-AdditionalResultAttributeValue-TextWithHighlightsValue)": { 
                     "[Highlights](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Highlights)": [ 
                        { 
                           "[BeginOffset](API_Highlight.md#Kendra-Type-Highlight-BeginOffset)": number,
                           "[EndOffset](API_Highlight.md#Kendra-Type-Highlight-EndOffset)": number,
                           "[TopAnswer](API_Highlight.md#Kendra-Type-Highlight-TopAnswer)": boolean
                        }
                     ],
                     "[Text](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Text)": "string"
                  }
               },
               "[ValueType](API_AdditionalResultAttribute.md#Kendra-Type-AdditionalResultAttribute-ValueType)": "string"
            }
         ],
         "[DocumentAttributes](API_QueryResultItem.md#Kendra-Type-QueryResultItem-DocumentAttributes)": [ 
            { 
               "[Key](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Key)": "string",
               "[Value](API_DocumentAttribute.md#Kendra-Type-DocumentAttribute-Value)": { 
                  "[DateValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-DateValue)": number,
                  "[LongValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-LongValue)": number,
                  "[StringListValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringListValue)": [ "string" ],
                  "[StringValue](API_DocumentAttributeValue.md#Kendra-Type-DocumentAttributeValue-StringValue)": "string"
               }
            }
         ],
         "[DocumentExcerpt](API_QueryResultItem.md#Kendra-Type-QueryResultItem-DocumentExcerpt)": { 
            "[Highlights](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Highlights)": [ 
               { 
                  "[BeginOffset](API_Highlight.md#Kendra-Type-Highlight-BeginOffset)": number,
                  "[EndOffset](API_Highlight.md#Kendra-Type-Highlight-EndOffset)": number,
                  "[TopAnswer](API_Highlight.md#Kendra-Type-Highlight-TopAnswer)": boolean
               }
            ],
            "[Text](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Text)": "string"
         },
         "[DocumentId](API_QueryResultItem.md#Kendra-Type-QueryResultItem-DocumentId)": "string",
         "[DocumentTitle](API_QueryResultItem.md#Kendra-Type-QueryResultItem-DocumentTitle)": { 
            "[Highlights](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Highlights)": [ 
               { 
                  "[BeginOffset](API_Highlight.md#Kendra-Type-Highlight-BeginOffset)": number,
                  "[EndOffset](API_Highlight.md#Kendra-Type-Highlight-EndOffset)": number,
                  "[TopAnswer](API_Highlight.md#Kendra-Type-Highlight-TopAnswer)": boolean
               }
            ],
            "[Text](API_TextWithHighlights.md#Kendra-Type-TextWithHighlights-Text)": "string"
         },
         "[DocumentURI](API_QueryResultItem.md#Kendra-Type-QueryResultItem-DocumentURI)": "string",
         "[Id](API_QueryResultItem.md#Kendra-Type-QueryResultItem-Id)": "string",
         "[Type](API_QueryResultItem.md#Kendra-Type-QueryResultItem-Type)": "string"
      }
   ],
   "[TotalNumberOfResults](#Kendra-Query-response-TotalNumberOfResults)": number
}
```

## Response Elements<a name="API_Query_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [FacetResults](#API_Query_ResponseSyntax) **   <a name="Kendra-Query-response-FacetResults"></a>
Contains the facet results\. A `FacetResult` contains the counts for each attribute key that was specified in the `Facets` input parameter\.  
Type: Array of [FacetResult](API_FacetResult.md) objects

 ** [QueryId](#API_Query_ResponseSyntax) **   <a name="Kendra-Query-response-QueryId"></a>
The unique identifier for the search\. You use `QueryId` to identify the search when using the feedback API\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.

 ** [ResultItems](#API_Query_ResponseSyntax) **   <a name="Kendra-Query-response-ResultItems"></a>
The results of the search\.  
Type: Array of [QueryResultItem](API_QueryResultItem.md) objects

 ** [TotalNumberOfResults](#API_Query_ResponseSyntax) **   <a name="Kendra-Query-response-TotalNumberOfResults"></a>
The number of items returned by the search\. Use this to determine when you have requested the last set of results\.  
Type: Integer

## Errors<a name="API_Query_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **AccessDeniedException**   
HTTP Status Code: 400

 **ConflictException**   
HTTP Status Code: 400

 **InternalServerException**   
HTTP Status Code: 500

 **ResourceNotFoundException**   
HTTP Status Code: 400

 **ServiceQuotaExceededException**   
HTTP Status Code: 400

 **ThrottlingException**   
HTTP Status Code: 400

 **ValidationException**   
HTTP Status Code: 400

## See Also<a name="API_Query_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/Query) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/Query) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Query) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Query) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/kendra-2019-02-03/Query) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/Query) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/Query) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/Query) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Query) 