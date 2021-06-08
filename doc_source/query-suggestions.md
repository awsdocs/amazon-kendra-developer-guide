--------

--------

# Suggesting popular search queries<a name="query-suggestions"></a>

*Query suggestions* make typing search queries faster for your users and helps guide their search\.

Amazon Kendra suggests queries relevant to your users based on popular queries in the *query log*, or query history\. Amazon Kendra uses all of the queries your users search for and learns from these queries to make suggestions to your users\. Amazon Kendra currently suggests popular queries to users when they start typing their query\. Amazon Kendra suggests a query if the *prefix* or first few characters of the query matches what the user starts typing as their query\.

For example, a user starts typing the query 'upcoming events'\. Amazon Kendra has learned from the query log that many users have searched for 'upcoming events 2050' many times\. The user sees 'upcoming events 2050' appear directly underneath their search bar, auto\-completing their search query\. The user selects this query suggestion by choosing the first search result, which is the document 'Upcoming events: What’s happening in 2050'\.

You can specify how Amazon Kendra selects eligible queries to suggest to your users\. For example, you can specify that a query suggestion must have been searched by at least 10 unique users \(default is 3\), have been searched within the last 30 days, and does not contain any words or phrases from your [block list](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions#suggestions-block-list)\. Amazon Kendra requires a query to have at least one search result and contain at least one word of more than four characters\.

Query suggestions are case insensitive\. Amazon Kendra converts the query prefix and the suggested query to lower case, ignores all single and double quotation marks, and replaces multiple white space characters with a single space\. Amazon Kendra matches all other special characters as they are\. Amazon Kendra does not show any suggestions if a user types fewer than two characters or more than 60 characters\.

You can retrieve query suggestions relevant to your users by using the [GetQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_GetQuerySuggestions.html) operation\. Query suggestions are enabled by default at no additional cost\. You can disable query suggestions at any time by using the [UpdateQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateQuerySuggestionsConfig.html) operation\. You can test your settings before you apply suggestions to your search application in two ways:
+ By using the [UpdateQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateQuerySuggestionsConfig.html) operation\.
+ In the console in **Query suggestions settings**\. 

You use the [GetQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_GetQuerySuggestions.html) operation to integrate query suggestions with your console application for your users to start seeing the suggestions\.

## Query suggestions settings<a name="suggestions-settings"></a>

You can configure the following settings using the [UpdateQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateQuerySuggestionsConfig.html) operation:
+ **Mode** – Query suggestions are either `ENABLED` or `LEARN_ONLY`\. Amazon Kendra enables query suggestions by default\. `LEARN_ONLY` turns off query suggestions\. If turned off, Amazon Kendra continues to learn suggestions but doesn't make query suggestions to users\.
+ **Query log time window** – How recent your queries are in your query log time window\. The time window is an integer value for the number of days from current day to past days\.
+ **Queries without user information** – Set to `true` to include all queries or set to `false` to only include queries with user information\. 
+ **Unique users** – The minimum number of unique users who must search a query for the query to be eligible to suggest to your users\. This number is an integer value\.
+ **Query count** – The minimum number of times a query must be searched for the query to be eligible to suggest to your users\. This number is an integer value\.

These settings affect how queries are selected as popular queries to suggest to your users\. How you tune your settings will depend on your specific needs, for example:


+ If your users usually search once a month on average, then you can set the number of days in the query log time window to 30, so that you capture most of your users' recent queries before they become outdated in the time window\. 
+ If only a small number of your queries include user information, and you don’t want to suggest queries based on a small sample size, then you can set queries to include all users\. 
+ If you define *popular queries* as being searched by at least 10 unique users and searched at least 100 times, then you set the unique users to 10 and the query count to 100\.

Your changes to settings might not take effect right away\. You can track the settings changes by using the [DescribeQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_DescribeQuerySuggestionsConfig.html) operation\. The time for your updated settings to take effect depends on the updates that you make and the number of search queries in your index\.

------
#### [ Console ]

**To check that query suggestions are enabled and ready**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. On the **Query suggestions** page, go to **Query suggestions settings** and do the following:

   1. Check that **Status** is **Enabled**\.

   1. Check that the number of **Queries ready for suggestions** is more than 0\.

**To edit query suggestions settings**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. On the **Query suggestions** page, go to **Query suggestions settings** and choose **Edit**\.

**To clear suggestions**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. On the **Query suggestions** page, go to **Query suggestions settings** and then for **Actions**, choose **Clear suggestions**\.

------
#### [ CLI ]

**To retrieve query suggestions**

```
aws kendra get-query-suggestions \
--index-id index-id \
--query-text "query-text" \
--max-suggestions-count 1     // If you want to limit the number of suggestions.
```

**To update query suggestions**

For example, to change the query log time window and the minimum number of times a query must be searched:

```
aws kendra update-query-suggestions-config \
--index-id index-id \
--query-log-look-back-window-in-days 30 \
--minimum-query-count 100
```

**Note**  
The time for your updated settings to take effect depends on the updates you make and the number of search queries in your index\.

**To clear suggestions**

```
aws  kendra clear-query-suggestions \
--index-id index-id \
```

**Note**  
Amazon Kendra learns new suggestions based on new queries added to the query log from the time you cleared suggestions\.

------
#### [ Python ]

**To retrieve query suggestions**

```
import boto3
from botocore.exceptions import ClientError

kendra = boto3.client("kendra")

print("Getting suggestions for a query.")

index_id = "index-id"
query_text = "query"

try:
    query_suggestions_response = kendra.get_query_suggestions(
        IndexId = index_id,
        QueryText = query_text,
        MaxSuggestionsCount = 5
    )

    # Printing out the suggestions you received.
    if ("Suggestions" in query_suggestions_response.keys()) {
        for (suggestion: query_suggestions_response["Suggestions"]) {
            print(suggestion["Value"]["Text"]["Text"]);
        }
    }
   
except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

**To update query suggestions**,

For example, to change the query log time window and the minimum number of times a query must be searched:

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Updating query suggestions settings/configuration for an index.")

query_log_look_back_window_in_days = 30
minimum_query_count = 100
thesaurus_role_arn = "role-arn"

index_id = "index-id"

s3_bucket_name = "bucket-name"
s3_key = "thesaurus-file"
source_s3_path= {
    'Bucket': s3_bucket_name,
    'Key': s3_key
}

try:
    kendra.update_query_suggestions_config(
        MinimumQueryCount = minimum_query_count,
        IndexId = index_id,
        QueryLogLookBackWindowInDays = query_log_look_back_window_in_days
    )

    print("Wait for Amazon Kendra to update the query suggestions.")

    while True:
        # Get query suggestions description of settings/configuration.
        query_sugg_config_response = kendra.describe_query_suggestions_config(
            IndexId = index_id
        )
        
        # If status is not UPDATING, then quit.
        status = query_sugg_config_response["Status"]
        print("Updating query suggestions config. Status: " + status)
        if status != "UPDATING":
            break
        time.sleep(60)

except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

**To clear suggestions**

```
import boto3
from botocore.exceptions import ClientError

kendra = boto3.client("kendra")

print("Clearing out query suggestions for an index.")

index_id = "index-id"

try:
    kendra.clear_query_suggestions(
        IndexId = index_id
    )

    # Confirm last cleared date-time and there are no suggestions:
    query_sugg_config_response = kendra.describe_query_suggestions_config(
        IndexId = index_id
    )
    print("Query Suggestions last cleared at: " + str(query_sugg_config_response["LastClearTime"]));
    print("Number of suggestions available to use after clearing: " + str(query_sugg_config_response["TotalSuggestionsCount"]));
        
except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------

You can check your current settings by using the [DescribeQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_DescribeQuerySuggestionsConfig.html) operation\. Additionally, this operation shows the following information about your query suggestions for an index:
+ **Mode** – Query suggestions are either `ENABLED` or `LEARN_ONLY`\. Amazon Kendra enables query suggestions by default\. `LEARN_ONLY` turns off query suggestions\. You can change the mode by using the [UpdateQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateQuerySuggestionsConfig.html) operation\. If turned off, Amazon Kendra continues to learn suggestions but doesn't make query suggestions to users\.
+ **Status** – Query suggestions are either `ACTIVE` or `UPDATING`\.
+ **Suggestions count** – The total number of queries ready to be suggested to your users\. If the count is much lower than you expected, it could be because Amazon Kendra needs more queries to learn from or your current query suggestions settings are too strict\.
+ **Suggestions last build time** – The last time suggestions were updated\. Amazon Kendra automatically updates suggestions every 24 hours, or when you change a setting or when you apply a [block list](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions.html#suggestions-block-list)\. 
+ **Suggestions last cleared time** – The last time suggestions were cleared\.

## Block certain queries from suggestions<a name="suggestions-block-list"></a>

A *block list* stops Amazon Kendra from suggesting certain popular queries to your users\. It is a list of words or phrases you want to exclude from query suggestions\. Amazon Kendra excludes queries containing an exact match of the words or phrases in the block list\.

You can use a block list to safeguard against offensive words or phrases that commonly appear in your query log and that Amazon Kendra could select as suggestions\. A block list can also prevent Amazon Kendra from suggesting popular queries that contain information that is not ready to be publicly released or announced\. For example, if your users commonly query about a release of a new product that you don’t want to suggest because you are not ready to release soon, then you can block queries that contain the product name and product information from suggestions\.

You can create a block list for queries by using the [CreateQuerySuggestionsBlockList](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateQuerySuggestionsBlockList.html) operation\. You put each block word or phrase on a separate line in a text file\. Then you upload the text file to your S3 bucket and provide the path or location to the file on Amazon S3\. Amazon Kendra currently supports creating only one block list\.

You can replace the text file of your blocked words and phrases in your S3 bucket and use the [UpdateQuerySuggestionsBlockList](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateQuerySuggestionsBlockList.html) to update the block list in Amazon Kendra\.

You can use the [DescribeQuerySuggestionsBlockList](https://docs.aws.amazon.com/kendra/latest/dg/API_DescribeQuerySuggestionsBlockList.html) operation to get the status of your block list and other useful information, such as when your block list was last updated, how many words or phrases are in your current block list, and helpful error messages when creating a block list\. You can also use the [ListQuerySuggestionsBlockLists](https://docs.aws.amazon.com/kendra/latest/dg/API_ListQuerySuggestionsBlockLists.html) operation to get a list of block list summaries for an index\.

To delete your block list, use the [DeleteQuerySuggestionsBlockList](https://docs.aws.amazon.com/kendra/latest/dg/API_DeleteQuerySuggestionsBlockList.html) operation\.

Your updates to the block list might not take effect right away\. You can track updates by using the [DescribeQuerySuggestionsBlockList](https://docs.aws.amazon.com/kendra/latest/dg/API_DescribeQuerySuggestionsBlockList.html) operation\.

------
#### [ Console ]

**To import a block list**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. On the **Query suggestions** page, go to **Block list** and choose **Import block list**\.

1. In the **Block list file location on S3**, field enter the location of your block list text file in your S3 bucket\. 

**To update and reload a block list**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. Replace the block list text file in the S3 bucket with your updated file\.

1. On the **Query suggestions** page, go to **Block list** and choose **Reload**\. 

**To delete a block list**

1. In the left navigation pane, under **Indexes**, go to your index, and then for **Enrichments**, select **Query suggestions**\.

1. On the **Query suggestions** page, go to **Block list** and then choose **Delete**\.

------
#### [ CLI ]

**To create a block list**

```
aws kendra create-query-suggestions-block-list \
--index-id index-id \
--name "block-list-name" \
--description "block-list-description" \
--source-s3-path "Bucket=bucket-name,Key=query-suggestions/block_list.txt" \
--role-arn role-arn
```

**To update a block list**

```
aws kendra update-query-suggestions-block-list \
--index-id index-id \
--name "block-list-name" \
--description "block-list-description" \
--source-s3-path "Bucket=bucket-name,Key=query-suggestions/block_list.txt" \
--role-arn role-arn
```

**To delete a block list**

```
aws kendra delete-query-suggestions-block-list \
--index-id index-id \
--id block-list-id
```

------
#### [ Python ]

**To create a block list**

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Create a query suggestions block list")

block_list_name = "block-list-name"
block_list_description = "block-list-description"
block_list_role_arn = "role-arn"

index_id = "index-id"

s3_bucket_name = "bucket-name"
s3_key = "query-suggestions/block_list.txt"
source_s3_path = {
    'Bucket': s3_bucket_name,
    'Key': s3_key
}

try:
    block_list_response = kendra.create_query_suggestions_block_list(
        Description = block_list_description,
        Name = block_list_name,
        RoleArn = block_list_role_arn,
        IndexId = index_id,
        SourceS3Path = source_s3_path
    )

    print(block_list_response)

    block_list_id = block_list_response["Id"]

    print("Wait for Kendra to create the block list.")

    while True:
        # Get block list description
        block_list_description = kendra.describe_query_suggestions_block_list(
            Id = block_list_id,
            IndexId = index_id
        )
        # If status is not CREATING, then quit.
        status = block_list_description["Status"]
        print("Creating block list. Status: " + status)
        if status != "CREATING":
            break
        time.sleep(60)
except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

**To update a block list**

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time
                        
kendra = boto3.client("kendra")
                        
print("Update a block list for query suggestions.")
                        
block_list_name = "block-list-name"
block_list_description = "block-list-description"
block_list_role_arn = "role-arn"
                        
block_list_id = "block-list-id"
index_id = "index-id"
                        
s3_bucket_name = "bucket-name"
s3_key = "query-suggestions/block_list_updated.txt"
source_s3_path = {
'Bucket': s3_bucket_name,
'Key': s3_key
}
                        
try:
kendra.update_query_suggestions_block_list (
Id = block_list_id,
IndexId = index_id,
Description = block_list_description,
Name = block_list_name,
RoleArn = block_list_role_arn,
SourceS3Path = source_s3_path
)
                        
print("Wait for Amazon Kendra to update the block list.")
                        
while True:
# Get block list description
block_list_description = kendra.describe_query_suggestions_block_list(
Id = block_list_id,
IndexId = index_id
)
# If status is not UPDATING, then the update has finished. 
status = block_list_description["Status"]
print("Updating block list. Status: " + status)
if status != "UPDATING":
break
time.sleep(60)
                        
except ClientError as e:
print("%s" % e)
                        
print("Program ends.")
```

**To delete a block list**

```
import boto3
from botocore.exceptions import ClientError

kendra = boto3.client("kendra")

print("Delete a block list for query suggestions.")

query_suggestions_block_list_id = "query-suggestions-block-list-id"
index_id = "index-id"

try:
    kendra.delete_query_suggestions_block_list(
        Id = query_suggestions_block_list_id,
        IndexId = index_id
    )

except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------

## Clear suggestions<a name="clear-suggestions"></a>

You can clear query suggestions by using the [ClearQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_ClearQuerySuggestions.html) operation\. Clearing suggestions deletes existing query suggestions only, not the queries in the query log\. After you clear suggestions, Amazon Kendra learns new suggestions based on new queries added to the query log from the time you cleared suggestions\.

## No suggestions available<a name="no-suggestions"></a>

If you don’t see suggestions for a query, it could be for one of the following reasons:
+ There are not enough queries in your index for Amazon Kendra to learn from\.
+ Your query suggestions settings are too strict, resulting in most queries being filtered out from suggestions\.
+ You recently cleared suggestions, and Amazon Kendra still needs time for new queries to accumulate in order to learn new suggestions\.

You can check your current settings using the [DescribeQuerySuggestionsConfig](https://docs.aws.amazon.com/kendra/latest/dg/API_DescribeQuerySuggestionsConfig.html) operation\.