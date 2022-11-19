--------

--------

# Searching indexes<a name="searching"></a>

To search an Amazon Kendra index, you use the [Query](API_Query.md) API\. The `Query` API returns information about the indexed documents that you use in your application\. This section shows you how to make a query, perform filters, and interpret the response that you get from the `Query` API\. This section also shows how to submit feedback about the quality of a search result\.

To search documents that you have indexed with Amazon Kendra for Amazon Lex, use [AMAZON\.KendraSearchIntent](https://docs.aws.amazon.com/lexv2/latest/dg/API_KendraConfiguration.html)\. For an example of configuring Amazon Kendra with Amazon Lex, see [Creating a FAQ Bot for an Amazon Kendra Index](https://docs.aws.amazon.com/lexv2/latest/dg/faq-bot-kendra-search.html)\.

**Topics**
+ [Querying an index](searching-example.md)
+ [Browsing an index](browsing.md)
+ [Filtering queries](filtering.md)
+ [Filtering on user context](user-context-filter.md)
+ [Query responses](query-response.md)
+ [Query suggestions](query-suggestions.md)
+ [Query spell checker](query-spell-check.md)
+ [Tuning responses](tuning-responses.md)
+ [Sorting responses](sorting.md)
+ [Response types](response-types.md)