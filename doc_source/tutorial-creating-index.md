--------

--------

# Step 4: Creating an Amazon Kendra index and ingesting the metadata<a name="tutorial-creating-index"></a>

To implement your intelligent search solution, you create an Amazon Kendra index and ingest your S3 data and metadata into it\.

Before you add metadata to your Amazon Kendra index, you create custom index fields corresponding to custom document attributes, which in turn correspond to the Amazon Comprehend entity types\. Amazon Kendra uses the index fields and custom document attributes you create to search and filter your documents\.

For more information, see [Index](https://docs.aws.amazon.com/kendra/latest/dg/hiw-index.html) and [Creating custom document attributes](https://docs.aws.amazon.com/kendra/latest/dg/custom-attributes.html)\.

**Topics**
+ [Creating an Amazon Kendra index](#tutorial-creating-index-index-creation)
+ [Updating the IAM role for Amazon S3 access](#tutorial-creating-index-update-IAM)
+ [Creating Amazon Kendra custom search index fields](#tutorial-creating-index-custom-fields)
+ [Adding the Amazon S3 bucket as a data source for the index](#tutorial-creating-index-connecting-data)
+ [Syncing the Amazon Kendra index](#tutorial-creating-index-sync)

## Creating an Amazon Kendra index<a name="tutorial-creating-index-index-creation"></a>

To query your source documents, you create an Amazon Kendra index\.

If you are using the AWS CLI in this step, you create and attach an AWS IAM role and policy that allows Amazon Kendra to access your CloudWatch logs before creating an index\. For more information, see [Prerequisites](https://docs.aws.amazon.com/kendra/latest/dg/gs-prerequisites.html)\.

### To create an Amazon Kendra index \(Console\)<a name="create-index-console"></a>

1. Open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.
**Important**  
Ensure that you are in the same region in which you created your Amazon Comprehend entities analysis job and your Amazon S3 bucket\. If you are in another region, choose the AWS region where you created your Amazon S3 bucket from the **Region selector** in the top navigation bar\.

1. Choose **Create an index**\.

1. For **Index details** on the **Specify index details** page, do the following:

   1. For **Index name**, enter **kendra\-index**\.

   1. Keep the **Description** field blank\.

   1. For **IAM role**, choose **Create a new role**\. This role provides access to your Amazon S3 bucket\.

   1. For **Role name**, enter **kendra\-role**\. The IAM role will have the prefix `AmazonKendra-`\.

   1. Keep default settings for **Encryption** and **Tags** and choose **Next**\.

1. For **Access control settings** on the **Configure user access control** page, choose **No** and then choose **Next**\.

1. For **Provisioning editions** on the **Provisioning details** page, choose **Developer edition** and choose **Create**\.

### To create an Amazon Kendra index \(AWS CLI\)<a name="create-index-cli"></a>

1. To create and attach an IAM role for Amazon Kendra that recognizes it as a trusted entity, do the following:

   1. Save the following trust policy as a JSON file called `kendra-trust-policy.json` in a text editor on your local device\.

      ```
      {
          "Version": "2012-10-17",
          "Statement": {
              "Effect": "Allow",
              "Principal": {
                  "Service": "kendra.amazonaws.com"
              },
              "Action": "sts:AssumeRole"
          }
      }
      ```

   1. To create an IAM role called `kendra-role` and attach your saved `kendra-trust-policy.json` file to it, use the [create\-role](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-role.html) command:

------
#### [ Linux ]

      ```
      aws iam create-role \
                --role-name kendra-role \
                --assume-role-policy-document file://path/kendra-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-trust-policy.json` on your local device\.

------
#### [ macOS ]

      ```
      aws iam create-role \
                --role-name kendra-role \
                --assume-role-policy-document file://path/kendra-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-trust-policy.json` on your local device\.

------
#### [ Windows ]

      ```
      aws iam create-role ^
                --role-name kendra-role ^
                --assume-role-policy-document file://path/kendra-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-trust-policy.json` on your local device\.

------

   1. Copy the Amazon Resource Name \(ARN\) to your text editor and save it locally as `kendra-role-arn`\.
**Note**  
The ARN has a format similar to *arn:aws:iam::123456789012:role/kendra\-role*\. You need the ARN you saved as `kendra-role-arn` to run Amazon Kendra jobs\.

1. Before you create an index, you must provide your `kendra-role` the permission to write to CloudWatch Logs\. To do this, complete the following steps:

   1. Save the following trust policy as a JSON file called `kendra-cloudwatch-policy.json` in a text editor on your local device\.

      ```
      {
         "Version":"2012-10-17",
         "Statement":[
            {
               "Effect":"Allow",
               "Action":"cloudwatch:PutMetricData",
               "Resource":"*",
               "Condition":{
                  "StringEquals":{
                     "cloudwatch:namespace":"Kendra"
                  }
               }
            },
            {
               "Effect":"Allow",
               "Action":"logs:DescribeLogGroups",
               "Resource":"*"
            },
            {
               "Effect":"Allow",
               "Action":"logs:CreateLogGroup",
               "Resource":"arn:aws:logs:aws-region:aws-account-id:log-group:/aws/kendra/*"
            },
            {
               "Effect":"Allow",
               "Action":[
                  "logs:DescribeLogStreams",
                  "logs:CreateLogStream",
                  "logs:PutLogEvents"
               ],
               "Resource":"arn:aws:logs:aws-region:aws-account-id:log-group:/aws/kendra/*:log-stream:*"
            }
         ]
      }
      ```

      Replace *aws\-region* with your AWS region, and *aws\-account\-id* with your 12\-digit AWS account ID\.

   1. To create an IAM policy to access CloudWatch Logs, use the [create\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-policy.html) command:

------
#### [ Linux ]

      ```
      aws iam create-policy \
                --policy-name kendra-cloudwatch-policy \
                --policy-document file://path/kendra-cloudwatch-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-cloudwatch-policy.json` on your local device\.

------
#### [ macOS ]

      ```
      aws iam create-policy \
                --policy-name kendra-cloudwatch-policy \
                --policy-document file://path/kendra-cloudwatch-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-cloudwatch-policy.json` on your local device\.

------
#### [ Windows ]

      ```
      aws iam create-policy ^
                --policy-name kendra-cloudwatch-policy ^
                --policy-document file://path/kendra-cloudwatch-policy.json
      ```

      Where:
      + *path/* is the filepath to `kendra-cloudwatch-policy.json` on your local device\.

------

   1. Copy the Amazon Resource Name \(ARN\) to your text editor and save it locally as `kendra-cloudwatch-arn`\.
**Note**  
The ARN has a format similar to *arn:aws:iam::123456789012:role/kendra\-cloudwatch\-policy*\. You need the ARN you saved as `kendra-cloudwatch-arn` to attach the `kendra-cloudwatch-policy` to your IAM role\.

   1. To attach the `kendra-cloudwatch-policy` to your IAM role, use the [attach\-role\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/attach-role-policy.html) command:

------
#### [ Linux ]

      ```
      aws iam attach-role-policy \
                --policy-arn policy-arn \
                --role-name kendra-role
      ```

      Where:
      + *policy\-arn* is your saved `kendra-cloudwatch-arn`\.

------
#### [ macOS ]

      ```
      aws iam attach-role-policy \
                --policy-arn policy-arn \
                --role-name kendra-role
      ```

      Where:
      + *policy\-arn* is your saved `kendra-cloudwatch-arn`\.

------
#### [ Windows ]

      ```
      aws iam attach-role-policy ^
                --policy-arn policy-arn ^
                --role-name kendra-role
      ```

      Where:
      + *policy\-arn* is your saved `kendra-cloudwatch-arn`\.

------

1. To create an index, use the [create\-index](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/create-index.html) command:

------
#### [ Linux ]

   ```
   aws kendra create-index \
           --name kendra-index \
           --edition DEVELOPER_EDITION \
           --role-arn role-arn \
           --region aws-region
   ```

   Where:
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra create-index \
           --name kendra-index \
           --edition DEVELOPER_EDITION \
           --role-arn role-arn \
           --region aws-region
   ```

   Where:
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra create-index ^
           --name kendra-index ^
           --edition DEVELOPER_EDITION ^
           --role-arn role-arn ^
           --region aws-region
   ```

   Where:
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------

1. Copy the index `Id` and save it in a text editor as `kendra-index-id`\. The `Id` helps you track the status of your index creation\.

1. To track the progress of your index creation job, use the [describe\-index](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/describe-index.html) command:

------
#### [ Linux ]

   ```
   aws kendra describe-index \
           --id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra describe-index \
           --id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra describe-index ^
           --id kendra-index-id ^
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------

The index creation process on average takes 15 minutes, but can take longer\. When the status of the index is active, your index is ready to use\. While your index is being created, you can start the next step\.

If you are using the AWS CLI in this step, you create and attach an IAM policy to your Amazon Kendra IAM role that gives your index permissions to access your S3 bucket\.

## Updating the IAM role for Amazon S3 access<a name="tutorial-creating-index-update-IAM"></a>

While the index is being created, you update your Amazon Kendra IAM role to allow the index you created to read data from your Amazon S3 bucket\. For more information, see [IAM access roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.

### To update your IAM role \(Console\)<a name="update-role-console"></a>

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the left navigation pane, choose **Roles** and enter **kendra\-role** in the **Search** box above **Role name**\.

1. From the suggested options, click on `kendra-role`\.

1. In **Summary**, choose **Attach policies**\.

1. In **Attach permissions**, in the **Search** box, enter **S3** and select the checkbox next to the **AmazonS3ReadOnlyAccess** policy from the suggested options\.

1. Choose **Attach policy**\. On the **Summary** page, you will now see two policies attached to the IAM role\.

1. Return to the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/) and wait for the status of your index to change from **Creating** to **Active** before continuing to the next step\.

### To update your IAM role \(AWS CLI\)<a name="update-role-cli"></a>

1. Save the following text in a JSON file called `kendra-S3-access-policy.json` in a text editor on your local device\.

   ```
   {
      "Version":"2012-10-17",
      "Statement":[
         {
            "Action":[
               "s3:GetObject"
            ],
            "Resource":[
               "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
            ],
            "Effect":"Allow"
         },
         {
            "Action":[
               "s3:ListBucket"
            ],
            "Resource":[
               "arn:aws:s3:::DOC-EXAMPLE-BUCKET"
            ],
            "Effect":"Allow"
         },
         {
            "Effect":"Allow",
            "Action":[
               "kendra:BatchPutDocument",
               "kendra:BatchDeleteDocument",
               "kendra:ListDataSourceSyncJobs"
            ],
            "Resource":[
               "arn:aws:kendra:aws-region:aws-account-id:index/kendra-index-id"
            ]
         }
      ]
   }
   ```

   Replace *DOC\-EXAMPLE\-BUCKET* with your S3 bucket name, *aws\-region* with your AWS region, *aws\-account\-id* with your 12\-digit AWS account ID, and *kendra\-index\-id* with your saved `kendra-index-id`\.

1. To create an IAM policy to access your S3 bucket, use the [create\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-policy.html) command:

------
#### [ Linux ]

   ```
   aws iam create-policy \
             --policy-name kendra-S3-access-policy \
             --policy-document file://path/kendra-S3-access-policy.json
   ```

   Where:
   + *path/* is the filepath to `kendra-S3-access-policy.json` on your local device\.

------
#### [ macOS ]

   ```
   aws iam create-policy \
             --policy-name kendra-S3-access-policy \
             --policy-document file://path/kendra-S3-access-policy.json
   ```

   Where:
   + *path/* is the filepath to `kendra-S3-access-policy.json` on your local device\.

------
#### [ Windows ]

   ```
   aws iam create-policy ^
             --policy-name kendra-S3-access-policy ^
             --policy-document file://path/kendra-S3-access-policy.json
   ```

   Where:
   + *path/* is the filepath to `kendra-S3-access-policy.json` on your local device\.

------

1. Copy the Amazon Resource Name \(ARN\) to your text editor and save it locally as `kendra-S3-access-arn`\.
**Note**  
The ARN has a format similar to *arn:aws:iam::123456789012:role/kendra\-S3\-access\-policy*\. You need the ARN you saved as `kendra-S3-access-arn` to attach the `kendra-S3-access-policy` to your IAM role\.

1. To attach the `kendra-S3-access-policy` to your Amazon Kendra IAM role, use the [attach\-role\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/attach-role-policy.html) command:

------
#### [ Linux ]

   ```
   aws iam attach-role-policy \
             --policy-arn policy-arn \
             --role-name kendra-role
   ```

   Where:
   + *policy\-arn* is your saved `kendra-S3-access-arn`\.

------
#### [ macOS ]

   ```
   aws iam attach-role-policy \
             --policy-arn policy-arn \
             --role-name kendra-role
   ```

   Where:
   + *policy\-arn* is your saved `kendra-S3-access-arn`\.

------
#### [ Windows ]

   ```
   aws iam attach-role-policy ^
             --policy-arn policy-arn ^
             --role-name kendra-role
   ```

   Where:
   + *policy\-arn* is your saved `kendra-S3-access-arn`\.

------

## Creating Amazon Kendra custom search index fields<a name="tutorial-creating-index-custom-fields"></a>

To prepare Amazon Kendra to recognize your metadata as custom document attributes, you create custom fields corresponding to Amazon Comprehend entity types\. You input the following nine Amazon Comprehend entity types as custom fields:
+ COMMERCIAL\_ITEM
+ DATE
+ EVENT
+ LOCATION
+ ORGANIZATION
+ OTHER
+ PERSON
+ QUANTITY
+ TITLE

**Important**  
Misspelled entity types will not be recognized by the index\.

### To create custom fields for your Amazon Kendra index \(Console\)<a name="create-attributes-console"></a>

1. Open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.

1. From the **Indexes** list, click on `kendra-index`\.

1. From the left navigation panel, under **Data management**, choose **Facet definition**\.

1. From the **Index fields** menu, choose **Add field**\.

1. In the **Add index field** dialog box, do the following:

   1. In **Field name**, enter **COMMERCIAL\_ITEM**\.

   1. In **Data type**, choose **String list**\.

   1. In **Usage types**, select **Facetable**, **Searchable**, and **Displayable**, and then choose **Add**\.

   1. Repeat steps a to c for each Amazon Comprehend entity type: COMMERCIAL\_ITEM, DATE, EVENT, LOCATION, ORGANIZATION, OTHER, PERSON, QUANTITY, TITLE\.

The console displays successful field addition messages\. You can choose to close them before you proceed with the next step\.

### To create custom fields for your Amazon Kendra index \(AWS CLI\)<a name="create-attributes-cli"></a>

1. Save the following text as a JSON file called `custom-attributes.json` in a text editor on your local device\.

   ```
   [
      {
          "Name": "COMMERCIAL_ITEM",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "DATE",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "EVENT",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "LOCATION",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "ORGANIZATION",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "OTHER",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "PERSON",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "QUANTITY",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      },
      {
          "Name": "TITLE",
          "Type": "STRING_LIST_VALUE",
          "Search": {
              "Facetable": true,
              "Searchable": true,
              "Displayable": true
          }
      }
   ]
   ```

1. To create custom fields in your index, use the [update\-index](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/update-index.html) command:

------
#### [ Linux ]

   ```
   aws kendra update-index \
           --id kendra-index-id \
           --document-metadata-configuration-updates file://path/custom-attributes.json \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `custom-attributes.json` on your local device,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra update-index \
           --id kendra-index-id \
           --document-metadata-configuration-updates file://path/custom-attributes.json \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `custom-attributes.json` on your local device,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra update-index ^
           --id kendra-index-id ^
           --document-metadata-configuration-updates file://path/custom-attributes.json ^
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `custom-attributes.json` on your local device,
   + *aws\-region* is your AWS region\.

------

1. To verify that the custom attributes have been added to your index, use the [describe\-index](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/describe-index.html) command:

------
#### [ Linux ]

   ```
   aws kendra describe-index \
           --id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra describe-index \
           --id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra describe-index ^
           --id kendra-index-id ^
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------

## Adding the Amazon S3 bucket as a data source for the index<a name="tutorial-creating-index-connecting-data"></a>

Before you can sync your index, you must connect your S3 data source to it\.

### To connect an S3 bucket to your Amazon Kendra index \(Console\)<a name="connecting-s3-console"></a>

1. Open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.

1. From the **Indexes** list, click on `kendra-index`\.

1. From the left navigation menu, under **Data management**, choose **Data sources**\.

1. Under the **Select data source connector type** section, navigate to **Amazon S3**, and choose **Add connector**\.

1. In the **Specify data source details** page, do the following:

   1. Under **Name and description**, for **Data source name**, enter **S3\-data\-source**\.

   1. Keep the **Description** section blank\.

   1. Keep the default settings for **Tags**\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, in the **Sync scope** section, do the following:

   1. In **Enter the data source location**, choose **Browse S3**\.

   1. In **Choose resources**, select your S3 bucket and then choose **Choose**\.

   1. In **Metadata files prefix folder location**, choose **Browse S3**\.

   1. In **Choose resources**, click on the name of your bucket from the list of buckets\.

   1. For **Objects**, select the option box for `metadata` and choose **Choose**\. The location field should now say `metadata/`\.

   1. Keep the default settings for **Access control list configuration file location**, **Select decryption key**, and **Additional configuration**\.

1. For **IAM role**, on the **Configure sync settings** page, choose `kendra-role`\.

1. On the **Configure sync settings** page, under **Sync run schedule**, for **Frequency**, choose **Run on demand** and then choose **Next**\.

1. On the **Review and create** page, review your choices for the data source details and choose **Add data source**\.

### To connect an S3 bucket to your Amazon Kendra index \(AWS CLI\)<a name="connecting-s3-cli"></a>

1. Save the following text as a JSON file called `S3-data-connector.json` in a text editor on your local device\.

   ```
   {
      "S3Configuration":{
         "BucketName":"DOC-EXAMPLE-BUCKET",
         "DocumentsMetadataConfiguration":{
            "S3Prefix":"metadata"
         }
      }
   }
   ```

   Replace *DOC\-EXAMPLE\-BUCKET* with the name of your S3 bucket\.

1. To connect your S3 bucket to your index, use the [create\-data\-source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/create-data-source.html) command:

------
#### [ Linux ]

   ```
   aws kendra create-data-source \
           --index-id kendra-index-id \
           --name S3-data-source \
           --type S3 \
           --configuration file://path/S3-data-connector.json \
           --role-arn role-arn \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `S3-data-connector.json` on your local device,
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra create-data-source \
           --index-id kendra-index-id \
           --name S3-data-source \
           --type S3 \
           --configuration file://path/S3-data-connector.json \
           --role-arn role-arn \
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `S3-data-connector.json` on your local device,
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra create-data-source ^
           --index-id kendra-index-id ^
           --name S3-data-source ^
           --type S3 ^
           --configuration file://path/S3-data-connector.json ^
           --role-arn role-arn ^
           --region aws-region
   ```

   Where:
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *path/* is the filepath to `S3-data-connector.json` on your local device,
   + *role\-arn* is your saved `kendra-role-arn`,
   + *aws\-region* is your AWS region\.

------

1. Copy the connector `Id` and save it in a text editor as `S3-connector-id`\. The `Id` helps you track the status of the data\-connection process\.

1. To ensure that your S3 data source was connected successfully, use the [describe\-data\-source](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/describe-data-source.html) command:

------
#### [ Linux ]

   ```
   aws kendra describe-data-source \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra describe-data-source \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra describe-data-source ^
           --id S3-connector-id ^
           --index-id kendra-index-id ^
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------

At the end of this step, your Amazon S3 data source is connected to the index\.

## Syncing the Amazon Kendra index<a name="tutorial-creating-index-sync"></a>

With the Amazon S3 data source added, you now sync your Amazon Kendra index to it\.

### To sync your Amazon Kendra index \(Console\)<a name="syncing-index-console"></a>

1. Open the Amazon Kendra console at [https://console\.aws\.amazon\.com/kendra/](https://console.aws.amazon.com/kendra/)\.

1. From the **Indexes** list, click on `kendra-index`\.

1. From the left navigation menu, choose **Data sources**\.

1. From **Data sources**, select `S3-data-source`\.

1. From the top navigation bar, choose **Sync now**\.

### To sync your Amazon Kendra index \(AWS CLI\)<a name="syncing-index-cli"></a>

1. To sync your index, use the [start\-data\-source\-sync\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/start-data-source-sync-job.html) command:

------
#### [ Linux ]

   ```
   aws kendra start-data-source-sync-job \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra start-data-source-sync-job \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra start-data-source-sync-job ^
           --id S3-connector-id ^
           --index-id kendra-index-id ^
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------

1. To check the status of the index sync, use the [list\-data\-source\-sync\-jobs](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kendra/list-data-source-sync-jobs.html) command:

------
#### [ Linux ]

   ```
   aws kendra list-data-source-sync-jobs \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws kendra list-data-source-sync-jobs \
           --id S3-connector-id \
           --index-id kendra-index-id \
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws kendra list-data-source-sync-jobs ^
           --id S3-connector-id ^
           --index-id kendra-index-id ^
           --region aws-region
   ```

   Where:
   + *S3\-connector\-id* is your saved `S3-connector-id`,
   + *kendra\-index\-id* is your saved `kendra-index-id`,
   + *aws\-region* is your AWS region\.

------

At the end of this step, you have created a searchable and filterable Amazon Kendra index for your dataset\.