--------

--------

# Updating a thesaurus<a name="index-synonyms-update"></a>

You can change the configuration of a thesaurus after it is created\. You can change details like thesaurus name and IAM information\. You can also change the location of the thesaurus file Amazon S3 path\. If you change the path to the thesaurus file, Amazon Kendra replaces the existing thesaurus with the thesaurus specified in the updated path\. 

It can take up to 30 minutes to see the effects of your updated thesaurus file\. 

**Note**  
If there are validation or syntax errors in the thesaurus file, the previously uploaded thesaurus file is retained\. 

The following procedures show how to modify thesaurus details\. 

------
#### [ Console ]

**To modify thesaurus details**

1. In the left navigation pane, under the index you want to modify, choose **Synonyms**\. 

1. On the **Synonym** page, select the thesaurus you want to modify and then choose **Edit**\. 

1. On the **Update thesaurus** page, update the thesaurus details\. 

1. \(Optional\) Choose **Change the thesaurus file path** and then specify an Amazon S3 path to the new thesaurus file\. Your existing thesaurus file is replaced by the file you specify\. If you do not change the path, Amazon Kendra reloads the thesaurus from the existing path\. 

   If you select **Keep the current thesaurus file**, Amazon Kendra does not reload the thesaurus file\. 

1. Choose **Save** to save the configuration\. 

You can also reload the thesaurus from the existing thesaurus path\. 

**To reload a thesaurus from an existing path**

1. In the left navigation pane, under the index you want to modify, choose **Synonyms**\. 

1. On the **Synonym** page, select the thesaurus you want to reload and then choose **Reload**\. 

1. On the **Reload thesaurus file** page, confirm you want to reload the thesaurus file\. 

------
#### [ CLI ]

To update a thesaurus, call `update-thesaurus`: 

```
aws kendra update-thesaurus \
--index-id index-id \
--name "thesaurus-name" \
--description "thesaurus-description" \
--source-s3-path "Bucket=bucket-name,Key=thesaurus/synonyms.txt" \
--role-arn role-arn
```

------