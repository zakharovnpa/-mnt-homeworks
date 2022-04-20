# Домашнее задание к занятию "10.04. ELK" - Захаров Сергей Николаевич

## Дополнительные ссылки

При выполнении задания пользуйтесь вспомогательными ресурсами:

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

**Ответ:**
Попытка использовать файлы из директории `help` для запуска стэка ELK была безуспешная. 
Для успешного запуска файлы были переработаны, а также добавлены некоторые новые файлы, например для `elasticsearch.yml`, `kibana.yml`.

[Репозиторий с рабочей конфигурацией ELK](https://github.com/zakharovnpa/ELK-7.16.2)

## Задание 1

Вам необходимо поднять в докере:
- elasticsearch(hot и warm ноды)
- logstash
- kibana
- filebeat

и связать их между собой.

Logstash следует сконфигурировать для приёма по tcp json сообщений (от какого сервиса?).

Filebeat следует сконфигурировать для отправки логов docker вашей системы в logstash.

В директории [help](./help) находится манифест docker-compose и конфигурации filebeat/logstash для быстрого 
выполнения данного задания.

Результатом выполнения данного задания должны быть:
- скриншот `docker ps` через 5 минут после старта всех контейнеров (их должно быть 5)
- скриншот интерфейса kibana
- docker-compose манифест (если вы не использовали директорию help)
- ваши yml конфигурации для стека (если вы не использовали директорию help)

**Ответ:**

Для запуска стэка ELK использовались [свои файлы](https://github.com/zakharovnpa/ELK-7.16.2), созданные на основе тех, что расположены в директории [help](./help)

* Скриншот `docker ps` через 5 минут после старта всех контейнеров:
![screen-cmd-elk](/10-monitoring-04-elk/Files/screen-cmd-elk.png)

* Скриншот интерфейса kibana:
![screen-kibana-elk](/10-monitoring-04-elk/Files/screen-kibana-elk.png)

## Задание 2

Перейдите в меню [создания index-patterns  в kibana](http://localhost:5601/app/management/kibana/indexPatterns/create)
и создайте несколько index-patterns из имеющихся.

Перейдите в меню просмотра логов в kibana (Discover) и самостоятельно изучите как отображаются логи и как производить 
поиск по логам.

В манифесте директории help также приведенно dummy приложение, которое генерирует рандомные события в stdout контейнера.
Данные логи должны порождать индекс logstash-* в elasticsearch. Если данного индекса нет - воспользуйтесь советами 
и источниками из раздела "Дополнительные ссылки" данного ДЗ.
 
 
**Ответ:**

1. Созданы паттерны:
![screen-kibana-index-pattern-2](/10-monitoring-04-elk/Files/screen-kibana-index-pattern-2.png)

2. Логи Filebeat:
![screen-logs-filebeat-elk-3](/10-monitoring-04-elk/Files/screen-logs-filebeat-elk-3.png)
---

3. Вот такой json файл приходит от Filebeat в Logstash при передачи логов.
```json
{
  "_index": "logstash-2022.04.20",
  "_type": "_doc",
  "_id": "rKw9RYABmp83w62qTgaY",
  "_version": 1,
  "_score": 1,
  "_source": {
    "log": {
      "offset": 476,
      "file": {
        "path": "/var/lib/docker/containers/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c-json.log"
      }
    },
    "agent": {
      "hostname": "d06ab0375ab7",
      "id": "6a11d0a9-d837-46fc-bf64-43a0e3db06b3",
      "type": "filebeat",
      "version": "7.16.2",
      "name": "d06ab0375ab7",
      "ephemeral_id": "bec8503a-e548-40a0-9ed1-a3e832f6f971"
    },
    "host": {
      "name": "d06ab0375ab7"
    },
    "ecs": {
      "version": "1.12.0"
    },
    "message": "ERROR:root:OH NO!!!!!!",
    "@timestamp": "2022-04-20T04:28:40.215Z",
    "input": {
      "type": "container"
    },
    "@version": "1",
    "container": {
      "image": {
        "name": "library/python:3.9-alpine"
      },
      "labels": {
        "com_docker_compose_container-number": "1",
        "com_docker_compose_depends_on": "",
        "com_docker_compose_project_config_files": "/root/learning-monitoring/ELK/docker-compose.yml",
        "com_docker_compose_project_working_dir": "/root/learning-monitoring/ELK",
        "com_docker_compose_service": "some_application",
        "com_docker_compose_oneoff": "False",
        "com_docker_compose_project": "elk",
        "com_docker_compose_version": "2.2.2",
        "com_docker_compose_config-hash": "29129dac1567d42191497fbdaa4e14f37ab58c37fe176c4148a36f16d7a6ea4a",
        "com_docker_compose_image": "sha256:c55bae5557c5c540d01302d5feb93a89035a224bb9d14346ec47ec2d5ebc3f3d"
      },
      "name": "some_app",
      "id": "7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c"
    },
    "stream": "stderr",
    "tags": [
      "_jsonparsefailure",
      "beats_input_codec_json_applied"
    ]
  },
  "fields": {
    "agent.version.keyword": [
      "7.16.2"
    ],
    "container.labels.com_docker_compose_project_working_dir.keyword": [
      "/root/learning-monitoring/ELK"
    ],
    "container.labels.com_docker_compose_project_working_dir": [
      "/root/learning-monitoring/ELK"
    ],
    "host.name.keyword": [
      "d06ab0375ab7"
    ],
    "container.labels.com_docker_compose_service": [
      "some_application"
    ],
    "container.id": [
      "7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c"
    ],
    "agent.hostname.keyword": [
      "d06ab0375ab7"
    ],
    "ecs.version.keyword": [
      "1.12.0"
    ],
    "container.name": [
      "some_app"
    ],
    "container.image.name": [
      "library/python:3.9-alpine"
    ],
    "container.labels.com_docker_compose_image": [
      "sha256:c55bae5557c5c540d01302d5feb93a89035a224bb9d14346ec47ec2d5ebc3f3d"
    ],
    "agent.name": [
      "d06ab0375ab7"
    ],
    "host.name": [
      "d06ab0375ab7"
    ],
    "container.name.keyword": [
      "some_app"
    ],
    "agent.id.keyword": [
      "6a11d0a9-d837-46fc-bf64-43a0e3db06b3"
    ],
    "input.type": [
      "container"
    ],
    "log.offset": [
      476
    ],
    "agent.hostname": [
      "d06ab0375ab7"
    ],
    "tags": [
      "_jsonparsefailure",
      "beats_input_codec_json_applied"
    ],
    "container.labels.com_docker_compose_project": [
      "elk"
    ],
    "container.labels.com_docker_compose_image.keyword": [
      "sha256:c55bae5557c5c540d01302d5feb93a89035a224bb9d14346ec47ec2d5ebc3f3d"
    ],
    "agent.id": [
      "6a11d0a9-d837-46fc-bf64-43a0e3db06b3"
    ],
    "ecs.version": [
      "1.12.0"
    ],
    "container.labels.com_docker_compose_project_config_files.keyword": [
      "/root/learning-monitoring/ELK/docker-compose.yml"
    ],
    "container.labels.com_docker_compose_version.keyword": [
      "2.2.2"
    ],
    "agent.version": [
      "7.16.2"
    ],
    "container.labels.com_docker_compose_depends_on": [
      ""
    ],
    "container.labels.com_docker_compose_container-number.keyword": [
      "1"
    ],
    "stream.keyword": [
      "stderr"
    ],
    "container.labels.com_docker_compose_config-hash": [
      "29129dac1567d42191497fbdaa4e14f37ab58c37fe176c4148a36f16d7a6ea4a"
    ],
    "input.type.keyword": [
      "container"
    ],
    "tags.keyword": [
      "_jsonparsefailure",
      "beats_input_codec_json_applied"
    ],
    "container.labels.com_docker_compose_depends_on.keyword": [
      ""
    ],
    "container.labels.com_docker_compose_service.keyword": [
      "some_application"
    ],
    "agent.type": [
      "filebeat"
    ],
    "stream": [
      "stderr"
    ],
    "container.labels.com_docker_compose_oneoff.keyword": [
      "False"
    ],
    "@version": [
      "1"
    ],
    "container.labels.com_docker_compose_config-hash.keyword": [
      "29129dac1567d42191497fbdaa4e14f37ab58c37fe176c4148a36f16d7a6ea4a"
    ],
    "container.image.name.keyword": [
      "library/python:3.9-alpine"
    ],
    "log.file.path.keyword": [
      "/var/lib/docker/containers/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c-json.log"
    ],
    "agent.type.keyword": [
      "filebeat"
    ],
    "agent.ephemeral_id.keyword": [
      "bec8503a-e548-40a0-9ed1-a3e832f6f971"
    ],
    "container.labels.com_docker_compose_project.keyword": [
      "elk"
    ],
    "agent.name.keyword": [
      "d06ab0375ab7"
    ],
    "message": [
      "ERROR:root:OH NO!!!!!!"
    ],
    "container.labels.com_docker_compose_version": [
      "2.2.2"
    ],
    "container.labels.com_docker_compose_oneoff": [
      "False"
    ],
    "@timestamp": [
      "2022-04-20T04:28:40.215Z"
    ],
    "log.file.path": [
      "/var/lib/docker/containers/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c/7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c-json.log"
    ],
    "agent.ephemeral_id": [
      "bec8503a-e548-40a0-9ed1-a3e832f6f971"
    ],
    "container.labels.com_docker_compose_container-number": [
      "1"
    ],
    "container.id.keyword": [
      "7de09c2ef6b59478883fc6568c99d7699326e270bcd99cc471df3eb458b4c57c"
    ],
    "container.labels.com_docker_compose_project_config_files": [
      "/root/learning-monitoring/ELK/docker-compose.yml"
    ]
  }
}
```
### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

 
