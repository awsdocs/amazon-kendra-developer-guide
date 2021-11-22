--------

--------

# Step 1: Adding documents to Amazon S3<a name="tutorial-search-metadata-add-documents"></a>

Before you run an Amazon Comprehend entities analysis job on your dataset, you create an Amazon S3 bucket to host the data, metadata, and the Amazon Comprehend entities analysis output\.

**Topics**
+ [Downloading the sample dataset](#tutorial-search-metadata-add-documents-download-extract)
+ [Creating an Amazon S3 bucket](#tutorial-search-metadata-add-documents-create-bucket)
+ [Creating data and metadata folders in your S3 bucket](#tutorial-search-metadata-add-documents-data-metadata)
+ [Uploading the input data](#tutorial-search-metadata-add-documents-upload-data)

## Downloading the sample dataset<a name="tutorial-search-metadata-add-documents-download-extract"></a>

Before Amazon Comprehend can run an entities analysis job on your data, you must download and extract the dataset and upload it to an S3 bucket\.

### To download and extract the dataset \(Console\)<a name="tutorial-search-metadata-download-extract-console"></a>

1. Download the [tutorial\-dataset\.zip](https://docs.aws.amazon.com/kendra/latest/dg/samples/tutorial-dataset.zip) folder on your device\.

1. Extract the `tutorial-dataset` folder to access the `data` folder\.

### To download and extract the dataset \(Terminal\)<a name="tutorial-search-metadata-download-extract-cli"></a>

1. To download the `tutorial-dataset`, run the following command on a terminal window:

------
#### [ Linux ]

   ```
   curl -o path/tutorial-dataset.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/tutorial-dataset.zip
   ```

   Where:
   + *path/* is the local filepath to the location you want to save the zip folder in\.

------
#### [ macOS ]

   ```
   curl -o path/tutorial-dataset.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/tutorial-dataset.zip
   ```

   Where:
   + *path/* is the local filepath to the location you want to save the zip folder in\.

------
#### [ Windows ]

   ```
   curl -o path/tutorial-dataset.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/tutorial-dataset.zip
   ```

   Where:
   + *path/* is the local filepath to the location you want to save the zip folder in\.

------

1. To extract the data from the zip folder, run the following command on the terminal window:

------
#### [ Linux ]

   ```
   unzip path/tutorial-dataset.zip -d path/
   ```

   Where:
   + *path/* is the local filepath to your saved zip folder\.

------
#### [ macOS ]

   ```
   unzip path/tutorial-dataset.zip -d path/
   ```

   Where:
   + *path/* is the local filepath to your saved zip folder\.

------
#### [ Windows ]

   ```
   tar -xf path/tutorial-dataset.zip -C path/
   ```

   Where:
   + *path/* is the local filepath to your saved zip folder\.

------

At the end of this step, you should have the extracted files in a decompressed folder called `tutorial-dataset`\. This folder contains a `README` file with an Apache 2\.0 open source attribution and a folder called `data` containing the dataset for this tutorial\. The dataset consists of 100 files with `.story` extensions\.

## Creating an Amazon S3 bucket<a name="tutorial-search-metadata-add-documents-create-bucket"></a>

After downloading and extracting the sample data folder, you store it in an Amazon S3 bucket\.

**Important**  
The name of an Amazon S3 bucket must be unique across all of AWS\.

### To create an S3 bucket \(Console\)<a name="tutorial-search-metadata-create-bucket-console"></a>

1. Sign in to the AWS Management Console and open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In **Buckets**, choose **Create bucket**\.

1. For **Bucket name**, enter a unique name\.

1. For **Region**, choose the AWS region where you want to create the bucket\.
**Note**  
You must choose a region that supports both Amazon Comprehend and Amazon Kendra\. You cannot change the region of a bucket after you have created it\.

1. Keep the default settings for **Block Public Access settings for this bucket**, **Bucket Versioning**, and **Tags**\.

1. For **Default encryption**, choose **Disable**\.

1. Keep the default settings for the **Advanced settings**\.

1. Review your bucket configuration and then choose **Create bucket**\.

### To create an S3 bucket \(AWS CLI\)<a name="tutorial-search-metadata-create-bucket-cli"></a>

1. To create an S3 bucket, use the [create\-bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/create-bucket.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3api create-bucket \
           --bucket DOC-EXAMPLE-BUCKET \
           --region aws-region \
           --create-bucket-configuration LocationConstraint=aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name,
   + *aws\-region* is the region you want to create your bucket in\.

------
#### [ macOS ]

   ```
   aws s3api create-bucket \
           --bucket DOC-EXAMPLE-BUCKET \
           --region aws-region \
           --create-bucket-configuration LocationConstraint=aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name,
   + *aws\-region* is the region you want to create your bucket in\.

------
#### [ Windows ]

   ```
   aws s3api create-bucket ^
           --bucket DOC-EXAMPLE-BUCKET ^
           --region aws-region ^
           --create-bucket-configuration LocationConstraint=aws-region
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name,
   + *aws\-region* is the region you want to create your bucket in\.

------
**Note**  
You must choose a region that supports both Amazon Comprehend and Amazon Kendra\. You cannot change the region of a bucket after you have created it\.

1. To ensure that your bucket was created successfully, use the [list](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/ls.html) command:

------
#### [ Linux ]

   ```
   aws s3 ls
   ```

------
#### [ macOS ]

   ```
   aws s3 ls
   ```

------
#### [ Windows ]

   ```
   aws s3 ls
   ```

------

## Creating data and metadata folders in your S3 bucket<a name="tutorial-search-metadata-add-documents-data-metadata"></a>

After creating your S3 bucket, you create data and metadata folders inside it\.

### To create folders in your S3 bucket \(Console\)<a name="tutorial-search-metadata-create-folders-console"></a>

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In **Buckets**, click on the name of your bucket from the list of buckets\.

1. From the **Objects** tab, choose **Create folder**\.

1. For the new folder name, enter **data**\.

1. For the encryption settings, choose **Disable**\.

1. Choose **Create folder**\.

1. Repeat steps 3 to 6 to create another folder for storing the Amazon Kendra metadata and name the folder created in step 4 **metadata**\.

### To create folders in your S3 bucket \(AWS CLI\)<a name="tutorial-search-metadata-create-folders-cli"></a>

1. To create the `data` folder in your S3 bucket, use the [put\-object](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-object.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3api put-object \
           --bucket DOC-EXAMPLE-BUCKET \
           --key data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ macOS ]

   ```
   aws s3api put-object \
           --bucket DOC-EXAMPLE-BUCKET \
           --key data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ Windows ]

   ```
   aws s3api put-object ^
           --bucket DOC-EXAMPLE-BUCKET ^
           --key data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------

1. To create the `metadata` folder in your S3 bucket, use the [put\-object](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/put-object.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3api put-object \
           --bucket DOC-EXAMPLE-BUCKET \
           --key metadata/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ macOS ]

   ```
   aws s3api put-object \
           --bucket DOC-EXAMPLE-BUCKET \
           --key metadata/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ Windows ]

   ```
   aws s3api put-object ^
           --bucket DOC-EXAMPLE-BUCKET ^
           --key metadata/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------

1. To ensure that your folders were created successfully, check the contents of your bucket using the [list](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/ls.html) command:

------
#### [ Linux ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ macOS ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ Windows ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------

## Uploading the input data<a name="tutorial-search-metadata-add-documents-upload-data"></a>

After creating your data and metadata folders, you upload the sample dataset into the `data` folder\.

### To upload the sample dataset into the data folder \(Console\)<a name="tutorial-search-metadata-upload-data-console"></a>

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In **Buckets**, click on the name of your bucket from the list of buckets and then click on `data`\.

1. Choose **Upload** and then choose **Add files**\.

1. In the dialog box, navigate to the `data` folder inside the `tutorial-dataset` folder in your local device, select all the files, and then choose **Open**\.

1. Keep the default settings for **Destination**, **Permissions**, and **Properties**\.

1. Choose **Upload**\.

### To upload the sample dataset into the data folder \(AWS CLI\)<a name="tutorial-search-metadata-upload-data-cli"></a>

1. To upload the sample data into the `data` folder, use the [copy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3 cp path/tutorial-dataset/data s3://DOC-EXAMPLE-BUCKET/data/ --recursive
   ```

   Where:
   + *path/* is the filepath to the `tutorial-dataset` folder on your device,
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ macOS ]

   ```
   aws s3 cp path/tutorial-dataset/data s3://DOC-EXAMPLE-BUCKET/data/ --recursive
   ```

   Where:
   + *path/* is the filepath to the `tutorial-dataset` folder on your device,
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------
#### [ Windows ]

   ```
   aws s3 cp path/tutorial-dataset/data s3://DOC-EXAMPLE-BUCKET/data/ --recursive
   ```

   Where:
   + *path/* is the filepath to the `tutorial-dataset` folder on your device,
   + *DOC\-EXAMPLE\-BUCKET* is your bucket name\.

------

1. To ensure that your dataset files were uploaded successfully to your `data` folder, use the [list](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/ls.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ macOS ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ Windows ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/data/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------

At the end of this step, you have an S3 bucket with your dataset stored inside the `data` folder, and an empty `metadata` folder, which will store your Amazon Kendra metadata\.