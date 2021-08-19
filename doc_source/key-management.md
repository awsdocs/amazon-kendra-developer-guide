--------

--------

# Key management<a name="key-management"></a>

Amazon Kendra encrypts the contents of your index using one of three types of keys\. You can choose one of the following:
+ An AWS owned customer master key \(CMK\)\. This is the default\.
+ An AWS managed CMK\. This key is created in your account and is managed and used on your behalf by Amazon Kendra\. 
+ A customer managed CMK\. You can create the key when you are creating an Amazon Kendra index or data source, or you can create the key using the AWS KMS console\. Select a symmetric customer managed CMK, Amazon Kendra does not support asymmetric CMKs\. For more information, see [Using Symmetric and Asymmetric Keys](https://docs.aws.amazon.com/kms/latest/developerguide/symmetric-asymmetric.html) in the *AWS Key Management Service Developer Guide*\.

When you create a key using the AWS KMS console, you must give the key the following policy that enables Amazon Kendra to use the key\. If you create a key with the Amazon Kendra console, the policy is applied to the key for you\. For more information, see [Using Key Policies in AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html) in the *AWS Key Management Service Developer Guide*\.

You should specify only the CMKs that Amazon Kendra needs to use in the Resource element to ensure permissions or actions are limited only to the specified CMKs\.

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Principal": {
        "Service": "kendra.amazonaws.com"
    },
    "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:ReEncrypt*",
        "kms:GenerateDataKey*",
        "kms:DescribeKey",
        "kms:CreateGrant",
        "kms:RetireGrant"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"]
  }
}
```