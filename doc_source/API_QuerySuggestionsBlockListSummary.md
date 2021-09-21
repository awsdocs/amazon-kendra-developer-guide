--------

--------

# QuerySuggestionsBlockListSummary<a name="API_QuerySuggestionsBlockListSummary"></a>

Summary information on a query suggestions block list\.

This includes information on the block list ID, block list name, when the block list was created, when the block list was last updated, and the count of block words/phrases in the block list\.

For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.

## Contents<a name="API_QuerySuggestionsBlockListSummary_Contents"></a>

<<<<<<< HEAD
 ** CreatedAt **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-CreatedAt"></a>
=======
 **CreatedAt**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-CreatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The date\-time summary information for a query suggestions block list was last created\.  
Type: Timestamp  
Required: No

<<<<<<< HEAD
 ** Id **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Id"></a>
=======
 **Id**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of a block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: No

<<<<<<< HEAD
 ** ItemCount **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-ItemCount"></a>
=======
 **ItemCount**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-ItemCount"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The number of items in the block list file\.  
Type: Integer  
Required: No

<<<<<<< HEAD
 ** Name **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Name"></a>
=======
 **Name**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name of the block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*`   
Required: No

<<<<<<< HEAD
 ** Status **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Status"></a>
=======
 **Status**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The status of the block list\.  
Type: String  
Valid Values:` ACTIVE | CREATING | DELETING | UPDATING | ACTIVE_BUT_UPDATE_FAILED | FAILED`   
Required: No

<<<<<<< HEAD
 ** UpdatedAt **   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-UpdatedAt"></a>
=======
 **UpdatedAt**   <a name="Kendra-Type-QuerySuggestionsBlockListSummary-UpdatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The date\-time the block list was last updated\.  
Type: Timestamp  
Required: No

## See Also<a name="API_QuerySuggestionsBlockListSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/QuerySuggestionsBlockListSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/QuerySuggestionsBlockListSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/QuerySuggestionsBlockListSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/QuerySuggestionsBlockListSummary) 