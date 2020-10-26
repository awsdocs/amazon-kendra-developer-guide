--------

--------

# Adding questions and answers directly to an index<a name="in-creating-faq"></a>

You can add questions and answers \(FAQs\) directly to your index using the console or the [CreateFaq](API_CreateFaq.md) operation\. You put the data for the FAQ in a file that you store in an Amazon Simple Storage Service \(Amazon S3\) bucket\. You can use comma\-separated values \(\.csv\) files or JSON files as input for your FAQ, as follows:
+ Basic \.csv – A \.csv file where each line contains a question, answer, and an optional URL with more information about the answer\.
+ Custom \.csv – A \.csv file that contains questions, answers, and a header that defines custom attributes that you can use to facet, display, or sort FAQ responses\. You can also define access control attributes to limit the FAQ response to certain users and groups\.
+ JSON – A JSON file that contains questions, answers, and, optionally, custom and access control attributes\. You can define attributes to facet, display\. and sort FAQ responses, or access control attributes that limit the FAQ response to certain users and groups\.

For example, the following is a basic \.csv file that provides answers to questions about the height of buildings in Seattle\.

```
What is the height of the Space Needle?, 605 feet, https://www.spaceneedle.com/
How tall is the Space Needle?, 605 feet, https://www.spaceneedle.com/
What is the height of the Smith Tower?, 484 feet, https://www.smithtower.com
How tall is the Smith Tower, 484 feet, https://www.smithtower.com/
```

When you use a custom \.csv or JSON file for input, you can declare custom attributes for your FAQ questions\. For example, you can create a custom attribute that assigns each FAQ question a department\. When the FAQ is returned in a response, you can use the department as a facet to narrow the search\.

A custom attribute must map to an index field\. You can use a built\-in field, or you can specify a custom index field\. When you use the console, you use the **Facet definition** page to create an index field\. When you use the API, you must first create an index field using the [UpdateIndex](API_UpdateIndex.md) operation\. 

The attribute type in the FAQ file must match the type of the associated index field\. For example, the built in `_authors` field is a `STRING_LIST` type field, so you must provide values for the `_authors` field as a string list in your FAQ file\. You can check the type of index fields using the **Facet definition** page in the console or by using the [DescribeIndex](API_DescribeIndex.md) operation\.

When you create an index field that maps to a custom attribute, you can mark it displayable, facetable, or sortable\. You can't make a custom attribute searchable\.

In addition to custom attributes that you provide, you can also use the following built\-in attributes in a custom \.csv or JSON file:
+ `_authors` \(String list\) – A list of authors of the answers to the FAQ question\.
+ `_category` \(String\) – A category that groups the answers to FAQ questions with other similar documents\.
+ `_created_at` \(ISO 8601\-encoded string\) – The date and time that the FAQ question was created\. The date and time should be ISO 8601\-encoded strings\. For example, `2020-09-15T22:40:46-08:00`\.
+ `_last_updated_at` \(ISO 8601\-encoded string\) – The date and time that the FAQ question was updated\. The date and time should be ISO 8601\-encoded strings\. For example, `2020-09-15T22:40:46-08:00`\.
+ `_source_uri` \(String\) – A URL for a document with more information about the FAQ answer\.
+ `_version` \(String\) – The version of the FAQ question\.
+ `_view_count` \(Long\) – The number of times that the FAQ question has been viewed in search results\.

## Basic \.csv file<a name="faq-basic-csv"></a>

Use a basic \.csv file when you want to use a simple structure for your FAQs\. In a basic \.csv file, each line has two or three fields: question, answer, and an optional source URI that points to a document with more information\.

