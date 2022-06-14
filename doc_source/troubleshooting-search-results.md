--------

--------

# Troubleshooting document search results<a name="troubleshooting-search-results"></a>

This section can help you fix issues in your Amazon Kendra search results\.

## Why do I only see 100 results?<a name="troubleshooting-search-results-missing-docs-only-hundred"></a>

Amazon Kendra returns the total count of relevant documents\. The top 100 are returned per query by default\. The results are paginated\. You can use `PageNumber` to access different pages\. 

You can enable Amazon Kendra to return up to 1000 documents or search results per query, with up to 100 results per page\. To return more than 100 results, you can request this by contacting [Quotas Support](https://console.aws.amazon.com/servicequotas/)\. Increasing the number of search results could impact latency\.

## Why are documents I expect to see missing?<a name="troubleshooting-search-results-missing-docs-expected-missing"></a>

Amazon Kendra supports access control lists \(ACLs\) based on user and groups\. Amazon Kendra ingests ACL policies via connectors\. If an index does not configure an ACL, only documents matching the attribute filter for user and group will be shown\. If a user or group attribute filter is provided, documents without an ACL will not be shown\. 

 If you are using token\-based access control, documents without an ACL policy and documents that match the user and groups will be shown\. 

## Why do I see documents that have an ACL policy?<a name="troubleshooting-search-results-missing-docs-acl"></a>

If an index does not configure an access control policy, then user and groups can be provided by the filter\. If no user and group filter is applied then all related documents will be returned\. Any ACL policy will be ignored\. 