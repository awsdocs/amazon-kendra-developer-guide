--------

--------

# Deleting a thesaurus<a name="index-synonyms-delete"></a>

The following procedures show how to delete a thesaurus\. 

------
#### [ Console ]

1. In the left navigation pane, under the index you want to modify, choose **Synonyms**\. 

1. On the **Synonym** page, select the thesaurus you want to delete\. 

1. On the **Thesaurus detail** page, choose **Delete** and then confirm to delete\. 

------
#### [ CLI ]

To delete a thesarus to an index with the AWS CLI, call `delete-thesaurus`: 

```
aws kendra create-thesaurus \
--index-id index-id \
--id thesaurus-id
```

------