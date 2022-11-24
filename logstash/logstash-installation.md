Pull the Logstash oss package with the OpenSearch output plugin image:

```
 docker pull opensearchproject/logstash-oss-with-opensearch-output-plugin:7.16.2
 ```

A network with name "opensearch-net" was created at the time of opensearch cluster creation

Run the docker container 

```
docker run -it --rm --name logstashconsole --net opensearch_opensearch-net opensearchproject/logstash-oss-with-opensearch-output-plugin:latest -e 'input { stdin { } } output {
   opensearch {
     hosts => ["https://68.183.81.16:9200"]
     index => "opensearch-saurabh-%{+YYYY.MM.dd}"
     user => "admin"
     password => "admin"
     ssl => true
     ssl_certificate_verification => false
   }
 }'

```

```
docker run -it --rm --name logstashconsole --net opensearch_opensearch-net opensearchproject/logstash-oss-with-opensearch-output-plugin:latest -e 'input { stdin { } } output {
   opensearch {
     hosts => ["https://68.183.81.16:9200"]
     index => "opensearch-latest-%{+YYYY.MM.dd}"
     user => "admin"
     password => "admin"
     ssl => true
     ssl_certificate_verification => false
   }

   stdout { codec => rubydebug }
 }'
 ```

Create an index pattern 

Navigate to Stack management >> Index Patterns >> Create and index pattern

docker run -d -it --rm --name logstash -v /root/logstash-conf/logstash-apache.conf:/usr/share/logstash/pipeline/logstash.conf --net opensearch_opensearch-net opensearchproject/logstash-oss-with-opensearch-output-plugin:latest

```
docker run -it --rm --name logstashconsole --net opensearch_opensearch-net opensearchproject/logstash-oss-with-opensearch-output-plugin:latest -e 'input { stdin { } } filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
  date {
    match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ]
  }
} output {
  opensearch { 
    hosts => ["https://68.183.81.16:9200"]
     index => "opensearch-apache-%{+YYYY.MM.dd}"
     user => "admin"
     password => "admin"
     ssl => true
     ssl_certificate_verification => false
   }
  stdout { codec => rubydebug }
}'
```

```

docker run -it --rm --name logstashconsole -v /root/config/logstash.conf:/usr/share/logstash/pipeline/logstash.conf --net opensearch_opensearch-net opensearchproject/logstash-oss-with-opensearch-output-plugin:latest 

```
