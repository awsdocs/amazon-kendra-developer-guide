--------

--------

# Amazon Kendra Intelligent Ranking for self\-managed OpenSearch<a name="opensearch-rerank"></a>

You can leverage Amazon Kendra's semantic search capabilities to improve search results from [OpenSearch](https://opensearch.org/docs/latest), the self managed open source search service based on the Apache 2\.0 License\. The Amazon Kendra Intelligent Ranking plugin semantically re\-ranks OpenSearch's results using Amazon Kendra\. It does this by understanding the meaning and context of a search query using specific fields, such as the document body or title, from the default OpenSearch search results\.

Take, for example, this query: "main keynote address"\. Since 'address' has several meanings, Amazon Kendra can infer the meaning behind the query to return relevant information aligned with the intended meaning\. In this context, it's a conference keynote address\. A simpler search service might not take into account the intent and could possibly return results for a street address on Main Street, for example\.

The Intelligent Ranking plugin for OpenSearch is available for OpenSearch \(self managed\) version 2\.4\.0 and later\. You can install the plugin using a quick start Bash script to build a new Docker image of OpenSearch with the Intelligent Ranking plugin included\. See [Setting up the intelligent search plugin](#setup-opensearch-rerank-plugin)—this is an example of a setup to get you up and running quickly\.

## How the intelligent search plugin works<a name="how-opensearch-rerank-plugin-works"></a>

The overall process of the Intelligent Ranking plugin for OpenSearch \(self managed\) is as follows:

1. An OpenSearch user issues a query, and OpenSearch provides a query response or a list of documents that are relevant to the query\.

1. The Intelligent Ranking plugin takes the query response and extracts information from the documents\.

1. The Intelligent Ranking plugin makes a call to Amazon Kendra Intelligent Ranking's [Rescore](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_Rescore.html) API\.

1. The `Rescore` API takes the extracted information from the documents and semantically re\-ranks the search results\.

1. The `Rescore` API sends the re\-ranked search results back to the plugin\. The plugin re\-arranges the search results in the OpenSearch search response to reflect the new semantic ranking\.

The Intelligent Ranking plugin re\-ranks results using the "body" and "title" fields\. These plugin fields can be mapped to fields in your OpenSearch index that would most fit the definition of a document body and title\. For example, if your index contains chapters of a book with fields like "chapter\_heading" and "chapter\_contents", you can map the former to "title" and the latter to "body" to get the best results\.

## Setting up the intelligent search plugin<a name="setup-opensearch-rerank-plugin"></a>

The following outlines how to quickly set up OpenSearch \(self managed\) with the Intelligent Ranking plugin\.

**Setting up OpenSearch \(self managed\) with the Intelligent Ranking plugin \(quick setup\)**

If you are already using Docker image `opensearch:2.4.0`, you can use this [Dockerfile](https://docs.aws.amazon.com/kendra/latest/dg/opensearch-rerank.html#dockerfile-build-opensearch-example) to build a new image of OpenSearch 2\.4\.0 with the Intelligent Ranking plugin\. You include a container for the new image in your [docker\-compose\.yml](https://docs.aws.amazon.com/kendra/latest/dg/opensearch-rerank.html#docker-compose-opensearch-example) file or opensearch\.yml file\. You also include your generated rescore execution plan ID from creating a rescore execution plan, along with your region and endpoint information—see step 2 for creating a rescore execution plan\.

If you had previously downloaded a version of the `opensearch` Docker image that's older than 2\.4\.0, you must use Docker image `opensearch:2.4.0` or later and build a new image with the Intelligent Ranking plugin included\.

1. Download and install [Docker Desktop](https://docs.docker.com/get-docker/) for your operating system\. Docker Desktop includes Docker Compose and Docker Engine\. It's recommended that you check whether your computer meets the system requirements mentioned in the Docker installation details\.

   You can also increase your memory usage requirements within the settings of your Docker Desktop\. You are responsible for the usage requirements of Docker outside the freely available usage limits for Docker services\. See [Docker subscriptions](https://docs.docker.com/subscription/)\.

   Check Docker Desktop status is "running"\.

1. Provision Amazon Kendra Intelligent Ranking and your [capacity](https://docs.aws.amazon.com/kendra/latest/dg/adjusting-capacity.html) requirements\. Once you provision Amazon Kendra Intelligent Ranking, you are charged hourly based on your set capacity units\. See [free tier and pricing information](http://aws.amazon.com/kendra/intelligent-ranking-pricing/)\.

   You use the [CreateRescoreExecutionPlan](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_CreateRescoreExecutionPlan.html) API to provision the `Rescore API`\. If you don't need more capacity units than the single unit default, don't add more units and provide only a name for your rescore execution plan\. You can also update your capacity requirements by using the [UpdateRescoreExecutionPlan](https://docs.aws.amazon.com/kendra/latest/dg/API_Ranking_UpdateRescoreExecutionPlan.html) API\. For more information, see [Semantically ranking a search service's results](https://docs.aws.amazon.com/kendra/latest/dg/search-service-rerank.html)\.

   Optionally, you can go to step 3 to create a default rescore execution plan when you run the quick start Bash script\.

   Note for step 4 the rescore execution plan ID included in the response\.

------
#### [ CLI ]

   ```
   aws kendra-ranking create-rescore-execution-plan \
     --name MyRescoreExecutionPlan \ 
     --capacity-units '{"RescoreCapacityUnits":<integer number of additional capacity units>}'
    
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

1. Download the [quick start Bash script](https://github.com/opensearch-project/search-processor/tree/main/helpers) from GitHub for your version of OpenSearch by selecting the version branch from the main branch dropdown\.

1. Open your terminal and in the directory of the Bash script, run the following command\.

   ```
   bash search_processing_kendra_quickstart.sh -p <execution-plan-id> -r <region>
   ```

   When you run this command, you provide the rescore execution plan ID that you noted in step 2 when you provisioned Amazon Kendra Intelligent Ranking, along with your region information\. Optionally, you can instead provision Amazon Kendra Intelligent Ranking by using the `--create-execution-plan` option\. This creates a rescore execution plan with a default name and default capacity\. If AWS credentials cannot be obtained from either environment variables, default profile, or Amazon EC2 instance, then provide your credentials using the `--profile` option\.

   To not lose your index when the default ephemeral container is removed, you can have your index persist across executions by providing the data volume name using the `--volume-name` option\. If you previously created an index, you can specify the volume in your docker\-compose\.yml or opensearch\.yml file\.

   This script uses Docker images for OpenSearch and OpenSearch Dashboards using your version you selected on the GitHub repository for the script\. It downloads a zip file for the Intelligent Ranking plugin, and generates a `Dockerfile` to build a new Docker image of OpenSearch that includes the plugin\. It also creates a [docker\-compose\.yml](https://docs.aws.amazon.com/kendra/latest/dg/opensearch-rerank.html#docker-compose-opensearch-example) file that includes containers for OpenSearch with the Intelligent Ranking plugin and OpenSearch Dashboards\. The script adds your rescore execution plan ID, region information, and endpoint \(uses the region\) to the docker\-compose\.yml file\. The script then runs `docker-compose up` to start the containers for OpenSearch with Intelligent Ranking included and OpenSearch Dashboards\. To stop the containers without removing them, run `docker-compose stop`\. To remove the containers, run `docker-compose down`\. To leave your volumes intact, **don't** run `docker-compose down -v`\.

### Example of docker\-compose\.yml<a name="docker-compose-opensearch-example"></a>

An example of a docker\-compose\.yml file using OpenSearch 2\.4\.0 or later with the Intelligent Ranking plugin and OpenSearch Dashboards 2\.4\.0 or later\.

```
version: '3'
networks:
  opensearch-net:
volumes: 
  <volume-name>:
services:
  opensearch-node:
    image: <Docker image tag name of OpenSearch with Intelligent Ranking plugin>
    container_name: opensearch-node
    environment: 
      - cluster.name=opensearch-cluster
      - node.name=opensearch-node
      - discovery.type=single-node
      - kendra_intelligent_ranking.service.endpoint=https://kendra-ranking.<region>.api.aws
      - kendra_intelligent_ranking.service.region=<region>
      - kendra_intelligent_ranking.service.execution_plan_id=<rescore-execution-plan-id>
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 65536
        hard: 65536
    ports:
      - 9200:9200
      - 9600:9600
    networks:
      - opensearch-net
  volumes:
    <docker-volume-name>:/usr/share/opensearch/data 
  opensearch-dashboard:
   image: opensearchproject/opensearch-dashboards:<your-version>
   container_name: opensearch-dashboards
   ports:
     - 5601:5601
   environment:
     OPENSEARCH_HOSTS: '["https://opensearch-node:9200"]'
   networks:
     - opensearch-net
```

### Example of a Dockerfile and building an image<a name="dockerfile-build-opensearch-example"></a>

An example of a `Dockerfile` for using OpenSearch 2\.4\.0 or later with the Intelligent Ranking plugin\.

```
FROM opensearchproject/opensearch:<your-version>
RUN /usr/share/opensearch/bin/opensearch-plugin install --batch  https://github.com/opensearch-project/search-processor/releases/download/<your-version>/search-processor.zip
```

Building a Docker image for OpenSearch with the Intelligent Ranking plugin\.

```
docker build --tag=<Docker image tag name of OpenSearch with Intelligent Ranking plugin>
```

## Interacting with the intelligent search plugin<a name="interact-opensearch-rerank-plugin"></a>

Once you have set up OpenSearch \(self managed\) with the Intelligent Ranking plugin, you can interact with the plugin using curl commands or OpenSearch client libraries\. The default credentials for accessing OpenSearch with the Intelligent Ranking plugin are user name 'admin' and password 'admin'\.

To apply the Intelligent Ranking plugin settings to an OpenSearch index:

------
#### [ Curl ]

```
curl -XPUT "https://localhost:9200/<your-docs-index>/_settings" -u 'admin:admin' --insecure -H 'Content-Type: application/json' -d'
{
  "index": {
    "plugin" : {
      "searchrelevance" : {
        "result_transformer" : {
          "kendra_intelligent_ranking": {
              "order": 1,
              "properties": {
                "title_field": "title_field_name_here",
                "body_field": "body_field_name_here"
              }
          }
        }
      }
    }
  }
}
'
```

------
#### [ Python ]

```
pip install opensearch-py

from opensearchpy import OpenSearch
host = 'localhost'
port = 9200
auth = ('admin', 'admin')

client = OpenSearch(
    hosts = [{'host': host, 'port': port}],
    http_compress = True, # enables gzip compression for request bodies
    http_auth = auth,
    # client_cert = client_cert_path,
    # client_key = client_key_path,
    use_ssl = True,
    verify_certs = False,
    ssl_assert_hostname = False,
    ssl_show_warn = False,
    ca_certs = ca_certs_path
)

setting_body = {
    "index": {
        "plugin" : {
            "searchrelevance" : {
                "result_transformer" : {
                    "kendra_intelligent_ranking": {
                            "order": 1,
                            "properties": {
                                "title_field": "title_field_name_here",
                                "body_field": "body_field_name_here"
                            }
                    }
                }
            }
        }
    }
}

response = client.indices.put_settings(index_name, body=setting_body)
```

------

You must include the name of the main text field you want to use to re\-rank on, such as a document body or document contents field\. You can also include other text fields, such as document title or document summary\.

Now you can issue any query and the results are ranked using the Intelligent Ranking plugin\.

------
#### [ Curl ]

```
curl -XGET "https://localhost:9200/<your-docs-index>/_search?pretty" -u 'admin:admin' --insecure -H 'Content-Type: application/json' -d'
{
  "query" : {
    "match" : {
      "body_field_name_here": "intelligent systems"
    }
  }
}
'
```

------
#### [ Python ]

```
from opensearchpy import OpenSearch
host = 'localhost'
port = 9200
auth = ('admin', 'admin')

client = OpenSearch(
    hosts = [{'host': host, 'port': port}],
    http_compress = True, # enables gzip compression for request bodies
    http_auth = auth,
    # client_cert = client_cert_path,
    # client_key = client_key_path,
    use_ssl = True,
    verify_certs = False,
    ssl_assert_hostname = False,
    ssl_show_warn = False,
    ca_certs = ca_certs_path
)

query = {
  'size': 10,
  "query" : {
    "match" : {
      "body_field_name_here": "intelligent systems"
    }
  }
}

response = client.search(
    body = query,
    index = index_name
)

print('\nSearch results:')
print(response)
```

------

To remove the Intelligent Ranking plugin settings for an OpenSearch index:

------
#### [ Curl ]

```
curl -XPUT "http://localhost:9200/<your-docs-index>/_settings" -H 'Content-Type: application/json' -d'
{
  "index": {
    "plugin": {
      "searchrelevance": {
        "result_transformer": {
          "kendra_intelligent_ranking.*": null
        }
      }
    }
  }
}
'
```

------
#### [ Python ]

```
from opensearchpy import OpenSearch
host = 'localhost'
port = 9200
auth = ('admin', 'admin')

client = OpenSearch(
    hosts = [{'host': host, 'port': port}],
    http_compress = True, # enables gzip compression for request bodies
    http_auth = auth,
    # client_cert = client_cert_path,
    # client_key = client_key_path,
    use_ssl = True,
    verify_certs = False,
    ssl_assert_hostname = False,
    ssl_show_warn = False,
    ca_certs = ca_certs_path
)

setting_body = {
  "index": {
    "plugin": {
      "searchrelevance": {
        "result_transformer": {
          "kendra_intelligent_ranking.*": null
        }
      }
    }
  }
}

response = client.indices.put_settings(index_name, body=setting_body)
```

------

To test the Intelligent Ranking plugin on a certain query or to test on certain body and title fields:

------
#### [ Curl ]

```
curl -XGET "https://localhost:9200/<your-docs-index>/_search?pretty" -u 'admin:admin' --insecure -H 'Content-Type: application/json' -d'
{
  "query": {
    "multi-match": {
      "query": "intelligent systems",
      "fields": ["body_field_name_here", "title_field_name_here"]
    }
  },
  "size": 25,
  "ext": {
    "search_configuration": {
      "result_transformer": {
        "kendra_intelligent_ranking": {
          "order": 1,
          "properties": {
            "title_field": "title_field_name_here",
            "body_field": "body_field_name_here"
          }
        }
      }
    }
  }
}
'
```

------
#### [ Python ]

```
from opensearchpy import OpenSearch
host = 'localhost'
port = 9200
auth = ('admin', 'admin')

client = OpenSearch(
    hosts = [{'host': host, 'port': port}],
    http_compress = True, # enables gzip compression for request bodies
    http_auth = auth,
    # client_cert = client_cert_path,
    # client_key = client_key_path,
    use_ssl = True,
    verify_certs = False,
    ssl_assert_hostname = False,
    ssl_show_warn = False,
    ca_certs = ca_certs_path
)

# Index settings null for kendra_intelligent_ranking

query = {
  "query": {
    "multi_match": {
      "query": "intelligent systems",
      "fields": ["body_field_name_here", "title_field_name_here"] 
    }
  },
  "size": 25,
  "ext": {
    "search_configuration": {
      "result_transformer": {
        "kendra_intelligent_ranking": {
          "order": 1,
          "properties": {
            "title_field": "title_field_name_here",
            "body_field": "body_field_name_here"
          }
        }
      }
    }
  }
}

response = client.search(
    body = query,
    index = index_name
)

print('\nSearch results:')
print(response)
```

------

## Comparing OpenSearch results with Amazon Kendra results<a name="compare-opensearch-rerank-plugin"></a>

You can compare side\-by\-side OpenSearch \(self managed\) ranked results against Amazon Kendra's re\-ranked results\. OpenSearch Dashboards version 2\.4\.0 and later offers side\-by\-side results so that you can compare how OpenSearch ranks documents with how Amazon Kendra or the plugin ranks documents for a search query\.

Before you can compare OpenSearch ranked results against Amazon Kendra re\-ranked results, make sure your OpenSearch Dashboards is backed by an OpenSearch server with the Intelligent Ranking plugin\. You can set this up using Docker and a quick start Bash script\. See [Setting up the intelligent search plugin](#setup-opensearch-rerank-plugin)\.

The following outlines how to compare OpenSearch and Amazon Kendra search results in OpenSearch Dashboards\. For more information, see the [OpenSearch Documentation](https://opensearch.org/docs/latest/search-plugins/search-relevance)\.

**Comparing search results in OpenSearch Dashboards**

1. Open http://localhost:5601 and sign in to OpenSearch Dashboards\. The default credentials are user name 'admin' and password 'admin'\.

1. Select **Search Relevance** from the OpenSearch plugins in the navigation menu\.

1. Enter the search text in the search bar\.

1. Select your index for **Query 1** and enter a query in the OpenSearch Query DSL\. You can use the `%SearchText%` variable to refer to the search text you entered in the search bar\. For an example of this query, see [OpenSearch Documentation](https://opensearch.org/docs/latest/search-plugins/search-relevance)\. The results returned for this query are the OpenSearch results without using the Intelligent Ranking plugin\.

1. Select the same index for **Query 2** and enter the same query in the OpenSearch Query DSL\. In addition, include the extension with `kendra_intelligent_ranking` and specify the mandatory `body_field` to rank on\. You can also specify the title field, but the body field is mandatory\. For an example of this query, see [OpenSearch Documentation](https://opensearch.org/docs/latest/search-plugins/search-relevance)\. The results returned for this query are the Amazon Kendra re\-ranked results using the Intelligent Ranking plugin\. The plugin ranks up to 25 results\.

1. Select **Search** to return and compare results\.