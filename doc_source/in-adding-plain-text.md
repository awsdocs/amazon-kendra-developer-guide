--------

--------

# Adding documents from an S3 bucket<a name="in-adding-plain-text"></a>

You can add documents directly to your index from an Amazon S3 bucket\. You can add up to 10 documents in the same call\. When you use an S3 bucket, you must provide an IAM role with permission to access the bucket that contains your documents\. You specify the role in the `RoleArn` parameter\.

Using the [BatchPutDocument](API_BatchPutDocument.md) API to add documents from an S3 bucket is a one\-time operation\. To keep an index synchronized with the contents of a bucket, create an S3 data source\. For more information, see [Amazon S3](data-source-s3.md)\.

For an example of creating an index using the AWS CLI and SDKs, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. To set up the CLI and SDKs, see [Setting up Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/setup.html)\. For information on creating an S3 bucket, see [Amazon Simple Storage Service documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)\.

In the following example, two Microsoft Word documents are added to the index using the `BatchPutDocument` API\.

------
#### [ Python ]

```
import boto3

kendra = boto3.client("kendra")

# Provide the index ID
index_id = "index-id"
# Provide the IAM role ARN required to index documents in an S3 bucket
role_arn = "arn:aws:iam::${acccountID}:policy/${roleName}"

doc1_s3_file_data = {
    "Bucket": "bucket-name",
    "Key": "document1.docx"
}

doc1_document = {
    "S3Path": doc1_s3_file_data,
    "Title": "Document 1 title",
    "Id": "doc_1"
}

doc2_s3_file_data = {
    "Bucket": "bucket-name",
    "Key": "document2.docx"
}

doc2_document = {
    "S3Path": doc2_s3_file_data,
    "Title": "Document 2 title",
    "Id": "doc_2"
}

documents = [
    doc1_document,
    doc2_document
]

result = kendra.batch_put_document(
    Documents = documents,
    IndexId = index_id,
    RoleArn = role_arn
)

print(result)
```

------
#### [ Java ]

```
package com.amazonaws.kendra;

import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.BatchPutDocumentRequest;
import software.amazon.awssdk.services.kendra.model.BatchPutDocumentResponse;
import software.amazon.awssdk.services.kendra.model.Document;
import software.amazon.awssdk.services.kendra.model.S3Path;

public class AddFilesFromS3Example {
    public static void main(String[] args) {
        KendraClient kendra = KendraClient.builder().build();

        String indexId = "yourIndexId";
        String roleArn = "yourIndexRoleArn";

        Document pollyDoc = Document
            .builder()
            .s3Path(
                S3Path.builder()
                .bucket("an-aws-kendra-test-bucket")
                .key("What is Amazon Polly.docx")
                .build())
            .title("What is Amazon Polly")
            .id("polly_doc_1")
            .build();

        Document rekognitionDoc = Document
            .builder()
            .s3Path(
                S3Path.builder()
                .bucket("an-aws-kendra-test-bucket")
                .key("What is Amazon Rekognition.docx")
                .build())
            .title("What is Amazon rekognition")
            .id("rekognition_doc_1")
            .build();

        BatchPutDocumentRequest batchPutDocumentRequest = BatchPutDocumentRequest
            .builder()
            .indexId(indexId)
            .roleArn(roleArn)
            .documents(pollyDoc, rekognitionDoc)
            .build();

        BatchPutDocumentResponse result = kendra.batchPutDocument(batchPutDocumentRequest);

        System.out.println(String.format("BatchPutDocument result: %s", result));
    }
}
```

------