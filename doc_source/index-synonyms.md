--------

--------

# Adding synonyms to an index<a name="index-synonyms"></a>

To add synonyms to an index, you specify them in a thesaurus file\. You can create synonyms to make it easier to find information in your documents\. Synonyms can also help keep your search results organized\. Amazon Kendra supports synonyms for `DOCUMENT` result types\. Synonyms are not currently applied to `QUESTION_ANSWER` or `ANSWER` result types\. 

Amazon Kendra provides different results based on your synonyms\. For example, using the synonym pair `Dynamo, Amazon DynamoDB`, Amazon Kendra correlates Dynamo with Amazon DynamoDB\. The query "What is dynamo?" then returns a document such as "What is Amazon DynamoDB?"\. With synonyms, Amazon Kendra can more easily pick up the correlation\. 

Synonyms can be useful in the following scenarios: 
+ Specialized terms that are not traditional English language synonyms such as `NLP, Natural Language Processing`\. 
+ Proper nouns with complex semantic associations\. These are nouns that the general public are unlikely to understand, for example, in machine learning, `cost, loss, model performance`\.  
+ Different forms of product names, for example, `Elastic Compute Cloud, EC2`\.
+ Domain\-specific concept terms for product names, for example, `Route53, DNS`\. 

Do not use synonyms in the following scenarios:
+ Generic English language synonyms such as `leader, head`\. These synonyms are not domain\-specific,and using synonyms in these scenarios might have unintended effects\. 
+ Typographical errors such as `teh => the`\. 
+ Morphological variants like the plurals and possessives of nouns, the comparative and superlative form of adjectives, and the past tense, past participle and progressive form of verbs\. One example of comparative and superlative adjectives is `good, better, best`\. 
+ Unigram \(single word\) stop words such as `WHO`\. Unigram stop words are not allowed in the thesaurus and are excluded from search\. For example, `WHO => World Health Organization` is rejected\. You can use `W.H.O.` however as a synonym term, and you can use stop words as part of a multi\-word synonym\. For example, `of` is not allowed but `United States of America` is accepted\. 

The thesaurus file uses the [Solr synonym format](https://lucene.apache.org/solr/guide/6_6/filter-descriptions.html#FilterDescriptions-SynonymGraphFilter)\. Each Amazon Kendra index can have a single thesaurus file\. 

**Topics**
+ [Creating a thesaurus file](index-synonyms-creating-thesaurus-file.md)
+ [Adding a thesaurus to an index](index-synonyms-adding-thesaurus-file.md)
+ [Updating a thesaurus](index-synonyms-update.md)
+ [Deleting a thesaurus](index-synonyms-delete.md)
+ [Toggling highlights in search results](index-synonyms-enabling-synonyms-in-results.md)