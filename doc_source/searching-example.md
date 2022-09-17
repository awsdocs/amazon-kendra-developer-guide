--------

--------

# Querying an index<a name="searching-example"></a>

When you search your index, Amazon Kendra uses all the information that you provided about your documents to determine the documents most relevant to the search terms entered\. Some of the items that Amazon Kendra considers are:
+ The text of the document\.
+ The title of the document\.
+ Custom text fields that you have marked searchable\.
+ The date field that you have indicated should be used to determine the "freshness" of a document\.

When a set of relevant documents has been selected from the index, Amazon Kendra filters the response based on any attribute filters that you have requested for the search\. For example, if you have a custom attribute called "department", you can filter the response to return only documents from a department called "legal"\. For more information, see [Creating custom document attributes or metadata fields](custom-attributes.md)\.

After finding the relevant documents and then filtering based on the attributes that you set, Amazon Kendra returns the results\. The results are sorted by the relevance that Amazon Kendra determined for each doc\. The results are paginated so that you can show a page at a time to your user\.

To search documents that you have indexed with Amazon Kendra for Amazon Lex, use [AMAZON\.KendraSearchIntent](https://docs.aws.amazon.com/lexv2/latest/dg/API_KendraConfiguration.html)\. For an example of configuring Amazon Kendra with Amazon Lex, see [Creating a FAQ Bot for an Amazon Kendra Index](https://docs.aws.amazon.com/lexv2/latest/dg/faq-bot-kendra-search.html)\.

The following Python example shows how to search an index by using the [Query](API_Query.md) API\. The example determines the type of the search result \(answer, document, question/answer\) and displays the answer text\. 

For information about the query responses, see [Query responses](query-response.md)\.

**Note**  
You can use this code to filter document attributes\. The topic [Filtering queries](filtering.md) contains examples that you can use to replace the following code\.  

```
response=kendra.query(
        QueryText = query,
        IndexId = index)
```

## Prerequisites<a name="searching-prerequisites"></a>

To run this example, you must:
+ Set up permissions\. For more information, see [IAM access roles for Amazon Kendra](iam-roles.md)\.
+ Set up the AWS CLI\. For more information, see [Setting up the AWS CLI](aws-kendra-set-up-aws-cli.md)\.
+ Create a data source and index\. For more information, see [Getting started with the Amazon Kendra console](gs-console.md)\.

## Searching an index \(console\)<a name="searching-index-console"></a>

You can use the Amazon Kendra console to search and test your index\. You can make queries and see the results\.

**To search an index with the console**

1. Sign in to the AWS Management Console and open the Amazon Kendra console at [http://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra)\.

1. On the navigation pane, choose **Indexes**\.

1. Choose your index\.

1. In the navigation menu, choose the option to search your index\.

1. Enter a query in the text box and then press enter\.

1. Amazon Kendra returns the results of the search\.

## Searching an index \(SDK\)<a name="searching-index-sdk"></a>

**To search an index with Python or Java**
+ The following example searches an index\. Change the value of `query` to your search query and `index_id` or `indexId` to the index identifier of the index that you want to search\.

------
#### [ Python ]

  ```
  import boto3
  import pprint
  
  kendra = boto3.client("kendra")
  
  # Provide the index ID
  index_id = "index-id"
  # Provide the query text
  query = "search-string"
  
  response = kendra.query(
          QueryText = query,
          IndexId = index_id)
  
  print("\nSearch results for query: " + query + "\n")        
  
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
  import software.amazon.awssdk.services.kendra.model.QueryResponse;
  import software.amazon.awssdk.services.kendra.model.QueryResultItem;
  
  public class SearchIndexExample {
      public static void main(String[] args) {
          KendraClient kendra = KendraClient.builder().build();
  
          String query = "some queries";
          String indexId = "anIndexId";
  
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
  
              switch(item.type()) {
                  case QUESTION_ANSWER:
                  case ANSWER:
                      String answerText = item.documentExcerpt().text();
                      System.out.println(answerText);
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

## Searching with advanced query syntax<a name="searching-index-query-syntax"></a>

You can create queries that are more specific than simple keyword or natural language queries by using advanced query syntax or operators\. This includes ranges, Booleans, wildcards, and more\. By using operators, you can give your query more context and further refine the search results\.

Amazon Kendra supports the following operators\.
+ Boolean: Logic to limit or broaden the search\. For example, `amazon AND sports` limits the search to only search for documents containing both terms\.
+ Parentheses: Reads nested query terms in order of precedence\. For example, `(amazon AND sports) NOT rainforest` reads `(amazon AND sports)` before `NOT rainforest`\.
+ Ranges: Date or numeric range values\. Ranges can be inclusive, exclusive, or unbounded\. For example, you can search for documents that were last updated between January 1st 2020 and December 31st 2020, inclusive of these dates\.
+ Fields: Uses a specific field to limit the search\. For example, you can search for documents that have 'United States' in the field 'location'\.
+ Wildcards: Partially match a string of text\. For example, `Cloud*` could match CloudFormation\. Amazon Kendra currently only supports trailing wildcards\.
+ Exact quotes: Exact match a string of text\. For example, documents that contain `"Amazon Kendra" "pricing"`\.

You can use a combination of any of the above operators\.

Note that excessive use of operators or highly complex queries could impact query latency\. Wildcards are some of the most expensive operators in terms of latency\. A general rule is the more terms and operators that you use, the greater potential impact on latency\. Other factors that affect latency include the average size of documents indexed, the size of your index, any filtering on search results, and the overall load on your Amazon Kendra index\.

### Boolean<a name="query-syntax-boolean"></a>

You can combine or exclude words using the Boolean operators `AND`, `OR`, `NOT`\.

The following are examples of using Boolean operators\.

 **`amazon AND sports`** 

Returns search results that contain both the terms 'amazon' and 'sports' in the text, such as Amazon Prime video sports or other similar content\.

 **`sports OR recreation`** 

Returns search results that contain the terms 'sports' or 'recreation', or both, in the text\.

 **`amazon NOT rainforest`** 

Returns search results that contain the term 'amazon' but not the term 'rainforest' in the text\. This is to search for documents about the company Amazon, not the Amazon Rainforest\.

### Parentheses<a name="query-syntax-parentheses"></a>

You can query nested words in order of precedence by using parentheses\. The parentheses indicate to Amazon Kendra how a query should be read\.

The following are examples of using parentheses operators\.

 **`(amazon AND sports) NOT rainforest`** 

Returns documents that contain both the terms 'amazon' and 'sports' in the text, but not the term 'rainforest'\. This is to search Amazon Prime video sports or other similar content, not adventure sports in the Amazon Rainforest\. The parentheses help indicate that `amazon AND sports` should be read before `NOT rainforest`\. The query should not be read as `amazon AND (sports NOT rainforest)`\.

 **`(amazon AND (sports OR recreation)) NOT rainforest`** 

Returns documents that contain the terms 'sports' or 'recreation', or both, and the term 'amazon'\. But it does not include the term 'rainforest'\. This is to search Amazon Prime video sports or recreation, not adventure sports in the Amazon Rainforest\. The parentheses help indicate that `sports OR recreation` should be read before combining with 'amazon', which is read before `NOT rainforest`\. The query should not be read as `amazon AND (sports OR (recreation NOT rainforest))`\.

### Ranges<a name="query-syntax-ranges"></a>

You can use a range of values to filter the search results\. You specify an attribute and the range values\. This can be date or numeric type\.

Date ranges must be in the following formats:
+ Epoch
+ YYYY
+ YYYY\-mm
+ YYYY\-mm\-dd
+ YYYY\-mm\-dd'T'HH

You can also specify whether to include or exclude the lower and higher values of the range\.

The following are examples of using range operators\.

 **`_processed_date:>2019-12-31 AND _processed_date:<2021-01-01`** 

Returns documents that were processed in 2020—greater than December 31st 2019 and less than January 1st 2021\.

 **`_processed_date:>=2020-01-01 AND _processed_date:<=2020-12-31`** 

Returns documents that were processed in 2020—greater than or equal to January 1st 2020 and less than or equal to December 31st 2020\.

 **`_document_likes:<1`** 

Returns documents with zero likes or no user feedback—less than 1 like\.

You can specify whether a range should be treated as inclusive or exclusive of the given range values\.

 **Inclusive** 

 **`_last_updated_at:[2020-01-01 TO 2020-12-31]`** 

Returns documents last updated in 2020—includes the days December 1st 2020 and December 31st 2020\.

 **Exclusive** 

 **`_last_updated_at:{2019-12-31 TO 2021-01-01}`** 

Returns documents last updated in 2020—excludes the days December 31st 2019 and January 1st 2021\.

For unbounded ranges that are neither inclusive or exclusive, simply use the < and > operators\. For example, `_last_updated_at:>2019-12-31 AND _last_updated_at:<2021-01-01` 

#### Fields<a name="query-syntax-fields"></a>

You can limit your search to only return documents that meet a value in a specific field\. The field can be of any type\.

The following are examples of using field\-level context operators\.

 **`status:"Incomplete" AND financial_year:2021`** 

Returns documents for the 2021 financial year with their status as incomplete\.

 **`(sports OR recreation) AND country:"United States" AND level:"professional"`** 

Returns documents that discuss professional sports or recreation in the United States\.

#### Wildcards<a name="query-syntax-wildcards"></a>

You can broaden your search to account for variants of words and phrases using the wildcard operator\. This is useful when searching for name variants\. Amazon Kendra currently only supports trailing wildcards\. The number of prefix characters for a trailing wildcard must be greater than two\.

The following are examples of using wildcard operators\.

 **`Cloud*`** 

Returns documents that contain variants such as CloudFormation and CloudWatch\.

 **`kendra*aws`** 

Returns documents that contain variants such as kendra\.amazonaws\.

 **`kendra*aws*`** 

Returns documents that contain variants such as kendra\.amazonaws\.com

#### Exact quotes<a name="query-syntax-exact-quote"></a>

You can use quotation marks to search for an exact match of a piece of text\.

The following are examples of using quotation marks\.

 **`"Amazon Kendra" "pricing"`** 

Returns documents that contain both the phrase 'Amazon Kendra' and the term 'pricing'\. Documents must contain both 'Amazon Kendra' and 'pricing' in order to return in the results\.

 **`"Amazon Kendra" "pricing" cost`** 

Returns documents that contain both the phrase 'Amazon Kendra' and the term 'pricing', and optionally the term 'cost'\. Documents must contain both 'Amazon Kendra' and 'pricing' in order to return in the results, but might not necessarily include 'cost'\. 

#### Invalid query syntax<a name="query-syntax-invalid"></a>

Amazon Kendra issues a warning if there are problems with your query syntax or your query is currently not supported by Amazon Kendra\. For more information, see the [API documentation for query warnings](https://docs.aws.amazon.com/kendra/latest/dg/API_Warning.html)\.

The following queries are examples of invalid query syntax\.

 **`_last_updated_at:<2021-12-32`** 

Invalid date\. Day 32 does not exist in the Gregorian calendar, which is used by Amazon Kendra\.

 **`_view_count:ten`** 

Invalid numeric value\. Digits must be used to represent numeric values\.

 **`nonExistentField:123`** 

Invalid field search\. The field must exist in order to use field search\.

 **`Product:[A TO D]`** 

Invalid range\. Numeric values or dates must be used for ranges\.

 **`OR Hello`** 

Invalid Boolean\. Operators must be used with terms and placed between terms\.

## Searching in languages<a name="searching-index-languages"></a>

You can search for documents in a supported language\. That makes it possible for users to search and find documents in their native language\. You pass the language code in the [AttributeFilter](https://docs.aws.amazon.com/kendra/latest/dg/API_AttributeFilter.html) to return filtered documents in your chosen language\. You can type the query in a supported language\. 

If you do not specify a language, Amazon Kendra queries documents in English by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.

To search for documents in a supported language in the console, select your index, then select the option to search your index from the navigation menu\. Choose the language that you want to return documents by selecting the search settings and then selecting a language from the dropdown **Language**\.

The following examples show how to search for documents in Spanish\.

**To search an index in Spanish in the console**

1. Sign in to the AWS Management Console and open the Amazon Kendra console at [http://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.

1. In the navigation menu, choose **Indexes** and choose your index\.

1. In the navigation menu, choose the option to search your index\.

1. In the search settings, select the **Languages** dropdown and choose Spanish\.

1. Enter a query into the text box and then press enter\.

1. Amazon Kendra returns the results of the search in Spanish\.

**To search an index in Spanish using the CLI, Python or Java**
+ The following example searches an index in Spanish\. Change the value `searchString` to your search query and the value `indexID` to the identifier of the index that you want to search\. The language code for Spanish is `es`\. You can replace this with your own language code\.

------
#### [ CLI ]

  ```
  {
    "EqualsTo":{      
      "Key": "_language_code",
      "Value": {
      "StringValue": "es"
      }
    }
  }
  ```

------
#### [ Python ]

  ```
  import boto3
  import pprint
  
  kendra = boto3.client("kendra")
  
  # Provide the index ID
  index_id = "index-id"
  # Provide the query text
  query = "search-string"
  
  # Includes the index ID, query text, and language attribute filter
  response = kendra.query(
          QueryText = query,
          IndexId = index_id,
          AttributeFilter = {
              "EqualsTo": {      
                  "Key": "_language_code",
                  "Value": {
                      "StringValue": "es"
                      }
                  }
              })
  
  print ("\nSearch results|Resultados de la búsqueda: " + query + "\n")        
  
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
  import software.amazon.awssdk.services.kendra.model.QueryResponse;
  import software.amazon.awssdk.services.kendra.model.QueryResultItem;
  
  public class SearchIndexExample {
      public static void main(String[] args) {
          KendraClient kendra = KendraClient.builder().build();
  
          String query = "searchString";
          String indexId = "indexID";
  
          QueryRequest queryRequest = QueryRequest.builder()
              .queryText(query)
              .indexId(indexId)
              .attributeFilter(
                   AttributeFilter.builder()
                       .withEqualsTo(
                           DocumentAttribute.builder()
                               .withKey("_language_code")
                               .withValue("es")
                               .build())
                       .build())
              .build();
  
          QueryResponse queryResponse = kendra.query(queryRequest);
  
          System.out.println(String.format("\nSearch results|
                                            Resultados de la búsqueda: %s", query));
          for(QueryResultItem item: queryResponse.resultItems()) {
              System.out.println("----------------------");
              System.out.println(String.format("Type: %s", item.type()));
  
              switch(item.type()) {
                  case QUESTION_ANSWER:
                  case ANSWER:
                      String answerText = item.documentExcerpt().text();
                      System.out.println(answerText);
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