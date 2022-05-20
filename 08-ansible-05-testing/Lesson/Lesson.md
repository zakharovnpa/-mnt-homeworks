## Ход выполнения ДЗ по теме "08.05 Тестирование Roles"
---
Рабочая директория:
```
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/
```
---

## Подготовка к выполнению
1. Установите molecule: `pip3 install "molecule==3.4.0"`
```ps
root@server1:~/learning-ansible/Lesson-ansible-05# molecule --version
molecule 3.6.1 using python 3.8 
    ansible:2.12.2
    delegated:3.6.1 from molecule
```
2. Установите ``molecule_docker
```ps
pip3 install "molecule_docker<0.3"
```
```ps
Installing collected packages: websocket-client, docker, molecule-docker
Successfully installed docker-5.0.3 molecule-docker-0.2.4 websocket-client-1.3.1
```
```ps
docker --version
Docker version 20.10.12, build e91ed57
```
```
root@server1:~/learning-ansible/Lesson-ansible-05# pip3 list | grep molecule-docker
molecule-docker        0.2.4 
```

3. Соберите локальный образ на основе [Dockerfile](/08-ansible-05-testing/Lecture/Dockerfile). Это нужно для тестиования TOX на роли Elasticsearche
```ps
FROM registry.redhat.io/rhel8/podman:latest

ENV MOLECULE_NO_LOG false

RUN yum reinstall glibc-common -y
RUN yum update -y && yum install tar gcc make python3-pip zlib-devel openssl-devel yum-utils libffi-devel -y

ADD https://www.python.org/ftp/python/3.6.13/Python-3.6.13.tgz Python-3.6.13.tgz
RUN tar xf Python-3.6.13.tgz && cd Python-3.6.13/ && ./configure && make && make altinstall
ADD https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tgz Python-3.7.10.tgz
RUN tar xf Python-3.7.10.tgz && cd Python-3.7.10/ && ./configure && make && make altinstall
ADD https://www.python.org/ftp/python/3.8.8/Python-3.8.8.tgz Python-3.8.8.tgz
RUN tar xf Python-3.8.8.tgz && cd Python-3.8.8/ && ./configure && make && make altinstall
ADD https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz Python-3.9.2.tgz
RUN tar xf Python-3.9.2.tgz && cd Python-3.9.2/ && ./configure && make && make altinstall
RUN python3 -m pip install --upgrade pip && pip3 install tox selinux
RUN rm -rf Python-*
```
* Альтернативный Dockerfile
```
FROM rancher/dind:latest

ENV MOLECULE_NO_LOG false

RUN apt reinstall glibc-common -y
RUN apt update -y && apt install tar gcc make python3-pip zlib-devel openssl-devel yum-utils libffi-devel -y

ADD https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tgz Python-3.7.10.tgz
RUN tar xf Python-3.7.10.tgz && cd Python-3.7.10/ && ./configure && make && make altinstall
ADD https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz Python-3.9.2.tgz
RUN tar xf Python-3.9.2.tgz && cd Python-3.9.2/ && ./configure && make && make altinstall
RUN python3 -m pip install --upgrade pip && pip3 install tox selinux
RUN rm -rf Python-*
```

Образ собран.
```ps
root@server1:~/learning-ansible/Lesson-ansible-05# docker image list
REPOSITORY                        TAG        IMAGE ID       CREATED         SIZE
<none>                            <none>     834eb9e51514   6 minutes ago   2.51GB
registry.redhat.io/rhel8/podman   latest     f58db8adf7bb   5 weeks ago     399MB

```

## Основная часть

Наша основная цель:
- настроить тестирование наших ролей. 

Задача: 
- сделать сценарии тестирования для:
  - kibana, 
  - filebeat. 

Ожидаемый результат: 
- все сценарии успешно проходят тестирование ролей.

### Molecule

#### 1. Запустите  `molecule test` внутри корневой директории `elasticsearch-role`, посмотрите на вывод команды.

* Необходимо, чтобы было установлено: - `molecule`, `docker`, `molecule_docker` пакетик.
```
root@server1:~# docker --version
Docker version 20.10.12, build e91ed57
root@server1:~# 
root@server1:~# molecule --version
molecule 3.4.0 using python 3.8 
    ansible:2.12.2
    delegated:3.4.0 from molecule
    docker:0.2.4 from molecule_docker

```
```
root@server1:~/learning-ansible/Lesson-ansible-05# pip3 list | grep molecule-docker
molecule-docker        0.2.4 
```

