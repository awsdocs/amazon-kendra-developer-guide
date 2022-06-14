--------

--------

# Browsing an index<a name="browsing"></a>

You can browse documents by their attributes or facets without having to type a search query\. Amazon Kendra *Index Browse* can help your users discover documents by freely browsing an index without a specific query in mind\. This also helps your users broadly browse an index as a starting point in their search\.

Index Browse can only be used for searching by document attribute or facet with a sorting type\. You cannot search an entire index using Index Browse\. If the query text is missing, then Amazon Kendra asks for a document attribute filter or a facet, and a sorting type\.

To allow index browsing using the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API, you must include [AttributeFilter](https://docs.aws.amazon.com/kendra/latest/dg/API_AttributeFilter.html) or [Facet](https://docs.aws.amazon.com/kendra/latest/dg/API_Facet.html), and [SortingConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SortingConfiguration.html)\. To allow index browsing in the console, select your index under **Indexes** in the navigation menu, then select the option to search your index\. In the search box, press the *Enter* key twice\. Select the dropdown **Filter search results** to choose a filter and select the dropdown **Sort** to choose a sorting type\.

The following is an example of browsing an index for documents in the language Spanish in descending order of document creation date\.

------
#### [ CLI ]

```
aws kendra query \
--index-id "index-id" \
--attribute-filter '{   
    "EqualsTo":{
      "Key": "_language_code",
      "Value": {
        "StringValue": "es"
      }
    }
  }' \
--sorting-configuration '{
    "DocumentAttributeKey": "_created_at",
    "SortOrder": "DESC"
  }'
```

------
#### [ Python ]

```
import boto3

kendra = boto3.client("kendra")

# Must include the index ID, the attribute filter, and sorting configuration
response = kendra.query(
        IndexId = "index-id",
        AttributeFilter = {
            "EqualsTo": {      
                "Key": "_language_code",
                "Value": {
                    "StringValue": "es"
                    }
                }
            },
        SortingConfiguration = {
            "DocumentAttributeKey": "_created_at',
            "SortOrder": "DESC"})

print("\nSearch results|Resultados de la búsqueda: \n")

for query_result in response["ResultItems"]:

    print("-------------------")
    print("Type: " + str(query_result["Type"]))
        
    if query_result["Type"]=="ANSWER" or query_result["Type"]=="QUESTION_ANSWER":
        answer_text = query_result["DocumentExcerpt"]["Text"]
        print(answer_text)

    if query_result["Type"]=="DOCUMENT":
        if "DocumentTitle" in query_result:
            document_title = query_result["DocumentTitle"]["Text"]
            print("Title: " + document_title)
        document_text = query_result["DocumentExcerpt"]["Text"]
        print(document_text)

    print("------------------\n\n")
```

------
#### [ Java ]

```
package com.amazonaws.kendra;

import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.QueryRequest;
import software.amazon.awssdk.services.kendra.model.QueryResult;
import software.amazon.awssdk.services.kendra.model.QueryResultItem;

public class SearchIndexExample {
    public static void main(String[] args) {
        KendraClient kendra = KendraClient.builder().build();
        QueryRequest queryRequest = QueryRequest.builder()
            .withIndexId("index-id")
            .withAttributeFilter(AttributeFilter.builder()
                .withEqualsTo(DocumentAttribute.builder()
                    .withKey("_language_code")
                    .withValue(DocumentAttributeValue.builder()
                        .withStringValue("es")
                        .build())
                    .build())
                .build())
            .withSortingConfiguration(SortingConfiguration.builder()
                .withDocumentAttributeKey("_created_at")
                .withSortOrder("DESC")
                .build())
            .build());
            
        QueryResult queryResult = kendra.query(queryRequest);
        for (QueryResultItem item : queryResult.getResultItems()) {
            System.out.println("----------------------");
            System.out.println(String.format("Type: %s", item.getType()));
        
            switch (item.getType()) {
                case QueryResultType.QUESTION_ANSWER:
                case QueryResultType.ANSWER:
                    String answerText = item.getDocumentExcerpt().getText();
                    System.out.println(answerText);
                    break;
                case QueryResultType.DOCUMENT:
                    String documentTitle = item.getDocumentTitle().getText();
                    System.out.println(String.format("Title: %s", documentTitle));
                    String documentExcerpt = item.getDocumentExcerpt().getText();
                    System.out.println(String.format("Excerpt: %s", documentExcerpt));
                    break;
                default:
                    System.out.println(String.format("Unknown query result type: %s", item.getType()));
            }
            System.out.println("-----------------------\n");
        }
    }
}
```

------