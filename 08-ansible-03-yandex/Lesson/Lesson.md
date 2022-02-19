### Ход выполнения ДЗ по теме "08.03 Использование Yandex Cloud"

# Домашнее задание к занятию "08.03 Использование Yandex Cloud"

## Подготовка к выполнению
1. Создайте свой собственный (или используйте старый) публичный репозиторий на github с произвольным именем.
2. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть
1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.
2. При создании tasks рекомендую использовать модули: `get_url`, `template`, `yum`, `apt`.
3. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.
4. Приготовьте свой собственный inventory файл `prod.yml`.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.
6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
9. Проделайте шаги с 1 до 8 для создания ещё одного play, который устанавливает и настраивает filebeat.
10. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.
11. Готовый playbook выложите в свой репозиторий, в ответ предоставьте ссылку на него.

---

#### После запуска тестовой среды (инстансы на Я.Облаке) 
##### Запуск плуйбука для установки Elasticsearch `ansible-playbook site.yml -i inventory/prod/hosts.yml `

```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible# ansible-playbook site.yml -i inventory/prod/hosts.yml 

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Download Elasticsearch's rpm] **************************************************************************************************************************************************************************
changed: [el-instance]

TASK [Install Elasticsearch] *********************************************************************************************************************************************************************************
changed: [el-instance]

TASK [Configure Elasticsearch] *******************************************************************************************************************************************************************************
changed: [el-instance]

RUNNING HANDLER [restart Elasticsearch] **********************************************************************************************************************************************************************
changed: [el-instance]

PLAY RECAP ***************************************************************************************************************************************************************************************************
el-instance                : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```

```ps
[root@el-instance ~]# systemctl status elasticsearch
● elasticsearch.service - Elasticsearch
   Loaded: loaded (/usr/lib/systemd/system/elasticsearch.service; disabled; vendor preset: disabled)
   Active: active (running) since Сб 2022-02-19 06:49:03 UTC; 11min ago
     Docs: https://www.elastic.co
 Main PID: 10029 (java)
   CGroup: /system.slice/elasticsearch.service
           ├─10029 /usr/share/elasticsearch/jdk/bin/java -Xshare:auto -Des.networkaddress.cache.ttl=60 -Des.networkaddress.cache.negative.ttl=10 -XX:+AlwaysPreTouch -Xss1m -Djava.awt.headless=true -Dfile...
           └─10232 /usr/share/elasticsearch/modules/x-pack-ml/platform/linux-x86_64/bin/controller

фев 19 06:48:40 el-instance.netology.yc systemd[1]: Starting Elasticsearch...
фев 19 06:49:03 el-instance.netology.yc systemd[1]: Started Elasticsearch.

```
*  Тест обращения к веб-интерфейсу Elasticsearch
```ps
[root@el-instance ~]# curl http://127.0.0.1:9200
{
  "name" : "node-a",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "9RMvH5PoTbKalEmhWUkyWA",
  "version" : {
    "number" : "7.14.0",
    "build_flavor" : "default",
    "build_type" : "rpm",
    "build_hash" : "dd5a0a2acaa2045ff9624f3729fc8a6f40835aa1",
    "build_date" : "2021-07-29T20:49:32.864135063Z",
    "build_snapshot" : false,
    "lucene_version" : "8.9.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```
![Страница сервера с Elasticsearch](/08-ansible-03-yandex/files/Elasticsearch-server-pages.png)

##### Добавление в плейбук плей для установки Kibana

```ps

```


### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
