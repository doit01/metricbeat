# metricbeat
dashboard 选择
[Metricbeat System] Host overview ECS
[Metricbeat PostgreSQL] Database Overview


docker run \
  --mount type=bind,source=/proc,target=/hostfs/proc,readonly \ 
  --mount type=bind,source=/sys/fs/cgroup,target=/hostfs/sys/fs/cgroup,readonly \ 
  --mount type=bind,source=/,target=/hostfs,readonly \ 
  --net=host \ 
  docker.elastic.co/beats/metricbeat:7.16.3 -e -system.hostfs=/hostfs




  hosts: ['${ELASTICSEARCH_HOST:elasticsearch}:${ELASTICSEARCH_PORT:9200}']
  username: ${ELASTICSEARCH_USERNAME}
  password: ${ELASTICSEARCH_PASSWORD}
  
    在非root下
  curl -L -O https://raw.githubusercontent.com/elastic/beats/7.16/deploy/docker/metricbeat.docker.yml

  
 docker run -d   --name=metricbeat   --user=root   --volume="$(pwd)/metricbeat.docker.yml:/usr/share/metricbeat/metricbeat.yml:ro"   --volume="/var/run/docker.sock:/var/run/docker.sock:ro"   --volume="/sys/fs/cgroup:/hostfs/sys/fs/cgroup:ro"   --volume="/proc:/hostfs/proc:ro"   --volume="/:/hostfs:ro"   docker.elastic.co/beats/metricbeat:7.16.3 metricbeat -e   -E output.elasticsearch.hosts=["192.168.5.60:9200"] -E output.elasticsearch.password=changeme -E output.elasticsearch.username=elastic
