--------

--------

# Tuning search relevance<a name="tuning"></a>

Amazon Kendra queries produce search results ranked by their relevance\. The searchable fields or attributes in the index all contribute to this ranking\. 

You can modify the effect of a field or attribute on the search relevance through *relevance tuning*\. Tuning search relevance can either be done manually at the index level, where you set tuning configurations for your index, or at the query level by overriding configurations set at the index level\.

When you use relevance tuning, a result is given a boost in the response when the query includes terms that match the field or attribute\. You also specify how much of a boost the document receives when there is a match\. Relevance tuning doesn't cause Amazon Kendra to include a document in the query response, it is only one of the factors that Amazon Kendra uses to determine the relevance of a document\.

You can boost specific fields or attributes in your index to assign more importance to specific responses\. For example when someone searches for "When is re:Invent?" you could boost the relevance of document freshness in the "\_last\_update\_at" field\. Or, in an index of research reports, you could boost a specific data source in the "source" field\.

You can also boost documents based on votes or view counts which is common in forums and other support knowledge bases\. You can combine boosts, for example to boost documents that are viewed more as well as more recent\.

You set the amount of boost that a document receives by using the `Importance` parameter\. The higher the `Importance`, the more the field or attribute boosts the relevance of a document\. When you tune your index or tune at the query level, increase the value of the `Importance` parameter in small increments until you get the effect that you want\. To determine if you are improving search results, perform the search and compare the results to previous queries \.

You can specify date, number, or string attributes to tune an index or tune at the query level\. You cannot tune fields or attributes that are of the type `StringList`\. Each field or attribute has specific criteria for when it boosts a result\.
+ **Date fields or attributes** – There are three specific criteria for date fields, `Duration`, `Freshness` and `RankOrder`\.
  +  `Duration` sets the time period that the boost applies to\. For example, if you set the time period to 86400 seconds \(i\.e\. one day\), the boost begins to lessen after one day\. The higher the importance, the faster the boost effect lessens\.
  + `Freshness` determines how recent a document is when applied to a field or attribute\. If you apply `Freshness` to either the field for date created or date last updated, then a more recently created or last updated document is considered "fresher" than an older document\. For example, if document 1 was created on November 14, and document 2 was created on November 5, document 1 is "fresher" than document 2\. And if document 1 was last updated on November 14, and document 2 was last updated on November 20, document 2 is "fresher" than document 1\. The fresher the document, the more this boost is applied\. You can only have one `Freshness` field in your index\. 
  + `RankOrder` applies the boost in either ascending or descending order\. If you specify `ASCENDING`, later dates have precedence \. If you specify `DESCENDING`, earlier dates have precedence\.
+ **Number fields or attributes** – For number fields or attributes, you can specify the rank order that Amazon Kendra should use when determining the relevance of the field or attribute\. If you specify `ASCENDING`, then higher numbers are given precedence\. If you specify `DESCENDING`, then lower numbers have precedence\.
+ **String fields or attributes** – For string fields or attributes, you can create categories of a field to give each category a different boost\. For example, if you boost a field or attribute called "Department", you can give a different boost to documents from "HR" than to documents from "Legal"\. You cannot boost a field or attribute of the type `StringList`\.

## Relevance tuning at the index level<a name="tuning-index"></a>

<<<<<<< HEAD
You tune the relevance of a field or attribute at the index level by using either the [console](https://console.aws.amazon.com/kendra/) to set tuning in the index details or the [ UpdateIndex ](API_UpdateIndex.md) operation\. The following example sets the "\_last\_updated\_at" field as the `Freshness` field for a document\.
=======
You tune the relevance of a field or attribute at the index level by using either the [console](https://console.aws.amazon.com/kendra/) to set tuning in the index details or the [UpdateIndex](API_UpdateIndex.md) operation\. The following example sets the "\_last\_updated\_at" field as the `Freshness` field for a document\.
>>>>>>> parent of 2b1c178 (updating tutorial)

```
"DocumentMetadataConfigurationUpdates" : [
    "Name": "_last_updated_at",
    "Type": "DATE_VALUE",
    "Relevance": {
        "Freshness": TRUE,
        "Importance": 2
    }
]
```

The following example applies different importance to the different categories in the "department" field\.

```
"DocumentMetadataConfigurationUpdates" : [
    "Name": "department",
    "Type": "STRING_VALUE",
    "Relevance": {
        "Importance": 2,
        "ValueImportanceMap": {
            "HR": 3,
            "Legal": 1
        }
    }
]
```

## Relevance tuning at the query level<a name="tuning-query"></a>

<<<<<<< HEAD
You tune the relevance of a field or attribute at the query level by using the [ Query ](API_Query.md) operation\. Tuning at the query level can speed up the process of testing relevance tuning because you don't need to manually update the tuning configurations in the index for each test\. You can tune the relevance of a document by passing tuning configurations in the query\. Then you can see the different results that you get from different configurations\. A configuration that is passed in the query overrides the configuration that is set at the index level\. 
=======
You tune the relevance of a field or attribute at the query level by using the [Query](API_Query.md) operation\. Tuning at the query level can speed up the process of testing relevance tuning because you don't need to manually update the tuning configurations in the index for each test\. You can tune the relevance of a document by passing tuning configurations in the query\. Then you can see the different results that you get from different configurations\. A configuration that is passed in the query overrides the configuration that is set at the index level\. 
>>>>>>> parent of 2b1c178 (updating tutorial)

The following example overrides the importance applied to the "department" field and each department category set at the index level, shown in the above example\. When a user inputs their search query, the "department" field has a fair level of importance and the Legal department has more importance than the HR department \.

```
"DocumentRelevanceOverrideConfigurations" : [
    "Name": "department",
    "Type": "STRING_VALUE",
    "Relevance": {
        "Importance": 5,
        "ValueImportanceMap": {
            "HR": 2,
            "Legal": 8
        }
    }
]
```

Relevance tuning at the query level is not supported in the console\.