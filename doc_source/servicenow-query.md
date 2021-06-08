--------

--------

# Specifying documents to index with a query<a name="servicenow-query"></a>

You can use a ServiceNow query to specify the documents you want to include in a Amazon Kendra index\. When you use a query, you can specify multiple knowledge bases, including private knowledge bases\. Access to the knowledge bases is determined by the user that you use to connect to the ServiceNow instance\.

To build a query, you use the ServiceNow query builder\. You can use the builder to create the query and to test that the query returns the correct list of documents\.

**To create a query using the ServiceNow console**

1. Log in to the ServiceNow console\.

1. From the left menu, choose **Knowledge**, then **Articles**, and the choose **All**\.

1. At the top of the page, choose the filter icon\.

1. Use the query builder to create the query\.

1. When the query is complete, right click the query and choose **Copy query** to copy the query from the query builder\. Save this query to use in Amazon Kendra\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/kendra/latest/dg/images/ServiceNowQuery.png)

Be careful that you don't change any query parameter when you copy the query\. If any of the query parameters are not recognized, ServiceNow treats the parameter as empty and doesn't use it to filter the results\.