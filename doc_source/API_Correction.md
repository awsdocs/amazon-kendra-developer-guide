--------

--------

# Correction<a name="API_Correction"></a>

A corrected misspelled word in a query\.

## Contents<a name="API_Correction_Contents"></a>

 ** BeginOffset **   <a name="Kendra-Type-Correction-BeginOffset"></a>
The zero\-based location in the response string or text where the corrected word starts\.  
Type: Integer  
Required: No

 ** CorrectedTerm **   <a name="Kendra-Type-Correction-CorrectedTerm"></a>
The string or text of a corrected misspelled word in a query\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** EndOffset **   <a name="Kendra-Type-Correction-EndOffset"></a>
The zero\-based location in the response string or text where the corrected word ends\.  
Type: Integer  
Required: No

 ** Term **   <a name="Kendra-Type-Correction-Term"></a>
The string or text of a misspelled word in a query\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_Correction_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Correction) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Correction) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Correction) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Correction) 