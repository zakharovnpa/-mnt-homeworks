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

2. Настройка входящего фильтра от ФБ для JSON
3. Проверка нод стэка
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

4. 