* Запуск `molecule test`
```make
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles# molecule test
INFO     default scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Guessed /root/learning-ansible/Lesson-ansible-05/ansible/playbook as project root directory
WARNING  Computed fully qualified role name of elasticsearch_roles does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Using /root/.cache/ansible-lint/ef1620/roles/elasticsearch_roles symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Added ANSIBLE_ROLES_PATH=~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/root/.cache/ansible-lint/ef1620/roles
INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > lint
INFO     Lint is disabled.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=el-instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
ok: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '185701469609.56699', 'results_file': '/root/.ansible_async/185701469609.56699', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [Log into a Docker registry] **********************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}) 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True})

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}) 

TASK [Discover local Docker images] ********************************************
ok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}, 'ansible_loop_var': 'item', 'i': 0, 'ansible_index_var': 'i'})

TASK [Build an Ansible compatible image (new)] *********************************
skipping: [localhost] => (item=molecule_local/docker.io/pycontribs/centos:7) 

TASK [Create docker network(s)] ************************************************

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True})

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=el-instance)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '282463602062.56888', 'results_file': '/root/.ansible_async/282463602062.56888', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=5    changed=2    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [el-instance]

TASK [Include elasticsearch_roles] *********************************************
[DEPRECATION WARNING]: "include" is deprecated, use include_tasks/import_tasks 
instead. This feature will be removed in version 2.16. Deprecation warnings can
 be disabled by setting deprecation_warnings=False in ansible.cfg.

TASK [elasticsearch_roles : Download Elasticsearch's rpm] **********************
changed: [el-instance]

TASK [elasticsearch_roles : Install Elasticsearch] *****************************
changed: [el-instance]

TASK [elasticsearch_roles : Configure Elasticsearch] ***************************
changed: [el-instance]

RUNNING HANDLER [elasticsearch_roles : restart Elasticsearch] ******************
fatal: [el-instance]: FAILED! => {"changed": false, "msg": "Service is in unknown state", "status": {}}

NO MORE HOSTS LEFT *************************************************************

PLAY RECAP *********************************************************************
el-instance                : ok=4    changed=3    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0

CRITICAL Ansible return code was 2, command was: ['ansible-playbook', '--inventory', '/root/.cache/molecule/elasticsearch_roles/default/inventory', '--skip-tags', 'molecule-notest,notest', '/root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles/molecule/default/converge.yml']
WARNING  An error occurred during the test sequence action: 'converge'. Cleaning up.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=el-instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '850062790143.58161', 'results_file': '/root/.ansible_async/850062790143.58161', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:7', 'name': 'el-instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory


```

* Заходим в директорию роли и запускаем `molecule init scenario`
```ps
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles# molecule init scenario Alfa --driver-name docker
CRITICAL The default scenario not found.  Please create a scenario named 'default' first.
```
```ps
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles# molecule init scenario default --driver-name docker
INFO     Initializing new scenario default...
INFO     Initialized scenario in /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles/molecule/default successfully.

```
```ps
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles# molecule test
INFO     default scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Guessed /root/learning-ansible/Lesson-ansible-05/ansible/playbook as project root directory
WARNING  Computed fully qualified role name of elasticsearch_roles does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Using /root/.cache/ansible-lint/ef1620/roles/elasticsearch_roles symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Added ANSIBLE_ROLES_PATH=~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/root/.cache/ansible-lint/ef1620/roles
INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > lint
INFO     Lint is disabled.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
ok: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '491121043162.51591', 'results_file': '/root/.ansible_async/491121043162.51591', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [Log into a Docker registry] **********************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}) 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True})

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}) 

TASK [Discover local Docker images] ********************************************
ok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item', 'i': 0, 'ansible_index_var': 'i'})

TASK [Build an Ansible compatible image (new)] *********************************
skipping: [localhost] => (item=molecule_local/docker.io/pycontribs/centos:8) 

TASK [Create docker network(s)] ************************************************

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True})

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (299 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (298 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (297 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (296 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (295 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (294 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (293 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (292 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (291 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (290 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (289 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (288 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (287 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (286 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (285 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '685605531567.51781', 'results_file': '/root/.ansible_async/685605531567.51781', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=5    changed=2    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include elasticsearch_roles] *********************************************
[DEPRECATION WARNING]: "include" is deprecated, use include_tasks/import_tasks 
instead. This feature will be removed in version 2.16. Deprecation warnings can
 be disabled by setting deprecation_warnings=False in ansible.cfg.

TASK [elasticsearch_roles : Download Elasticsearch's rpm] **********************
changed: [instance]

TASK [elasticsearch_roles : Install Elasticsearch] *****************************
fatal: [instance]: FAILED! => {"changed": false, "msg": "Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist", "rc": 1, "results": []}

PLAY RECAP *********************************************************************
instance                   : ok=2    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0

CRITICAL Ansible return code was 2, command was: ['ansible-playbook', '--inventory', '/root/.cache/molecule/elasticsearch_roles/default/inventory', '--skip-tags', 'molecule-notest,notest', '/root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/elasticsearch_roles/molecule/default/converge.yml']
WARNING  An error occurred during the test sequence action: 'converge'. Cleaning up.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '864738462699.52986', 'results_file': '/root/.ansible_async/864738462699.52986', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory

```

