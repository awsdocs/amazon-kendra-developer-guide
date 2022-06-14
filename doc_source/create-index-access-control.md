--------

--------

# Controlling access to documents in an index<a name="create-index-access-control"></a>

Amazon Kendra supports token\-based user access control using the following token types:
+ Open ID
+ JWT with a shared secret
+ JWT with a public key
+ JSON

Amazon Kendra delivers highly secure enterprise search for your search applications\. Your search results reflect the security model of your organization\. Customers are responsible for authenticating and authorizing users to gain access to their search application\. At search time, the Amazon Kendra service filters search results based on user ID provided by the customer's search application, and document ACLs collected by the Amazon Kendra connectors during crawl/indexing time\. The search results return URLs pointing back to the original document repositories plus short excerpts\. Access to the full document is still enforced by the original repository\. 

**Topics**
+ [Using OpenID](create-index-access-control-tokens-openid.md)
+ [Using a JSON Web Token \(JWT\) with a shared secret](create-index-access-control-tokens-jwtshared.md)
+ [Using a JSON Web Token \(JWT\) with a public key](create-index-access-control-tokens-jwtpublic.md)
+ [Using JSON](create-index-access-control-tokens-json.md)