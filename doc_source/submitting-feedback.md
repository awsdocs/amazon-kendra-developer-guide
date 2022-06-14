--------

--------

# Submitting feedback for incremental learning<a name="submitting-feedback"></a>

Amazon Kendra uses incremental learning to improve search results\. Using feedback from queries, incremental learning improves the ranking algorithms and optimizes search results for greater accuracy\.

For example, suppose that your users search for the phrase "health care benefits\." If users consistently choose the second result from the list, over time Amazon Kendra boosts that result to the first place result\. The boost decreases over time, so if users stop selecting a result, Amazon Kendra eventually removes it and shows another more popular result instead\. This helps Amazon Kendra prioritize results based on relevance, age, and content\.

Incremental learning is enabled for all indexes and for all document types\. For more information, see [Response types](response-types.md)\.

Amazon Kendra starts learning as soon as you provide feedback, though it can take over 24 hours to see the results of the feedback\. Amazon Kendra provides three methods for you to submit feedback: the AWS console, a JavaScript library that you can include on your search results page, and an API that you can use\.

Amazon Kendra accepts two types of user feedback:
+ **Clicks** \- Information about which query results the user chose\. The feedback includes the result ID and the Unix timestamp of the date and time that the search result was chosen\. 

  To submit click feedback, your application must collect click information from the activities of your users, and then submit that information to Amazon Kendra\. You can collect click information with the console, the JavaScript library, and the Amazon Kendra API\.
+ **Relevance** \- Information about the relevance of a search result, which the user typically provides\. The feedback contains the result ID and a relevance indicator \(`RELEVANT` or `NOT_RELEVANT`\)\. The user determines the relevance information\. 

  To submit relevance feedback, your application must provide a feedback mechanism that enables the user to choose the appropriate relevance for a query result, and then submit that information to Amazon Kendra\. You can only collect relevance information with the console and the Amazon Kendra API\.

Feedback is used while the index is active\. Feedback only affects the index that it is submitted to, it can't be used across indexes or for different accounts\.

You should provide additional user context when you query your Amazon Kendra index\. When you provide user context, Amazon Kendra is able to tell if the feedback is provided by a single user or by multiple users and adjust search results accordingly\.

When you provide user context, the feedback for the query is associated with the specific user provided in the context\. If you don't specify user context, you can provide a visitor ID that is used to group and aggregate queries\. 

If you don't provide user context or a visitor ID, the feedback is anonymous and aggregated with other anonymous feedback\.

The following code shows how to include user context as a token or the visitor ID\.

```
response = kendra.query(
    QueryText = query,
    IndexId = index,
    UserToken = {
        Token = "token"
    })
    
    OR
    
    response = kendra.query(
    QueryText = query,
    IndexId = index,
    VisitorId = "visitor-id")
```

For web applications, you can use cookies, locations, or browser users to generate a visitor ID for each user\.

For head queries, the largest volume of queries, providing click\-through feedback provides enough information to improve overall accuracy\. For tail queries, those that are rare, subject matter experts should submit relevant and non\-relevant feedback to improve accuracy for those queries\.

In addition to the console, you can use one of two methods: a JavaScript library or the [SubmitFeedback](API_SubmitFeedback.md) API\. You should only use one method of gathering feedback\. For best results, you should submit feedback within 24 hours of making the query\.

**Topics**
+ [Using the Amazon Kendra JavaScript library to submit feedback](feedback-javascript.md)
+ [Using the Amazon Kendra API to submit feedback](feedback-api.md)