#### 2. Перейдите в каталог с ролью `kibana-role` и создайте сценарий тестирования по умолчаню при помощи `molecule init scenario --driver-name docker`.
Можно использовать любые драверы. (а какме есть? Delegate, )
```ps
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles# molecule init scenario --driver-name docker
INFO     Initializing new scenario default...
INFO     Initialized scenario in /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/molecule/default successfully.
```
После выполнения команды созданы директории и файлы:
```
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles# ls -l molecule/default/
total 12
-rw-r--r-- 1 root root 127 Mar  8 09:44 converge.yml
-rw-r--r-- 1 root root 206 Mar  8 09:44 molecule.yml
-rw-r--r-- 1 root root 177 Mar  8 09:44 verify.yml

```
```
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles# tree
.
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── molecule        # Новая директория
│   └── default     # Новая директория. Это же является именем сценария тестирования
│       ├── converge.yml        # Новый файл
│       ├── molecule.yml        # Новый файл
│       └── verify.yml        # Новый файл
├── README.md
├── tasks
│   ├── configure_kibana.yml
│   ├── download_kibana_rpm.yml
│   ├── install_kibana.yml
│   └── main.yml
├── templates
│   └── kibana.yml.j2
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml

9 directories, 15 files
```

* Отключена задача "Конфигурирование Кибана". Была ошибка недоступности Elasticsearch
* На Contos7 не проходит установка. Там не работает systemctl.
* На Ubuntu Kibana установилась, тест молекулы прошел успешно:
```ps
root@server1:~/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles# molecule test
INFO     default scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Guessed /root/learning-ansible/Lesson-ansible-05/ansible/playbook as project root directory
WARNING  Computed fully qualified role name of kibana_roles does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Using /root/.cache/ansible-lint/ef1620/roles/kibana_roles symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Added ANSIBLE_ROLES_PATH=~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/root/.cache/ansible-lint/ef1620/roles
INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > lint
INFO     Lint is disabled.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
ok: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '719388041524.14278', 'results_file': '/root/.ansible_async/719388041524.14278', 'changed': True, 'item': {'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [Log into a Docker registry] **********************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}) 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True})

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}) 

TASK [Discover local Docker images] ********************************************
ok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item', 'i': 0, 'ansible_index_var': 'i'})

TASK [Build an Ansible compatible image (new)] *********************************
skipping: [localhost] => (item=molecule_local/docker.io/pycontribs/ubuntu) 

TASK [Create docker network(s)] ************************************************

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True})

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '322818549455.14474', 'results_file': '/root/.ansible_async/322818549455.14474', 'changed': True, 'item': {'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=5    changed=2    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include kibana_roles] ****************************************************

TASK [kibana_roles : include_tasks] ********************************************
included: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/tasks/download_kibana_deb.yml for instance

TASK [kibana_roles : Download Kibana's deb] ************************************
changed: [instance]

TASK [kibana_roles : include_tasks] ********************************************
included: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/tasks/install_kibana_deb.yml for instance

TASK [kibana_roles : Install Kibana] *******************************************
changed: [instance]

RUNNING HANDLER [kibana_roles : restart kibana] ********************************
changed: [instance]

PLAY RECAP *********************************************************************
instance                   : ok=6    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running default > idempotence

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include kibana_roles] ****************************************************

TASK [kibana_roles : include_tasks] ********************************************
included: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/tasks/download_kibana_deb.yml for instance

TASK [kibana_roles : Download Kibana's deb] ************************************
ok: [instance]

TASK [kibana_roles : include_tasks] ********************************************
included: /root/learning-ansible/Lesson-ansible-05/ansible/playbook/roles/kibana_roles/tasks/install_kibana_deb.yml for instance

TASK [kibana_roles : Install Kibana] *******************************************
ok: [instance]

PLAY RECAP *********************************************************************
instance                   : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier

PLAY [Verify] ******************************************************************

TASK [Example assertion] *******************************************************
ok: [instance] => {
    "changed": false,
    "msg": "All assertions passed"
}

PLAY RECAP *********************************************************************
instance                   : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Verifier completed successfully.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '514117568756.16411', 'results_file': '/root/.ansible_async/514117568756.16411', 'changed': True, 'item': {'image': 'docker.io/pycontribs/ubuntu', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

TASK [Delete docker network(s)] ************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory


```

