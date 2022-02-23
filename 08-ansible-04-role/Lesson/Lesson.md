### Ход выполнения ДЗ по теме "8.4 Работа с Roles"

## Домашнее задание к занятию "8.4 Работа с Roles" - Захаров Сергей Николаевич

## Подготовка к выполнению
1. Создайте два пустых публичных репозитория в любом своём проекте: kibana-role и filebeat-role.
2. Добавьте публичную часть своего ключа к своему профилю в github.

Локальная директория на учебном ПК `root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible# `

## Основная часть

Наша основная цель - разбить наш playbook на отдельные roles. 
Задача: 
* сделать roles для:
  - elastic, 
  - kibana, 
  - filebeat и 
* написать playbook для использования этих ролей. 

Ожидаемый результат: 
- существуют:
  - два ваших репозитория с roles и 
  - один репозиторий с playbook.

1. Создать в старой версии playbook файл `requirements.yml` и заполнить его следующим содержимым:
   ```yaml
   ---
     - src: git@github.com:netology-code/mnt-homeworks-ansible.git
       scm: git
       version: "2.1.4"
       name: elastic 
   ```
2. При помощи `ansible-galaxy` скачать себе эту роль.
* Скачать себе - это значит в свой локальный репозиторий, где расположен `ansible-playbook`, запустить команду 
  - `ansible-galaxy install -r requirements.yml -p elasticsearch_role`
* Скачивание произойдет с удаленного репозитрия на основании данный в файле `requirements.yml`

```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible# ansible-galaxy install -r requirements.yml -p roles
Starting galaxy role install process
- extracting elastic to /root/ansible-learning/yandex-cloud/Dzeta/ansible/roles/elastic
- elastic (2.1.4) was installed successfully
```
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible# ansible-galaxy role list /root/ansible-learning/yandex-cloud/Dzeta/ansible/roles/elastic/
# /root/ansible-learning/yandex-cloud/Dzeta/ansible/roles/elastic
- /root/ansible-learning/yandex-cloud/Dzeta/ansible/roles/elastic/, 2.1.4

```


* Примеры установки, удаления ролей с помощью `ansible-galaxy`

 ```ps
 root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Epsilon/Galaxy# ansible-galaxy install -r requirements.yml -p elasticsearch_role
Starting galaxy role install process
- extracting elastic to /root/ansible-learning/yandex-cloud/Galaxy/roles/elastic
- elastic (2.1.4) was installed successfully

 ```
 
 ```ps
 root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list elastic
# /root/.ansible/roles
- elastic, 2.1.4
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list kibana_role
[WARNING]: - the role kibana_role was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list kibana_roles
[WARNING]: - the role kibana_roles was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list kibana_role
[WARNING]: - the role kibana_role was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# 
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy remove elastic
- successfully removed elastic
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list elastic
[WARNING]: - the role elastic was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy install -r requirements.yml -p roles
Starting galaxy role install process
- extracting elastic to /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic
- elastic (2.1.4) was installed successfully
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list elastic
[WARNING]: - the role elastic was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic
# /root/ansible-learning/yandex-cloud/Alfa/ansible/roles
- /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic, 2.1.4
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy remove /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic
- successfully removed /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic
 ```
 
 ```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Alfa/ansible# ansible-galaxy role list /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic
