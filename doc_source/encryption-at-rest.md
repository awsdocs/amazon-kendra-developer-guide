--------

--------

# Encryption at rest<a name="encryption-at-rest"></a>

Amazon Kendra encrypts your data at rest with your choice of an encryption key\. You can choose one of the following:
+ An AWS\-owned AWS KMS key\. If you don't specify an encryption key your data is encrypted with this key by default\.
+ An AWS\-managed KMS key in your account\. This key is created, managed, and used on your behalf by Amazon Kendra\. The key name is `aws/kendra`\.
+ A customer\-managed key\. You can provide the ARN of an encryption key that you created in your account\. When you use a customer\-managed KMS key, you must give the key a key policy that allows Amazon Kendra to use the key\. Select a symmetric encryption customer\-managed KMS key, Amazon Kendra does not support asymmetric KMS keys\. For more information, see [Key management](key-management.md)\.