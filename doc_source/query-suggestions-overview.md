--------

--------

# Query suggestions<a name="query-suggestions-overview"></a>

*Query suggestions* make typing search queries faster for your users and helps guide their search\. Amazon Kendra suggests queries that are relevant to your users based on popular queries in the *query log*, or query history\. Amazon Kendra uses all the queries your users search for and learns from these queries to make suggestions to your users\.

For example, a user starts typing the query 'upcoming events'\. Amazon Kendra has learned from the query log that many users have searched for 'upcoming events 2050' many times\. The user sees 'upcoming events 2050' appear directly underneath their search bar, auto\-completing their search query\. The user selects this query suggestion by choosing the first search result, which is the document 'Upcoming events: What’s happening in 2050'\.

You can specify how Amazon Kendra selects eligible queries to suggest to your users\. You can also block certain queries from being suggested to your users\.

For more information, see [Suggesting popular search queries](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions.html)\.