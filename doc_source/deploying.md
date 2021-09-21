--------

--------

# Deploying Amazon Kendra<a name="deploying"></a>

When it comes time to deploy Amazon Kendra search to your website, we provide source code that you can use with React to get a head start on your application\. The source code is provided free of charge under a modified MIT license so that you can use it as is or change it for your own needs\. There are two examples:
+ [https://kendrasamples\.s3\.amazonaws\.com/kendrasamples\-react\-app\.zip](https://kendrasamples.s3.amazonaws.com/kendrasamples-react-app.zip) – An example React application that provides sample data and a search page\.
+ [https://kendrasamples\.s3\.amazonaws\.com/kendrasamples\.zip](https://kendrasamples.s3.amazonaws.com/kendrasamples.zip) – A library that you can add to an existing React application\. 

The examples are modeled after the search page of the Amazon Kendra console\. They have the same features for searching and displaying search results\. You can use the whole example, or you can choose just one of the features for your own use\.

To see the three components of the search page in the Amazon Kendra console, choose the code icon \(**</>**\) from the right menu\. Hover your pointer over each section to see a brief description of the component and to get the URL of the component's source\.

**Topics**
+ [Overview](#example-overview)
+ [Prerequisites](#example-prereqs)
+ [Setting up the example](#example-install)
+ [Main search page](#main-component)
+ [Search component](#search-component)
+ [Results component](#results-component)
+ [Facets component](#facets-component)
+ [Pagination component](#pagination-component)

## Overview<a name="example-overview"></a>

You add the example code to an existing React application to enable search\. The search files and components are structured as follows:
+ Main search page – this is the main page that contains all of the components\. This is where you will integrate your application with the Amazon Kendra API\.
+ Search bar – this is the component where a user enters a search term and that calls the search function\.
+ Results – this is the component that displays the results from Amazon Kendra\. It has three components: Suggested answers, FAQ results, and recommended documents\.
+ Facets – This is the component that shows the facets in the search results and enables you to choose a facet to limit the search\.
+ Pagination – this is the component that paginates the response from Amazon Kendra\.

## Prerequisites<a name="example-prereqs"></a>

Before you begin you need the following:
+ An existing React Web application or the example application\.
+ A development environment configured with the correct libraries\.
+ The SDK for Java or AWS SDK for JavaScript\.

Information about the required libraries and AWS SDKs is in the Readme file in the \.zip files\.

## Setting up the example<a name="example-install"></a>

A complete procedure for adding Amazon Kendra search to a React application is in the Readme included in the example zip files\.

## Main search page<a name="main-component"></a>

<<<<<<< HEAD
The main search page contains all of the example search components\. It includes the search bar component for output, the results components to display the response from the [ Query ](API_Query.md) operation, and a pagination component that enables you to page through the response\.

## Search component<a name="search-component"></a>

The search component provides a text box to enter query text\. The `onSearch` function is a hook that calls the main function in `Search.tsx` to make the Amazon Kendra [ Query ](API_Query.md) operation call\.
=======
The main search page contains all of the example search components\. It includes the search bar component for output, the results components to display the response from the [Query](API_Query.md) operation, and a pagination component that enables you to page through the response\.

## Search component<a name="search-component"></a>

The search component provides a text box to enter query text\. The `onSearch` function is a hook that calls the main function in `Search.tsx` to make the Amazon Kendra [Query](API_Query.md) operation call\.
>>>>>>> parent of 2b1c178 (updating tutorial)

## Results component<a name="results-component"></a>

The results component shows the response from the `Query` operation\. The results are shown in three separate areas\.
+ Suggested answers – These are the top results returned by the `Query` operation\. It contains up to three suggested answers\. In the response, they have the result type `ANSWER`\.
+ FAQ answers – These are the frequently asked questions results returned by the response\. FAQs are added to the index separately\. In the response, they have the type `QUESTION_ANSWER`\. For more information, see [Adding questions and answers directly to an index](in-creating-faq.md)\. 
+ Recommended documents – These are additional documents that Amazon Kendra returns in the response\. In the response from the `Query` operation, they have the type `DOCUMENT`\.

The results components share a set of components for features like highlighting, titles, links, etc\. The shared components must be present for the result components to work\. 

## Facets component<a name="facets-component"></a>

The facets component lists the facets available in the search results\. Each facet classifies the response along a specific dimension, such as author\. You can refine the search to a specific facet by choosing one from the list\.

After you select a facet, the component calls the `Query` operation with an attribute filter that restricts the search to only those documents that match the facet\.

## Pagination component<a name="pagination-component"></a>

The pagination component enables you to display the search results from the `Query` operation in multiple pages\. It calls the `Query` operation with the `PageSize` and `PageNumber` parameters to get a specific page of results\.