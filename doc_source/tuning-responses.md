--------

--------

# Tuning responses<a name="tuning-responses"></a>

By default, query responses are sorted by the relevance score that Amazon Kendra determines for each result in the response\.

You can modify the effect of a field or attribute on the search relevance through *relevance tuning*\. To quickly test relevance tuning, use the [ Query ](API_Query.md) operation to pass in tuning configurations in the query\. Then you can see the different search results that you get from different configurations\. Relevance tuning at the query level is not supported in the console\. You cannot tune fields or attributes that are of the type `StringList`\.

You can tune results for any built\-in or custom attribute of the following types:
+ Date value
+ Long value
+ String value

You can't sort attributes of the following type:
+ String list values

**Rank and tune document results \(AWS SDK\)**  
Set the `Searchable` parameter to true to boost the document metadata configuration\.

To tune an attribute in a query, set the `DocumentRelevanceOverrideConfigurations` parameter of the `Query` operation and specify the name of the attribute to tune\.

The following JSON example shows a `DocumentRelevanceOverrideConfigurations` structure that overrides the tuning for the attribute called "department" in the index\.

```
"DocumentRelevanceOverrideConfigurations" : [
    "Name": "department",
    "Relevance": {
        "Importance": 1,
        "ValueImportanceMap": {
            "IT": 3,
            "HR": 7
        }
    }
]
```