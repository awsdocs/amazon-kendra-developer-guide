--------

--------

# Principal<a name="API_Principal"></a>

Provides user and group information for document access filtering\.

## Contents<a name="API_Principal_Contents"></a>

<<<<<<< HEAD
 ** Access **   <a name="Kendra-Type-Principal-Access"></a>
=======
 **Access**   <a name="Kendra-Type-Principal-Access"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Whether to allow or deny access to the principal\.  
Type: String  
Valid Values:` ALLOW | DENY`   
Required: Yes

<<<<<<< HEAD
 ** DataSourceId **   <a name="Kendra-Type-Principal-DataSourceId"></a>
=======
 **DataSourceId**   <a name="Kendra-Type-Principal-DataSourceId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the data source the principal should access documents from\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

<<<<<<< HEAD
 ** Name **   <a name="Kendra-Type-Principal-Name"></a>
=======
 **Name**   <a name="Kendra-Type-Principal-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name of the user or group\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^\P{C}*$`   
Required: Yes

<<<<<<< HEAD
 ** Type **   <a name="Kendra-Type-Principal-Type"></a>
=======
 **Type**   <a name="Kendra-Type-Principal-Type"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The type of principal\.  
Type: String  
Valid Values:` USER | GROUP`   
Required: Yes

## See Also<a name="API_Principal_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/Principal) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/Principal) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/Principal) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/Principal) 