--------

--------

# GroupOrderingIdSummary<a name="API_GroupOrderingIdSummary"></a>

Information on the processing of `PUT` and `DELETE` actions for mapping users to their groups\.

## Contents<a name="API_GroupOrderingIdSummary_Contents"></a>

<<<<<<< HEAD
 ** FailureReason **   <a name="Kendra-Type-GroupOrderingIdSummary-FailureReason"></a>
=======
 **FailureReason**   <a name="Kendra-Type-GroupOrderingIdSummary-FailureReason"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The reason an action could not be processed\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** LastUpdatedAt **   <a name="Kendra-Type-GroupOrderingIdSummary-LastUpdatedAt"></a>
=======
 **LastUpdatedAt**   <a name="Kendra-Type-GroupOrderingIdSummary-LastUpdatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The last date\-time an action was updated\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** OrderingId **   <a name="Kendra-Type-GroupOrderingIdSummary-OrderingId"></a>
=======
 **OrderingId**   <a name="Kendra-Type-GroupOrderingIdSummary-OrderingId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The order in which actions should complete processing\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 32535158400000\.  
Required: No

<<<<<<< HEAD
 ** ReceivedAt **   <a name="Kendra-Type-GroupOrderingIdSummary-ReceivedAt"></a>
=======
 **ReceivedAt**   <a name="Kendra-Type-GroupOrderingIdSummary-ReceivedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The date\-time an action was received by Amazon Kendra\. An action can be a `PUT` or `DELETE` action for mapping users to their groups\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** Status **   <a name="Kendra-Type-GroupOrderingIdSummary-Status"></a>
=======
 **Status**   <a name="Kendra-Type-GroupOrderingIdSummary-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
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