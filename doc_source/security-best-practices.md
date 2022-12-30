--------

--------

# Security best practices<a name="security-best-practices"></a>

Amazon Kendra provides a number of security features to consider as you develop and implement your own security policies\. The following best practices are general guidelines and don't represent a complete security solution\. Because these best practices might not be appropriate or sufficient for your environment, treat them as helpful considerations rather than prescriptions\.

## Apply principle of least privilege<a name="security-least-privilege"></a>

Amazon Kendra provides a granular access policy for applications using IAM roles\. We recommend that the roles be granted only the minimum set of privileges required by the job, such as covering your application and access to log destination\. We also recommend auditing the jobs for permissions on a regular basis and upon any change to your application\.

## Role\-based access control \(RBAC\) permissions<a name="security-practice-rbac"></a>

Administrators should strictly control Role\-based access control \(RBAC\) permissions for Amazon Kendra applcations\.