--------

--------

# Types of documents<a name="index-document-types"></a>

An index can contain multiple documents and multiple types of documents\. An index can also include both structured and unstructured text\.

## Structured text<a name="index-structured-text"></a>
+ Frequently asked questions and answers

Frequently asked question and answer format documents are used to answer questions such as *How tall is the Space Needle?* You can specify multiple questions that return the same answer\. You specify the questions and answers in a comma\-separated values \(CSV\) file stored in an Amazon S3 bucket\. 

If you want to use a JSON file for your set of frequently asked questions and answers, JSON files are treated as plain text and is a type of unstructured text\.

For an example, see [Adding questions and answers directly to an index](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html)\.

## Unstructured text<a name="index-unstructured-text"></a>

Amazon Kendra supports the following types of unstructured text:
+ HTML files
+ Microsoft PowerPoint \(PPT\) presentations
+ MS WORD documents
+ Plain text documents
+ PDFs
+ Comma Separated Values \(CSV\) files
+ Microsoft Excel \(MS EXCEL\) files
+ XML files
+ JSON files
+ Markdown Documentation \(MD\) files
+ Rich Text Format \(RTF\) files
+ Extensible Stylesheet Language Transformation \(XSLT\) files

You can add unstructured documents to your index in three ways:
+ Using the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API\.
+ As a data source\. For more information, see [Adding documents from a data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source.html)\.
+ As binary data\. For more information, see [Adding documents with the API](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-binary-doc.html)\.