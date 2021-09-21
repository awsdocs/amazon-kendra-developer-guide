--------

--------

# Step 3: Formatting the entities analysis output as Amazon Kendra metadata<a name="tutorial-search-metadata-format-output"></a>

To convert the entities extracted by Amazon Comprehend to the metadata format required by an Amazon Kendra index, you run a Python 3 script\. The results of the conversion are stored in the `metadata` folder in your Amazon S3 bucket\.

For more information on Amazon Kendra metadata format and structure, see [S3 document metadata](https://docs.aws.amazon.com/kendra/latest/dg/s3-metadata.html)\.

**Topics**
+ [Downloading and extracting the Amazon Comprehend output](#tutorial-search-metadata-format-output-download-extract)
+ [Uploading the output into the S3 bucket](#tutorial-search-metadata-format-output-upload)
+ [Converting the output to Amazon Kendra metadata format](#tutorial-search-metadata-format-output-script)
+ [Cleaning up your Amazon S3 bucket](#tutorial-search-metadata-format-output-cleanup)

## Downloading and extracting the Amazon Comprehend output<a name="tutorial-search-metadata-format-output-download-extract"></a>

To format the Amazon Comprehend entities analysis output, you must first download the Amazon Comprehend entities analysis `output.tar.gz` archive and extract the entities analysis file\.

### To download and extract the output file \(Console\)<a name="tutorial-search-metadata-download-extract-console"></a>

1. In the Amazon Comprehend console navigation pane, navigate to **Analysis jobs**\.

1. Choose your entities analysis job `data-entities-analysis`\.

1. Under **Output**, choose the link displayed next to **Output data location**\. This redirects you to the `output.tar.gz` archive in your S3 bucket\.

1. In the **Overview** tab, choose **Download**\.
**Tip**  
The output of all Amazon Comprehend analysis jobs have the same name\. Renaming your archive will help you track it more easily\.

1. Decompress and extract the downloaded Amazon Comprehend file to your device\.

### To download and extract the output file \(AWS CLI\)<a name="tutorial-search-metadata-download-extract-cli"></a>

1. To access the name of the Amazon Comprehend auto\-generated folder in your S3 bucket which contains the results of the entities analysis job, use the [describe\-entities\-detection\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/comprehend/describe-entities-detection-job.html) command:

------
#### [ Linux ]

   ```
   aws comprehend describe-entities-detection-job \
             --job-id entities-job-id \
             --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id` from [Step 2: Running an entities analysis job on Amazon Comprehend](tutorial-search-metadata-entities-analysis.md),
   + *aws\-region* is your AWS region\.

------
#### [ macOS ]

   ```
   aws comprehend describe-entities-detection-job \
             --job-id entities-job-id \
             --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id` from [Step 2: Running an entities analysis job on Amazon Comprehend](tutorial-search-metadata-entities-analysis.md),
   + *aws\-region* is your AWS region\.

------
#### [ Windows ]

   ```
   aws comprehend describe-entities-detection-job ^
             --job-id entities-job-id ^
             --region aws-region
   ```

   Where:
   + *entities\-job\-id* is your saved `comprehend-job-id` from [Step 2: Running an entities analysis job on Amazon Comprehend](tutorial-search-metadata-entities-analysis.md),
   + *aws\-region* is your AWS region\.

------

1. From the `OutputDataConfig` object in your entities job description, copy and save the `S3Uri` value as `comprehend-S3uri` on a text editor\.
**Note**  
The `S3Uri` value has a format similar to *s3://*DOC\-EXAMPLE\-BUCKET*/\.\.\./output/output\.tar\.gz*\.

1. To download the entities output archive, use the [copy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html) command:

------
#### [ Linux ]

   ```
   aws s3 cp s3://DOC-EXAMPLE-BUCKET/.../output/output.tar.gz path/output.tar.gz
   ```

   Where:
   + *s3://*DOC\-EXAMPLE\-BUCKET*/\.\.\./output/output\.tar\.gz* is the `S3Uri` value you saved as `comprehend-S3uri`,
   + *path/* is the local directory where you wish to save the output\.

------
#### [ macOS ]

   ```
   aws s3 cp s3://DOC-EXAMPLE-BUCKET/.../output/output.tar.gz path/output.tar.gz
   ```

   Where:
   + *s3://*DOC\-EXAMPLE\-BUCKET*/\.\.\./output/output\.tar\.gz* is the `S3Uri` value you saved as `comprehend-S3uri`,
   + *path/* is the local directory where you wish to save the output\.

------
#### [ Windows ]

   ```
   aws s3 cp s3://DOC-EXAMPLE-BUCKET/.../output/output.tar.gz path/output.tar.gz
   ```

   Where:
   + *s3://*DOC\-EXAMPLE\-BUCKET*/\.\.\./output/output\.tar\.gz* is the `S3Uri` value you saved as `comprehend-S3uri`,
   + *path/* is the local directory where you wish to save the output\.

------

1. To extract the entities output, run the following command on a terminal window:

------
#### [ Linux ]

   ```
   tar -xf path/output.tar.gz -C path/
   ```

   Where:
   + *path/* is the filepath to the downloaded `output.tar.gz` archive on your local device\.

------
#### [ macOS ]

   ```
   tar -xf path/output.tar.gz -C path/
   ```

   Where:
   + *path/* is the filepath to the downloaded `output.tar.gz` archive on your local device\.

------
#### [ Windows ]

   ```
   tar -xf path/output.tar.gz -C path/
   ```

   Where:
   + *path/* is the filepath to the downloaded `output.tar.gz` archive on your local device\.

------

At the end of this step, you should have a file on your device called `output` with a list of Amazon Comprehend identified entities\.

## Uploading the output into the S3 bucket<a name="tutorial-search-metadata-format-output-upload"></a>

After downloading and extracting the Amazon Comprehend entities analysis file, you upload the extracted `output` file to your Amazon S3 bucket\.

### To upload the extracted Amazon Comprehend output file \(Console\)<a name="tutorial-search-metadata-upload-output-console"></a>

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In **Buckets**, click on the name of your bucket and then choose **Upload**\.

1. In **Files and folders**, choose **Add files**\.

1. In the dialog box, navigate to your extracted `output` file in your device, select it, and choose **Open**\.

1. Keep the default settings for **Destination**, **Permissions**, and **Properties**\.

1. Choose **Upload**\.

### To upload the extracted Amazon Comprehend output file \(AWS CLI\)<a name="tutorial-search-metadata-upload-output-cli"></a>

1. To upload the extracted `output` file to your bucket, use the [copy](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/cp.html) command:

------
#### [ Linux ]

   ```
   aws s3 cp path/output s3://DOC-EXAMPLE-BUCKET/output
   ```

   Where:
   + *path/* is the local filepath to your extracted `output` file,
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ macOS ]

   ```
   aws s3 cp path/output s3://DOC-EXAMPLE-BUCKET/output
   ```

   Where:
   + *path/* is the local filepath to your extracted `output` file,
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ Windows ]

   ```
   aws s3 cp path/output s3://DOC-EXAMPLE-BUCKET/output
   ```

   Where:
   + *path/* is the local filepath to your extracted `output` file,
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------

1. To ensure that the `output` file was uploaded successfully to your S3 bucket, check its contents by using the [list](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/ls.html) command:

------
#### [ Linux ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ macOS ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ Windows ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------

## Converting the output to Amazon Kendra metadata format<a name="tutorial-search-metadata-format-output-script"></a>

To convert the Amazon Comprehend output to Amazon Kendra metadata, you run a Python 3 script\. If you are using the Console, you use AWS CloudShell for this step\.

### To run the Python 3 script \(Console\)<a name="tutorial-search-metadata-format-output-console"></a>

1. Download the [converter\.py\.zip](https://docs.aws.amazon.com/kendra/latest/dg/samples/converter.py.zip) zipped file on your device\.

1. Extract the Python 3 file `converter.py`\.

1. Sign into the [AWS Management Console](https://aws.amazon.com/console/) and make sure your AWS region is set to the same region as your S3 bucket and your Amazon Comprehend analysis job\.

1. Choose the **AWS CloudShell icon** or type **AWS CloudShell** in the **Search** box on the top navigation bar to launch an environment\.
**Note**  
When AWS CloudShell launches in a new browser window for the first time, a welcome panel displays and lists key features\. The shell is ready for interaction after you close this panel and the command prompt displays\.

1. After the terminal is prepared, choose **Actions** from the navigation pane and then choose **Upload file** from the menu\.

1. In the dialog box that opens, choose **Select file** and then choose the downloaded Python 3 file `converter.py` from your device\. Choose **Upload**\.

1. In the AWS CloudShell environment, enter the following command:

   ```
   python3 converter.py
   ```

1. When the shell interface prompts you to **Enter the name of your S3 bucket**, enter the name of your S3 bucket and press enter\.

1. When the shell interface prompts you to **Enter the full filepath to your Comprehend output file**, enter **output** and press enter\.

1. When the shell interface prompts you to **Enter the full filepath to your metadata folder**, enter **metadata/** and press enter\.

**Important**  
For the metadata to be formatted correctly, the input values in steps 8\-10 must be exact\.

### To run the Python 3 script \(AWS CLI\)<a name="tutorial-search-metadata-format-output-cli"></a>

1. To download the Python 3 file `converter.py`, run the following command on a terminal window:

------
#### [ Linux ]

   ```
   curl -o path/converter.py.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/converter.py.zip
   ```

   Where:
   + *path/* is the filepath to the location you want to save the zipped file in\.

------
#### [ macOS ]

   ```
   curl -o path/converter.py.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/converter.py.zip
   ```

   Where:
   + *path/* is the filepath to the location you want to save the zipped file in\.

------
#### [ Windows ]

   ```
   curl -o path/converter.py.zip https://docs.aws.amazon.com/kendra/latest/dg/samples/converter.py.zip
   ```

   Where:
   + *path/* is the filepath to the location you want to save the zipped file in\.

------

1. To extract the Python 3 file, run the following command on the terminal window:

------
#### [ Linux ]

   ```
   unzip path/converter.py.zip -d path/
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------
#### [ macOS ]

   ```
   unzip path/converter.py.zip -d path/
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------
#### [ Windows ]

   ```
   tar -xf path/converter.py.zip -C path/
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------

1. Make sure that Boto3 is installed on your device by running the following command\.

------
#### [ Linux ]

   ```
   pip3 show boto3
   ```

------
#### [ macOS ]

   ```
   pip3 show boto3
   ```

------
#### [ Windows ]

   ```
   pip3 show boto3
   ```

------
**Note**  
If you do not have Boto3 installed, run `pip3 install boto3` to install it\.

1. To run the Python 3 script to convert the `output` file, run the following command\.

------
#### [ Linux ]

   ```
   python path/converter.py
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------
#### [ macOS ]

   ```
   python path/converter.py
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------
#### [ Windows ]

   ```
   python path/converter.py
   ```

   Where:
   + *path/* is the filepath to your saved `converter.py.zip`\.

------

1. When the AWS CLI prompts you to `Enter the name of your S3 bucket`, enter the name of your S3 bucket and press enter\.

1. When the AWS CLI prompts you to `Enter the full filepath to your Comprehend output file`, enter **output** and press enter\.

1. When the AWS CLI prompts you to `Enter the full filepath to your metadata folder`, enter **metadata/** and press enter\.

**Important**  
For the metadata to be formatted correctly, the input values in steps 5\-7 must be exact\.

At the end of this step, the formatted metadata is deposited inside the `metadata` folder in your S3 bucket\.

## Cleaning up your Amazon S3 bucket<a name="tutorial-search-metadata-format-output-cleanup"></a>

Since the Amazon Kendra index syncs all files stored in a bucket, we recommend you clean up your Amazon S3 bucket to prevent redundant search results\.

### To clean up your Amazon S3 bucket \(Console\)<a name="tutorial-search-metadata-cleanup-bucket-console"></a>

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In **Buckets**, choose your bucket and then select the Amazon Comprehend entity analysis output folder, the Amazon Comprehend entity analysis `.temp` file, and the extracted Amazon Comprehend `output` file\.

1. From the **Overview** tab choose **Delete**\.

1. In **Delete objects**, choose **Permanently delete objects?** and enter **permanently delete** in the text input field\.

1. Choose **Delete objects**\.

### To clean up your Amazon S3 bucket \(AWS CLI\)<a name="tutorial-search-metadata-cleanup-bucket-cli"></a>

1. To delete all files and folders in your S3 bucket except the `data` and `metadata` folders, use the [remove](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/rm.html) command in the AWS CLI:

------
#### [ Linux ]

   ```
   aws s3 rm s3://DOC-EXAMPLE-BUCKET/ --recursive --exclude "data/*" --exclude "metadata/*"
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ macOS ]

   ```
   aws s3 rm s3://DOC-EXAMPLE-BUCKET/ --recursive --exclude "data/*" --exclude "metadata/*"
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ Windows ]

   ```
   aws s3 rm s3://DOC-EXAMPLE-BUCKET/ --recursive --exclude "data/*" --exclude "metadata/*"
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------

1. To ensure that the objects were successfully deleted from your S3 bucket, check its contents by using the [list](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/ls.html) command:

------
#### [ Linux ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ macOS ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------
#### [ Windows ]

   ```
   aws s3 ls s3://DOC-EXAMPLE-BUCKET/
   ```

   Where:
   + *DOC\-EXAMPLE\-BUCKET* is the name of your S3 bucket\.

------

At the end of this step, you have converted the Amazon Comprehend entities analysis output to Amazon Kendra metadata\. You are now ready to create an Amazon Kendra index\.