The contents of the file should follow the [RFC 4180 Common Format and MIME Type for Comma\-Separated Values \(CSV\) Files](https://tools.ietf.org/html/rfc4180)\.

The following is a FAQ file in basic \.csv format\.

```
What is the height of the Space Needle?, 605 feet, https://www.spaceneedle.com/
How tall is the Space Needle?, 605 feet, https://www.spaceneedle.com/
What is the height of the Smith Tower?, 484 feet, https://www.smithtower.com
How tall is the Smith Tower, 484 feet, https://www.smithtower.com/
```

## Custom \.csv file<a name="faq-custom-csv"></a>

Use a custom \.csv file when you want to add custom attributes to your FAQ questions\. You use a header row in your \.csv file to define the additional attributes\.

The \.csv file must contain the following two required attributes:
+ `_question` – The frequently asked question
+ `_answer` – The answer to the frequently asked question

Your file can contain built\-in and custom attributes\. The following is an example of a custom \.csv file\.

```
_question,_answer,_authors,custom_string
How tall is the Space Needle?, 605 feet, Jorge Souza, custom string value
How tall is Smith Tower?, 484 feet, Richard Roe, custom string value
```

The contents of the custom attributes file should follow the [RFC 4180 Common Format and MIME Type for Comma\-Separated Values \(CSV\) Files](https://tools.ietf.org/html/rfc4180)\.

There are four types of custom attributes:
+ Date – ISO 8601\-encoded date and time values\. For example, `2020-08-25T22:40:46-08:00`\.
+ Long – Numbers, such as `1234`\.
+ String – String values\. If your string contains commas, enclose the value in double quotation marks \("\)\. For example, `"custom attribute, and more"`\.
+ String list – A list of string values\. List the values in a comma\-separated list that is enclosed in quotation marks\. For example, `"item1, item2, item3"`\. If the list contains only a single entry, you can omit the quotation marks\. For example, `item1`\.

A custom \.csv file can contain user context fields, which you can use to limit access to the FAQ to certain users and groups\. To filter on user context, the user must provide user and group information in the query\. Otherwise, all relevant FAQs are returned\. For more information, see [Filtering on user context](user-context-filter.md)\.

There are four user context filters for FAQs:
+ `_acl_user_allow` – Users in the allow list can see the FAQ in the query response\. The FAQ isn't returned to other users\.
+ `_acl_user_deny` – Users in the deny list can't see the FAQ in the query response\. The FAQ is returned to all other users when it is relevant to the query\.
+ `_acl_group_allow` – Users that are members of an allowed group can see the FAQ in the query response\. The FAQ isn't returned to users that are members of another group\.
+ `_acl_group_deny` – Users that are members of a denied group can't see the FAQ in the query response\. The FAQ is returned to other groups when it is relevant to the query\.

Provide the values for the allow and deny lists in comma\-separated lists enclosed in quotation marks\. For example, `"user1,user2,user3"`\. You can include a user or a group in either an allow list or a deny list, but not both\. If you include a user or group in both, you receive an error\.

The following is an example of a custom \.csv file with user context information\.

```
_question, _answer, _acl_user_allow, _acl_user_deny, _acl_group_allow, _acl_group_deny
How tall is the Space Needle?, 605 feet, user1, “user2,user3”, group1, “group2,group3,group4”
```

## JSON file<a name="faq-custom-json"></a>

You can use a JSON file to provide questions, answers, and attributes for your index\. You can add any of the built\-in attributes and custom attributes to the FAQ\. This is the schema schema for the JSON file\.

```
{
    "SchemaVersion": 1,
    "FaqDocuments": [
        {
            "Question": string,
            "Answer": string,
            "Attributes": {
                string: object
                additional attributes
            },
            "AccessControlList": [
               {
                   "Name": string,
                   "Type": enum( "GROUP" | "USER" ),
                   "Access": enum( "ALLOW" | "DENY" )
               },
               additional user context
            ]
        },
        additional FAQ documents
    ]
}
```

This example JSON file shows a two FAQ documents, one with just the required question and answer, and one with additional attributes and user context information\.

```
{
    "SchemaVersion": 1,
    "FaqDocuments": [
        {
            "Question": "How tall is the Space Needle?",
            "Answer": "605 feet"
        },
        {
            "Question": "How tall is Smith Tower?",
            "Answer": "484 feet",
            "Attributes": {
                "_source_uri": "https://www.smithtower.com",
                "_authors": ["Richard Roe", "Jorge Souza"],
                "_category": "Buildings",
                "_created_at": "2020-09-15T22:40:46Z",
                "_last_updated_at": "2020-09-15T22:40:46-08:00",
                "_version": "v1",
                "_view_count": 123
            },
            "AccessControlList": [
               {
                   "Name": "user@amazon.com",
                   "Type": "USER",
                   "Access": "ALLOW"
               },
               {
                   "Name": "Admin",
                   "Type": "GROUP",
                   "Access": "ALLOW"
               }
            ]
        }
    ]
}
```

There are four types of custom attributes for JSON files:
+ Date – A JSON string value with ISO 8601\-encoded date and time values\. For example, `"2020-08-25T22:40:46-08:00"`\.
+ Long – A JSON number value, such as `1234`\.
+ String – A JSON string value\. For example, `"custom attribute"`\.
+ String list – A JSON array of string values\. For example, `["item1,item2,item3"]`\.

In addition to built\-in and custom attributes, you can provide user context information for the FAQ in a JSON file\. You can provide user context information to limit access to the FAQ content based on users and groups\. You can include a user or a group in either an allow list or a deny list, but not both\. If you include a user or group in both, you receive an error\. To filter on user context, you must provide user and group information in the query\. Otherwise, all relevant FAQs are returned\. For more information, see [Filtering on user context](user-context-filter.md)\.

This JSON example adds user context to a FAQ\.

```
             "AccessControlList": [
                {
                    "Name": "group or user name",
                    "Type": "GROUP | USER",
                    "Access": "ALLOW | DENY"
                },
                additional user context
            ]
```

## Using your FAQ file<a name="using-faq-file"></a>

After you store your FAQ input file in an Amazon S3 bucket, you use the console or the `CreateFaq` operation to put the questions and answers into your index\. You must provide an IAM role that has access to the S3 bucket containing your source files\. You specify the role in the console or in the `RoleArn` parameter\. The following is an example of a program that adds a FAQ file to an index\.

------
#### [ Python ]

```
import boto3


kendra = boto3.client('kendra')

index_id = '${indexId}'
role_arn = 'arn:aws:iam::${accountId}:role/${roleName}'

faq_path = {
    'Bucket': '${bucketName}',
    'Key': 'SeattleBuildings.csv'
}

response = kendra.create_faq(
    S3Path =  faq_path,
    Name = 'SeattleBuildings',
    IndexId = index_id,
    RoleArn = role_arn
)

print(response)
```

------
#### [ Java ]

```
package com.amazonaws.kendra;

import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.CreateFaqRequest;
import software.amazon.awssdk.services.kendra.model.CreateFaqResponse;
import software.amazon.awssdk.services.kendra.model.S3Path;

public class AddFaqExample {
    public static void main(String[] args) {
        KendraClient kendra = KendraClient.builder().build();

        String indexId = "yourIndexId";
        String roleArn = "your role for accessing S3 files";

        CreateFaqRequest createFaqRequest = CreateFaqRequest
            .builder()
            .indexId(indexId)
            .name("SeattleBuildings")
            .roleArn(roleArn)
            .s3Path(
                S3Path
                    .builder()
                    .bucket("an-aws-kendra-test-bucket")
                    .key("SeattleBuildings.csv")
                    .build())
            .build();

        CreateFaqResponse response = kendra.createFaq(createFaqRequest);

        System.out.println(String.format("The result of creating FAQ: %s", response));

    }
}
```

------