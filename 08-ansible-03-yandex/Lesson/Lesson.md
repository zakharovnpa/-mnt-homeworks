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
- name: Install Kubana
  hosts: kibana
  handlers:
    - name: restart Kibana
      become: true
      service:
        name: kibana
        state: restarted
  tasks:
    - name: "Download Kibana's rpm"
      get_url:
        url: "https://artifacts.elastic.co/downloads/kibana/kibana-{{ elk_stack_version }}-x86_64.rpm"
        dest: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
      register: download_kibana
      until: download_kibana is succeeded
    - name: Install Kibana
      become: true
      yum:
        name: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
        state: present
    - name: Configure Kibana
      become: true
      template:
        src: kibana.yml.j2
        dest: /etc/kibana/kibana.yml
      notify: restart kibana



```
* Т.к. нам необходимо соблюcти единство версий для Elasticdearch  и Kibana, то переносим файл `elasticsearch.yml`  в директорию `inventory/prod/group_vars/all` 
* Также предварительно в файл `hosts.yml` был добавлен IP адреса нового инстанса для Кибаны
#### Запуск `ansible-playbook` для установки Кибана
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible# ansible-playbook site.yml -i inventory/prod/hosts.yml

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Download Elasticsearch's rpm] **************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Install Elasticsearch] *********************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Configure Elasticsearch] *******************************************************************************************************************************************************************************
ok: [el-instance]

PLAY [Install Kubana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Download Kibana's rpm] *********************************************************************************************************************************************************************************
changed: [k-instance]

TASK [Install Kibana] ****************************************************************************************************************************************************************************************
changed: [k-instance]

TASK [Configure Kibana] **************************************************************************************************************************************************************************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: If you are using a module and expect the file to exist on the remote, see the remote_src option
fatal: [k-instance]: FAILED! => {"changed": false, "msg": "Could not find or access 'kibana.yml.j2'\nSearched in:\n\t/root/ansible-learning/yandex-cloud/Epsilon/ansible/templates/kibana.yml.j2\n\t/root/ansible-learning/yandex-cloud/Epsilon/ansible/kibana.yml.j2\n\t/root/ansible-learning/yandex-cloud/Epsilon/ansible/templates/kibana.yml.j2\n\t/root/ansible-learning/yandex-cloud/Epsilon/ansible/kibana.yml.j2 on the Ansible Controller.\nIf you are using a module and expect the file to exist on the remote, see the remote_src option"}

PLAY RECAP ***************************************************************************************************************************************************************************************************
el-instance                : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
k-instance                 : ok=3    changed=2    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   

```
```ps
[root@k-instance ~]# systemctl status kibana
● kibana.service - Kibana
   Loaded: loaded (/etc/systemd/system/kibana.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://www.elastic.co

```

* Завершилось с ошибкой конфигурирования Кибана, т.к. ранее не был настроен файл шаблона.
#### Перенос на `control_node` файла `kibana.yml` для создания шаблона конфигурации
```ps
[root@k-instance ~]# ls /etc/kibana/kibana.yml 
/etc/kibana/kibana.yml

```
```ps
[root@k-instance ~]# exit
logout
[centos@k-instance ~]$ 
[centos@k-instance ~]$ cp /etc/kibana/kibana.yml ~
cp: не удалось выполнить stat для «/etc/kibana/kibana.yml»: Отказано в доступе
[centos@k-instance ~]$ 
[centos@k-instance ~]$ sudo cp /etc/kibana/kibana.yml ~
[centos@k-instance ~]$ 
[centos@k-instance ~]$ ls
kibana.yml

```
* Меняем пользоватеоя файла
```ps
[centos@k-instance ~]$ ls -l
итого 8
-rw-r-----. 1 root root 5060 фев 19 08:33 kibana.yml
[centos@k-instance ~]$ 
[centos@k-instance ~]$ chown centos:centos kibana.yml
chown: изменение владельца «kibana.yml»: Операция не позволена
[centos@k-instance ~]$ 
[centos@k-instance ~]$ sudo chown centos:centos kibana.yml
[centos@k-instance ~]$ 
[centos@k-instance ~]$ ls -l
итого 8
-rw-r-----. 1 centos centos 5060 фев 19 08:33 kibana.yml

```
* Подключаемся с `control_node` к инстансу с Кибаной и переносим файл `kibana.yml.j2
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible/templates# scp centos@62.84.127.237:/home/centos/kibana.yml ../templates/kibana.yml.j2
kibana.yml                                                                                                                                                                  100% 5060   191.8KB/s   00:00    
  
```
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible/templates# ls -l
итого 20
-rw-r--r-- 1 root root  224 фев 19 06:21 elasticsearch.yml.j2
-rw-r----- 1 root root 5060 фев 19 12:35 kibana.yml
-rw-r----- 1 root root 5060 фев 19 12:43 kibana.yml.j2

```
* Создан шаблон для Кибана
```ps
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://{{ hostvars['el-instance']['ansible_facts']['default_ipv4']['address'] }}:9200"]
kibana.index: ".kibana"
```
#### Снова запускаем `ansible-playbook`
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible# ansible-playbook site.yml -i inventory/prod/hosts.yml

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Download Elasticsearch's rpm] **************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Install Elasticsearch] *********************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Configure Elasticsearch] *******************************************************************************************************************************************************************************
ok: [el-instance]

PLAY [Install Kubana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Download Kibana's rpm] *********************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Install Kibana] ****************************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Configure Kibana] **************************************************************************************************************************************************************************************
ERROR! The requested handler 'restart kibana' was not found in either the main handlers list nor in the listening handlers list

```
Ошибка связяна с тем, что в файле `site.yml` не одинаково назывались параметры `restart Kibana` `restart kibana`
```ps
  handlers:
    - name: restart kibana
```

```ps
 notify: restart kibana
```
#### После исправления ошибки запускаем `ansible-playbook`
* Все ОК
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/ansible# ansible-playbook site.yml -i inventory/prod/hosts.yml

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Download Elasticsearch's rpm] **************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Install Elasticsearch] *********************************************************************************************************************************************************************************
ok: [el-instance]

TASK [Configure Elasticsearch] *******************************************************************************************************************************************************************************
ok: [el-instance]

PLAY [Install Kubana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Download Kibana's rpm] *********************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Install Kibana] ****************************************************************************************************************************************************************************************
ok: [k-instance]

TASK [Configure Kibana] **************************************************************************************************************************************************************************************
ok: [k-instance]

PLAY RECAP ***************************************************************************************************************************************************************************************************
el-instance                : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
k-instance                 : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
