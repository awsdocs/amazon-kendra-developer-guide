--------

--------

# Filtering queries<a name="filtering"></a>

You can improve the response from the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API by using filters\. Filters restrict the documents in the response to ones that directly apply to the query\. To create faceted search suggestions, use Boolean logic to filter out specific document attributes from the response or documents that don't match specific criteria\. You can specify facets using the `Facets` parameter in the `Query` API\.

To search documents that you have indexed with Amazon Kendra for Amazon Lex, use [AMAZON\.KendraSearchIntent](https://docs.aws.amazon.com/lexv2/latest/dg/API_KendraConfiguration.html)\. For an example of configuring Amazon Kendra with Amazon Lex, see [Creating a FAQ Bot for an Amazon Kendra Index](https://docs.aws.amazon.com/lexv2/latest/dg/faq-bot-kendra-search.html)\. You can also provide a filter for the response by using [AttributeFilter](https://docs.aws.amazon.com/kendra/latest/dg/API_AttributeFilter.html)\. This is the query filter in JSON when configuring `AMAZON.KendraSearchIntent`\. To provide an attribute filter when configuring a search intent in the console, go to the intent editor and choose Amazon Kendra query to provide a query filter in JSON\. For more information about `AMAZON.KendraSearchIntent`, see the [Amazon Lex documentation guide](https://docs.aws.amazon.com/lexv2/latest/dg/built-in-intent-kendra-search.html)\.

## Facets<a name="search-facets"></a>

Facets are scoped views of a set of search results\. For example, you can provide search results for cities across the world, where documents are filtered by a specific city with which they are associated\. Or, you can create facets to display results by a specific author\. 

You can use a document attribute or metadata field associated with a document as a facet so that your users can search by categories or values within that facet\. You can also display nested facets in the search results so that your users can search not only by a category or field but also by a sub category or sub field\.

The following example shows how to get facet information for the "City" custom attribute\.

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        Facets = [
            {
                "DocumentAttributeKey" : "City"
            }
        ]
        )
```

You can use nested facets to further narrow the search\. For example, the document attribute or facet "City" includes a value called "Seattle"\. In addition, the document attribute or facet "CityRegion" includes the values "North" and "South" for documents assigned to "Seattle"\. You can display nested facets with their counts in the search results so that documents can be searched not only by city but also by a region within a city\.

Note that nested facets could impact query latency\. A general rule is the more nested facets that you use, the greater potential impact on latency\. Other factors that affect latency include the average size of documents indexed, the size of your index, highly complex queries, and the overall load on your Amazon Kendra index\.

The following example shows how to get facet information for the "CityRegion" custom attribute, as a nested facet within "City"\.

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        Facets = [
            {
                "DocumentAttributeKey" : "City",
                "Facets": [
                    {
                        "DocumentAttributeKey" : "CityRegion"
                    }
                ]
            }
        ]
        )
```

Facet information, such as the document count, is returned in the `FacetResults` response array\. You use the contents to display faceted search suggestions in your application\. For example, if the document attribute "City" contains the city that a search could apply to, use that information to display a list of city searches\. Users can choose a city to filter their search results\. To make the faceted search, call the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API and use the chosen document attribute to filter the results\.

