--------

--------

# Key management<a name="key-management"></a>

Amazon Kendra encrypts the contents of your index using one of three types of keys\. You can choose one of the following:
+ An AWS owned customer master key \(CMK\)\. This is the default\.
+ An AWS managed CMK\. This key is created in your account and is managed and used on your behalf by Amazon Kendra\. 
+ A customer managed CMK\. You can create the key when you are creating an Amazon Kendra index or data source, or you can create the key using the AWS KMS console\. Select a symmetric encryption customer managed CMK, Amazon Kendra does not support asymmetric CMKs\. For more information, see [Using Symmetric and Asymmetric Keys](https://docs.aws.amazon.com/kms/latest/developerguide/symmetric-asymmetric.html) in the *AWS Key Management Service Developer Guide*\.