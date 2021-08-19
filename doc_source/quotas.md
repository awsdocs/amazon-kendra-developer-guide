--------

--------

# Quotas for Amazon Kendra<a name="quotas"></a>

## Supported regions<a name="regions"></a>

For a list of AWS Regions where Amazon Kendra is available, see [ AWS Regions and Endpoints ](https://docs.aws.amazon.com/general/latest/gr/kendra.html) in the *Amazon Web Services General Reference*\.

## Quotas<a name="quota-details"></a>

Service quotas, also referred to as limits, are the maximum number of service resources for your AWS account\. For more information, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.




| Description | Default | Adjustable | 
| --- | --- | --- | 
| Maximum number of developer edition indexes per account | 5 | Yes | 
| Maximum number of enterprise edition indexes per account | 5 | Yes | 
| Maximum number of data sources per developer edition index | 5 | No | 
| Maximum number of data sources per enterprise edition index | 50 | Yes | 
| Maximum amount of text extracted for a developer edition index or a single unit of storage capacity | 3 GB | Yes | 
| Maximum amount of text extracted for an enterprise edition index or a single unit of storage capacity | 30 GB | Yes | 
| Maximum number of queries per second for a developer edition index or a single unit of query capacity | 0\.05 | Yes | 
| Maximum number of queries per second for an enterprise edition index or a single unit of query capacity | 0\.1 | Yes | 
| Maximum number of storage capacity units per enterprise edition index | 100 | Yes | 
| Maximum number of query capacity units per enterprise edition index | 100 | Yes | 
| Maximum size of a single document for all editions | 50 MB | Yes | 
| Maximum amount of text extracted from a single document for all editions | 5 MB | Yes | 
| Maximum user group list size per query attribute for all editions | 10 | Yes | 
| Maximum string list size per query attribute for all editions | 10 | Yes | 
| Maximum number of custom attributes per index for all editions | 500 | No | 
| Maximum number of FAQs per index for all editions | 30 | Yes | 
| Maximum size of 1 FAQ for all editions | 1 MB | Yes | 
| Maximum number of thesauri per index for all editions | 1 | No | 
| Maximum size of a thesaurus file for all editions | 5 MB | Yes | 
| Maximum number of synonym rules per thesaurus for all editions | 10,000 | Yes | 
| Maximum number of synonyms per term in all thesauri in a index \(all editions\) | 10 | No | 
| Maximum number of block lists per index for all editions | 1 | No | 
| Maximum size of a block list text file for all editions | 2 MB | Yes | 
| Maximum number of items \(words or phrases\) in a block list for all editions | 20,000 | Yes | 

For more information about Amazon Kendra service quotas and to request a quota increase, see [Service Quotas](https://console.aws.amazon.com/servicequotas/)\.