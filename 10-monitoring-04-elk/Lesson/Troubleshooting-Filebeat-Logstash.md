## Ход работ по связыванию Filebeat и Logstash

### 1. Описание ситуации

1. Не поступают данные (логи) контейнеров в Logastash
2. Logstash может передавать данные в Elasticksearch
3. В Kibana от Elastic индекс поступает

### 2. Описание связки Filebeat и Logstash

1. Порт Логстэш, принимающий от ФБ - 9600, судя по его логам

```
logstash  | [2022-04-15T18:01:17,438][INFO ][logstash.agent           ] Successfully started Logstash API endpoint {:port=>9600, :ssl_enabled=>false}
```
```
logstash  | [2022-04-15T18:01:29,270][INFO ][logstash.inputs.tcp      ][main][2a645a01954fb75b8efb5b4ed2431d900cd929dd8bcebdc13e0d7840b4037b6c] Starting tcp input listener {:address=>"0.0.0.0:5046", :ssl_e>
```
Вывод: правильный `tcp input listener` порт - 5046

2. Настройка входящего фильтра от ФБ для JSON
* Фиксируется ошибка:
```

```


3. Проверка нод стэка. [Источник информаци - Run with Docker Compose](https://www.elastic.co/guide/en/elastic-stack-get-started/7.16/get-started-docker.html)
```
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec es-hot curl -X GET "localhost:9200/_cat/nodes?v&pretty"
ip         heap.percent ram.percent cpu load_1m load_5m load_15m node.role  master name
172.24.0.3           71          76   3    0.30    0.23     0.25 cdfhimrstw *      es-hot
172.24.0.2           74          76   3    0.30    0.23     0.25 cdfhimrstw -      es-warm
root@server1:~/learning-monitoring/ELK/pinger# 
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec es-warm curl -X GET "localhost:9200/_cat/nodes?v&pretty"
ip         heap.percent ram.percent cpu load_1m load_5m load_15m node.role  master name
172.24.0.3           33          76   3    0.24    0.22     0.25 cdfhimrstw *      es-hot
172.24.0.2           37          76   3    0.24    0.22     0.25 cdfhimrstw -      es-warm

```

4. Убеждаемся, что Elasticsearch запущен и работает.
Чтобы проверить, запущен ли демон Elasticsearch, попробуйте отправить HTTP-запрос GET на порт 9200.
```
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec es-warm curl http://localhost:9200
{
  "name" : "es-warm",
  "cluster_name" : "es-docker-cluster",
  "cluster_uuid" : "V6JcOag3SEizV7t4nYi1Cg",
  "version" : {
    "number" : "7.16.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "2b937c44140b6559905130a8650c64dbd0879cfb",
    "build_date" : "2021-12-18T19:42:46.604893745Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```
```
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec es-hot curl http://localhost:9200
{
  "name" : "es-hot",
  "cluster_name" : "es-docker-cluster",
  "cluster_uuid" : "V6JcOag3SEizV7t4nYi1Cg",
  "version" : {
    "number" : "7.16.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "2b937c44140b6559905130a8650c64dbd0879cfb",
    "build_date" : "2021-12-18T19:42:46.604893745Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```

```
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec kibana curl http://es-hot:9200
{
  "name" : "es-hot",
  "cluster_name" : "es-docker-cluster",
  "cluster_uuid" : "V6JcOag3SEizV7t4nYi1Cg",
  "version" : {
    "number" : "7.16.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "2b937c44140b6559905130a8650c64dbd0879cfb",
    "build_date" : "2021-12-18T19:42:46.604893745Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
```
root@server1:~/learning-monitoring/ELK/pinger# docker-compose exec kibana curl http://es-warm:9200
{
  "name" : "es-warm",
  "cluster_name" : "es-docker-cluster",
  "cluster_uuid" : "V6JcOag3SEizV7t4nYi1Cg",
  "version" : {
    "number" : "7.16.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "2b937c44140b6559905130a8650c64dbd0879cfb",
    "build_date" : "2021-12-18T19:42:46.604893745Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```
5. Проверка того, что ФБ генерирует сообщения с логами.
[Filebeat quick start: installation and configuration](https://www.elastic.co/guide/en/beats/filebeat/7.16/filebeat-installation-configuration.html)


6. Проверка того, что ФБ передает сообщения с логами.
