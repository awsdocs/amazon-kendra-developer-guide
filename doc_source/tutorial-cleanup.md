--------

--------

# Step 6: Cleaning up<a name="tutorial-cleanup"></a>

## Cleaning up your files<a name="tutorial-cleanup-deleting"></a>

To stop incurring charges in your AWS account after you complete this tutorial, you can take the following steps:

1. **Delete your Amazon S3 bucket**

   For information about deleting a bucket, see [Deleting a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html)\.

1. **Delete your Amazon Kendra index**

   For information about deleting an Amazon Kendra index, see [Deleting an index](https://docs.aws.amazon.com/kendra/latest/dg/delete-index.html)\.

1. **Delete `converter.py`**
   + **For Console:** Go to [AWS CloudShell](https://console.aws.amazon.com/cloudshell/), and make sure the region is set to your AWS region\. After the bash shell has loaded, type the following command into the environment and press enter\.

     ```
     rm converter.py
     ```
   + **For AWS CLI:** Run the following command on a terminal window\.

------
#### [ Linux ]

     ```
     rm file/converter.py
     ```

     Where:
     + *file/* is the filepath to `converter.py` on your local device\.

------
#### [ macOS ]

     ```
     rm file/converter.py
     ```

     Where:
     + *file/* is the filepath to `converter.py` on your local device\.

------
#### [ Windows ]

     ```
     rm file/converter.py
     ```

     Where:
     + *file/* is the filepath to `converter.py` on your local device\.

------

## <a name="tutorial-cleanup-more"></a>

### Learn more<a name="tutorial-cleanup-2-more"></a>

To learn more about integrating Amazon Kendra into your workflow, you can check out the following blogposts:
+ [Content metadata tagging for enhanced search](https://comprehend-immersionday.workshop.aws/lab8.html)
+ [Build an intelligent search solution with automated content enrichment](https://aws.amazon.com/blogs/machine-learning/build-an-intelligent-search-solution-with-automated-content-enrichment/)

To learn more about Amazon Comprehend, you can look at the [https://docs.aws.amazon.com/comprehend/index.html](https://docs.aws.amazon.com/comprehend/index.html)\.