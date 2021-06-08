--------

--------

# AWS managed policies for Amazon Kendra<a name="security-iam-awsmanpol"></a>







To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.









## AWS managed policy: AmazonKendraReadOnly<a name="security-iam-awsmanpol-AmazonKendraReadOnly"></a>

Grants read\-only access to Amazon Kendra resources\. This policy includes the following permissions\.
+ `kendra` – Allows users to perform actions that return either a list of items or details about an item\. This includes API operations that start with Describe, List, Query, or GetQuerySuggestions\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "kendra:Describe*",
                "kendra:List*",
                "kendra:Query",
                "kendra:GetQuerySuggestions"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AmazonKendraFullAccess<a name="security-iam-awsmanpol-AmazonKendraFullAccess"></a>

Grants full access to create, read, update, delete, tag, and run all Amazon Kendra resources\. This policy includes the following permissions\.
+ `kendra` – Allows principals read and write access to all actions in the Amazon Kendra\.
+ `s3` – Allows principals get Amazon S3 bucket locations and list buckets\.
+ `iam` – Allows principals to pass and list roles\.
+ `kms` – Allows principals to describe and list AWS KMS keys and aliases\.
+ `secretsmanager` – Allows principals to create, describe, and list secrets\.
+ `ec2` – Allows principals to describe security groups, VCPs \(Virtual Private Cloud\), and subnets\.
+ `cloudwatch` – Allows principals to view Cloud Watch metrics\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "kendra.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:ListRoles"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeVpcs",
                "ec2:DescribeSubnets"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kms:ListKeys",
                "kms:ListAliases",
                "kms:DescribeKey"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "secretsmanager:ListSecrets"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:GetMetricData"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "secretsmanager:CreateSecret",
                "secretsmanager:DescribeSecret"
            ],
            "Resource": "arn:aws:secretsmanager:*:*:secret:AmazonKendra-*"
        },
        {
            "Effect": "Allow",
            "Action": "kendra:*",
            "Resource": "*"
        }
    ]
}
```





## Amazon Kendra updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for Amazon Kendra since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Amazon Kendra Document history page\.




| Change | Description | Date | 
| --- | --- | --- | 
|  [AmazonKendraReadOnly – Add permission to support GetQuerySuggestions operation](https://docs.aws.amazon.com/kendra/latest/dg/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonKendraReadOnly)  |  Amazon Kendra added a new action `GetQuerySuggestions` that allows access to get query suggestions for popular search queries, helping guide your users' search\. When users type their search query, the suggested query helps autocomplete their search\. This action is associated with the `GetQuerySuggestions` API operation\.  | May 27, 2021 | 
|  Amazon Kendra started tracking changes  |  Amazon Kendra started tracking changes for its AWS managed policies\.  | May 27, 2021 | 