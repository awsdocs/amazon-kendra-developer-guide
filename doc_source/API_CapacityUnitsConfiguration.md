--------

--------

# CapacityUnitsConfiguration<a name="API_CapacityUnitsConfiguration"></a>

Specifies capacity units configured for your enterprise edition index\. You can add and remove capacity units to tune an index to your requirements\.

## Contents<a name="API_CapacityUnitsConfiguration_Contents"></a>

 ** QueryCapacityUnits **   <a name="Kendra-Type-CapacityUnitsConfiguration-QueryCapacityUnits"></a>
The amount of extra query capacity for an index and [GetQuerySuggestions](https://docs.aws.amazon.com/kendra/latest/dg/API_GetQuerySuggestions.html) capacity\.  
A single extra capacity unit for an index provides 0\.1 queries per second or approximately 8,000 queries per day\.  
 `GetQuerySuggestions` capacity is five times the provisioned query capacity for an index, or the base capacity of 2\.5 calls per second, whichever is higher\. For example, the base capacity for an index is 0\.1 queries per second, and `GetQuerySuggestions` capacity has a base of 2\.5 calls per second\. If you add another 0\.1 queries per second to total 0\.2 queries per second for an index, the `GetQuerySuggestions` capacity is 2\.5 calls per second \(higher than five times 0\.2 queries per second\)\.  
Type: Integer  
Valid Range: Minimum value of 0\.  
Required: Yes

 ** StorageCapacityUnits **   <a name="Kendra-Type-CapacityUnitsConfiguration-StorageCapacityUnits"></a>
The amount of extra storage capacity for an index\. A single capacity unit provides 30 GB of storage space or 100,000 documents, whichever is reached first\.  
Type: Integer  
Valid Range: Minimum value of 0\.  
Required: Yes

## See Also<a name="API_CapacityUnitsConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CapacityUnitsConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CapacityUnitsConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CapacityUnitsConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CapacityUnitsConfiguration) 