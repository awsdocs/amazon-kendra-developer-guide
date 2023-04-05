--------

--------

# Adjusting capacity<a name="adjusting-capacity"></a>

Amazon Kendra provides resources for your index in *capacity units*\. Each capacity unit provides additional resources for your index\. There are separate capacity units for document storage and for queries\. You can only add capacity units to Amazon Kendra Enterprise Edition indexes\. You can't add capacity to a Developer Edition index\.

A document storage capacity unit provides the following additional storage for your index\.
+ 100,000 documents or 30 GB of storage\.

A query capacity unit provides the following additional queries for your index\.
+ 0\.1 queries per second or approximately 8,000 queries per day\.

Each index comes with a base capacity equal to 1 capacity unit \(30 GB of storage and 0\.1 queries per second\)\. There is an additional cost for each additional capacity unit\. For details, see [Amazon Kendra pricing](http://aws.amazon.com/kendra/pricing/)\.

You can add up to 100 extra capacity units to your storage and query resources for an index\. If you need more units, [contact AWS support](http://aws.amazon.com/contact-us/)\.

You can adjust capacity units up to 5 times per day to fit your usage requirements\. You can't reduce document storage capacity below the number of documents stored in your index\. For example, if you are storing 150,000 documents, you can't reduce the storage capacity below 1 additional unit\.

You can view the resources an index is using in the console by selecting the name of the index to open the index settings and other information, or you can use the [DescribeIndex](API_DescribeIndex.md) API\. Amazon Kendra also returns exceptions when you exceed the capacity of an index\. You get a `ServiceQuotaExceededException` when the total extracted size of all the documents exceeds the limit for an index\. You get a `InvalidRequest` for each document when the number of documents exceeds the limit for an index\. You get a `ThrottlingException` when the number of queries per second exceeds the limit\. For more information on limits, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.

## Viewing capacity<a name="viewing-capacity"></a>

View the resources that your index is using with the Amazon Kendra console by selecting the name of your index to access the details\. The console also provides usage graphs so you can determine how much storage and query capacity your index uses\. You can use this information to help you plan when to add additional capacity\.

**To view document storage and query use \(console\)**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index you want to access\.

1. Scroll to the settings section to view the current total document storage and query capacity\.

To view capacity using the Amazon Kendra API, use the `CapacityUnits` parameter in the [DescribeIndex](API_DescribeIndex.md) API\.

## Adding and removing capacity<a name="adding-capacity"></a>

If you need additional capacity for your index, you can add it using the console or the Amazon Kendra API\.

**To add or remove storage or query capacity \(console\)**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to access\.

1. Select **Edit**, or select **Edit** from the **Actions** dropdown\.

1. Select **Next** to go to the provisioning details page\.

1. Add or remove document storage and/or query capacity units\.

1. Continue to select **Next** to go to the review page and then select **Update** to save your changes\.

After you update the capacity of your index, it can take several minutes for the changes to take effect\.

To add or remove capacity using the Amazon Kendra API, use the `CapacityUnits` parameter in the [UpdateIndex](API_UpdateIndex.md) API\.

## Amazon Kendra Intelligent Ranking capacity<a name="intelligent-ranking-capacity"></a>

A capacity unit provides the following additional rescore requests per second for a rescore execution plan\. A rescore execution plan is a resource used to provision the [Rescore](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_Rescore.html) API\.
+ 0\.01 requests per second\.

Each rescore execution plan comes with a base capacity equal to 1 capacity unit \(0\.01 requests per second\)\. There is an additional cost for each additional capacity unit\. For details, see [Amazon Kendra pricing](http://aws.amazon.com/kendra/pricing/)\.

You can add up to 1000 extra capacity units for a rescore execution plan\. If you need more units, [contact AWS support](http://aws.amazon.com/contact-us/)\.

## Query suggestions capacity<a name="query-suggestions-capacity"></a>

When using [query suggestions](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions.html), there’s a base query capacity of 2\.5 [GetQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_GetQuerySuggestions.html) calls per second\. The `GetQuerySuggestions` capacity is five times the provisioned query capacity for an index, or the base capacity of 2\.5 calls per second, whichever is higher\. For example, the base capacity for an index is 0\.1 queries per second, and `GetQuerySuggestions` capacity has a base of 2\.5 calls per second\. If you add another 0\.1 queries per second to total 0\.2 queries per second for an index, the `GetQuerySuggestions` capacity is 2\.5 calls per second \(higher than five times 0\.2 queries per second\)\.

## Amazon Kendra experience capacity<a name="amazon-kendra-experience-capacity"></a>

### Search experience capacity<a name="search-experience-capacity"></a>

Amazon Kendra starts to throttle `Query`, `QuerySuggestions`, `SubmitFeedback` for your Amazon Kendra experience at 15 requests per second and 40 requests per second for query bursting\. For an index with more than 150 query capacity units, these limits still apply\.

For example, your query capacity units for your index is 150, so your search experience application can handle 15 requests per second\. However, if you scaled to 200 query capacity units, then your search experience app would still only handle 15 requests per second\. If you limit your index to 100 query capacity units, then your search experience app would only handle 10 requests per second\.

## Adaptive query bursting<a name="adaptive-query-bursting"></a>

Amazon Kendra has a provisioned base capacity of 1 query capacity unit\. You can use up to 8,000 queries per day with a minimum throughput of 0\.1 queries per second \(per query capacity unit\)\. Accumulated queries will last up to 24 hours and can accommodate bursts of traffic\. The amount of burst allowed varies because it depends on the cluster's load at any given time\. Provision enough query capacity units to handle your peak load levels\. 

An adaptive approach to handling unexpected bursts of traffic beyond the provisioned throughput is Amazon Kendra's built\-in *adaptive query bursting*\. Adaptive query bursting is available in the Enterprise Edition of Amazon Kendra\.

Adaptive query bursting is a built\-in capability that allows you to apply unused query capacity to handle unexpected traffic\. Amazon Kendra accumulates your unused queries at your provisioned queries per second rate, every second, up to the maximum number of queries you've provisioned for your Amazon Kendra index\. These accumulated queries are used for unexpected traffic above the allocated capacity\. Optimal performance of adaptive query bursting can vary, depending on several factors such as your total index size, query complexity, accumulated unused queries, and overall load on your index\. It is recommended that you perform your own load tests to accurately measure bursting capacity\.