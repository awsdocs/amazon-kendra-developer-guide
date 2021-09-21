--------

--------

# GroupMembers<a name="API_GroupMembers"></a>

A list of users or sub groups that belong to a group\. Users and groups are useful for filtering search results to different users based on their group's access to documents\.

## Contents<a name="API_GroupMembers_Contents"></a>

<<<<<<< HEAD
 ** MemberGroups **   <a name="Kendra-Type-GroupMembers-MemberGroups"></a>
A list of sub groups that belong to a group\. For example, the sub groups "Research", "Engineering", and "Sales and Marketing" all belong to the group "Company"\.  
Type: Array of [ MemberGroup ](API_MemberGroup.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 1000 items\.  
Required: No

 ** MemberUsers **   <a name="Kendra-Type-GroupMembers-MemberUsers"></a>
A list of users that belong to a group\. For example, a list of interns all belong to the "Interns" group\.  
Type: Array of [ MemberUser ](API_MemberUser.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 1000 items\.  
Required: No

 ** S3PathforGroupMembers **   <a name="Kendra-Type-GroupMembers-S3PathforGroupMembers"></a>
If you have more than 1000 users and/or sub groups for a single group, you need to provide the path to the S3 file that lists your users and sub groups for a group\. Your sub groups can contain more than 1000 users, but the list of sub groups that belong to a group \(and/or users\) must be no more than 1000\.  
You can download this [example S3 file](https://docs.aws.amazon.com/kendra/latest/dg/samples/group_members.zip) that uses the correct format for listing group members\. Note, `dataSourceId` is optional\. The value of `type` for a group is always `GROUP` and for a user it is always `USER`\.  
Type: [ S3Path ](API_S3Path.md) object  
=======
 **MemberGroups**   <a name="Kendra-Type-GroupMembers-MemberGroups"></a>
A list of sub groups that belong to a group\. For example, the sub groups "Research", "Engineering", and "Sales and Marketing" all belong to the group "Company"\.  
Type: Array of [MemberGroup](API_MemberGroup.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 1000 items\.  
Required: No

 **MemberUsers**   <a name="Kendra-Type-GroupMembers-MemberUsers"></a>
A list of users that belong to a group\. For example, a list of interns all belong to the "Interns" group\.  
Type: Array of [MemberUser](API_MemberUser.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 1000 items\.  
Required: No

 **S3PathforGroupMembers**   <a name="Kendra-Type-GroupMembers-S3PathforGroupMembers"></a>
If you have more than 1000 users and/or sub groups for a single group, you need to provide the path to the S3 file that lists your users and sub groups for a group\. Your sub groups can contain more than 1000 users, but the list of sub groups that belong to a group \(and/or users\) must be no more than 1000\.  
Type: [S3Path](API_S3Path.md) object  
>>>>>>> parent of 2b1c178 (updating tutorial)
Required: No

## See Also<a name="API_GroupMembers_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GroupMembers) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GroupMembers) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GroupMembers) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GroupMembers) 