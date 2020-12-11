--------

--------

# Adding a thesaurus to an index<a name="index-synonyms-adding-thesaurus-file"></a>

The following procedures show how to add a thesaurus file containing synonyms to an index\. It can take up to 30 minutes to see the effects of your updated thesaurus file\. For more information about the thesaurus file, see [Creating a thesaurus file](index-synonyms-creating-thesaurus-file.md)\. 

------
#### [ Console ]

**To add a thesaurus**

1. In the left navigation pane, under the index where you want to add a list of synonyms, your thesaurus, choose **Synonyms**\. 

1. On the **Synonym** page, choose **Add Thesaurus**\. 

1. In **Define thesaurus**, give your thesaurus a name and an optional description\.

1. In **Thesaurus settings**, provide the Amazon S3 path to your thesaurus file\. The file must be smaller than 5 MB\.

1. For **IAM Role**, select a role or select **Create a new role** and specify a role name to create a new role\. Amazon Kendra uses this role to access the Amazon S3 resource on your behalf\. The IAM role has the prefix "AmazonKendra\-"\. 

1. Choose **Save** to save the configuration and add the thesaurus\. Once the thesaurus is ingested, it is active and synonyms are highlighted in results\. It can take up to 30 minutes to see the effects of your thesaurus file\. 

------
#### [ CLI ]

To add a thesarus to an index with the AWS CLI, call `create-thesaurus`: 

```
aws kendra create-thesaurus \
--index-id index-id \
--name "thesaurus-name" \
--description "thesaurus-description" \
--source-s3-path "Bucket=bucket-name,Key=thesaurus/synonyms.txt" \
--role-arn role-arn
```

Call `list-thesauri` to see a list of thesauruses:

```
aws kendra list-thesauri \
--index-id index-id
```

To view details for a thesaurus, call `describe-thesaurus`:

```
aws kendra describe-thesaurus \
--index-id index-id \
--index-id thesaurus-id
```

It can take up to 30 minutes to see the effects of your thesaurus file\.

------