#### 3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

* Для успешного тестирования с помощью Молекулы ролей, используемых на разных дитсрибутивах, необходимо:
  * В каждой роли обезличить название файлов для тасок. Например было `diwnload_kibana_rpm.yml` станет `download_rmp.yml`.
  * Добавить в таски для каждой роли (/tasks) проверку фактов каждого инстанса на то, какой установлчный пакет там действует. 
```
- include_tasks: "download_{{ ansible_facts.pkg_mgr }}.yml"
- include_tasks: "install_{{ ansible_facts.pkg_mgr }}.yml"

```
  * Сделать разные файлы для скачивания и установки пактов с дистрибутивами
  * cat download_apt.yml 
```

---
- name: "Download Elasticsearch's deb"
  get_url:
    url: "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{{ elasticsearch_version }}-amd64.deb"
    dest: "files/elasticsearch-{{ elasticsearch_version }}-amd64.deb"
    validate_certs: false
  delegate_to: localhost
  register: download_elastic
  until: download_elastic is succeeded
  when: elastic_install_type == 'remote'
- name: Copy Elasticsearch to manage host
  copy:
    src: "files/elasticsearch-{{ elasticsearch_version }}-amd64.deb"
    mode: 0755
    dest: "/tmp/elasticsearch-{{ elasticsearch_version }}-amd64.deb"

```
  * cat download_yum.yml 
```
---
- name: "Download Elasticsearch's rpm"
  get_url:
    url: "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"
    dest: "files/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"
    validate_certs: false
  register: download_elastic
  delegate_to: localhost
  until: download_elastic is succeeded
  when: elastic_install_type == 'remote'
- name: Copy Elasticsearch to managed node
  copy:
    src: "files/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"
    mode: 0755
    dest: "/tmp/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"

```
  * cat install_apt.yml 
```
---
- name: Install Elasticsearch
  become: true
  apt:
    deb: "/tmp/elasticsearch-{{ elasticsearch_version }}-amd64.deb"
    state: present
  notify: restart Elasticsearch

```
  * cat install_yum.yml 
```
---
- name: Install Elasticsearch
  become: true
  yum:
    name: "/tmp/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"
    state: present
  notify: restart Elasticsearch

```
* План такой:
  * В файле /molecule/default/molecule.yml указать какие инстансы будут собираться на каких дитсрибутивах


* Для этого необходимо в файл `molecule.yml` или `create.yml` добавить информацию.

* файл `molecule.yml`
```yml
---
dependency:
  name: galaxy
driver:
  name: docker
platforms:
  - name: centos-7-instance
    image: docker.io/pycontribs/centos:7
    pre_build_image: true
  - name: ubuntu-instance
    image: docker.io/pycontribs/ubuntu:latest
    pre_build_image: true
  - name: centos-8-instance
    image: docker.io/pycontribs/centos:8
    pre_build_image: true
provisioner:
  name: ansible
verifier:
  name: ansible
```

* Ошибки при запуске тестов:

