--------

--------

# Tabular search for HTML<a name="searching-tables"></a>

Amazon Kendra's tabular search feature can search and extract answers from tables embedded in HTML documents\. When you search your index, Amazon Kendra includes an excerpt from a table if it's relevant to the query and provides useful information\.

Amazon Kendra looks at all of the information within the body text of a document, including useful information in tables\. For example, an index contains business reports with tables on operation costs, income, and other financial information\. For the query, "what is the annual operation cost from 2020\-2022?", Amazon Kendra can return an excerpt from a table that contains relevant table columns "Operations \(millions USD\)" and "Financial year", and table rows containing income values for 2020, 2021, and 2022\. The table excerpt is included in the result, along with the document title, a link to the full document, and any other document fields you choose to include\.

Table excerpts can be displayed in the search results whether the information is found in one cell of a table or multiple cells\. For example, Amazon Kendra can display a table excerpt tailored to each of these kinds of queries:
+ "highest interest rate credit card in 2020"
+ "highest interest rate credit card from 2020\-2022"
+ "top 3 highest interest rate credit cards in 2020\-2022"
+ "credit cards with interest rates less than 10%"
+ "all available low interest credit cards"

Amazon Kendra highlights the table cell or cells that are most relevant to the query\. The most relevant cells with their corresponding rows, columns and column names are displayed in the search result\. The table excerpt displays up to five columns and three rows, depending on how many table cells are relevant to the query and how many columns are available in the original table\. The top most relevant cell is displayed in the table excerpt, along with the next most relevant cells\.

By default, tables aren't given a higher level of importance or more weight than other components of a document\. Within a document, if a table is only slightly relevant to a query, but there's a highly relevant paragraph, Amazon Kendra returns an excerpt of the paragraph\. Search results display the piece of content that provides the best possible answer and most useful information, in the same document or other documents\. If the confidence for a table falls below `MEDIUM` confidence, then the table excerpt is not returned in the response\.

To use tabular search on an existing index, you must re\-index your content\.

Amazon Kendra only supports documents in English with HTML tables that are within the table tag\. Tabular search is currently not supported in Asia Pacific \(Mumbai\)\.

The following example shows a query response, which includes table excerpts\.

------
#### [ Python ]

```
import boto3
import pprint

kendra = boto3.client("kendra")

# Provide the index ID
index_id = <index-id>
# Provide the query text
query = "search string"

response = kendra.query(
        QueryText = query,
        IndexId = index_id)

print("\nSearch results for query: " + query + "\n")        

for query_result in response["ResultItems"]:

    print("-------------------")
    print("Type: " + str(query_result["Type"]))
    print("Type: " + str(query_result["Format"]))
        
    if query_result["Type"]=="ANSWER" and query_result["Format"]=="TABLE":
        answer_table = query_result["TableExcerpt"]
        print(answer_table)
        
    if query_result["Type"]=="ANSWER" and query_result["Format"]=="TEXT":
        answer_text = query_result["DocumentExcerpt"]
        print(answer_text)
        
    if query_result["Type"]=="QUESTION_ANSWER":
        question_answer_text = query_result["DocumentExcerpt"]["Text"]
        print(question_answer_text)

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
import software.amazon.awssdk.services.kendra.model.QueryResponse;
import software.amazon.awssdk.services.kendra.model.QueryResultItem;

public class SearchIndexExample {
    public static void main(String[] args) {
        KendraClient kendra = KendraClient.builder().build();

        String query = "search string";
        String indexId = "index-id";

        QueryRequest queryRequest = QueryRequest
            .builder()
            .queryText(query)
            .indexId(indexId)
            .build();

        QueryResponse queryResponse = kendra.query(queryRequest);

        System.out.println(String.format("\nSearch results for query: %s", query));
        for(QueryResultItem item: queryResponse.resultItems()) {
            System.out.println("----------------------");
            System.out.println(String.format("Type: %s", item.type()));
            System.out.println(String.format("Format: %s", item.format()));
            
            switch(item.format()) {
                case TABLE:
                    String answerTable = item.TableExcerpt();
                    System.out.println(answerTable);
                    break;
            }

            switch(item.format()) {
                case TEXT:
                    String answerText = item.DocumentExcerpt();
                    System.out.println(answerText);
                    break;
            }

            switch(item.type()) {
                case QUESTION_ANSWER:
                    String questionAnswerText = item.documentExcerpt().text();
                    System.out.println(questionAnswerText);
                    break;
                case DOCUMENT:
                    String documentTitle = item.documentTitle().text();
                    System.out.println(String.format("Title: %s", documentTitle));
                    String documentExcerpt = item.documentExcerpt().text();
                    System.out.println(String.format("Excerpt: %s", documentExcerpt));
                    break;
                default:
                    System.out.println(String.format("Unknown query result type: %s", item.type()));

            }

            System.out.println("-----------------------\n");
        }
    }
}
```

------