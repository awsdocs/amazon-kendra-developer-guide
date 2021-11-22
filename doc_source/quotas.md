--------

--------

# Quotas for Amazon Kendra<a name="quotas"></a>

## Supported regions<a name="regions"></a>

For a list of AWS Regions where Amazon Kendra is available, see [ AWS Regions and Endpoints ](https://docs.aws.amazon.com/general/latest/gr/kendra.html) in the *Amazon Web Services General Reference*\.

## Quotas<a name="quota-details"></a>

Service quotas, also referred to as limits, are the maximum number of service resources for your AWS account\. For more information, see [AWS Service Quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.




| Description | Default | Edition | Adjustable | 
| --- | --- | --- | --- | 
| Maximum number of indexes per account | 5 | Developer | Yes | 
| Maximum number of indexes per account | 5 | Enterprise | Yes | 
| Maximum number of data sources per index | 5 | Developer | No | 
| Maximum number of data sources per index | 50 | Enterprise | Yes | 
| Maximum amount of text extracted for an index or a single unit of storage capacity | 3 GB | Developer | Yes | 
| Maximum amount of text extracted for an index or a single unit of storage capacity | 30 GB | Enterprise | Yes | 
| Maximum number of documents for an index or a single unit of storage capacity\. You must also not exceed the maximum text extracted\. | 10,000 | Developer | Yes | 
| Maximum number of documents for an index or a single unit of storage capacity\. You must also not exceed the maximum text extracted\. | 100,000 | Enterprise | Yes | 
| Maximum number of queries per second for an index or a single unit of query capacity | 0\.05 | Developer | Yes | 
| Maximum number of queries per second for an index or a single unit of query capacity | 0\.1 | Enterprise | Yes | 
| Maximum number of storage capacity units per index | 100 | Enterprise | Yes | 
| Maximum number of query capacity units per index | 100 | Enterprise | Yes | 
| Maximum number of search results retrieved for a query | 100 | All editions | Yes | 
| Maximum size of a single document | 50 MB | All editions | Yes | 
| Maximum amount of text extracted from a single document | 5 MB | All editions | Yes | 
| Maximum user group list size per query attribute | 10 | All editions | Yes | 
| Maximum string list size per query attribute | 10 | All editions | Yes | 
| Maximum number of custom attributes per index | 500 | All editions | No | 
| Maximum number of FAQs per index | 30 | All editions | Yes | 
| Maximum size of 1 FAQ | 1 MB | All editions | Yes | 
| Maximum number of results returned for FAQ | 4 | All editions | Yes | 
| Maximum number of thesauri per index | 1 | All editions | No | 
| Maximum size of a thesaurus file | 5 MB | All editions | Yes | 
| Maximum number of synonym rules per thesaurus | 10,000 | All editions | Yes | 
| Maximum number of synonyms per term in all thesauri in an index | 10 | All editions | No | 
| Maximum number of block lists per index | 1 | All editions | No | 
| Maximum size of a block list text file | 2 MB | All editions | Yes | 
| Maximum number of items \(words or phrases\) in a block list | 20,000 | All editions | Yes | 

For more information about Amazon Kendra service quotas and to request a quota increase, see [Service Quotas](https://console.aws.amazon.com/servicequotas/)\.