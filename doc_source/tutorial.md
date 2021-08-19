--------

--------

# Tutorial: Building a metadata\-enriched, intelligent search solution with Amazon Kendra<a name="tutorial"></a>

This tutorial shows you how to build a metadata\-enriched, natural language based, intelligent search solution for your enterprise data using [Amazon Kendra](https://aws.amazon.com/kendra/), [Amazon Comprehend](https://aws.amazon.com/comprehend/), [Amazon Simple Storage Service](https://aws.amazon.com/s3/) \(S3\), and [AWS CloudShell](https://aws.amazon.com/cloudshell/)\.

Amazon Kendra is an intelligent search service that can build a search index for your unstructured, natural language data repositories\. To make it easier for your customers to find and filter relevant answers, you can use Amazon Comprehend to extract metadata from your data and ingest it into your Amazon Kendra search index\.

Amazon Comprehend is a natural language processing \(NLP\) service that can identify entities\. Entities are references to people, places, locations, organizations, and objects in your data\.

This tutorial uses a sample dataset of news articles to extract entities, convert them to metadata, and ingest them into your Amazon Kendra index to run searches on\. The added metadata lets you filter your search results using any subset of these entities, and improves search accuracy\. By following this tutorial, you will learn how to create a search solution for your enterprise data without any specialized machine learning knowledge\.

**This tutorial shows you how to build your search solution using the following steps:**

1. Storing a sample dataset of news articles in Amazon S3\.

1. Using Amazon Comprehend to extract entities from your data\.

1. Running a Python 3 script to convert the entities into Amazon Kendra index metadata format and storing this metadata in S3\.

1. Creating an Amazon Kendra search index and ingesting the data and the metadata\.

1. Querying the search index\.

**The following diagram shows the workflow:**

![\[Workflow diagram of the procedures in the tutorial.\]](http://docs.aws.amazon.com/kendra/latest/dg/images/tutorial-workflow.png)

**Estimated time to complete this tutorial:** 1 hour

**Estimated cost:** Some of the actions in this tutorial incur charges on your AWS account\. For more information on the cost of each service, see the price pages for [Amazon S3](https://aws.amazon.com/s3/pricing/), [Amazon Comprehend](https://aws.amazon.com/comprehend/pricing/), [AWS CloudShell](https://aws.amazon.com/cloudshell/pricing/), and [Amazon Kendra](https://aws.amazon.com/kendra/pricing/)\.

**Topics**
+ [Prerequisites](#tutorial-prereqs)
+ [Step 1: Adding documents to Amazon S3](tutorial-adding-documents.md)
+ [Step 2: Running an entities analysis job on Amazon Comprehend](tutorial-entities-analysis.md)
+ [Step 3: Formatting the entities analysis output as Amazon Kendra metadata](tutorial-formatting-output.md)
+ [Step 4: Creating an Amazon Kendra index and ingesting the metadata](tutorial-creating-index.md)
+ [Step 5: Querying the Amazon Kendra index](tutorial-querying-kendra.md)
+ [Step 6: Cleaning up](tutorial-cleanup.md)

## Prerequisites<a name="tutorial-prereqs"></a>

To complete this tutorial, you need the following resources:
+ An AWS account\. If you do not have an AWS account, follow the steps in [Setting up Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/setup.html#aws-kendra-set-up-aws-account) to set up your AWS account\.
+ A development computer running Windows, macOS, or Linux, to access the AWS Management Console\. For more information, see [Configuring the AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/working-with-console.html)\.
+ An [AWS Identity and Access Management](https://aws.amazon.com/iam/) \(IAM\) user\. To learn how to set up an IAM user and group for your account, see the [Getting Started](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html) section in the *IAM User Guide*\.

  If you are using the AWS Command Line Interface, you also need to attach the following policy to your IAM user to grant it the basic permissions required to complete this tutorial\.

  

  

  For more information, see [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html) and [Adding and removing IAM identity permissions\.](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)
+ The [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\. To reduce latency, you should choose the AWS region closest to your geographic location that is supported by both Amazon Comprehend and Amazon Kendra\.
+ \(Optional\) An [AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\. While this tutorial does not use encryption, you might want to use encryption best practices for your specific use case\.
+ \(Optional\) An [Amazon Virtual Private Cloud](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)\. While this tutorial does not use a VPC, you might want to use VPC best practices to ensure data security for your specific use case\.