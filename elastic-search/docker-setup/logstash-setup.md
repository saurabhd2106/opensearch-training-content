
// Run with a simple logstash

docker run -it --rm --name logstashconsole --net root_es-net logstash:8.5.1 -e 'input { stdin { } } output {
   elasticsearch {
     hosts => ["159.89.160.240:9200"]
     index => "opensearch-logstash-docker-%{+YYYY.MM.dd}"
     
   }
 }'



docker run -d -it --rm --name logstash -v /root/logs/logstash.conf:/usr/share/logstash/pipeline/logstash.conf --net root_es-net logstash:8.5.1