You can display up to 10 facet values per facet for a query, and only one nested facet within a facet\. If you want to increase these limits, contact [Support](http://aws.amazon.com/contact-us/)\. If you want to limit the number of facet values per facet to less than 10, you can specify this in the `Facet` object\.

The following sample JSON response shows facets scoped to the "City" document attribute\. The response includes the count of documents for the facet value\.

```
{
    'FacetResults': [
        {
            'DocumentAttributeKey': 'City',
            'DocumentAttributeValueCountPairs': [
                {
                    'Count': 3,
                    'DocumentAttributeValue': {
                        'StringValue': 'Dubai'
                    }
                },
                {
                    'Count': 3,
                    'DocumentAttributeValue': {
                        'StringValue': 'Seattle'
                    }
                },
                {
                    'Count': 1,
                    'DocumentAttributeValue': {
                        'StringValue': 'Paris'
                    }
                }
            ]
        }
    ]
```

You can also display facet information for a nested facet, such as a region within a city, to further filter the search results\.

The following sample JSON response shows facets scoped to the "CityRegion" document attribute, as a nested facet within "City"\. The response includes the count of documents for the nested facet values\.

```
{
    'FacetResults': [
        {
            'DocumentAttributeKey': 'City',
            'DocumentAttributeValueCountPairs': [
                {
                    'Count': 3,
                    'DocumentAttributeValue': {
                        'StringValue': 'Dubai'
                    },
                    'FacetResults': [
                        {
                            'DocumentAttributeKey': 'CityRegion',
                            'DocumentAttributeValueCountPairs': [
                                 {
                                     'Count': 2,
                                     'DocumentAttributeValue': {
                                         'StringValue': 'Bur Dubai'
                                     }
                                 },
                                 {
                                     'Count': 1,
                                     'DocumentAttributeValue': {
                                         'StringValue': 'Deira'
                                     }
                                 }
                             ]
                        }
                    ]
                },
                {
                    'Count': 3,
                    'DocumentAttributeValue': {
                        'StringValue': 'Seattle'
                    },
                    'FacetResults': [
                        {
                            'DocumentAttributeKey': 'CityRegion',
                            'DocumentAttributeValueCountPairs': [
                                 {
                                     'Count': 1,
                                     'DocumentAttributeValue': {
                                         'StringValue': 'North'
                                     }
                                 },
                                 {
                                     'Count': 2,
                                     'DocumentAttributeValue': {
                                         'StringValue': 'South'
                                     }
                                 }
                             ]
                        }
                    ]
                },
                {
                    'Count': 1,
                    'DocumentAttributeValue': {
                        'StringValue': 'Paris'
                    },
                    'FacetResults': [
                        {
                            'DocumentAttributeKey': 'CityRegion',
                            'DocumentAttributeValueCountPairs': [
                                 {
                                     'Count': 1,
                                     'DocumentAttributeValue': {
                                         'StringValue': 'City center'
                                     }
                                 }
                             ]
                        }
                    ]
                }
        }
    ]
}
```

When you use a string list field to create facets, the facet results returned are based on the contents of the string list\. For example, if you have a string list field that contains two items, one with the list "dachshund", "sausage dog" and one with the value "husky", you get `FacetResults` with three facets\.

For more information, see [Query responses and response types](query-responses-types.md)\.

## Using document attributes to filter search results<a name="search-filtering"></a>

By default, `Query` returns all search results\. To filter responses, you can perform logical operations on the document attributes\. For example, if you only want documents for a specific city, you can filter on the "City" and "State" custom document attributes\. You use [AttributeFilter](https://docs.aws.amazon.com/kendra/latest/dg/API_AttributeFilter.html) to create a Boolean operation on filters that you supply\.

Most attributes can be used to filter responses for all [response types](https://docs.aws.amazon.com/kendra/latest/dg/query-responses-types.html)\. However, the `_excerpt_page_number` attribute is only applicable to `ANSWER` response types when filtering responses\.

The following example shows how to perform a logical AND operation by filtering on a specific city, *Seattle*, and state, *Washington*\. 

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        AttributeFilter = {'AndAllFilters': 
            [ 
                {"EqualsTo": {"Key": "City","Value": {"StringValue": "Seattle"}}},
                {"EqualsTo": {"Key": "State","Value": {"StringValue": "Washington"}}}
            ]
            }
        )
```

The following example shows how to perform a logical OR operation for when any of the `Fileformat`, `Author`, or `SourceURI` keys match the specified values\. 

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        AttributeFilter = {'OrAllFilters': 
            [ 
                {"EqualsTo": {"Key": "Fileformat","Value": {"StringValue": "AUTO_DETECT"}}},
                {"EqualsTo": {"Key": "Author","Value": {"StringValue": "Ana Carolina"}}},
                {"EqualsTo": {"Key": "SourceURI","Value": {"StringValue": "https://aws.amazonaws.com/234234242342"}}}
            ]
            }
        )
```

For `StringList` fields, use the `ContainsAny` or `ContainsAll` attribute filters to return documents with the specified string\. The following example shows how to return all documents that have the values "Seattle" or "Portland" in their `Locations` custom attribute\.

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        AttributeFilter = {
                "ContainsAny": { "Key": "Locations", "Value": { "StringListValue": [ "Seattle", "Portland"] }}
            }
        )
```

## Filtering each document's attributes in the search results<a name="filtering-document-attributes"></a>

Amazon Kendra returns document attributes for each document in the search results\. You can filter certain document attributes you want to include in the response as part of the search results\. By default, all document attributes assigned to a document are returned in the response\.

In the following example, only the `_source_uri` and `_author` document attributes are included in the response for a document\.

```
response=kendra.query(
        QueryText = query,
        IndexId = index,
        RequestedDocumentAttributes = ["_source_uri", "_author"]
        )
```