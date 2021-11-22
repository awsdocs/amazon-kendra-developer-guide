--------

--------

# Adding documents in languages other than English<a name="in-adding-languages"></a>

You can index documents in multiple languages\. If you do not specify a language, Amazon Kendra indexes documents in English by default\. You include the language code for a document in the document metadata as a field \- see information on [field mappings](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html) and [custom attributes](https://docs.aws.amazon.com/kendra/latest/dg/custom-attributes.html) to include `_language_code` for a document\.

You can specify the language code for all your documents in your data source when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. If a document does not have a language code specified in a metadata field, the document is indexed using the language code specified for all documents at the data source level\. In the console, you can index documents in a supported language only at the data source level\. Go to **Data sources**, then the **Specify data source details** page, and choose a language from the dropdown **Language**\.

You can index a FAQ in a supported language\. Amazon Kendra indexes FAQs in English by default if you do not specify a language\. You specify the language code when you call the [CreateFaq](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateFaq.html) operation or you can include the language code for a FAQ in the FAQ metadata as a field\. If a FAQ does not have a language code in its metadata specified in a metadata field, the FAQ is indexed using the language code specified when you call the `CreateFAQ` operation\. To index a FAQ document in a supported language in the console, go to **FAQs** and select **Add FAQ**\. You choose a language from the dropdown **Languages** and select **Add**\.

The following languages and their codes are supported \(English or `en` is supported by default if you do not specify a language\):


| **Language name** | **Language code** | 
| --- | --- | 
| Spanish | es | 
| French | fr | 
| German | de | 
| Portuguese | pt | 
| Japanese | ja | 
| Korean | ko | 
| Chinese | zh | 
| Italian | it | 
| Hindi | hi | 
| Arabic | ar | 
| Armenian | hy | 
| Basque | eu | 
| Bengali | bn | 
| Brazilian | pt\-BR | 
| Bulgarian | bg | 
| Catalan | ca | 
| Czech | cs | 
| Danish | da | 
| Dutch | nl | 
| Finnish | fi | 
| Galician | gl | 
| Greek | el | 
| Hungarian | hu | 
| Indonesian | id | 
| Irish | ga | 
| Latvian | lv | 
| Lithuanian | lt | 
| Norwegian | no | 
| Persian | fa | 
| Romanian | ro | 
| Russian | ru | 
| Sorani | ckb | 
| Swedish | sv | 
| Turkish | tr | 

Not all Amazon Kendra features are currently available for languages other than English\. The following features are not available for non\-English indexes:
+ Semantic search of [FAQs](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html) and extracted answers from documents\. Keyword search is used for retrieving relevant FAQs and for document ranking\.
+ [Custom synonyms](https://docs.aws.amazon.com/kendra/latest/dg/index-synonyms.html) for domain\-specific, business\-specific, or specialized terms\.
+ [Query suggestions](https://docs.aws.amazon.com/kendra/latest/dg/query-suggestions-overview.html) of popular queries relevant to a search\.
+ [Confidence scores](https://docs.aws.amazon.com/kendra/latest/dg/API_ScoreAttributes.html) in the search results\.