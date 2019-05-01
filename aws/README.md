# cloudflare-elastic
AWS Lambda Function for Forwarding Cloudflare Logs to Elasticsearch


### Build
```./gradlew clean build```


### Install

Upload build/distributions/cloudflare-elastic-lambda.zip to AWS. Due to the size of the distribution, you may need to upload the file to an S3 bucket before configuring.


### Configure

##### Configure handler method

com.cloudflare.elastic.ElasticLambdaForwarder::handleRequest

##### Configure environment variables

Certain environment variables must be configured so that the function can connect to the Elasticsearch cluster.

| Environment Variable | Description |
| --- | --- |
| elastic_hostname | Fully qualified domain name of the Elasticsearch endpoint |
| elastic_username | The username of the Elasticsearch user, e.g. elastic |
| elastic_password | The password of the Elasticsearch user |

Additionally, the following environment variables can optionally be configured.

| Environment Variable | Description | Default value |
| --- | --- | --- |
| elastic_port | Endpoint port number | 9243 |
| elastic_index | The index pattern to use | cloudflare-* |
| elastic_pipeline | The ingest pipeline to use for pre-processing | cloudflare-pipeline |
| elastic_use_https | Whether to use SSL/TLS to connect | true |
| elastic_bulk_actions | Number of log messages to send to Elasticsearch per batch; can be tuned for scale and speed | 100 |
| elastic_bulk_concurrency | Number of concurrent requests to Elasticsearch; can be tuned for scale and speed | 2 |
| elastic_debug | Enable verbose logging | false |
| aws_access_key | Can be used to override permissions from execution role; typically not needed |  |
| aws_secret_key | Can be used to override permissions from execution role; typically not needed |  |

##### Configure Elasticsearch

The lambda function depends on Elasticsearch being configured with an ingest pipeline and an index template. Definitions for these are in the conf/ folder. To install to your Elasticsearch cluster, run this command:

```./install-artifacts.sh -e https://<REST API ENDPOINT>:<PORT> -u <ELASTIC USER> -p <ELASTIC PASSWORD>```





