--------

--------

# Deploying Amazon Kendra<a name="deploying"></a>

When it comes time to deploy Amazon Kendra search to your website, we provide source code that you can use with React to get a head start on your application\. The source code is provided with no charge under a modified MIT license\. You can use it as is or change it for your own needs\. The provided React app is an example to help you get started\. It's not a production ready app\.

To deploy a search application with no code and generate an endpoint URL to your search page with access control, see [Amazon Kendra Experience Builder](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

There are two examples you can use with React:
+ [https://kendrasamples\.s3\.amazonaws\.com/kendrasamples\-react\-app\.zip](https://kendrasamples.s3.amazonaws.com/kendrasamples-react-app.zip)—An example React application that provides sample data and a search page\.
+ [https://kendrasamples\.s3\.amazonaws\.com/kendrasamples\.zip](https://kendrasamples.s3.amazonaws.com/kendrasamples.zip)—A library that you can add to an existing React application\. 

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
+ [Building a search experience with no code](deploying-search-experience-no-code.md)

## Overview<a name="example-overview"></a>

You add the example code to an existing React application to activate search\. The search files and components are structured as follows:
+ Main search page—This is the main page that contains all of the components\. This is where you will integrate your application with the Amazon Kendra API\.
+ Search bar—This is the component where a user enters a search term and that calls the search function\.
+ Results—This is the component that displays the results from Amazon Kendra\. It has three components: Suggested answers, FAQ results, and recommended documents\.
+ Facets—This is the component that shows the facets in the search results and allows you to choose a facet to limit the search\.
+ Pagination—This is the component that paginates the response from Amazon Kendra\.

## Prerequisites<a name="example-prereqs"></a>

Before you begin, you need the following:
+ An existing React Web application or the example application\.
+ A development environment configured with the correct libraries\.
+ Node\.js and npm [installed](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)\.
+ The SDK for Java or AWS SDK for JavaScript\.

Information about the required libraries and AWS SDKs is in the Readme file in the zip files\.

## Setting up the example<a name="example-install"></a>

A complete procedure for adding Amazon Kendra search to a React application is in the Readme included in the example zip files\.

**To get started using kendra\-samples\-react\-app\.zip**

1. Make sure you have completed the [Prerequisites](#example-prereqs), including downloading and installing Node\.js and npm\.

1. Download kendra\-samples\-react\-app\.zip and unzip\.

1. Open your terminal and go to `aws-kendra-sample-app/src/services/`\. Open `local-dev-credentials-template.json` and provide your credentials\. Do not add this file to any public repository\.

1. Go to `aws-kendra-sample-app/src` and install the dependencies\. Run `npm install`\.

1. Launch a demo version of your app on your local server\. Run `npm start`\. You can stop the local server by entering on your keyboard `Cmd/Ctrl + C`\.

1. You can change the port or host \(for example, IP address\) by going to `package.json` and update the host and port: `"start": "HOST=[host] PORT=[port] react-scripts start"`\. If you use Windows: `"start": "set HOST=[host] && set PORT=[port] && react-scripts start"`\.

1. If you have a registered website domain, you can specify this in `package.json` after your app name\. For example, `"homepage": "https://mywebsite.com"`\. You must run `npm install` again to update new dependencies, and then run `npm start`\.

1. To build the app, run `npm build`\. Upload the contents of the build directory to your hosting provider\.
**Warning**  
The React app is **not** production ready\. It's an example of deploying an app for Amazon Kendra search\.

## Main search page<a name="main-component"></a>

The main search page contains all of the example search components\. It includes the search bar component for output, the results components to display the response from the [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API, and a pagination component for paging through the response\.

## Search component<a name="search-component"></a>

The search component provides a text box to enter query text\. The `onSearch` function is a hook that calls the main function in `Search.tsx` to make the Amazon Kendra [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) API call\.

## Results component<a name="results-component"></a>

The results component shows the response from the `Query` API\. The results are shown in three separate areas\.
+ Suggested answers—These are the top results returned by the `Query` API\. It contains up to three suggested answers\. In the response, they have the result type `ANSWER`\.
+ FAQ answers—These are the frequently asked questions results returned by the response\. FAQs are added to the index separately\. In the response, they have the type `QUESTION_ANSWER`\. For more information, see [Questions and answers](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html)\. 
+ Recommended documents—These are additional documents that Amazon Kendra returns in the response\. In the response from the `Query` API, they have the type `DOCUMENT`\.

The results components share a set of components for features like highlighting, titles, links, and more\. The shared components must be present for the result components to work\. 

## Facets component<a name="facets-component"></a>

The facets component lists the facets available in the search results\. Each facet classifies the response along a specific dimension, such as author\. You can refine the search to a specific facet by choosing one from the list\.

After you select a facet, the component calls `Query` with an attribute filter that restricts the search to documents that match the facet\.

## Pagination component<a name="pagination-component"></a>

The pagination component allows you to display the search results from the `Query` API in multiple pages\. It calls the `Query` API with the `PageSize` and `PageNumber` parameters to get a specific page of results\.