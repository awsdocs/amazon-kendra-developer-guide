--------

--------

# Featured search results<a name="featured-results"></a>

You can feature certain documents in the search results when your users issue certain queries\. This helps make the results more visible and prominent for your users\. Featured results are separated out from the usual list of results, and displayed at the top of the search page\. You can experiment with featuring different documents for different queries, or ensure certain documents get the visibility they deserve\.

You map specific queries to specific documents for featuring in the results\. If a query contains an exact match, then one or more specific documents are featured in the search results\.

For example, you can specify that if your users issue the query 'new products 2023', then select the documents titled 'What's new' and 'Coming soon' to feature at the top of the search results page\. This helps ensure these documents on new products get the visibility they deserve\.

Amazon Kendra doesn't duplicate search results if a result is already selected for featuring at the top of the search results page\. A featured result isn't again ranked as the first result if it is already featured above all other results\.

In order to feature certain results, you must specify an exact match of a full text query, not a partial match of a query using a keyword or phrase contained within a query\. For example, if you only specify the query 'Kendra' in a featured result set, queries such as 'How does Kendra semantically rank results?' will not render the featured results\. Featured results are designed for specific queries, rather than queries that are too broad in scope\. Amazon Kendra naturally handles keyword type queries to rank the most useful documents in the search results, avoiding excessive featuring of results based on simple keywords\.

If there are certain queries that your users frequently use, then you can specify these queries for featured results\. For example, if you look at your top queries using [Amazon Kendra Analytics](https://docs.aws.amazon.com/kendra/latest/dg/search-analytics.html) and find that specific queries, such as 'How does kendra semantically rank results?' and 'kendra semantic search', are frequently used, then these queries might be useful to specify for featuring the document titled 'Amazon Kendra search 101'\.

Amazon Kendra treats queries for featured results as case insensitive\. Amazon Kendra converts a query to lower case, and replaces trailing white space characters with a single space\. Amazon Kendra matches all other characters as they are when you specify your queries for featured results\.

You create a set of featured results that you map to certain queries using the [CreateFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateFeaturedResultsSet.html) API\. If you use the console, you select your index and then select **Featured results** in the navigation menu to create a featured results set\.You can create up to 50 sets of featured results per index and add up to four documents to be featured per set\. You can request to increase these limits by contacting [Support](http://aws.amazon.com/contact-us/)\.

You can select the same document across multiple sets of featured results\. However, you must not use the same exact match query text across multiple sets\. The queries you specify for featured results must be unique per featured results set for each index\.

You can arrange the order of documents when selecting up to four featured documents\. If you use the API, the order you list the featured documents is the same as displayed in the featured results\. If you use the console, you can simply drag and drop the order of documents when you select documents for featuring in the results\.

Access control, where certain users and groups have access to certain documents and others don't, is still honored when configuring featured results\. That's also true for user context filtering\. For example, user A belongs to the 'Interns' company group, which shouldn't access documents on company secrets\. If user A enters a query that features a company secret document, user A doesn't see this document featured in their results\. That's also true for any other results on the search results page\. You can also use tags to control access to a featured results set, which is an Amazon Kendra resource for which you control access\.

The following is an example of creating a set of featured results with the queries "new products 2023", "new products available" mapped to the documents titled "What's new" \(doc\-id\-1\) and "Coming soon" \(doc\-id\-2\)\.

------
#### [ CLI ]

```
aws kendra create-featured-results-set \
 --featured-results-set-name 'New product docs to feature' \
 --description "Featuring What's new and Coming soon docs" \
 --index-id index-id \
 --query-texts 'new products 2023' 'new products available' \
 --featured-documents '{"Id":"doc-id-1", "Id":"doc-id-2"}'
```

------
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Create a featured results set.")

# Provide a name for the featured results set
featured_results_name = "New product docs to feature"
# Provide an optional decription for the featured results set
description = "Featuring What's new and Coming soon docs"
# Provide the index ID for the featured results set
index = index-id
# Provide a list of query texts for the featured results set
queries = ['new products 2023', 'new products available']
# Provide a list of document IDs for the featured results set
featured_doc_ids = ['doc-id-1', 'doc-id-2']

try:
    featured_results_set_response = kendra.create_featured_results_set(
        FeaturedResultsSetName = featured_results_name,
        Decription = description,
        Index = index,
        QueryTexts = queries,
        FeaturedDocuments = featured_doc_ids
    )

    pprint.pprint(featured_results_set_response)

    featured_results_set_id = featured_results_set_response["FeaturedResultsSetId"]

    while True:
        # Get the details of the featured results set, such as the status
        featured_results_set_description = kendra.describe_featured_results_set(
            Id = featured_results_set_id
        )
        status = featured_results_set_description["Status"]
        print(" Featured results set status: "+status)
            
except  ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------