--------

--------

# Building a search experience with no code<a name="deploying-search-experience-no-code"></a>

You can build and deploy an Amazon Kendra search application without the need for any front\-end code\. Amazon Kendra *Experience Builder* helps you build and deploy a fully functional search application in a few clicks so that you can start searching right away\. You can custom design your search page and tune your search to tailor the experience to your users' needs\. Amazon Kendra generates a unique, fully hosted endpoint URL of your search page to start searching your documents and FAQs\. You can quickly build a proof of concept of your search experience and share it with others\.

You use the search experience template available in the builder to customize your search\. You can invite others to collaborate in building your search experience, or evaluate search results for tuning purposes\. Once your search experience is ready for your users to start searching, you simply share the secure endpoint URL\.

## How the search Experience Builder works<a name="how-search-experience-builder-works"></a>

The overall process of building a search experience is as follows:

1. You create your search experience by giving it a name, description, and choosing your data sources you want to use for your search experience\.

1. You configure your list of users and groups in AWS IAM Identity Center \(successor to AWS Single Sign\-On\) and then assign them access rights to your search experience\. You include yourself as an owner of the experience\. For more information, see [Providing access to your search page](#access-search-experience)\.

1. You open the Amazon Kendra Experience Builder to design and tune your search page\. You can share your endpoint URL of your search experience with others who you assign own\-edit access rights or view\-search access rights\.

You call the [CreateExperience](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateExperience.html) API to create and configure your search experience\. If you use the console, you select your index and then select and **Experiences** in the navigation menu to configure your experience\.

## Design and tune your search experience<a name="design-tune-search-experience"></a>

Once you create and configure your search experience, you open the search experience using an endpoint URL to start customizing your search as an owner with editor access rights\. You type your query into the search box, then customize your search using the editing options on the side panel to see how they apply to your page\. When you are ready to publish, select **Publish**\. You can also toggle between **Switch to live view**, to view the latest published version of your search page, and **Switch to build mode**, to edit or customize your search page\.

The following are ways you can customize your search experience\.

### Filter<a name="search-experience-filter"></a>

Add faceted search or filter by document attributes\. This includes custom attributes\. You can add a filter using your own configured metadata fields\. For example, to facet search by each city category, use a `_category` custom document attribute that contains all the city categories\.

### Suggested answer<a name="search-experience-suggested-answer"></a>

Add machine learning generated answers to your users' queries\. For example, *'How difficult is this course?'*\. Amazon Kendra can retrieve the most relevant text across all documents referring to a course's difficultly and suggest the most relevant answer\.

### FAQ<a name="search-experience-faq"></a>

Add a FAQ document to provide answers to frequently asked questions\. For example, *'How many hours to complete this course?'*\. Amazon Kendra can use the FAQ document containing the answer to this question and give the correct answer\.

### Sort<a name="search-experience-sort"></a>

Add sorting of the search results so that your users can organize the results by relevancy, created time, last updated time, and other sorting criteria\.

### Documents<a name="search-experience-documents"></a>

Configure how documents or search results are displayed on your search page\. You can configure how many results display on the page, include pagination such as page numbers, enable a user feedback button, and arrange how document metadata fields are displayed in a search result\.

### Language<a name="search-experience-language"></a>

Select a language to filter the search results or documents in the selected language\.

### Search box<a name="search-experience-search-box"></a>

Configure the size and placeholder text of your search box, as well as enable query suggestions\.

### Relevance tuning<a name="search-experience-relevance-tuning"></a>

Add boosting to document metadata fields to place more weight on these fields when your users search for documents\. You can add a weight that starts at 1 and incrementally increases to 10\. You can boost text, date, and numeric field types\. For example, to give `_last_updated_at` and `_created_at` more weight or importance than other fields, give these fields a weight of 1 to 10, depending on their importance\. You can apply different relevance tuning configurations for each search application or experience\.

## Providing access to your search page<a name="access-search-experience"></a>

Access to your search experience is through IAM Identity Center\. When you configure your search experience, you grant other people listed in your Identity Center directory access to your Amazon Kendra search page\. They receive an email that directs them to sign in using their credentials in IAM Identity Center to access the search page\. You must set up IAM Identity Center at the organization level or account holder level in AWS Organizations\. For more information on setting up IAM Identity Center, see [Getting started with IAM Identity Center](https://docs.aws.amazon.com/kendra/latest/dg/getting-started-aws-sso.html)\.

You enable user identities in IAM Identity Center with your search experience and assign *Viewer* or *Owner* access permissions using the API or the console\.
+ **Viewer**: Allowed to issue queries, receive suggested answers relevant to their search, and contribute their feedback to Amazon Kendra so that it keeps improving the search\.
+ **Owner**: Allowed to customize the design of the search page, tune the search, and use the search application as a *Viewer*\. Disabling access to viewers in the console is currently not supported\.

To assign other people access to your search experience, you first enable user identities in IAM Identity Center with your Amazon Kendra experience by using the [ExperienceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ExperienceConfiguration.html) object\. You specify the field name that contains the identifiers of your users such as user name or email address\. You then grant your list of users access to your search experience using the [AssociateEntitiesToExperience](https://docs.aws.amazon.com/kendra/latest/dg/API_AssociateEntitiesToExperience.html) API and define their permissions as *Viewer* or *Owner* using the [AssociatePersonasToEntities](https://docs.aws.amazon.com/kendra/latest/dg/API_AssociatePersonasToEntities.html) API\. You specify each user or group using the [EntityConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_EntityConfiguration.html) object and whether that user or group is a *Viewer* or *Owner* using the [EntityPersonaConfiguraton](https://docs.aws.amazon.com/kendra/latest/dg/API_EntityPersonaConfiguration.html) object\.

To assign other people access to your search experience using the console, you first need to create an experience and confirm your identity and that you are an owner\. Then you can assign other users or groups as viewers or owners\. In the console, select your index and then select **Experiences** in the navigation menu\. After you create your experience, you can select your experience from the list\. Go to **Access management** to assign users or groups as viewers or owners\.

## Configuring a search experience<a name="config-search-experience"></a>

The following is an example of configuring or creating a search experience\.

------
#### [ Console ]

**To create an Amazon Kendra search experience**

1. In the left navigation pane, under **Indexes**, select **Experiences** and then select **Create experience**\.

1. On the **Configure experience** page, enter a name and description for your experience, choose your content sources, and choose the IAM role for your experience\. For more information on IAM roles, see [IAM roles for Amazon Kendra experiences](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.

1. On the **Confirm your identity from an Identity Center directory** page, select your user ID such as your email\. If you do not have an Identity Center directory, simply enter your full name and email to create an Identity Center directory\. This includes you as a user of the experience and automatically assigns you owner access rights\.

1. On the **Review to open Experience Builder** page, review your configuration details and select **Create experience and open Experience Builder** to start editing your search page\.

------
#### [ CLI ]

**To create an Amazon Kendra experience**

```
aws kendra create-experience \
 --name experience-name \
 --description "experience description" \
 --index-id index-id \
 --role-arn arn:aws:iam::account-id:role/role-name \
 --configuration '{"ExperienceConfiguration":[{"ContentSourceConfiguration":{"DataSourceIds":["data-source-1","data-source-2"]}, "UserIdentityConfiguration":"identity attribute name"}]}' 

aws kendra describe-experience \
 --endpoints experience-endpoint-URL(s)
```

------
#### [ Python ]

**To create an Amazon Kendra experience**

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Create an experience.")

# Provide a name for the experience
name = "experience-name"
# Provide an optional description for the experience
description = "experience description"
# Provide the index ID for the experience
index_id = "index-id"
# Provide the IAM role ARN required for Amazon Kendra experiences
role_arn = "arn:aws:iam::${account-id}:role/${role-name}"
# Configure the experience
configuration = {"ExperienceConfiguration":
        [{
            "ContentSourceConfiguration":{"DataSourceIds":["data-source-1","data-source-2"]},
            "UserIdentityConfiguration":"identity attribute name"
        }]
    }

try:
    experience_response = kendra.create_experience(
        Name = name,
        Description = description,
        IndexId = index_id,
        RoleArn = role_arn,
        Configuration = configuration
    )

    pprint.pprint(experience_response)

    experience_endpoints = experience_response["Endpoints"]

    print("Wait for Amazon Kendra to create the experience.")

    while True:
        # Get the details of the experience, such as the status
        experience_description = kendra.describe_experience(
            Endpoints = experience_endpoints
        )
        status = experience_description["Status"]
        print(" Creating experience. Status: "+status)
        time.sleep(60)
        if status != "CREATING":
            break

except  ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

**To create an Amazon Kendra**

```
package com.amazonaws.kendra;

import java.util.concurrent.TimeUnit;
import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.CreateExperienceRequest;
import software.amazon.awssdk.services.kendra.model.CreateExperienceResponse;
import software.amazon.awssdk.services.kendra.model.DescribeExperienceRequest;
import software.amazon.awssdk.services.kendra.model.DescribeExperienceResponse;
import software.amazon.awssdk.services.kendra.model.ExperienceStatus;


public class CreateExperienceExample {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("Create an experience");
        
        String experienceName = "experience-name";
        String experienceDescription = "experience description";
        String indexId = "index-id";
        String experienceRoleArn = "arn:aws:iam::account-id:role/role-name";

        KendraClient kendra = KendraClient.builder().build();
        
        CreateExperienceRequest createExperienceRequest = CreateExperienceRequest 
            .builder()
            .name(experienceName)
            .description(experienceDescription)
            .roleArn(experienceRoleArn)
            .configuration(
                ExperienceConfiguration
                    .builder()
                    .contentSourceConfiguration(
                        ContentSourceConfiguration(
                            .builder()
                            .dataSourceIds("data-source-1","data-source-2")
                            .build()
                        )
                    )
                    .userIdentityConfiguration(
                        UserIdentityConfiguration(
                            .builder()
                            .identityAttributeName("identity-attribute-name")
                            .build()
                        )
                    ).build()
            ).build();
        
        CreateExperienceResponse createExperienceResponse = kendra.createExperience(createExperienceRequest);
        System.out.println(String.format("Experience response %s", createExperienceResponse));

        String experienceEndpoints = createExperienceResponse.endpoints();

        System.out.println(String.format("Wait for Kendra to create the experience.", experienceEndpoints));
        while (true) {
            DescribeExperienceRequest describeExperienceRequest = DescribeExperienceRequest.builder().endpoints(experienceEndpoints).build();
            DescribeExperienceResponse describeEpxerienceResponse = kendra.describeExperience(describeExperienceRequest);
            ExperienceStatus status = describeExperienceResponse.status();
            TimeUnit.SECONDS.sleep(60);
            if (status != ExperienceStatus.CREATING) {
                break;
            }
        }

        System.out.println("Experience creation is complete.");
    }
}
```

------