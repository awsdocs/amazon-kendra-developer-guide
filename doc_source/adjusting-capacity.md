--------

--------

# Adjusting capacity<a name="adjusting-capacity"></a>

Amazon Kendra provides resources for your index in *capacity units*\. Each capacity unit provides additional resources for your index\. There are separate capacity units for storage and for queries\. You can only add capacity units to Amazon Kendra Enterprise indexes\. You can't add capacity to a Developer edition index\.

A document storage capacity unit provides the following additional storage for your index\.
+ 100,000 documents or 30 GB of storage\.

A query capacity unit provides the following additional queries for your index\.
+ 0\.1 queries per second or approximately 8,000 queries per day\.

Each index comes with a base capacity equal to 1 capacity unit\. There is an additional cost for each additional capacity unit\. For details, see [ Amazon Kendra pricing](https://aws.amazon.com/kendra/pricing/)\.

You can adjust capacity units up to 5 times per day to tune the capacity of your index to the expected usage\. You can't reduce document storage capacity below the number of documents stored in your index\. For example, if you are storing 150,000 documents, you can't reduce the storage capacity below 1 additional unit\.

You can add up to 100 capacity units to your storage and query resources\. If you need additional resources, [contact AWS support](https://console.aws.amazon.com/support/home?#/)\.

You can use the Amazon Kendra console or the [ DescribeIndex ](API_DescribeIndex.md) operation to view the resources that your index is using\. Amazon Kendra also returns exceptions when you exceed the capacity of an index\. You get a `ServiceQuotaExceededException` exception when you exceed your storage capacity and a `ThrottlingException` exception when you exceed your queries per second capacity\.

## Viewing capacity<a name="viewing-capacity"></a>

View the resources that your index is using with the Amazon Kendra console\. The console provides graphs that you can use to determine how much storage and query capacity your index uses\. You can use this information to help you plan when to add additional capacity\.

**To view document storage and query use \(Console\)**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index to view capacity\.

1. The **Document count** and **Storage used ** fields of the **Index details** show you the amount of storage that your index uses\. Scroll to the the **Queries per second** chart to see a graph of the queries per second for your index\.

## Adding and removing capacity<a name="adding-capacity"></a>

If you need additional capacity for your index, you can add it using the console or the Amazon Kendra API\. When you add capacity, don't add more than you need to help reduce costs\.

**To add or remove storage or query capacity \(Console\)**

1. Sign into the AWS Management Console and open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/home](https://console.aws.amazon.com/kendra/home)\.

1. From the list of indexes, choose the index that you want to add or remove capacity\.

1. From the **Actions** menu, choose **Edit**\.

1. On the **Specify index details** page, choose **Next**\.

1. On the **Add additional capacity** page, choose the new query per second and document storage capacity units that you want to use for the index\.

1. Choose **Update** to save your changes and update your index to the new capacity\.

After you update the capacity of your index, it can take up 60 minutes for the changes to take effect\.

To add or remove capacity using the Amazon Kendra API, use the `CapacityUnits` parameter [ UpdateIndex ](API_UpdateIndex.md) operation\.

## Query suggestions capacity<a name="query-suggestions-capacity"></a>

When using [query suggestions](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions.html), there’s a base query capacity of 2\.5 [GetQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_GetQuerySuggestions.html) calls per second\. The `GetQuerySuggestions` capacity is five times the provisioned query capacity for an index, or the base capacity of 2\.5 calls per second, whichever is higher\. For example, the base capacity for an index is 0\.1 queries per second, and `GetQuerySuggestions` capacity has a base of 2\.5 calls per second\. If you add another 0\.1 queries per second to total 0\.2 queries per second for an index, the `GetQuerySuggestions` capacity is 2\.5 calls per second \(higher than five times 0\.2 queries per second\)\.

## Adaptive query bursting<a name="adaptive-query-bursting"></a>

Amazon Kendra has a provisioned base capacity of 1 query capacity unit\. You can use up to 8,000 queries per day with a minimum throughput of 0\.1 queries per second \(per query capacity unit\)\.

An adaptive approach to handling unexpected traffic beyond the provisioned throughput is Amazon Kendra's built in *adaptive query bursting*\. This allows you to apply unused query capacity to handle unexpected traffic\. Amazon Kendra accumulates your unused queries at your provisioned queries per second rate, every second, up to the maximum number of queries you've provisioned for your Amazon Kendra index\. These accumulated queries are used for unexpected traffic above the allocated capacity\. Optimal performance of adaptive query bursting can vary, depending on several factors such as your total index size, query complexity, accumulated unused queries, and overall load on your index\. It is recommended that you perform your own load tests to accurately measure bursting capacity\.

Adaptive query bursting is only available in the enterprise edition of Amazon Kendra\.