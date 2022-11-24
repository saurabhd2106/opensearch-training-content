

docker run docker.elastic.co/beats/metricbeat-oss:7.10.1 setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["https://68.183.81.16:9200"]' -E output.elasticsearch.ssl.verification_mode="none" -E 'output.elasticsearch.username="admin"' -E 'output.elasticsearch.password="admin"' -E 'setup.ilm.overwrite=true' -E 'setup.template.overwrite=true'

docker run -d --rm \
  --name=metricbeat \
  --user=root \
  --volume="$(pwd)/metricbeat.yml:/usr/share/metricbeat/metricbeat.yml:ro" \
  --volume="/var/run/docker.sock:/var/run/docker.sock:ro" \
  --volume="/sys/fs/cgroup:/hostfs/sys/fs/cgroup:ro" \
  --volume="/proc:/hostfs/proc:ro" \
  --volume="/:/hostfs:ro" \
  docker.elastic.co/beats/metricbeat-oss:7.10.1 metricbeat -e \
  -E output.elasticsearch.hosts=["https://68.183.81.16:9200"] \
  -E output.elasticsearch.ssl.verification_mode="none"