--------

--------

# Step 2: Running an entities analysis job on Amazon Comprehend<a name="tutorial-entities-analysis"></a>

After storing the sample dataset in your S3 bucket, you run an Amazon Comprehend entities analysis job to extract entities from your documents\. These entities will form Amazon Kendra custom attributes and help you filter search results on your index\. For more information, see [Detect Entities](https://docs.aws.amazon.com/comprehend/latest/dg/how-entities.html)\.

**Topics**
+ [Running an Amazon Comprehend entities analysis job](#tutorial-entities-analysis-job)

## Running an Amazon Comprehend entities analysis job<a name="tutorial-entities-analysis-job"></a>

To extract entities from your dataset, you run an Amazon Comprehend entities analysis job\.

If you are using the AWS CLI in this step, you first create and attach an AWS IAM role and policy for Amazon Comprehend and then run an entities analysis job\. To run an entities analysis job on your sample data, Amazon Comprehend needs:
+ an AWS Identity and Access Management \(IAM\) role that recognizes it as a trusted entity
+ an AWS IAM policy attached to the IAM role that gives it permissions to access your S3 bucket

For more information, see [Overview of managing access permissions to Amazon Comprehend resources](https://docs.aws.amazon.com/comprehend/latest/dg/access-control-overview.html) and [Using Identity\-Based Policies \(IAM Policies\) for Amazon Comprehend](https://docs.aws.amazon.com/comprehend/latest/dg/access-control-managing-permissions.html)\.

### To run an Amazon Comprehend entities analysis job \(Console\)<a name="entities-analysis-console"></a>

1. Open the Amazon Comprehend console at [https://console\.aws\.amazon\.com/comprehend/](https://console.aws.amazon.com/comprehend/)\.
**Important**  
Ensure that you are in the same region in which you created your Amazon S3 bucket\. If you are in another region, choose the AWS region where you created your S3 bucket from the **Region selector** in the top navigation bar\.

1. Choose **Launch Amazon Comprehend**\.

1.  In the left navigation pane, choose **Analysis jobs**\.

1.  Choose **Create job**\.

1. In the **Job settings** section, do the following:

   1.  For **Name**, enter **data\-entities\-analysis**\.

   1. For **Analysis type**, choose **Entities**\.

   1. For **Language**, choose **English**\.

   1. Keep **Job encryption** turned off\.

1. In the **Input data** section, do the following:

   1. For **Data source**, choose **My documents**\.

   1. For **S3 location**, choose **Browse S3**\.

   1. For **Choose resources**, click on the name of your bucket from the list of buckets\.

   1. For **Objects**, select the option button for `data` and choose **Choose**\.

   1. For **Input format**, choose **One document per file**\.

1. In the **Output data** section, do the following:

   1. For **S3 location**, choose **Browse S3** and then select the option box for your bucket from the list of buckets and choose **Choose**\.

   1. Keep **Encryption** turned off\.

1. In the **Access permissions** section, do the following:

   1. For **IAM role**, choose **Create an IAM role**\.

   1. For **Permissions to access**, choose **Input and Output S3 buckets**\.

   1. For **Name suffix**, enter **comprehend\-role**\. This role provides access to your Amazon S3 bucket\.

1. Keep the default **VPC settings**\.

1. Choose **Create job**\.

### To run an Amazon Comprehend entities analysis job \(AWS CLI\)<a name="entities-analysis-cli"></a>

1. To create and attach an IAM role for Amazon Comprehend that recognizes it as a trusted entity, do the following:

   1. Save the following trust policy as a JSON file called `comprehend-trust-policy.json` in a text editor on your local device\.

      ```
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Principal": {
              "Service": "comprehend.amazonaws.com"
            },
            "Action": "sts:AssumeRole"
          }
        ]
      }
      ```

   1. To create an IAM role called `comprehend-role` and attach your saved `comprehend-trust-policy.json` file to it, use the [create\-role](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-role.html) command:

------
#### [ Linux ]

      ```
      aws iam create-role \
                --role-name comprehend-role \
                --assume-role-policy-document file://path/comprehend-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-trust-policy.json` on your local device\.

------
#### [ macOS ]

      ```
      aws iam create-role \
                --role-name comprehend-role \
                --assume-role-policy-document file://path/comprehend-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-trust-policy.json` on your local device\.

------
#### [ Windows ]

      ```
      aws iam create-role ^
                --role-name comprehend-role ^
                --assume-role-policy-document file://path/comprehend-trust-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-trust-policy.json` on your local device\.

------

   1. Copy the Amazon Resource Name \(ARN\) to your text editor and save it locally as `comprehend-role-arn`\.
**Note**  
The ARN has a format similar to *arn:aws:iam::123456789012:role/comprehend\-role*\. You need the ARN you saved as `comprehend-role-arn` to run the Amazon Comprehend analysis job\.

1. To create and attach an IAM policy to your IAM role that grants it permissions to access your S3 bucket, do the following:

   1. Save the following trust policy as a JSON file called `comprehend-S3-access-policy.json` in a text editor on your local device\.

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Action": [
                      "s3:GetObject"
                  ],
                  "Resource": [
                      "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
                  ],
                  "Effect": "Allow"
              },
              {
                  "Action": [
                      "s3:ListBucket"
                  ],
                  "Resource": [
                      "arn:aws:s3:::DOC-EXAMPLE-BUCKET"
                  ],
                  "Effect": "Allow"
              },
              {
                  "Action": [
                      "s3:PutObject"
                  ],
                  "Resource": [
                      "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
                  ],
                  "Effect": "Allow"
              }
          ]
      }
      ```

   1. To create an IAM policy called `comprehend-S3-access-policy` to access your S3 bucket, use the [create\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/create-policy.html) command:

------
#### [ Linux ]

      ```
      aws iam create-policy \
                --policy-name comprehend-S3-access-policy \
                --policy-document file://path/comprehend-S3-access-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-S3-access-policy.json` on your local device\.

