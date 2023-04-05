--------

--------

# Adding documents in languages other than English<a name="in-adding-languages"></a>

You can index documents in multiple languages\. If you don't specify a language, Amazon Kendra indexes documents in English by default\. You include the language code for a document in the document metadata as a field\. See [Field mappings](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html) and [Custom attributes](https://docs.aws.amazon.com/kendra/latest/dg/custom-attributes.html) for more information on the `_language_code` field for a document\.

You can specify the language code for all your documents in your data source when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. If a document doesn't have a language code specified in a metadata field, the document is indexed using the language code specified for all documents at the data source level\. In the console, you can index documents in a supported language only at the data source level\. Go to **Data sources**, then the **Specify data source details** page, and choose a language from the dropdown **Language**\.

You can also search or query documents in a supported language\. For more information, see [Searching in languages](https://docs.aws.amazon.com/kendra/latest/dg/searching-example.html#searching-index-languages)\.

The following languages and their codes are supported \(English or `en` is supported by default if you don't specify a language\)\. This table includes languages that Amazon Kendra supports with full semantic search, as well as languages that only support simple keyword matching\. Languages that support full semantic search are marked with an asterisk and are in bold text in the following table\. English \(default language\) is also supported with full semantic search\.


| **Language name** | **Language code** | 
| --- | --- | 
| Arabic | ar | 
| Armenian | hy | 
| Basque | eu | 
| Bengali | bn | 
| Bulgarian | bg | 
| Catalan | ca | 
| Chinese – simplified and traditional\* | zh | 
| Czech | cs | 
| Danish | da | 
| Dutch | nl | 
| Finnish | fi | 
| French – includes French \(Canada\)\* | fr | 
| Galician | gl | 
| German\* | de | 
| Greek | el | 
| Hindi | hi | 
| Hungarian | hu | 
| Indonesian | id | 
| Irish | ga | 
| Italian | it | 
| Japanese\* | ja | 
| Korean\* | ko | 
| Latvian | lv | 
| Lithuanian | lt | 
| Norwegian | no | 
| Persian | fa | 
| Portuguese | pt | 
| Portuguese \(Brazil\)\* | pt\-BR | 
| Romanian | ro | 
| Russian | ru | 
| Sorani | ckb | 
| Spanish – includes Spanish \(Mexico\)\* | es | 
| Swedish | sv | 
| Turkish | tr | 

*\*Semantic search is supported for the language\.*

For languages that support semantic search, the following features are supported\.
+ Document relevance beyond simple keyword matching\.
+ FAQs beyond simple keyword matching\.
+ Extracting answers from documents based on Amazon Kendra's reading comprehension\.
+ Confidence buckets \(very high, high, medium, and low\) of the search results\.

For languages that don't support semantic search, simple keyword matching is supported for document relevance and FAQs\.

[Synonyms](https://docs.aws.amazon.com/kendra/latest/dg/index-synonyms.html) \(including custom synonyms\), [incremental learning and feedback](https://docs.aws.amazon.com/kendra/latest/dg/submitting-feedback.html), and [query suggestions](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions.html) are only supported for English \(default language\)\.