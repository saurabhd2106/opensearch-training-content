# Installing OpenSearch using Docker –

Official OpenSearch images are hosted on Docker Hub and Amazon ECR. If you want to inspect the images, you can pull them individually using docker pull, such as in the following examples.

Docker Hub:
```
    docker pull opensearchproject/opensearch:latest
    docker pull opensearchproject/opensearch-dashboards:latest
```

Amazon ECR:
```
    docker pull public.ecr.aws/opensearchproject/opensearch:latest
    docker pull public.ecr.aws/opensearchproject/opensearch-dashboards:latest
```

Before continuing, you should verify that Docker is working correctly by deploying OpenSearch in a single container.

1.	Run the following command:
 
 This command maps ports 9200 and 9600, sets the discovery type to "single-node" and requests the newest image of OpenSearch
 
 docker run -d -p 9200:9200 -p 9600:9600 -e "discovery.type=single-node" opensearchproject/opensearch:latest

2.	Send a request to port 9200. The default username and password are admin.

3.	 ` curl https://localhost:9200 -ku 'admin:admin'`

You should get a response that looks like this:

```

{
  "name" : "a937e018cee5",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "GLAjAG6bTeWErFUy_d-CLw",
  "version" : {
    "distribution" : "opensearch",
    "number" : "2.3.0",
    "build_type" : "tar",
    "build_hash" : "6f6e84ebc54af31a976f53af36a5c69d474a5140",
    "build_date" : "2022-09-09T00:07:24.896263462Z",
    "build_snapshot" : false,
    "lucene_version" : "9.3.0",
    "minimum_wire_compatibility_version" : "7.10.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "The OpenSearch Project: https://opensearch.org/"
}

```