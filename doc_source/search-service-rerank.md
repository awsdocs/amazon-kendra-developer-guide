--------

--------

# Semantically ranking a search service's results<a name="search-service-rerank"></a>

Amazon Kendra Intelligent Ranking uses Amazon Kendra's semantic search capabilities to re\-rank a search service's results\. It does this by taking into account the search query's intent and context, plus all the available information from the search service documents\. Amazon Kendra Intelligent Ranking can improve simple keyword matching\.

The [CreateRescoreExecutionPlan](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_CreateRescoreExecutionPlan.html) API creates an Amazon Kendra Intelligent Ranking resource used for provisioning the [Rescore](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_Rescore.html) API\. The `Rescore` API re\-ranks search results from a search service such as [OpenSearch \(self managed\)](https://docs.aws.amazon.com/kendra/latest/dg/opensearch-rerank.html)\.

When you call `CreateRescoreExecutionPlan`, you set your required capacity units for re\-ranking a search service's results\. If you don't need more capacity units beyond the single unit default, don't change the default\. Provide only a name for your rescore execution plan\. You can set up to 1000 extra units\. For information on what is included in a single capacity unit, see [Adjusting capacity](https://docs.aws.amazon.com/kendra/latest/dg/adjusting-capacity.html)\. Once you provision Amazon Kendra Intelligent Ranking, you are charged hourly based on your set capacity units\. See [free tier and pricing information](http://aws.amazon.com/kendra/intelligent-ranking-pricing/)\.

A rescore execution plan ID is generated and returned in the response when you call `CreateRescoreExecutionPlan`\. The `Rescore` API uses the rescore execution plan ID to re\-rank a search service's results using the capacity you set\. You include the rescore execution plan ID in the configuration files of your search service\. For example, if you use OpenSearch \(self managed\), you include the rescore execution plan ID in your docker\-compose\.yml or opensearch\.yml file—see [Intelligently ranking OpenSearch \(self service\) results](https://docs.aws.amazon.com/kendra/latest/dg/opensearch-rerank.html)\.

An Amazon Resource Name \(ARN\) is also generated in the response when you call `CreateRescoreExecutionPlan`\. You can use this ARN to create a permissions policy in AWS Identity and Access Management \(IAM\) to restrict user access to a specific ARN for a specific rescore execution plan\.

The following is an example of creating a rescore execution plan with capacity units set to 1\.

------
#### [ CLI ]

```
aws kendra-ranking create-rescore-execution-plan \
  --name MyRescoreExecutionPlan \ 
  --capacity-units '{"RescoreCapacityUnits":1}'
 
Response:
 
{
    "Id": "<rescore execution plan ID>",
    "Arn": "arn:aws:kendra-ranking:<region>:<account-id>:rescore-execution-plan/<rescore-execution-plan-id>"
}
```

------
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra_ranking = boto3.client("kendra-ranking")

print("Create a rescore execution plan.")

# Provide a name for the rescore execution plan
name = "MyRescoreExecutionPlan"
# Set your required additional capacity units
# Don't set capacity units if you don't require more than 1 unit given by default
capacity_units = 1

try:
    rescore_execution_plan_response = kendra_ranking.create_rescore_execution_plan(
        Name = name,
        CapacityUnits = {"RescoreCapacityUnits":capacity_units}
    )

    pprint.pprint(rescore_execution_plan_response)

    rescore_execution_plan_id = rescore_execution_plan_response["Id"]

    print("Wait for Amazon Kendra to create the rescore execution plan.")

    while True:
        # Get the details of the rescore execution plan, such as the status
        rescore_execution_plan_description = kendra_ranking.describe_rescore_execution_plan(
            Id = rescore_execution_plan_id
        )
        # When status is not CREATING quit.
        status = rescore_execution_plan_description["Status"]
        print(" Creating rescore execution plan. Status: "+status)
        time.sleep(60)
        if status != "CREATING":
            break

except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

```
import java.util.concurrent.TimeUnit;

import software.amazon.awssdk.services.kendraranking.KendraRankingClient;
import software.amazon.awssdk.services.kendraranking.model.CapacityUnitsConfiguration;
import software.amazon.awssdk.services.kendraranking.model.CreateRescoreExecutionPlanRequest;
import software.amazon.awssdk.services.kendraranking.model.CreateRescoreExecutionPlanResponse;
import software.amazon.awssdk.services.kendraranking.model.DescribeRescoreExecutionPlanRequest;
import software.amazon.awssdk.services.kendraranking.model.DescribeRescoreExecutionPlanResponse;
import software.amazon.awssdk.services.kendraranking.model.RescoreExecutionPlanStatus;

public class CreateRescoreExecutionPlanExample {

  public static void main(String[] args) throws InterruptedException {

    String rescoreExecutionPlanName = "MyRescoreExecutionPlan";
    int capacityUnits = 1;

    KendraRankingClient kendraRankingClient = KendraRankingClient.builder().build();

    System.out.println(String.format("Creating a rescore execution plan named %s", rescoreExecutionPlanName));

    CreateRescoreExecutionPlanResponse createResponse = kendraRankingClient.createRescoreExecutionPlan(
        CreateRescoreExecutionPlanRequest.builder()
            .name(rescoreExecutionPlanName)
            .capacityUnits(
                CapacityUnitsConfiguration.builder()
                    .rescoreCapacityUnits(capacityUnits)
                    .build()
            )
            .build()
    );

    String rescoreExecutionPlanId = createResponse.id();
    System.out.println(String.format("Waiting for rescore execution plan with id %s to finish creating.", rescoreExecutionPlanId));
    while (true) {
      DescribeRescoreExecutionPlanResponse describeResponse = kendraRankingClient.describeRescoreExecutionPlan(
          DescribeRescoreExecutionPlanRequest.builder()
              .id(rescoreExecutionPlanId)
              .build()
      );
      RescoreExecutionPlanStatus rescoreExecutionPlanStatus = describeResponse.status();
      if (rescoreExecutionPlanStatus != RescoreExecutionPlanStatus.CREATING) {
        break;
      }
      TimeUnit.SECONDS.sleep(60);
    }

    System.out.println("Rescore execution plan creation is complete.");
  }
}
```

------

The following is an example of updating a rescore execution plan to set capacity units to 2\.

------
#### [ CLI ]

```
aws kendra-ranking update-rescore-execution-plan \
  --id <rescore execution plan ID> \ 
  --capacity-units '{"RescoreCapacityUnits":2}'
```

------
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra_ranking = boto3.client("kendra-ranking")
                    
print("Update a rescore execution plan.")
                    
# Provide the ID of the rescore execution plan
id = <rescore execution plan ID>
# Re-set your required additional capacity units
capacity_units = 2
                        
try:
    kendra_ranking.update_rescore_execution_plan(
        Id = id,
        CapacityUnits = {"RescoreCapacityUnits":capacity_units}
    )
                        
    print("Wait for Amazon Kendra to update the rescore execution plan.")
                        
    while True:
        # Get the details of the rescore execution plan, such as the status
        rescore_execution_plan_description = kendra_ranking.describe_rescore_execution_plan(
            Id = id
        )
        # When status is not UPDATING quit.
        status = rescore_execution_plan_description["Status"]
        print(" Updating rescore execution plan. Status: "+status)
        time.sleep(60)
        if status != "UPDATING":
            break
                        
except ClientError as e:
        print("%s" % e)
                        
print("Program ends.")
```

------
#### [ Java ]

```
import java.util.concurrent.TimeUnit;

import software.amazon.awssdk.services.kendraranking.KendraRankingClient;
import software.amazon.awssdk.services.kendraranking.model.CapacityUnitsConfiguration;
import software.amazon.awssdk.services.kendraranking.model.DescribeRescoreExecutionPlanRequest;
import software.amazon.awssdk.services.kendraranking.model.DescribeRescoreExecutionPlanResponse;
import software.amazon.awssdk.services.kendraranking.model.RescoreExecutionPlanStatus;
import software.amazon.awssdk.services.kendraranking.model.UpdateRescoreExecutionPlanRequest;
import software.amazon.awssdk.services.kendraranking.model.UpdateRescoreExecutionPlanResponse;

public class UpdateRescoreExecutionPlanExample {

  public static void main(String[] args) throws InterruptedException {

    String rescoreExecutionPlanId = <rescore execution plan ID>;
    int newCapacityUnits = 2;

    KendraRankingClient kendraRankingClient = KendraRankingClient.builder().build();

    System.out.println(String.format("Updating a rescore execution plan named %s", rescoreExecutionPlanId));

    UpdateRescoreExecutionPlanResponse updateResponse = kendraRankingClient.updateRescoreExecutionPlan(
        UpdateRescoreExecutionPlanRequest.builder()
            .id(rescoreExecutionPlanId)
            .capacityUnits(
                CapacityUnitsConfiguration.builder()
                    .rescoreCapacityUnits(newCapacityUnits)
                    .build()
            )
            .build()
    );

    System.out.println(String.format("Waiting for rescore execution plan with id %s to finish updating.", rescoreExecutionPlanId));
    while (true) {
      DescribeRescoreExecutionPlanResponse describeResponse = kendraRankingClient.describeRescoreExecutionPlan(
          DescribeRescoreExecutionPlanRequest.builder()
              .id(rescoreExecutionPlanId)
              .build()
      );
      RescoreExecutionPlanStatus rescoreExecutionPlanStatus = describeResponse.status();
      if (rescoreExecutionPlanStatus != RescoreExecutionPlanStatus.UPDATING) {
        break;
      }
      TimeUnit.SECONDS.sleep(60);
    }

    System.out.println("Rescore execution plan update is complete.");
  }
}
```

------

The following is an example of using the `Rescore` API\.

------
#### [ CLI ]

```
aws kendra-ranking rescore \
  --rescore-execution-plan-id <rescore execution plan ID> \
  --search-query "intelligent systems" \
  --documents "[{\"Id\": \"DocId1\",\"Title\": \"Smart systems\", \"Body\": \"intelligent systems in everyday life\",\"OriginalScore\": 2.0}, {\"Id\": \"DocId2\",\"Title\": \"Smarter systems\", \"Body\": \"living with intelligent systems\",\"OriginalScore\": 1.0}]"
```

------
#### [ Python ]

```
import boto3
from botocore.exceptions import ClientError
import pprint

kendra_ranking = boto3.client("kendra-ranking")
                    
print("Use the Rescore API.")
                    
# Provide the ID of the rescore execution plan
id = <rescore execution plan ID>
# The search query from the search service
query = "intelligent systems"
# The list of documents for Intelligent Ranking to rescore
document_list = [
    {"Id": "DocId1", "Title": "Smart systems", "Body": "intelligent systems in everyday life", "OriginalScore": 2.0},
    {"Id": "DocId2", "Title": "Smarter systems", "Body": "living with intelligent systems", "OriginalScore": 1.0}
]
                        
try:
    rescore_response = kendra_ranking.rescore(
        rescore_execution_plan_id = id,
        search_query = query,
        documents = document_list
    )
    
    print(rescore_response["RescoreId"])
    print(rescore_resposne["ResultItems"])
	
except ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

```
import java.util.ArrayList;
import java.util.List;

import software.amazon.awssdk.services.kendraranking.KendraRankingClient;
import software.amazon.awssdk.services.kendraranking.model.RescoreRequest;
import software.amazon.awssdk.services.kendraranking.model.RescoreResponse;
import software.amazon.awssdk.services.kendraranking.model.Document;

public class RescoreExample {

  public static void main(String[] args) {

    String rescoreExecutionPlanId = <rescore execution plan ID>;
    String query = "intelligent systems";

    List<Document> documentList = new ArrayList<>();
    documentList.add(
        Document.builder()
            .id("DocId1")
            .originalScore(2.0F)
            .body("intelligent systems in everyday life")
            .title("Smart systems")
            .build()
    );
    documentList.add(
        Document.builder()
            .id("DocId2")
            .originalScore(1.0F)
            .body("living with intelligent systems")
            .title("Smarter systems")
            .build()
    );

    KendraRankingClient kendraRankingClient = KendraRankingClient.builder().build();

    RescoreResponse rescoreResponse = kendraRankingClient.rescore(
        RescoreRequest.builder()
            .rescoreExecutionPlanId(rescoreExecutionPlanId)
            .searchQuery(query)
            .documents(documentList)
            .build()
    );
    
    System.out.println(rescoreResponse.rescoreId());
    System.out.println(rescoreResponse.resultItems());
  }
}
```

------