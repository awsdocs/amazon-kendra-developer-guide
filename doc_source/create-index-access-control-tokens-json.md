--------

--------

# Using JSON<a name="create-index-access-control-tokens-json"></a>

The following examples show how to use a JWT with certificate token for user access control when you create an index\. 

**Warning**  
The JSON token is a non\-validated payload\. This should only be used when requests to Amazon Kendra come from a trusted server and never from a browser\. 

------
#### [ Console ]

1. Choose **Create index** to start creating a new index\.

1. On the **Specify index details** page, give your index a name and a description\. 

1. For **IAM role**, select a role or select **Create a new role** to and specify a role name to create a new role\. The IAM role will have the prefix "AmazonKendra\-"\. 

1. Leave all of the other fields at their defaults\. Choose **Next**\.

1. In the **Configure user access control** page, under **Access control settings**, choose **Yes** to use tokens for access control\. 

1. Under **Token configuration**, select **JSON** as the **Token type**\. 

1. Specify a **User name** to use in the ACL check\.

1. Specify one or more **Groups** to use in the ACL check\.

1. Choose**Next**\. 

1. In the **Provisioning details** page, choose **Developer edition**\.

1. Choose **Create** to create your index\.

1. Wait for your index to be created\. Amazon Kendra provisions the hardware for your index\. This operation can take some time\.

------
#### [ CLI ]

To create an index with the AWS CLI using a JSON input file, first create a JSON file with your desired parameters:

```
{
    "Name": "user-context",
    "Edition": "ENTERPRISE_EDITION",
    "RoleArn": "arn:aws:iam::account-id:role:/my-role",
    "UserTokenConfigurations": [
        {
            "JsonTokenTypeConfiguration": {
                "UserNameAttributeField": "user",
                "GroupAttributeField": "group"
            }
        }
    ],
    "UserContextPolicy": "USER_TOKEN"
}
```

Next, call `create-index` using the input file\. For example, if the name of your JSON file is `create-index-openid.json`, you can use the following: 

```
aws kendra create-index --cli-input-json file://create-index-openid.json
```

If you are not using Open ID for AWS IAM Identity Center \(successor to AWS Single Sign\-On\), you can send us the token in JSON format\. If you do, you must specify which field in the JSON token contains the user name and which field contains the groups\. The group field values must be a JSON string array\. For example, if you are using SAML, your token would be similar to the following:

```
{
     "username" : "saligram", 
     "groups": [
        "aws-kendra-dev", 
        "aws-kendra-engg"
     ]
}
```

The `TokenConfiguration` would specify the user name and group field names:

```
{
    "UserNameAttributeField":"username",
    "GroupAttributeField":"groups"
}
```

------
#### [ Python ]

```
response = kendra.create_index(
    Name='user-context',
    Edition='ENTERPRISE_EDITION',
    RoleArn='arn:aws:iam::account-id:role:/my-role',
    UserTokenConfigurationList=[
        {
            "JwtTokenTypeConfiguration": {
                "UserNameAttributeField": "user",
                "GroupAttributeField": "group",
            }
        }
    ],
    UserContextPolicy='USER_TOKEN'
)
```

------