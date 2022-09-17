--------

--------

# OnPremiseConfiguration<a name="API_OnPremiseConfiguration"></a>

Provides the configuration information to connect to GitHub Enterprise Server \(on premises\)\.

## Contents<a name="API_OnPremiseConfiguration_Contents"></a>

 ** HostUrl **   <a name="Kendra-Type-OnPremiseConfiguration-HostUrl"></a>
The GitHub host URL or API endpoint URL\. For example, *https://on\-prem\-host\-url/api/v3/*   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: Yes

 ** OrganizationName **   <a name="Kendra-Type-OnPremiseConfiguration-OrganizationName"></a>
The name of the organization of the GitHub Enterprise Server \(in\-premise\) account you want to connect to\. You can find your organization name by logging into GitHub desktop and selecting **Your organizations** under your profile picture dropdown\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 60\.  
Pattern: `^[A-Za-z0-9_.-]+$`   
Required: Yes

 ** SslCertificateS3Path **   <a name="Kendra-Type-OnPremiseConfiguration-SslCertificateS3Path"></a>
The path to the SSL certificate stored in an Amazon S3 bucket\. You use this to connect to GitHub if you require a secure SSL connection\.  
You can simply generate a self\-signed X509 certificate on any computer using OpenSSL\. For an example of using OpenSSL to create an X509 certificate, see [Create and sign an X509 certificate](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/configuring-https-ssl.html)\.  
Type: [S3Path](API_S3Path.md) object  
Required: Yes

## See Also<a name="API_OnPremiseConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/OnPremiseConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/OnPremiseConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/OnPremiseConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/OnPremiseConfiguration) 