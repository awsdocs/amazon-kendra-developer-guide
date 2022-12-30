--------

--------

# TableCell<a name="API_TableCell"></a>

Provides information about a table cell in a table excerpt\.

## Contents<a name="API_TableCell_Contents"></a>

 ** Header **   <a name="Kendra-Type-TableCell-Header"></a>
 `TRUE` means that the table cell should be treated as a header\.  
Type: Boolean  
Required: No

 ** Highlighted **   <a name="Kendra-Type-TableCell-Highlighted"></a>
 `TRUE` means that the table cell has a high enough confidence and is relevant to the query, so the value or content should be highlighted\.  
Type: Boolean  
Required: No

 ** TopAnswer **   <a name="Kendra-Type-TableCell-TopAnswer"></a>
 `TRUE` if the response of the table cell is the top answer\. This is the cell value or content with the highest confidence score or is the most relevant to the query\.  
Type: Boolean  
Required: No

 ** Value **   <a name="Kendra-Type-TableCell-Value"></a>
The actual value or content within a table cell\. A table cell could contain a date value of a year, or a string value of text, for example\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## See Also<a name="API_TableCell_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/TableCell) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/TableCell) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/TableCell) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/TableCell) 