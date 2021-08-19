--------

--------

# GroupOrderingIdSummary<a name="API_GroupOrderingIdSummary"></a>

Information on the processing of `PUT` and `DELETE` actions for mapping users to their groups\.

## Contents<a name="API_GroupOrderingIdSummary_Contents"></a>

 **FailureReason**   <a name="Kendra-Type-GroupOrderingIdSummary-FailureReason"></a>
The reason an action could not be processed\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

 **LastUpdatedAt**   <a name="Kendra-Type-GroupOrderingIdSummary-LastUpdatedAt"></a>
The last date\-time an action was updated\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Timestamp  
Required: No

 **OrderingId**   <a name="Kendra-Type-GroupOrderingIdSummary-OrderingId"></a>
The order in which actions should complete processing\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 32535158400000\.  
Required: No

 **ReceivedAt**   <a name="Kendra-Type-GroupOrderingIdSummary-ReceivedAt"></a>
The date\-time an action was received by Amazon Kendra\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Timestamp  
Required: No

 **Status**   <a name="Kendra-Type-GroupOrderingIdSummary-Status"></a>
The current processing status of actions for mapping users to their groups\. The status can be either `PROCESSING`, `SUCCEEDED`, `DELETING`, `DELETED`, or `FAILED`\.  
Type: String  
Valid Values:` FAILED | SUCCEEDED | PROCESSING | DELETING | DELETED`   
Required: No

## See Also<a name="API_GroupOrderingIdSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GroupOrderingIdSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GroupOrderingIdSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GroupOrderingIdSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GroupOrderingIdSummary) 