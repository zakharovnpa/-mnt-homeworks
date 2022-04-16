### Ход выполнения ДЗ к занятию "10.04. ELK"

#### Директория выполнения ДЗ:

```
root@server1:~/learning-monitoring/ELK# 
```
```
root@server1:~/learning-monitoring/ELK# tree
.
├── configs
│   ├── filebeat.yml
│   ├── logstash.conf
│   └── logstash.yml
├── docker-compose.yml
├── pinger
│   └── run.py
└── README.md

2 directories, 6 files

```

## Дополнительные ссылки

При выполнении задания пользуйтесь вспомогательными ресурсами:

- [Документация по Filebeat](https://www.elastic.co/guide/en/beats/filebeat/7.16/index.html)
- [Running the Elastic Stack on Docker-Compose](https://www.elastic.co/guide/en/elastic-stack-get-started/7.16/get-started-docker.html)
- [Index management](https://www.elastic.co/guide/en/elasticsearch/reference/7.16/index-mgmt.html)
- 

- [поднимаем elk в докер](https://www.elastic.co/guide/en/elastic-stack-get-started/current/get-started-docker.html)
- [поднимаем elk в докер с filebeat и докер логами](https://www.sarulabs.com/post/5/2019-08-12/sending-docker-logs-to-elasticsearch-and-kibana-with-filebeat.html)
- [конфигурируем logstash](https://www.elastic.co/guide/en/logstash/current/configuration.html)
- [плагины filter для logstash](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)
- [конфигурируем filebeat](https://www.elastic.co/guide/en/beats/libbeat/5.3/config-file-format.html)
- [привязываем индексы из elastic в kibana](https://www.elastic.co/guide/en/kibana/current/index-patterns.html)
- [как просматривать логи в kibana](https://www.elastic.co/guide/en/kibana/current/discover.html)
- [решение ошибки increase vm.max_map_count elasticsearch](https://stackoverflow.com/questions/42889241/how-to-increase-vm-max-map-count)

В процессе выполнения задания могут возникнуть также не указанные тут проблемы в зависимости от системы.

Используйте output stdout filebeat/kibana и api elasticsearch для изучения корня проблемы и ее устранения.

## Задание повышенной сложности

Не используйте директорию [help](./help) при выполнении домашнего задания.

## Задание 1

### 1. Вам необходимо поднять в докере:
- elasticsearch(hot и warm ноды)
- logstash
- kibana
- filebeat

и связать их между собой.

**Ответ:**

Запуск `docker-compose up -d` приводит к ошибке:
```

```
* Причина ошибки - ограничение доступа по территоиальному признаку.
* С обходом данной ситуации через приватные частные сети позволяет нормально собрать образы и запустить контейнеры:
```
⠿ filebeat Pulled                                                                                                                                                                                     252.5s
   ⠿ a4f595742a5b Pull complete                                                                                                                                                                        193.9s
   ⠿ 3581c22b2b4e Pull complete                                                                                                                                                                        221.8s
   ⠿ 7208c262d709 Pull complete                                                                                                                                                                        223.3s
   ⠿ 43589b2d6d0e Pull complete                                                                                                                                                                        223.6s
   ⠿ 123296607618 Pull complete                                                                                                                                                                        223.9s
   ⠿ 326b60db75d5 Pull complete                                                                                                                                                                        243.4s
   ⠿ 57dfc02aeffa Pull complete                                                                                                                                                                        244.0s
   ⠿ 382fd98b4209 Pull complete                                                                                                                                                                        244.4s
   ⠿ 31247e830430 Pull complete                                                                                                                                                                        245.5s
   ⠿ 8307b5ba0ded Pull complete                                                                                                                                                                        245.8s
   ⠿ 10edc5e6eaf2 Pull complete                                                                                                                                                                        246.5s
 ⠿ some_application Pulled                                                                                                                                                                              79.2s
   ⠿ df9b9388f04a Pull complete                                                                                                                                                                         57.5s
   ⠿ a1ef3e6b7a02 Pull complete                                                                                                                                                                         63.0s
   ⠿ bf5b42ba4ad7 Pull complete                                                                                                                                                                         73.1s
   ⠿ 149beaa72b5f Pull complete                                                                                                                                                                         73.3s
   ⠿ 5c7b50b69f68 Pull complete                                                                                                                                                                         77.0s
 ⠿ es-hot Pulled                                                                                                                                                                                       261.1s
   ⠿ c0f9908af642 Pull complete                                                                                                                                                                         25.5s
   ⠿ dc193d8d7c71 Pull complete                                                                                                                                                                        257.8s
   ⠿ e3deb19b2c38 Pull complete                                                                                                                                                                        258.2s
[+] Running 10/10
 ⠿ Network elk_elastic  Created                                                                                                                                                                          0.2s
 ⠿ Network elk_default  Created                                                                                                                                                                          0.1s
 ⠿ Volume "elk_data02"  Created                                                                                                                                                                          0.0s
 ⠿ Volume "elk_data01"  Created                                                                                                                                                                          0.0s
 ⠿ Container es-warm    Started                                                                                                                                                                          2.5s
 ⠿ Container some_app   Started                                                                                                                                                                          2.4s
 ⠿ Container es-hot     Started                                                                                                                                                                          3.9s
 ⠿ Container logstash   Started                                                                                                                                                                          6.7s
 ⠿ Container kibana     Started                                                                                                                                                                          6.6s
 ⠿ Container filebeat   Started                    
```
* Состояние контейнеров сразу после их запуска:
```
root@server1:~/learning-monitoring/ELK# docker ps
CONTAINER ID   IMAGE                                     COMMAND                  CREATED          STATUS          PORTS                                                           NAMES
7ef1b93fa1e8   docker.elastic.co/beats/filebeat:7.16.2   "/usr/bin/tini -- /u…"   22 seconds ago   Up 13 seconds                                                                   filebeat
59e1770d0d2f   kibana:7.16.2                             "/bin/tini -- /usr/l…"   22 seconds ago   Up 15 seconds   0.0.0.0:5601->5601/tcp, :::5601->5601/tcp                       kibana
7ac3eedd149e   logstash:7.16.2                           "/usr/local/bin/dock…"   22 seconds ago   Up 15 seconds   5044/tcp, 9600/tcp, 0.0.0.0:5046->5046/tcp, :::5046->5046/tcp   logstash
f2758a81619c   elasticsearch:7.16.2                      "/bin/tini -- /usr/l…"   22 seconds ago   Up 18 seconds   0.0.0.0:9200->9200/tcp, :::9200->9200/tcp, 9300/tcp             es-hot
cf5431bf3027   elasticsearch:7.16.2                      "/bin/tini -- /usr/l…"   23 seconds ago   Up 20 seconds   9200/tcp, 9300/tcp                                              es-warm
d7cd758e2cc7   python:3.9-alpine                         "python3 /opt/run.py"    23 seconds ago   Up 20 seconds                                                                   some_app

```

* Состояние контейнеров через 30 минут:
```
root@server1:~/learning-monitoring/ELK# docker ps -a
CONTAINER ID   IMAGE                                     COMMAND                  CREATED          STATUS                        PORTS                                                           NAMES
7ef1b93fa1e8   docker.elastic.co/beats/filebeat:7.16.2   "/usr/bin/tini -- /u…"   33 minutes ago   Up 33 minutes                                                                                 filebeat
59e1770d0d2f   kibana:7.16.2                             "/bin/tini -- /usr/l…"   33 minutes ago   Up 33 minutes                 0.0.0.0:5601->5601/tcp, :::5601->5601/tcp                       kibana
7ac3eedd149e   logstash:7.16.2                           "/usr/local/bin/dock…"   33 minutes ago   Up 33 minutes                 5044/tcp, 9600/tcp, 0.0.0.0:5046->5046/tcp, :::5046->5046/tcp   logstash
f2758a81619c   elasticsearch:7.16.2                      "/bin/tini -- /usr/l…"   33 minutes ago   Exited (137) 32 minutes ago                                                                   es-hot
cf5431bf3027   elasticsearch:7.16.2                      "/bin/tini -- /usr/l…"   33 minutes ago   Exited (137) 32 minutes ago                                                                   es-warm

```

* Решение вопроса по `vm.max_map_count`:
```
ERROR: [1] bootstrap checks failed. You must address the points described in the following [1] lines before starting Elasticsearch.
bootstrap check failure [1] of [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

```

```
root@PC-Ubuntu:~# cat /proc/sys/vm/max_map_count
65530
```
```
root@PC-Ubuntu:~# sysctl -w vm.max_map_count=262144
vm.max_map_count = 262144
```
```
root@PC-Ubuntu:~# cat /proc/sys/vm/max_map_count
262144
```
```
root@PC-Ubuntu:~# echo "vm.max_map_count=262144" >> /etc/sysctl.conf
```
```
root@PC-Ubuntu:~# sysctl --system
* Applying /etc/sysctl.d/10-console-messages.conf ...
kernel.printk = 4 4 1 7
* Applying /etc/sysctl.d/10-ipv6-privacy.conf ...
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
* Applying /etc/sysctl.d/10-kernel-hardening.conf ...
kernel.kptr_restrict = 1
* Applying /etc/sysctl.d/10-link-restrictions.conf ...
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
* Applying /etc/sysctl.d/10-magic-sysrq.conf ...
kernel.sysrq = 176
* Applying /etc/sysctl.d/10-network-security.conf ...
net.ipv4.conf.default.rp_filter = 2
net.ipv4.conf.all.rp_filter = 2
* Applying /etc/sysctl.d/10-ptrace.conf ...
kernel.yama.ptrace_scope = 1
* Applying /etc/sysctl.d/10-zeropage.conf ...
vm.mmap_min_addr = 65536
* Applying /usr/lib/sysctl.d/30-tracker.conf ...
fs.inotify.max_user_watches = 65536
* Applying /usr/lib/sysctl.d/50-default.conf ...
net.ipv4.conf.default.promote_secondaries = 1
sysctl: setting key "net.ipv4.conf.all.promote_secondaries": Недопустимый аргумент
net.ipv4.ping_group_range = 0 2147483647
net.core.default_qdisc = fq_codel
fs.protected_regular = 1
fs.protected_fifos = 1
* Applying /usr/lib/sysctl.d/50-pid-max.conf ...
kernel.pid_max = 4194304
* Applying /etc/sysctl.d/99-sysctl.conf ...
vm.max_map_count = 262144
* Applying /usr/lib/sysctl.d/protect-links.conf ...
fs.protected_fifos = 1
fs.protected_hardlinks = 1
fs.protected_regular = 2
fs.protected_symlinks = 1
* Applying /etc/sysctl.conf ...
vm.max_map_count = 262144
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cat /proc/sys/vm/max_map_count
262144
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cat /proc/sys/vm/max_map_count
262144
root@PC-Ubuntu:~# 

```

```
root@PC-Ubuntu:~/learning-monitoring/ELK# docker-compose exec es-hot cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal

```

```
root@PC-Ubuntu:~/learning-monitoring/ELK# docker-compose exec es-hot bash
root@3aeca93dc0a8:/usr/share/elasticsearch# 
root@3aeca93dc0a8:/usr/share/elasticsearch# ls -lha
total 688K
drwxrwxr-x  1 root          root 4.0K Apr 13 19:41 .
drwxr-xr-x  1 root          root 4.0K Apr 13 19:41 ..
-rw-r--r--  1 root          root  220 Dec 19 00:19 .bash_logout
-rw-r--r--  1 root          root 3.7K Dec 19 00:19 .bashrc
drwxrwxr-x  3 elasticsearch root 4.0K Apr 13 19:41 .cache
-rw-r--r--  1 root          root  807 Dec 19 00:19 .profile
-r--r--r--  1 root          root 3.8K Dec 18 19:40 LICENSE.txt
-r--r--r--  1 root          root 614K Dec 18 19:45 NOTICE.txt
-r--r--r--  1 root          root 2.7K Dec 18 19:40 README.asciidoc
drwxrwxr-x  1 elasticsearch root 4.0K Dec 19 00:18 bin
drwxrwxr-x  1 elasticsearch root 4.0K Apr 13 19:41 config
drwxrwxr-x  3 elasticsearch root 4.0K Apr 13 17:16 data
dr-xr-xr-x  1 root          root 4.0K Dec 18 19:48 jdk
dr-xr-xr-x  3 root          root 4.0K Dec 18 19:48 lib
drwxrwxr-x  1 elasticsearch root 4.0K Apr 13 19:48 logs
dr-xr-xr-x 61 root          root 4.0K Dec 18 19:48 modules
drwxrwxr-x  1 elasticsearch root 4.0K Dec 18 19:45 plugins

```

```
root@3aeca93dc0a8:/usr/share/elasticsearch/config# cat elasticsearch.yml 
cluster.name: "docker-cluster"
network.host: 0.0.0.0

```

### Связывание между собой:

#### N. Тестирование подключений

* На `es-hot` выполняем `curl -v http://localhost:9200/_template/logstash`

```
curl http://localhost:9200/_template/logstash

```
```
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}
```

```
root@server1:~/learning-monitoring/ELK# docker-compose exec es-hot curl -v http://localhost:9200/_template/logstash
*   Trying 127.0.0.1:9200...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 9200 (#0)
> GET /_template/logstash HTTP/1.1
> Host: localhost:9200
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< X-elastic-product: Elasticsearch
< Warning: 299 Elasticsearch-7.16.2-2b937c44140b6559905130a8650c64dbd0879cfb "Elasticsearch built-in security features are not enabled. Without authentication, your cluster could be accessible to anyone. See https://www.elastic.co/guide/en/elasticsearch/reference/7.16/security-minimal-setup.html to enable security."
< content-type: application/json; charset=UTF-8
< content-length: 696
< 
* Connection #0 to host localhost left intact
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}
```

#### 2. Logstash следует сконфигурировать для приёма по tcp json сообщений.

```
root@server1:~/learning-monitoring/ELK# docker-compose exec es-hot curl http://localhost:9200/_template/logstash
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}root@server1:~/learning-monitoring/ELK# 
root@server1:~/learning-monitoring/ELK# 
root@server1:~/learning-monitoring/ELK# 
root@server1:~/learning-monitoring/ELK# docker-compose exec kibana curl http://es-hot:9200/_template/logstash
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}root@server1:~/learning-monitoring/ELK# 
```

#### 3. Filebeat следует сконфигурировать для отправки логов docker вашей системы в logstash.

```
[root@579145f2712b filebeat]# curl http://logstash:5046
```

```
[root@579145f2712b filebeat]# 
[root@579145f2712b filebeat]# curl http://logstash:9600
{"host":"b24497fb9412","version":"7.16.2","http_address":"0.0.0.0:9600","id":"6c856762-610d-4c66-ad5b-7c138349fe38","name":"b24497fb9412","ephemeral_id":"6d719791-eff5-4df4-8b1f-397dcfe0ea78","status":"green","snapshot":false,"pipeline":{"workers":3,"batch_size":125,"batch_delay":50},"build_date":"2021-12-18T19:42:46Z","build_sha":"f1d497fd30cdb16dccebf2de1a788aad1005be9a","build_snapshot":false}[root@579145f2712b filebeat]# 
```

```
[root@579145f2712b filebeat]# curl http://logstash:5044
curl: (7) Failed connect to logstash:5044; Connection refused
```

```
[root@579145f2712b filebeat]# curl -v http://logstash:5046
* About to connect() to logstash port 5046 (#0)
*   Trying 172.18.0.4...
* Connected to logstash (172.18.0.4) port 5046 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.29.0
> Host: logstash:5046
> Accept: */*
> 
^C
```

```
[root@579145f2712b filebeat]# curl -v http://es-hot:9200
* About to connect() to es-hot port 9200 (#0)
*   Trying 172.18.0.3...
* Connected to es-hot (172.18.0.3) port 9200 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.29.0
> Host: es-hot:9200
> Accept: */*
> 
< HTTP/1.1 200 OK
< X-elastic-product: Elasticsearch
< Warning: 299 Elasticsearch-7.16.2-2b937c44140b6559905130a8650c64dbd0879cfb "Elasticsearch built-in security features are not enabled. Without authentication, your cluster could be accessible to anyone. See https://www.elastic.co/guide/en/elasticsearch/reference/7.16/security-minimal-setup.html to enable security."
< content-type: application/json; charset=UTF-8
< content-length: 543
< 
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
* Connection #0 to host es-hot left intact
[root@579145f2712b filebeat]# 
[root@579145f2712b filebeat]# curl -v http://es-warm:9200
* About to connect() to es-warm port 9200 (#0)
*   Trying 172.18.0.2...
* Connected to es-warm (172.18.0.2) port 9200 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.29.0
> Host: es-warm:9200
> Accept: */*
> 
< HTTP/1.1 200 OK
< X-elastic-product: Elasticsearch
< Warning: 299 Elasticsearch-7.16.2-2b937c44140b6559905130a8650c64dbd0879cfb "Elasticsearch built-in security features are not enabled. Without authentication, your cluster could be accessible to anyone. See https://www.elastic.co/guide/en/elasticsearch/reference/7.16/security-minimal-setup.html to enable security."
< content-type: application/json; charset=UTF-8
< content-length: 544
< 
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
* Connection #0 to host es-warm left intact

```

```
root@server1:~/learning-monitoring/ELK# docker-compose exec es-hot curl -v http://localhost:9200/_template/logstash
*   Trying 127.0.0.1:9200...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 9200 (#0)
> GET /_template/logstash HTTP/1.1
> Host: localhost:9200
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< X-elastic-product: Elasticsearch
< Warning: 299 Elasticsearch-7.16.2-2b937c44140b6559905130a8650c64dbd0879cfb "Elasticsearch built-in security features are not enabled. Without authentication, your cluster could be accessible to anyone. See https://www.elastic.co/guide/en/elasticsearch/reference/7.16/security-minimal-setup.html to enable security."
< content-type: application/json; charset=UTF-8
< content-length: 696
< 
* Connection #0 to host localhost left intact
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}root@server1:~/learning-monitoring/ELK# 
```

```
root@server1:~/learning-monitoring/ELK# docker-compose exec es-hot curl http://localhost:9200/_template/logstash
{"logstash":{"order":0,"version":60001,"index_patterns":["logstash-*"],"settings":{"index":{"number_of_shards":"1","refresh_interval":"5s"}},"mappings":{"dynamic_templates":[{"message_field":{"path_match":"message","mapping":{"norms":false,"type":"text"},"match_mapping_type":"string"}},{"string_fields":{"mapping":{"norms":false,"type":"text","fields":{"keyword":{"ignore_above":256,"type":"keyword"}}},"match_mapping_type":"string","match":"*"}}],"properties":{"@timestamp":{"type":"date"},"geoip":{"dynamic":true,"properties":{"ip":{"type":"ip"},"latitude":{"type":"half_float"},"location":{"type":"geo_point"},"longitude":{"type":"half_float"}}},"@version":{"type":"keyword"}}},"aliases":{}}}root@server1:~/learning-monitoring/ELK# 
root@server1:~/learning-monitoring/ELK# 

```

#### 4. В директории [help](./help) находится манифест docker-compose и конфигурации filebeat/logstash для быстрого 
выполнения данного задания.

* Быстро выполнить не удается. Контейнеры es-hot, es-warm падают через минуту после запуска.
* Логи es-hot `docker start es-hot -i`:
```
{"type": "server", "timestamp": "2022-04-13T18:58:48,339Z", "level": "ERROR", "component": "o.e.b.ElasticsearchUncaughtExceptionHandler", "cluster.name": "es-docker-cluster", "node.name": "es-hot", "message": "uncaught exception in thread [main]", 
"stacktrace": ["org.elasticsearch.bootstrap.StartupException: ElasticsearchException[Failure running machine learning native code. This could be due to running on an unsupported OS or distribution, missing OS libraries, or a problem with the temp directory. To bypass this problem by running Elasticsearch without machine learning functionality set [xpack.ml.enabled: false].]",

```

#### 5. Результатом выполнения данного задания должны быть:
- скриншот `docker ps` через 5 минут после старта всех контейнеров (их должно быть 5)
- скриншот интерфейса kibana
- docker-compose манифест (если вы не использовали директорию help)
- ваши yml конфигурации для стека (если вы не использовали директорию help)

## Задание 2

Перейдите в меню [создания index-patterns  в kibana](http://localhost:5601/app/management/kibana/indexPatterns/create)
и создайте несколько index-patterns из имеющихся.

Перейдите в меню просмотра логов в kibana (Discover) и самостоятельно изучите как отображаются логи и как производить 
поиск по логам.

В манифесте директории help также приведенно dummy приложение, которое генерирует рандомные события в stdout контейнера.
Данные логи должны порождать индекс logstash-* в elasticsearch. Если данного индекса нет - воспользуйтесь советами 
и источниками из раздела "Дополнительные ссылки" данного ДЗ.
 
---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

 