[WARNING]: - the role /root/ansible-learning/yandex-cloud/Alfa/ansible/roles/elastic was not found
[WARNING]: - the configured path /usr/share/ansible/roles does not exist.
[WARNING]: - the configured path /etc/ansible/roles does not exist.

 ```
 
 
3. Создать новый каталог с ролью при помощи `ansible-galaxy role init kibana-role`.
* Перейти в каталог `roles` и запустить команду. Все каталоги для новой роли будут созданы здесь.

```ps
 root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# 
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# ansible-galaxy role init kibana
- Role kibana was created successfully
```
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# 
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# ansible-galaxy role init filebeat
- Role filebeat was created successfully
```
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# ls -l
итого 12
drwxr-xr-x 10 root root 4096 фев 23 15:43 elastic
drwxr-xr-x 10 root root 4096 фев 23 16:02 filebeat
drwxr-xr-x 10 root root 4096 фев 23 16:02 kibana
```
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Dzeta/ansible/roles# tree
.
├── elastic
│   ├── defaults
│   │   └── main.yml
│   ├── handlers
│   │   └── main.yml
│   ├── Jenkinsfile
│   ├── meta
│   │   └── main.yml
│   ├── molecule
│   │   ├── alternative
│   │   │   ├── converge.yml
│   │   │   ├── molecule.yml
│   │   │   └── verify.yml
│   │   └── default
│   │       ├── converge.yml
│   │       ├── files
│   │       │   └── empty
│   │       ├── molecule.yml
│   │       └── verify.yml
│   ├── README.md
│   ├── tasks
│   │   ├── configure.yml
│   │   ├── download_apt.yml
│   │   ├── download_yum.yml
│   │   ├── install_apt.yml
│   │   ├── install_yum.yml
│   │   ├── main.yml
│   │   └── precheck.yml
│   ├── templates
│   │   └── elasticsearch.yml.j2
│   ├── test-requirements.txt
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   ├── tox.ini
│   └── vars
│       └── main.yml
├── filebeat
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── README.md
│   ├── tasks
│   │   └── main.yml
│   ├── templates
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
└── kibana
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── README.md
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml

30 directories, 41 files

 ```

4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 


Разбираем плейбук на отдельные файлы

* `/roles/kibana/handler/main.yml`

```yml
---
# handlers file for kibana

  - name: restart Elasticsearch
    become: true
    service:
      name: elasticsearch
      state: restarted

```
* `/roles/kibana/tasks/main.yml`

```yml

```
* `/roles/kibana/tasks/configure.yml`
```yml
---

    - name: Configure Kibana
      become: true
      template:
        src: kibana.yml.j2
        dest: /etc/kibana/kibana.yml
      notify: restart kibana


```
* `/roles/kibana/tasks/download_kibana_rpm.yml`
```yml
---

- name: "Download Kibana's rpm"
      get_url:
        url: "https://artifacts.elastic.co/downloads/kibana/kibana-{{ elk_stack_version }}-x86_64.rpm"
        dest: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
      register: download_kibana
      until: download_kibana is succeeded

```
* `/roles/kibana/tasks/install_kibana.yml`
```yml
---

    - name: Install Kibana
      become: true
      yum:
        name: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
        state: present
      notify: restart kibana

```

* Разнесим переменные между `vars` и `default`.

`/roles/kibana/default/main.yml`
```yml
---
# defaults file for kibana
#
#

elk_stack_version: "7.14.0"

kibana_version: "7.14.0"

```
5. Перенести нужные шаблоны конфигов в `templates`.
* `/roles/kibana/templates/kibana.yml.j2`
```ps
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://{{ hostvars['el-instance']['ansible_facts']['default_ipv4']['address'] }}:9200"]
kibana.index: ".kibana"

```
6. Создать новый каталог с ролью при помощи `ansible-galaxy role init filebeat-role`.
* Перейти в каталог `roles` и запустить команду. Все каталоги для новой роли будут созданы здесь.
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Galaxy/roles# ansible-galaxy role init filebeat_role
- Role filebeat_role was created successfully

```
7. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 

```ps

```
8. Перенести нужные шаблоны конфигов в `templates`.

```ps

```
9. Описать в `README.md` обе роли и их параметры.

```ps

```
10. Выложите все roles в репозитории. Проставьте тэги, используя семантическую нумерацию.

```ps

```
11. Добавьте roles в `requirements.yml` в playbook.

```yml
   ---
     - src: git@github.com:
       scm: git
       version: "2.1.4"
       name: elastic 
     - src: git@github.com:
       scm: git
       version: "2.1.4"
       name: kibana 
     - src: git@github.com:
       scm: git
       version: "2.1.4"
       name: filebeat 

```
12. Переработайте playbook на использование roles.

```yml

```
13. Выложите playbook в репозиторий.

```ps

```
14. В ответ приведите ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли logstash.

```ps

```
2. Создайте дополнительный набор tasks, который позволяет обновлять стек ELK.

```ps

```
3. Убедитесь в работоспособности своего стека: установите logstash на свой хост с elasticsearch, настройте конфиги logstash и filebeat так, чтобы они взаимодействовали друг с другом и elasticsearch корректно.

```ps

```
4. Выложите logstash-role в репозиторий. В ответ приведите ссылку.

```ps

```

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
