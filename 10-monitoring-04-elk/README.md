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
2. Страница с логами контейнера **filebeat**:

![screen-logs-filebeat-elk](/10-monitoring-04-elk/Files/screen-logs-filebeat-elk.png)

3. Логи Filebeat:
![screen-logs-filebeat-elk-2](/10-monitoring-04-elk/Files/screen-logs-filebeat-elk-2.png)
---

4. Вот такой json файл приходит от Filebeat в Logstash при нормальной передачи логов.
```json
{
  "_index": "logstash-2022.04.19",
  "_type": "_doc",
  "_id": "E8cVQIAB4iChi9AGHMV2",
  "_version": 1,
  "_score": 1,
  "_source": {
    "port": 33088,
    "message": "\\xDBl\\xE0\\xAC­嚇\\a\\xF0p3\\x8Fo3\\xB8oxj玩\\x9D\\x86'\\x90\\u0018\\x9E@\\xA2#\\x81\\xC4+\\xF3\\u0005\\xD6|\\b\\f?\\x85\\xC9\\xF0S\\x98\\f?\\x85\\xE9`Oa\\\"`z\\xD6\\xED\\u0003\\xD5.Xw\\b\\u0013X\\x87\\x8E\\xEB[\\xE5n\\u0004\\\"\\xE4\\u0019\\x87\\xD30H\\xCA\\u0014Ex\\x949~\\xF5\\xDC \\u0011\\xF2\\xB4V\\x8A|\\x9A\\xE4\\xBBD\\xC9\\xEB\\u000E\\xA6\\xA0V\\xA5@#(\\x9BnYj\\x91\\xEDsѾ\\xB8\\xD4\\xD4<\\xAB7/\\ew\\xF7\\xD1y\\xBE\\xDA\\xF9*\\rd\\u000F\\u0000\\xB85\\u0012\\xA0\\xFF\\u001C\\xE5m\\x8B+M\\xD8{ͽ\\xAFP\\xE1\\xEC\\x83\\v8\\xF3LY\\xCD\\u0005\\xD0p<\\xFD\\x9C\\xC0\\x99[\\xCAj*@\\u0004\\u0013,\\x81K=<\\xC1\\x99R\\xB2\\xAAE6\\xBE\\u000F\\u0004\\xC8\\u001A\\u0004j\\u0000\\xC0\\xB5&\\u0004\\xE8\\u001A\\\"*\\x84H\\xB1\\u0014ti\\xA2\\xC39\\u00040X\\x9D\\b\\xC9",
    "@version": "1",
    "@timestamp": "2022-04-19T04:29:26.845Z",
    "host": "filebeat.elk_elastic",
    "tags": [
      "_jsonparsefailure"
    ]
  },
  "fields": {
    "@timestamp": [
      "2022-04-19T04:29:26.845Z"
    ],
    "port": [
      33088
    ],
    "tags.keyword": [
      "_jsonparsefailure"
    ],
    "@version": [
      "1"
    ],
    "host": [
      "filebeat.elk_elastic"
    ],
    "host.keyword": [
      "filebeat.elk_elastic"
    ],
    "message": [
      "\\xDBl\\xE0\\xAC­嚇\\a\\xF0p3\\x8Fo3\\xB8oxj玩\\x9D\\x86'\\x90\\u0018\\x9E@\\xA2#\\x81\\xC4+\\xF3\\u0005\\xD6|\\b\\f?\\x85\\xC9\\xF0S\\x98\\f?\\x85\\xE9`Oa\\\"`z\\xD6\\xED\\u0003\\xD5.Xw\\b\\u0013X\\x87\\x8E\\xEB[\\xE5n\\u0004\\\"\\xE4\\u0019\\x87\\xD30H\\xCA\\u0014Ex\\x949~\\xF5\\xDC \\u0011\\xF2\\xB4V\\x8A|\\x9A\\xE4\\xBBD\\xC9\\xEB\\u000E\\xA6\\xA0V\\xA5@#(\\x9BnYj\\x91\\xEDsѾ\\xB8\\xD4\\xD4<\\xAB7/\\ew\\xF7\\xD1y\\xBE\\xDA\\xF9*\\rd\\u000F\\u0000\\xB85\\u0012\\xA0\\xFF\\u001C\\xE5m\\x8B+M\\xD8{ͽ\\xAFP\\xE1\\xEC\\x83\\v8\\xF3LY\\xCD\\u0005\\xD0p<\\xFD\\x9C\\xC0\\x99[\\xCAj*@\\u0004\\u0013,\\x81K=<\\xC1\\x99R\\xB2\\xAAE6\\xBE\\u000F\\u0004\\xC8\\u001A\\u0004j\\u0000\\xC0\\xB5&\\u0004\\xE8\\u001A\\\"*\\x84H\\xB1\\u0014ti\\xA2\\xC39\\u00040X\\x9D\\b\\xC9"
    ],
    "tags": [
      "_jsonparsefailure"
    ]
  }
}
```
### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

 
