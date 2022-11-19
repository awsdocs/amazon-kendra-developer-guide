--------

--------

# Adding documents in languages other than English<a name="in-adding-languages"></a>

You can index documents in multiple languages\. If you don't specify a language, Amazon Kendra indexes documents in English by default\. You include the language code for a document in the document metadata as a field\. See [Field mappings](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html) and [Custom attributes](https://docs.aws.amazon.com/kendra/latest/dg/custom-attributes.html) for more information on the `_language_code` field for a document\.

You can specify the language code for all your documents in your data source when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. If a document doesn't have a language code specified in a metadata field, the document is indexed using the language code specified for all documents at the data source level\. In the console, you can index documents in a supported language only at the data source level\. Go to **Data sources**, then the **Specify data source details** page, and choose a language from the dropdown **Language**\.

The following languages and their codes are supported \(English or `en` is supported by default if you don't specify a language\):


| **Language name** | **Language code** | 
| --- | --- | 
| Arabic | ar | 
| Armenian | hy | 
| Basque | eu | 
| Bengali | bn | 
| Bulgarian | bg | 
| Catalan | ca | 
| Chinese \(simplified and traditional\) | zh | 
| Czech | cs | 
| Danish | da | 
| Dutch | nl | 
| Finnish | fi | 
| French | fr | 
| Galician | gl | 
| German | de | 
| Greek | el | 
| Hindi | hi | 
| Hungarian | hu | 
| Indonesian | id | 
| Irish | ga | 
| Italian | it | 
| Japanese | ja | 
| Korean | ko | 
| Latvian | lv | 
| Lithuanian | lt | 
| Norwegian | no | 
| Persian | fa | 
| Portuguese | pt | 
| Portuguese \(Brazil\) | pt\-BR | 
| Romanian | ro | 
| Russian | ru | 
| Sorani | ckb | 
| Spanish | es | 
| Swedish | sv | 
| Turkish | tr | 

Not all Amazon Kendra features are currently available for languages other than English\. The following features aren't available for non\-English indexes:
+ Semantic search of [FAQs](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html) and extracted answers from documents\. Keyword search is used for retrieving relevant FAQs and for document ranking\.
+ [Synonyms](https://docs.aws.amazon.com/kendra/latest/dg/index-synonyms.html), including custom synonyms for domain specific or specialized terms\.
+ [Query suggestions](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions-overview.html) of popular queries relevant to a search\.
+ [Confidence ranks](https://docs.aws.amazon.com/kendra/latest/dg/API_ScoreAttributes.html) of the search results\.