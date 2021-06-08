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
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Update a thesaurus")

thesaurus_name = "thesaurus-name"
thesaurus_description = "thesaurus-description"
thesaurus_role_arn = "role-arn"

thesaurus_id = "thesaurus-id"
index_id = "index-id"

s3_bucket_name = "bucket-name"
s3_key = "thesaurus-file"
source_s3_path= {
    'Bucket': s3_bucket_name,
    'Key': s3_key
}

try:
    kendra.update_thesaurus(
        Id = thesaurus_id,
        IndexId = index_id,
        Description = thesaurus_description,
        Name = thesaurus_name,
        RoleArn = thesaurus_role_arn,
        SourceS3Path = source_s3_path
    )
    
    print("Wait for Kendra to update the thesaurus.")

    while True:
        # Get thesaurus description
        thesaurus_description = kendra.describe_thesaurus(
            Id = thesaurus_id,
            IndexId = index_id
        )
        # If status is not UPDATING quit
        status = thesaurus_description["Status"]
        print("Updating thesaurus. Status: " + status)
        if status != "UPDATING":
            break
        time.sleep(60)

except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

```
package com.amazonaws.kendra;

import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.UpdateThesaurusRequest;
import software.amazon.awssdk.services.kendra.model.DescribeThesaurusRequest;
import software.amazon.awssdk.services.kendra.model.DescribeThesaurusResponse;
import software.amazon.awssdk.services.kendra.model.S3Path;
import software.amazon.awssdk.services.kendra.model.ThesaurusStatus;

public class UpdateThesaurusExample {

  public static void main(String[] args) throws InterruptedException {

    KendraClient kendra = KendraClient.builder().build();

    String thesaurusName = "thesaurus-name";
    String thesaurusDescription = "thesaurus-description";
    String thesaurusRoleArn = "role-arn";

    String s3BucketName = "bucket-name";
    String s3Key = "thesaurus-file";

    String thesaurusId = "thesaurus-id";
    String indexId = "index-id";

    UpdateThesaurusRequest updateThesaurusRequest = UpdateThesaurusRequest
        .builder()
        .id(thesaurusId)
        .indexId(indexId)
        .name(thesaurusName)
        .description(thesaurusDescription)
        .roleArn(thesaurusRoleArn)
        .sourceS3Path(S3Path.builder()
            .bucket(s3BucketName)
            .key(s3Key)
            .build())
        .build();
    kendra.updateThesaurus(updateThesaurusRequest);

    System.out.println(String.format("Waiting until the thesaurus with ID %s is updated.", thesaurusId));

    // a new source s3 path requires re-consumption by Kendra 
    // and so can take as long as a Create Thesaurus operation
    while (true) {
      DescribeThesaurusRequest describeThesaurusRequest = DescribeThesaurusRequest.builder()
          .id(thesaurusId)
          .indexId(indexId)
          .build();
      DescribeThesaurusResponse describeThesaurusResponse = kendra.describeThesaurus(describeThesaurusRequest);
      ThesaurusStatus status = describeThesaurusResponse.status();
      if (status != ThesaurusStatus.UPDATING) {
        break;
      }

      TimeUnit.SECONDS.sleep(60);
    }

    System.out.println("Thesaurus update is complete.");
  }
}
```

------