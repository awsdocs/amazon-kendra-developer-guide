--------

--------

# Resilience in Amazon Kendra<a name="disaster-recovery-resiliency"></a>

The AWS global infrastructure is built around AWS Regions and Availability Zones\. AWS Regions provide multiple physically separated and isolated Availability Zones, which are connected with low\-latency, high\-throughput, and highly redundant networking\. With Availability Zones, you can design and operate applications and databases that automatically fail over between zones without interruption\. Availability Zones are more highly available, fault tolerant, and scalable than traditional single or multiple data center infrastructures\. 

For more information about AWS Regions and Availability Zones, see [AWS Global Infrastructure](http://aws.amazon.com/about-aws/global-infrastructure/)\.

With AWS global infrastructure, Amazon Kendra Enterprise Edition is fault tolerant, scalable, and highly available\. Rolling back to previous versions of an index is not currently supported, but you can refresh or recreate portions of your index by [deleting](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchDeleteDocument.html) and [adding](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) existing data sources back into your index\.