--------

--------

# Using the Amazon Kendra API to submit feedback<a name="feedback-api"></a>

To use the Amazon Kendra API to submit query feedback, use the [SubmitFeedback](API_SubmitFeedback.md) API\. To identify the query, you supply the `IndexID` of the index that the query applies to, and the `QueryId` returned in the response from the [Query](API_Query.md) API\.

The following example shows how to submit click and relevance feedback using the Amazon Kendra API\. You can submit multiple sets of feedback through the `ClickFeedbackItems` and `RelevanceFeedbackItems` arrays\. This example submits a single click and a single relevance feedback item\. The feedback submittal uses the current time\.

**To submit feedback for a search \(AWS SDK\)**

1. Use the following code and change the following values:

   1. `index id` \- Change to the ID of the index that the query applies to\.

   1. `query id` \- Change to the query that you want to provide feedback on\.

   1. `result id` \- Change to the ID of the query result that you want to provide feedback on\. The query response contains the result ID\.

   1. `relevance value` \- Change to either `RELEVANT` \(the query result is relevant\) or `NOT_RELEVANT` \(the query result is not relevant\)\.

------
#### [ Python ]

   ```
   import boto3
   import time
   
   kendra = boto3.client("kendra")
   
   # Provide the index ID
   index_id = "index-id"
   # Provide the query ID
   query_id = "query-id"
   # Provide the search result ID
   result_id = "result-id"
   
   # Configure the feedback item
   feedback_item = {"ClickTime": int(time.time()),
       "ResultId":result_id}
   
   # Configure the relevance value
   relevance_value = "RELEVANT"
   relevance_item = {"RelevanceValue": relevance_value,
       "ResultId": result_id
       }
   
   response = kendra.submit_feedback(
       QueryId = query_id,
       IndexId = index_id,
       ClickFeedbackItems = [feedback_item],
       RelevanceFeedbackItems = [relevance_item]
   )
   
   
   print("Submitted feedback for query: " + query_id)
   ```

------
#### [ Java ]

   ```
   package com.amazonaws.kendra;
   
   import java.time.Instant;
   import software.amazon.awssdk.services.kendra.KendraClient;
   import software.amazon.awssdk.services.kendra.model.ClickFeedback;
   import software.amazon.awssdk.services.kendra.model.RelevanceFeedback;
   import software.amazon.awssdk.services.kendra.model.RelevanceType;
   import software.amazon.awssdk.services.kendra.model.SubmitFeedbackRequest;
   import software.amazon.awssdk.services.kendra.model.SubmitFeedbackResponse;
   
   public class SubmitFeedbackExample {
       public static void main(String[] args) {
           KendraClient kendra = KendraClient.builder().build();
   
           SubmitFeedbackRequest submitFeedbackRequest = SubmitFeedbackRequest
               .builder()
               .indexId("anIndexId")
               .queryId("aQueryId")
               .clickFeedbackItems(
                   ClickFeedback
                   .builder()
                   .clickTime(Instant.now())
                   .resultId("aResultId")
                   .build())
               .relevanceFeedbackItems(
                   RelevanceFeedback
                   .builder()
                   .relevanceValue(RelevanceType.RELEVANT)
                   .resultId("aResultId")
                   .build())
               .build();
   
           SubmitFeedbackResponse response = kendra.submitFeedback(submitFeedbackRequest);
   
           System.out.println("Feedback is submitted");
       }
   }
   ```

------

1. Run the code\. After the feedback has been submitted, the code displays a message\.