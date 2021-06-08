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
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError

kendra = boto3.client("kendra")

print("Delete a thesaurus")

thesaurus_id = "thesaurus-id"
index_id = "index-id"

try:
    kendra.delete_thesaurus(
        Id = thesaurus_id,
        IndexId = index_id
    )

except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

```
package com.amazonaws.kendra;

import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.DeleteThesaurusRequest;

public class DeleteThesaurusExample {

  public static void main(String[] args) throws InterruptedException {

    KendraClient kendra = KendraClient.builder().build();

    String thesaurusId = "thesaurus-id";
    String indexId = "index-id";

    DeleteThesaurusRequest updateThesaurusRequest = DeleteThesaurusRequest
        .builder()
        .id(thesaurusId)
        .indexId(indexId)
        .build();
    kendra.deleteThesaurus(updateThesaurusRequest);
  }
}
```

------