```make
TASK [elasticsearch_roles : Install Elasticsearch] *****************************

fatal: [ubuntu-instance]: 
FAILED! => {"ansible_facts": {"pkg_mgr": "apt"}, "changed": false, "msg": ["Could not detect which major revision of yum is in use, which is required to determine module backend.", "You should manually specify use_backend to tell the module whether to use the yum (yum3) or dnf (yum4) backend})"]}

fatal: [centos-8-instance]: 
FAILED! => {"changed": false, "msg": "Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist", "rc": 1, "results": []}

changed: [centos-7-instance]

TASK [elasticsearch_roles : Configure Elasticsearch] ***************************
changed: [centos-7-instance]

RUNNING HANDLER [elasticsearch_roles : restart Elasticsearch] ******************
fatal: [centos-7-instance]: FAILED! => {"changed": false, "msg": "Service is in unknown state", "status": {}}


```

* Тоже пример: файл `molecule.yml`
  ```yml
  ---
   dependency:
     name: galaxy
   driver: 
     name: docker #по умолчанию delegated
   platforms:     # перечисление ВМ, которые будут создаваться этим драйвером
   - name: Centos7
     image: docker.io/.../centos:7
     pre_build_image: true  # значит, что образ готов, бери его и используй с именем Centos7
                            # если бы тут было false,то сожно в эту же директорию положить Dockerfile. Molecole автоматически этот образ бы собирала
                            # и использовала
                            
   - name: Ubuntu
      image: docker.io/.../ubuntu:latest
      pre_build_image: true
      
   provisioner:   # кто запускает против тех платформ, которые описаны
     name: ansible
     # сюда же можно разместить group_vars, host_vars
       inventory:
         group_vars:
           group_name:
             name_variables
   verifier:
     ansible
     
   lint: |             # сюда можно добавить линтер. Статический анализ. Здесь прописан bash-script, который построчно вызывает ansible-lint и потом yamllint
                       # скрипты должны лежать здесь: etc/bash_completion.d.
     ansible-lint .
     yamllint .
   
   scenario:            # сюда можно добавить какие scenario будут запускаться. Определение последовательности выполнения шагов внутри сценария
     - default
     - <name_scenery>
   ```

4. Добавьте несколько assert'ов в `verify.yml` файл, для  проверки работоспособности kibana-role (проверка, что web отвечает, проверка логов, etc).   Например,`curl http://localhost` или проверить, что файл лога создался. Хотябы такой `verify.yml` сделать.

* Запустите тестирование роли повторно и проверьте, что оно прошло успешно. 

5. Повторите шаги 2-4 для `filebeat-role`. Тлько проверки какие-то другие будут.
6. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием. И пушим все это дело.

### Tox

1. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/elasticsearch-role -w /opt/elasticsearch-role -it <image_name> /bin/bash`, где path_to_repo - путь до корня репозитория с elasticsearch-role на вашей файловой системе.

2. Внутри контейнера выполните команду `tox`, посмотрите на вывод.

3. Добавьте файл `tox.ini` в корень репозитория каждой своей роли.
Можно взять готовый файл от Алексея Метлякова.
4. Создайте облегчённый сценарий для `molecule`. Проверьте его на исполнимость. Облегченный (destroy, create, converge, destroy). `molecule test -s <name_new_scenery>`. И он просто прогонится.
5. Пропишите правильную команду в `tox.ini` для того чтобы запускался облегчённый сценарий.
6. Запустите `docker` контейнер так, чтобы внутри оказались обе ваши роли.
7. Зайдти поочерёдно в каждую из них и запустите команду `tox`. Убедитесь, что всё отработало успешно.
8. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

После выполнения у вас должно получится:
- два сценария `molecule` и один `tox.ini` файл в каждом репозитории. 
 
Ссылки на репозитории являются ответами на домашнее задание. Не забудьте указать в ответе теги решений Tox и Molecule заданий.

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли logstash.
2. Создайте дополнительный набор tasks, который позволяет обновлять стек ELK.
3. В ролях добавьте тестирование в раздел `verify.yml`. Данный раздел должен проверять, что logstash через команду `logstash -e 'input { stdin { } } output { stdout {} }'`  отвечате адекватно.
4. Создайте сценарий внутри любой из своих ролей, который умеет поднимать весь стек при помощи всех ролей.
5. Убедитесь в работоспособности своего стека. Создайте отдельный `verify.yml`, который будет проверять работоспособность интеграции всех инструментов между ними.
6. Выложите свои roles в репозитории. В ответ приведите ссылки.
