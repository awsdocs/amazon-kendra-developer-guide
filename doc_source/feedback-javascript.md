--------

--------

# Using the Amazon Kendra JavaScript library to submit feedback<a name="feedback-javascript"></a>

Amazon Kendra provides a JavaScript library that you can use to add click feedback to your search results page\. To use the library, you insert a script tag in your client code that displays the search result, then add information to each of the document links in your result list\. When a user chooses a link to view a document, click information is sent to Amazon Kendra\.

The library works with browsers that support JavaScript version ES6/ES2015\.

## Step 1: Insert a script tag into your Amazon Kendra search application<a name="javascript-step-1"></a>

In your client code that renders the Amazon Kendra search results, insert a <script> tag and add a reference to the JavaScript library:

```
<script>
 (function(w, d, s, c, g, n) {
   if(!w[n]) {
     w[n] = w[n] || function () {
           (w[n].q = w[n].q || []).push(arguments);
     }
     w[n].st = new Date().getTime();
     w[n].ep = g;
     var e = document.createElement(s),
         j = document.getElementsByTagName(s)[0];
     e.async = 1;
     e.src = c;
     e.type = 'module';
     j.parentNode.insertBefore(e, j);
   }
 })(window, document, 'script', 
 'library download URL', 
 'feedback endpoint',
 'kendraFeedback');
</script>
```

The script asynchronously downloads the JavaScript library from an Amazon Kendra hosted CDN and initializes a global variable called `kendraFeedback` that enables you to set optional parameters\.

Replace *library download URL* and *feedback endpoint* with an identifier from the following table based on the region that hosts your Amazon Kendra index\.


| Region | Download URL | Feedback endpoint | 
| --- | --- | --- | 
| us\-east\-1 | https://d2zm0lpns956f8\.cloudfront\.net/ksf\-v1\.js | https://ujxwp5s92h\.execute\-api\.us\-east\-1\.amazonaws\.com/prod/submit | 
| us\-east\-2 |  https://d2crv7fufeg244\.cloudfront\.net/ksf\-v1\.js | https://i6h76zwzf3\.execute\-api\.us\-east\-2\.amazonaws\.com/prod/submit | 
| us\-west\-2 | https://d2iezfpnpcoujy\.cloudfront\.net/ksf\-v1\.js | https://wg6nim909c\.execute\-api\.us\-west\-2\.amazonaws\.com/prod/submit | 
| ca\-central\-1 | https://d1zbkfomowykaq\.cloudfront\.net/ksf\-v1\.js | https://budi8txevj\.execute\-api\.ca\-central\-1\.amazonaws\.com/prod/submit | 
| eu\-west\-1 | https://d3gptlxtulu4us\.cloudfront\.net/ksf\-v1\.js | https://po2b11740b\.execute\-api\.eu\-west\-1\.amazonaws\.com/prod/submit | 
| ap\-southeast\-1 | https://d1vvuam7g4taoe\.cloudfront\.net/ksf\-v1 | https://9je5uw7t5l\.execute\-api\.ap\-southeast\-1\.amazonaws\.com/prod/submit | 
| ap\-southeast\-2 | https://dopqntoe6z0ce\.cloudfront\.net/ksf\-v1\.js | https://oovf4nvjj7\.execute\-api\.ap\-southeast\-2\.amazonaws\.com/prod/submit | 

For example, if your index is in US East \(N\. Virginia\), *library download URL* is `https://d2zm0lpns956f8.cloudfront.net/ksf-v1.js` and *feedback endpoint* is `https://ujxwp5s92h.execute-api.us-east-1.amazonaws.com/prod/submit`\.

There are two optional settings that you can make for the Amazon Kendra JavaScript library:
+ `disableCookies` – By default, Amazon Kendra sets a cookie that uniquely identifies the user\. Set this to `true` to disable the cookie\.

  ```
  kendraFeedback('disableCookie', 'true | false');
  ```

  `searchDivClassName` – By default, Amazon Kendra monitors all links on your search results page for clicks\. Set this to a `<div>` class name to monitor only links in the specified class\.

  ```
  kendraFeedback('searchDivClassName', 'class name');
  ```

## Step 2: Add the feedback token to search results<a name="javascript-step-2"></a>

On your result page, add an HTML attribute called `data-kendra-token` to the anchor tag or immediate parent div tag that contains a link to the document from the query response\. For example:

```
<a href="document location" data-kendra-token="feedback token value"></a>
OR
<div data-url="document location" data-kendra-token="feedback token value"></div>
```

A query response contains a token in the `feedbackToken` field\. The token uniquely identifies the response if the user chooses it\. Assign the value of the token to the `data-kendra-token` attribute\. The Amazon Kendra JavaScript library looks for this token when the user chooses the result and submits it to an Amazon Kendra endpoint as feedback\.

The Amazon Kendra JavaScript library only submits the feedback token and other metadata such as the time the result was chosen and a unique visitor ID\.

## Step 3: Test the feedback script<a name="javascript-step-3"></a>

To make sure that the JavaScript library is configured correctly and sending feedback to the right endpoint, do the following\. This example uses the Chrome browser\.

1. Open the Web developer tools in the browser\. On Chrome, open the **Chrome menu** in the upper right corner of the browser, choose **More tools** and then choose **Developer tools**\.

1. Make sure that there are no errors related to the Amazon Kendra JavaScript library in the console tab\.

1. Make a search and choose any result\. In the **Network** tab of the developer tools\. You should see a request sent to the feedback endpoint, the token for the result, and a 200 OK status\.