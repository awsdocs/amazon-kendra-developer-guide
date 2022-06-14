--------

--------

# Setting up the AWS SDKs<a name="aws-kendra-set-up-sdks"></a>

Download and install the AWS SDKs that you want to use\. This guide provides examples for Python\. For information about other AWS SDKs, see [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.

The package for the Python SDK is called *Boto3*\.

Before you run the below Python commands, you must first download and install [Python 3\.6 or later](https://www.python.org/downloads/) for your operating system\. Support for Python 3\.5 and earlier is deprecated\. If you do not have pip included in your Python Scripts directory, you can download [get\-pip\.py](https://bootstrap.pypa.io/get-pip.py) and store this in your Scripts directory\. You can also set your Python directory as a [Path or environment variable](https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH) using a terminal program\.

```
# Install the latest Boto3 release via pip
pip install boto3

# You can install a specific version of Boto3 for compatibility reasons
# Install Boto3 version 1.0 specifically
pip install boto3==1.0.0

# Make sure Boto3 is no older than version 1.15.0
pip install boto3>=1.15.0

# Avoid versions of Boto3 newer than version 1.15.3
pip install boto3<=1.15.3
```

To use Boto3, you must set up authentication credentials for your AWS account using the [IAM console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey)\.