------
#### [ macOS ]

      ```
      aws iam create-policy \
                --policy-name comprehend-S3-access-policy \
                --policy-document file://path/comprehend-S3-access-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-S3-access-policy.json` on your local device\.

------
#### [ Windows ]

      ```
      aws iam create-policy ^
                --policy-name comprehend-S3-access-policy ^
                --policy-document file://path/comprehend-S3-access-policy.json
      ```

      Where:
      + *path/* is the filepath to `comprehend-S3-access-policy.json` on your local device\.

------

   1. Copy the Amazon Resource Name \(ARN\) to your text editor and save it locally as `comprehend-S3-access-arn`\.
**Note**  
The ARN has a format similar to *arn:aws:iam::123456789012:role/comprehend\-S3\-access\-policy*\. You need the ARN you saved as `comprehend-S3-access-arn` to attach the `comprehend-S3-access-policy` to your IAM role\.

   1. To attach the `comprehend-S3-access-policy` to your IAM role, use the [attach\-role\-policy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iam/attach-role-policy.html) command:

------
#### [ Linux ]

      ```
      aws iam attach-role-policy \
                --policy-arn policy-arn \
                --role-name comprehend-role
      ```

      Where:
      + *policy\-arn* is the ARN you saved as `comprehend-S3-access-arn`\.

------
#### [ macOS ]

      ```
      aws iam attach-role-policy \
                --policy-arn policy-arn \
                --role-name comprehend-role
      ```

      Where:
      + *policy\-arn* is the ARN you saved as `comprehend-S3-access-arn`\.

------
#### [ Windows ]

      ```
      aws iam attach-role-policy ^
                --policy-arn policy-arn ^
                --role-name comprehend-role
      ```

      Where:
      + *policy\-arn* is the ARN you saved as `comprehend-S3-access-arn`\.

------

1. To run an Amazon Comprehend entities analysis job, use the [start\-entities\-detection\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/comprehend/start-entities-detection-job.html) command:

------
#### [ Linux ]

   ```
   aws comprehend start-entities-detection-job \
           --input-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/data/,InputFormat=ONE_DOC_PER_FILE \
           --output-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/ \
           --data-access-role-arn role-arn \
           --job-name data-entities-analysis \
           --language-code en \
           --region aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket,
   + *role\-arn* is the ARN you saved as `comprehend-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws comprehend start-entities-detection-job \
           --input-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/data/,InputFormat=ONE_DOC_PER_FILE \
           --output-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/ \
           --data-access-role-arn role-arn \
           --job-name data-entities-analysis \
           --language-code en \
           --region aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket,
   + *role\-arn* is the ARN you saved as `comprehend-role-arn`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws comprehend start-entities-detection-job ^
           --input-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/data/,InputFormat=ONE_DOC_PER_FILE ^
           --output-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET/ ^
           --data-access-role-arn role-arn ^
           --job-name data-entities-analysis ^
           --language-code en ^
           --region aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket,
   + *role\-arn* is the ARN you saved as `comprehend-role-arn`,
   + *aws\-region* is your AWS region\.

------

1. Copy the entities analysis `JobId` and save it in a text editor as `comprehend-job-id`\. The `JobId` helps you track the status of your entities analysis job\.

1. To track the progress of your entities analysis job, use the [describe\-entities\-detection\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/comprehend/describe-entities-detection-job.html) command:

------
#### [ Linux ]

   ```
   aws comprehend describe-entities-detection-job \
           --job-id entities-job-id \
           --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id`,
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws comprehend describe-entities-detection-job \
           --job-id entities-job-id \
           --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id`,
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws comprehend describe-entities-detection-job ^
           --job-id entities-job-id ^
           --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id`,
   + *aws\-region* is your AWS region\.

------

It can take several minutes for the `JobStatus` to change to `COMPLETED`\.

At the end of this step, Amazon Comprehend stores the entity analysis results as a zipped `output.tar.gz` file inside an `output` folder within an auto\-generated folder in your S3 bucket\. Make sure that your analysis job status is complete before you move on to the next step\.