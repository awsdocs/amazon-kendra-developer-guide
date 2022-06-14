--------

--------

# Using OpenID<a name="create-index-access-control-tokens-openid"></a>

To configure an Amazon Kendra index to use an OpenID token for access control, you need the JWKS \(JSON Web Key Set\) URL from the OpenID provider\. In most cases the JWKS URL is in the following format \(if they're following openId discovery\) `https://domain-name/.well_known/jwks.json`\. 

The following examples show how to use an OpenID token for user access control when you are create an index\. 

------
#### [ Console ]

1. Choose **Create index** to start creating a new index\.

1. On the **Specify index details** page, give your index a name and a description\. 

1. For **IAM role**, select a role or select **Create a new role** to and specify a role name to create a new role\. The IAM role will have the prefix "AmazonKendra\-"\. 

1. Leave all of the other fields at their defaults\. Choose **Next**\.

1. In the **Configure user access control** page, under **Access control settings**, choose **Yes** to use tokens for access control\. 

1. Under **Token configuration**, select **OpenID** as the **Token type**\. 

1. Specify a **Signing key URL**\. The URL should point to a set of JSON web keys\. 

1. *Optional* Under **Advanced configuration**: 

   1. Specify a **Username** to use in the ACL check\. 

   1. Specify one or more **Groups** to use in the ACL check\. 

   1. Specify the **Issuer** that will validate the token issuer\. 

   1. Specify the **Client Id\(s\)**\. You must specify a regular expression that match the audience in the JWT\.

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
            "JwtTokenTypeConfiguration": {
                "KeyLocation": "URL",
                "Issuer": "optional: specify the issuer url",
                "ClaimRegex": "optional: regex to validate claims in the token",
                "UserNameAttributeField": "optional: user",
                "GroupAttributeField": "optional: group",
                "URL": "https://example.com/.well-known/jwks.json"
            }
        }
    ],
    "UserContextPolicy": "USER_TOKEN"
}
```

You can override the default user and group field names\. The default value for `UserNameAttributeField` is "user"\. The default value for `GroupAttributeField` is "groups"\. 

Next, call `create-index` using the input file\. For example, if the name of your JSON file is `create-index-openid.json`, you can use the following: 

```
aws kendra create-index --cli-input-json file://create-index-openid.json
```

------
#### [ Python ]

```
response = kendra.create_index(
    Name='user-context',
    Edition='ENTERPRISE_EDITION',
    RoleArn='arn:aws:iam::account-id:role:/my-role',
    UserTokenConfigurations=[
        {
            "JwtTokenTypeConfiguration": {
                "KeyLocation": "URL",
                "Issuer": "optional: specify the issuer url",
                "ClaimRegex": "optional: regex to validate claims in the token",
                "UserNameAttributeField": "optional: user",
                "GroupAttributeField": "optional: group",
                "URL": "https://example.com/.well-known/jwks.json"
            }
        }
    ],
    UserContextPolicy='USER_TOKEN'
)
```

------