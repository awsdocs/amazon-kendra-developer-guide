--------

--------

# Creating a thesaurus file<a name="index-synonyms-creating-thesaurus-file"></a>

An Amazon Kendra thesaurus file is a UTF\-8\-encoded file containing a list of synonyms in the Solr synonym list format\. Synonyms are case sensitive\. The thesaurus file must be less than 5 MB\. 

There are two ways to specify synonym mappings:
+ *Bidirectional synonyms* are specified as a comma\-separated list of terms\. If the token matches any of the terms, then all the terms in the list are substituted, which includes the original token\. 
+ *Unidirectional synonyms* are specified as two comma\-separated lists of terms with the symbol "=>" between them\. If the token matches any word on the left, then the list on the right is substituted\. Mapping is only from the left to the right\. 

The following example shows a thesaurus file with synonyms for the sample AWS documentation for Amazon Kendra\. Each line contains a single synonym rule\. A synonym does not do an exact match on special characters\. For example, if you search for `dead-letter-queue`, Kendra matches documents with the phrase `dead letter queue`\. Blank lines and comments are ignored\. 

```
# Lines starting with pound are comments and blank lines are ignored.

# Synonym relationships can be defined as unidirectional or bidirectional relationships.

# Unidirection relationships are represented by any term sequence 
# on the left hand side (LHS) of "=>" followed by synonyms on the right hand side (RHS)
CodeStar => AWS CodeStar
# This will map CodeStar to AWS CodeStar, but not vice-versa

# Multiple synonym relationships may be defined in one line as well by comma seperation.
autoscaling group, ASG => Auto Scaling group, autoscaling
# The above is equivalent to:
# autoscaling group => Auto Scaling group, autoscaling
# ASG => Auto Scaling group, autoscaling

# Bi-directional synonyms are comma separated terms with no "=>"
DNS, Route53, Route 53
# DNS, Route53, and Route 53 map to one another and are interchangeable at match time
# The above is equivalent to:
# DNS => Route53, Route 53
# Route53 => DNS, Route 53
# Route 53 => DNS, Route53

# Overlapping LHS terms will be merged
Beta => Alpha
Beta => Gamma
Beta, Delta
# is equivalent to:
# Beta => Alpha, Gamma, Delta
# Delta => Beta

# Synonym rule count is the total number of lines defining synonym relationships
# Term count is the total number of unique terms for all rules. 
# This thesaurus has a synonym rule count of 6 and a term count of 18. 
# Comments and blanks lines do not count.
```

This example has 6 rules and 18 terms\. Each line contains a single synonym rule\. Blank lines and comments are ignored\. Some rules are ignored\. For example, `a => b` is a rule, but `a => a` is ignored and does not count as a rule\. A synonym does not do an exact match on special characters\. For example, if you search for `dead-letter-queue`, Amazon Kendra will match document containing `dead letter queue` \(no hyphen\)\. You can have a maximum of 10,000 synonym rules per thesaurus\. 

The term count is the number of unique terms in the theaurus file\. This example has the following terms: `AWS CodeStar`, `autoscaling group`, `asg`, `Auto Scaling group`, `autoscaling`, `DNS`, `Route53`, `Route 53`, `dns`, `route53`, `route 53`, `beta`, `Alpha`, `Gamma`, `Delta`, and `delta`\. You can have up to 10 synonyms per term\. 

For more information about Amazon Kendra quotas, see [Quotas for Amazon Kendra](quotas.md)\. 
