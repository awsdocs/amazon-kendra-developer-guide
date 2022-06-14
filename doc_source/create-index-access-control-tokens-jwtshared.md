--------

--------

# Using a JSON Web Token \(JWT\) with a shared secret<a name="create-index-access-control-tokens-jwtshared"></a>

The following examples show how to use a JSON Web Token \(JWT\) with a shared secret token for user access control when you are create an index\. 

------
#### [ Console ]

1. Choose **Create index** to start creating a new index\.

1. On the **Specify index details** page, give your index a name and a description\. 

1. For **IAM role**, select a role or select **Create a new role** to and specify a role name to create a new role\. The IAM role will have the prefix "AmazonKendra\-"\. 

1. Leave all of the other fields at their defaults\. Choose **Next**\.

1. In the **Configure user access control** page, under **Acces control settings**, choose **Yes** to use tokens for access control\. 

1. Under **Token configuration**, select **JWT with shared secret** as the **Token type**\. 

1. Under **Parameters for signing public key**, choose the **Type of secret**\. You can use an existing AWS Secrets Manager shared secret or create a new shared secret\. 

   To create a new shared secret, choose **New** and then follow these steps:

   1. Under **New AWS Secrets Manager secret**, specify a **Secret name**\. The prefix `AmazonKendra-` will added when you save the public key\. 

   1. Specify a **Key ID**\. The key id is a hint that indicates which key was used to secure the JSON web signature of the token\. 

   1. Choose the signing **Algorithm** for the token\. This is the cryptographic algorithm used to secure the ID token\. For more information on RSA, see [RSA Cryptography](https://tools.ietf.org/html/rfc3447)\. 

   1. Specify a **Shared secret**\. Select **Generate secret** to have a secret generated for you\. 

   1. *Optional*Specify when the shared secret is valid\. You can specify the date and time a secret is valid from, valid to, or both\. The secret will be valid in the interval specified\. 

   1. Select **Save secret** to save the new secret\. 

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

You can use JWT with a shared key token inside of a AWS Secrets Manager\. You need the Secrets Manager ARN, and your Amazon Kendra role must have access to `GetSecretValue` on the Secrets Manager resource\. If you are encrypting the Secrets Manager resource with AWS KMS, the role must also have access to the decrypt action\. 

To create an index with the AWS CLI using a JSON input file, first create a JSON file with your desired parameters: 

```
{
    "Name": "user-context",
    "Edition": "ENTERPRISE_EDITION",
    "RoleArn": "arn:aws:iam::account-id:role:/my-role",
    "UserTokenConfigurations": [
        {
            "JwtTokenTypeConfiguration": {
                "KeyLocation": "SECRET_MANAGER",
                "Issuer": "optional: specify the issuer url",
                "ClaimRegex": "optional: regex to validate claims in the token",
                "UserNameAttributeField": "optional: user",
                "GroupAttributeField": "optional: group",
                "SecretManagerArn": "arn:aws:secretsmanager:us-west-2:account id:secret:/my-user-context-secret
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

The secret must have the following format in AWS Secrets Manager:

```
{
  "keys": [
    {
      "kid": "key_id",
      "alg": "HS256|HS384|HS512",
      "kty": "OCT", 
      "use": "sig", //this value can be sig only for now
      "k": "secret",
      "nbf":"ISO1806 date format"
      "exp":"ISO1806 date format"
    }
  ]
}
```

For more information about JWT, see [jwt\.io](http://jwt.io)\. 

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
                "SecretManagerArn": "arn:aws:secretsmanager:us-west-2:account id:secret:/my-user-context-secret"
            }
        }
    ],
    UserContextPolicy='USER_TOKEN'
)
```

------