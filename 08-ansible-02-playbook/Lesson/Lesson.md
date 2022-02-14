### Ход выполнения ДЗ по теме "08.02 Работа с Playbook"

## Подготовка к выполнению
1. Создайте свой собственный (или используйте старый) публичный репозиторий на github с произвольным именем.

Создан репозиторий для выполнения ДЗ [ansible-02-playbook](https://github.com/zakharovnpa/ansible-02-playbook)

2. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

Выполнено

3. Подготовьте хосты в соотвтествии с группами из предподготовленного playbook. 



4. Скачайте дистрибутив [java](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) и положите его в директорию `playbook/files/`. 

* Для скачивания пришлось создать УЗ на сайте Oracle npazakharov@gmail.com pass !+1
* Затем архив перенесен в Яндекс облако.
* Ссылка на скачивание была взята из панели разработчика браузера из кода ссылки на кнопке скачать
* Взятая ссылка была добавлена в ansible-playbook
```yml
---
- name: Check version Java
  hosts: localhost
  tasks:
    - name: Get Java
      ansible.builtin.get_url: 
        url: "https://s804sas.storage.yandex.net/rdisk/1.........Jr3yw5--6yZCSqDDextBgY"
        dest: "/tmp"
        mode: 0755

```

* Также архив был скачан по взятой с облака ссылке командой 
```ps
curl -O https://s804sas.storage.yandex.net/rdisk/139082549d55ac46f6a77591ecb08eb0a6906d0cbdcb3835c5e53c9eb23bc425/6204f0f5/duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A==?uid=34414669&filename=jdk-11.0.14_linux-x64_bin.tar.gz&disposition=attachment&hash=&limit=0&content_type=application%2Fx-gzip&owner_uid=34414669&fsize=168679847&hid=0fef40a053897309e30543619d23226c&media_type=compressed&tknv=v2&etag=c2037b5f2e2a6ddcfbdfe1489bccfd63&rtoken=e7eIqFuC5HZY&force_default=yes&ycrid=na-3c5259ce3e65a7b6dbd193a5b311927b-downloader9h&ts=5d7a7e5b66740&s=0de7ebb3429f68eb20383eac62727d17cf25e161c2a0002a6999baa8a823e503&pb=U2FsdGVkX19pztWLYUf_22d2O81EXLpp5UmZMzfEl5RRL1Fqgz16R1Gmfxbb7NxvH4SRfEK7S94DqcstbEIB5Jr3yw5--6yZCSqDDextBgY
[1] 23125
[2] 23126
[3] 23127
[4] 23128
[5] 23129
[6] 23130
[7] 23131
[8] 23132
[9] 23133
[10] 23134
[11] 23135
[12] 23136
[13] 23137
[14] 23138
[15] 23139
[16] 23140
[17] 23141
[2]   Done                    filename=jdk-11.0.14_linux-x64_bin.tar.gz
[3]   Done                    disposition=attachment
[4]   Done                    hash=
[5]   Done                    limit=0
[6]   Done                    content_type=application%2Fx-gzip
[7]   Done                    owner_uid=34414669
[8]   Done                    fsize=168679847
[9]   Done                    hid=0fef40a053897309e30543619d23226c
[10]   Done                    media_type=compressed
[11]   Done                    tknv=v2
[12]   Done                    etag=c2037b5f2e2a6ddcfbdfe1489bccfd63
[13]   Done                    rtoken=e7eIqFuC5HZY
[14]   Done                    force_default=yes
root@server1:~/TMP#   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   188  100   188    0     0   1382      0 --:--:-- --:--:-- --:--:--  1382

[1]   Done                    curl -O https://s804sas.storage.yandex.net/rdisk/139082549d55ac46f6a77591ecb08eb0a6906d0cbdcb3835c5e53c9eb23bc425/6204f0f5/duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A==?uid=34414669
[15]   Done                    ycrid=na-3c5259ce3e65a7b6dbd193a5b311927b-downloader9h
[16]-  Done                    ts=5d7a7e5b66740
[17]+  Done                    s=0de7ebb3429f68eb20383eac62727d17cf25e161c2a0002a6999baa8a823e503

```

```ps
root@server1:/tmp# ls -lha
total 161M
drwxrwxrwt 11 root root 4.0K Feb 10 07:30  .
drwxr-xr-x 20 root root 4.0K Feb 10 07:26  ..
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
```

```ps
root@server1:/tmp# cp duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A== jdk-11.0.14_linux-x64_bin.tar.gz
root@server1:/tmp# 
root@server1:/tmp# 
root@server1:/tmp# ls -lha
total 322M
drwxrwxrwt 11 root root 4.0K Feb 10 07:37  .
drwxr-xr-x 20 root root 4.0K Feb 10 07:26  ..
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
-rwxr-xr-x  1 root root 161M Feb 10 07:37  jdk-11.0.14_linux-x64_bin.tar.gz


```

```ps
root@server1:/tmp# file jdk-11.0.14_linux-x64_bin.tar.gz
jdk-11.0.14_linux-x64_bin.tar.gz: gzip compressed data, last modified: Tue Dec  7 21:54:31 2021, from Unix, original size modulo 2^32 282060800 gzip compressed data, reserved method, ASCII, extra field, has comment, encrypted, from FAT filesystem (MS-DOS, OS/2, NT), original size modulo 2^32 282060800

```

```ps
root@server1:/tmp# tar -xvf jdk-11.0.14_linux-x64_bin.tar.gz
```

```ps
root@server1:/tmp# ls -lha
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
drwxr-xr-x  9 root root 4.0K Feb 10 07:39  jdk-11.0.14
-rwxr-xr-x  1 root root 161M Feb 10 07:37  jdk-11.0.14_linux-x64_bin.tar.gz


```
```ps
root@server1:/tmp/jdk-11.0.14# ls -lha
total 44K
drwxr-xr-x  9 root  root  4.0K Feb 10 07:39 .
drwxrwxrwt 12 root  root  4.0K Feb 10 07:39 ..
drwxr-xr-x  2 root  root  4.0K Feb 10 07:39 bin
drwxr-xr-x  4 root  root  4.0K Feb 10 07:39 conf
drwxr-xr-x  3 root  root  4.0K Feb 10 07:39 include
drwxr-xr-x  2 root  root  4.0K Feb 10 07:39 jmods
drwxr-xr-x 72 root  root  4.0K Feb 10 07:39 legal
drwxr-xr-x  6 root  root  4.0K Feb 10 07:39 lib
drwxr-xr-x  3 root  root  4.0K Feb 10 07:39 man
-r--r--r--  1 10668 10668  160 Dec  7 21:54 README.html
-rw-r--r--  1 10668 10668 1.3K Dec  7 21:54 release

```
Затем архив перенесен в директорию /files

Доустановка ` ansible-lint `
```ps
root@server1:/tmp# pip3 install ansible-lint
Collecting ansible-lint
  Downloading ansible_lint-5.3.2-py3-none-any.whl (115 kB)
     |████████████████████████████████| 115 kB 1.4 MB/s 
Collecting tenacity
  Downloading tenacity-8.0.1-py3-none-any.whl (24 kB)
Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from ansible-lint) (21.3)
Collecting ruamel.yaml<1,>=0.15.37; python_version >= "3.7"
  Downloading ruamel.yaml-0.17.20-py3-none-any.whl (109 kB)
     |████████████████████████████████| 109 kB 12.5 MB/s 
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from ansible-lint) (5.3.1)
Collecting enrich>=1.2.6
  Downloading enrich-1.2.7-py3-none-any.whl (8.7 kB)
Collecting wcmatch>=7.0
  Downloading wcmatch-8.3-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 1.3 MB/s 
Collecting rich>=9.5.1
  Downloading rich-11.2.0-py3-none-any.whl (217 kB)
     |████████████████████████████████| 217 kB 7.1 MB/s 
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->ansible-lint) (3.0.7)
Collecting ruamel.yaml.clib>=0.2.6; platform_python_implementation == "CPython" and python_version < "3.11"
  Downloading ruamel.yaml.clib-0.2.6-cp38-cp38-manylinux1_x86_64.whl (570 kB)
     |████████████████████████████████| 570 kB 9.0 MB/s 
Collecting bracex>=2.1.1
  Downloading bracex-2.2.1-py3-none-any.whl (12 kB)
Collecting commonmark<0.10.0,>=0.9.0
  Downloading commonmark-0.9.1-py2.py3-none-any.whl (51 kB)
     |████████████████████████████████| 51 kB 5.2 MB/s 
Collecting pygments<3.0.0,>=2.6.0
  Downloading Pygments-2.11.2-py3-none-any.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 8.6 MB/s 
Requirement already satisfied: colorama<0.5.0,>=0.4.0 in /usr/lib/python3/dist-packages (from rich>=9.5.1->ansible-lint) (0.4.3)
Installing collected packages: tenacity, ruamel.yaml.clib, ruamel.yaml, commonmark, pygments, rich, enrich, bracex, wcmatch, ansible-lint
Successfully installed ansible-lint-5.3.2 bracex-2.2.1 commonmark-0.9.1 enrich-1.2.7 pygments-2.11.2 rich-11.2.0 ruamel.yaml-0.17.20 ruamel.yaml.clib-0.2.6 tenacity-8.0.1 wcmatch-8.3

```

```ps
root@server1:/tmp# type ansible-lint
ansible-lint is /usr/local/bin/ansible-lint
root@server1:/tmp# 
root@server1:/tmp# which ansible-lint
/usr/local/bin/ansible-lint


```

## Основная часть
1. Приготовьте свой собственный inventory файл `prod.yml`.

**Ответ:**

- inventory файл `prod.yml`
``` yml
---
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker

  elasticsearch:
    hosts:
      fedore:
        ansible_connection: docker

  kibana:
    hosts:
      fedore-core:
        ansible_connection: docker


```

2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.

**Ответ:**
```
Kibana – тиражируемая свободная программная панель визуализации данных. В процессе использования программы информация, 
проиндексированная в кластере Elasticsearch, представляется в виде диаграмм различных видов, таких как:
- столбчатые,
- линейные,
- точечные,
- круговые,
- а также возможна визуализация данных в привязке к географическим картам.

Как правило, Kibana используется для мониторинга и анализа ИТ-инфраструктуры в составе Elastic Stack (ранее ELK Stack), 
в который помимо нее входят Elasticsearch и Logstash. Logstash отвечает за логирование и поставляет входящий поток данных 
в Elasticsearch для хранения, классификации и поиска. Kibana, в свою очередь, получает доступ к данным Elasticsearch для 
их визуализации в различных визуальных форматах, например – в виде информационных панелей (dashboards) с различными видами диаграмм.
```


Находим в википедии ссылку на [сайт кибаны](https://www.elastic.co/kibana/) 
Находим ссылку на скачивание кибаны [https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz](https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz)

Дописываем playbook 
```yml
---
- name: Install Kibana
  hosts: kibana
  tasks:
    - name: Upload tar.gz Kibana from remote URL
      get_url:
        url: "https://artifacts.elastic.co/downloads/kibana/kibana-{{ kibana_version }}-linux-x86_64.tar.gz"
        dest: "/tmp/kibana-{{ kibana_version }}-linux-x86_64.tar.gz"
        mode: 0755
        timeout: 60
        force: true
        validate_certs: false
      register: get_kibana
      until: get_kibana is succeeded
      tags: kibana
    - name: Create directrory for Kibana
      become: true
      file:
        state: directory
        path: "{{ kibana_home }}"
      tags: kibana
    - name: Extract Kibana in the installation directory
      become: true
      unarchive:
        copy: false
        src: "/tmp/kibana-{{ kibana_version }}-linux-x86_64.tar.gz"
        dest: "{{ kibana_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ kibana_home }}/bin/kibana"
      tags: kibana
    - name: Set environment Kibana
      become: true
      template:
        src: templates/kib.sh.j2
        dest: /etc/profile.d/kib.sh
      tags: kibana


```


3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.

**Ответ:**
Данные модули использованы.

4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.

**Ответ:**

- Версия Кибаны скачивается в соответствии с версией Elasrticsearch
```sh
---
elastic_version: "7.10.1"
elastic_home: "/opt/elastic/{{ elastic_version }}"
```

```sh
---
kibana_version: "7.10.1"
kibana_home: "/opt/kibana/{{ kibana_version }}"

```

- Распаковка выпоняется модулем `unarchive` в сгенеррированную параметрами директорию `/opt/kibana/7.10.1`
```ps
      unarchive:
        copy: false
        src: "/tmp/kibana-{{ kibana_version }}-linux-x86_64.tar.gz"
        dest: "{{ kibana_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ kibana_home }}/bin/kibana"
```


5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

**Ответ:**

Проверка идет на таком окружении: три различных докер-контейнера.
Линтер собщает о том, что не установлены права доступа к файлам.
Данные директории и файлы еще не созданы.

```yml
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-lint 7-site.yml 
WARNING  Overriding detected file kind 'yaml' with 'playbook' for given positional argument: 7-site.yml
WARNING  Listing 7 violation(s) that are fatal
risky-file-permissions: File permissions unset or incorrect
7-site.yml:10 Task/Handler: Upload .tar.gz file containing binaries from local storage

risky-file-permissions: File permissions unset or incorrect
7-site.yml:18 Task/Handler: Ensure installation dir exists

risky-file-permissions: File permissions unset or incorrect
7-site.yml:35 Task/Handler: Export environment variables

risky-file-permissions: File permissions unset or incorrect
7-site.yml:56 Task/Handler: Create directrory for Elasticsearch

risky-file-permissions: File permissions unset or incorrect
7-site.yml:72 Task/Handler: Set environment Elastic

risky-file-permissions: File permissions unset or incorrect
7-site.yml:93 Task/Handler: Create directrory for Kibana

risky-file-permissions: File permissions unset or incorrect
7-site.yml:108 Task/Handler: Set environment Kibana

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - experimental  # all rules tagged as experimental

Finished with 0 failure(s), 7 warning(s) on 1 files.

```

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
 Он может не запуститься. Это нормально. Попытаться сделать так, чтобы с чеком отработал.

**Ответ:**

- Вывод команды  с включенным режимом debug [ansible-playbook -i inventory/2-prod.yml 2-site.yml --check](/08-ansible-02-playbook/Lesson/Files/ansible-playbook-check-2.md) на окружении 2-prod.yml

- Вывод команды  с включенным режимом debug [ansible-playbook -i inventory/3-prod.yml 3-site.yml --check](/08-ansible-02-playbook/Lesson/Files/ansible-playbook-check-3.md) на окружении 3-prod.yml

Найдена причина ошибки: в контейнере Centos7  отсутствует утилита`sudo`, повышающая права пользователя до уровня ROOT
```ps
fatal: [centos7]: FAILED! => {
    "msg": "Failed to get information on remote file (/etc/profile.d/jdk.sh): /bin/sh: sudo: command not found\n"
```
- Вывод: на разном окружении могут быть различные результаты выполнения плейбука.

- Вывод команды  с включенным режимом debug [ansible-playbook -i inventory/4-prod.yml 4-site.yml --check](/08-ansible-02-playbook/Lesson/Files/ansible-playbook-check-4.md) на окружении 4-prod.yml


- Успешная отработка плейбука с флагом --check:
```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook 7-site.yml -i inventory/7-prod.yml --check

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]
ok: [ubuntu]
ok: [fedore-core]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
changed: [fedore-core]
ok: [fedore]
ok: [ubuntu]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
ok: [fedore]
ok: [ubuntu]
changed: [fedore-core]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
skipping: [ubuntu]
skipping: [fedore]
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: NoneType: None
fatal: [fedore-core]: FAILED! => {"changed": false, "msg": "dest '/opt/jdk/11.0.14' must be an existing dir"}

TASK [Export environment variables] **************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]

TASK [Upload tar.gz Elasticsearch from remote URL] ***********************************************************************************************************************************************************
changed: [fedore]

TASK [Create directrory for Elasticsearch] *******************************************************************************************************************************************************************
ok: [fedore]

TASK [Extract Elasticsearch in the installation directory] ***************************************************************************************************************************************************
skipping: [fedore]

TASK [Set environment Elastic] *******************************************************************************************************************************************************************************
ok: [fedore]

PLAY [Install Kibana] ****************************************************************************************************************************************************************************************

PLAY RECAP ***************************************************************************************************************************************************************************************************
fedore                     : ok=9    changed=1    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
fedore-core                : ok=4    changed=2    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0  
```


7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

Также можно зайти на систему и там посмотреть
**Ответ:**

```sh
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook 7-site.yml -i inventory/7-prod.yml --diff

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore-core]
ok: [fedore]
ok: [ubuntu]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
ok: [fedore]
ok: [ubuntu]
ok: [fedore-core]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
skipping: [ubuntu]
skipping: [fedore]
skipping: [fedore-core]

TASK [Export environment variables] **************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]

TASK [Upload tar.gz Elasticsearch from remote URL] ***********************************************************************************************************************************************************
ok: [fedore]

TASK [Create directrory for Elasticsearch] *******************************************************************************************************************************************************************
ok: [fedore]

TASK [Extract Elasticsearch in the installation directory] ***************************************************************************************************************************************************
skipping: [fedore]

TASK [Set environment Elastic] *******************************************************************************************************************************************************************************
ok: [fedore]

PLAY [Install Kibana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Upload tar.gz Kibana from remote URL] ******************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Create directrory for Kibana] **************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Extract Kibana in the installation directory] **********************************************************************************************************************************************************
skipping: [fedore-core]

TASK [Set environment Kibana] ********************************************************************************************************************************************************************************
ok: [fedore-core]

PLAY RECAP ***************************************************************************************************************************************************************************************************
fedore                     : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
fedore-core                : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
ubuntu                     : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0 

```

8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

**Ответ:**

```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook 7-site.yml -i inventory/7-prod.yml --diff

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore-core]
ok: [fedore]
ok: [ubuntu]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
ok: [fedore]
ok: [ubuntu]
ok: [fedore-core]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
skipping: [ubuntu]
skipping: [fedore]
skipping: [fedore-core]

TASK [Export environment variables] **************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]

TASK [Upload tar.gz Elasticsearch from remote URL] ***********************************************************************************************************************************************************
ok: [fedore]

TASK [Create directrory for Elasticsearch] *******************************************************************************************************************************************************************
ok: [fedore]

TASK [Extract Elasticsearch in the installation directory] ***************************************************************************************************************************************************
skipping: [fedore]

TASK [Set environment Elastic] *******************************************************************************************************************************************************************************
ok: [fedore]

PLAY [Install Kibana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Upload tar.gz Kibana from remote URL] ******************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Create directrory for Kibana] **************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Extract Kibana in the installation directory] **********************************************************************************************************************************************************
skipping: [fedore-core]

TASK [Set environment Kibana] ********************************************************************************************************************************************************************************
ok: [fedore-core]

PLAY RECAP ***************************************************************************************************************************************************************************************************
fedore                     : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
fedore-core                : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
ubuntu                     : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   

root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# 
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# 
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# 
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook 7-site.yml -i inventory/7-prod.yml --diff

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]
ok: [fedore-core]
ok: [ubuntu]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore-core]
ok: [fedore]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore-core]
ok: [fedore]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
skipping: [ubuntu]
skipping: [fedore]
skipping: [fedore-core]

TASK [Export environment variables] **************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [fedore]
ok: [fedore-core]

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore]

TASK [Upload tar.gz Elasticsearch from remote URL] ***********************************************************************************************************************************************************
ok: [fedore]

TASK [Create directrory for Elasticsearch] *******************************************************************************************************************************************************************
ok: [fedore]

TASK [Extract Elasticsearch in the installation directory] ***************************************************************************************************************************************************
skipping: [fedore]

TASK [Set environment Elastic] *******************************************************************************************************************************************************************************
ok: [fedore]

PLAY [Install Kibana] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Upload tar.gz Kibana from remote URL] ******************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Create directrory for Kibana] **************************************************************************************************************************************************************************
ok: [fedore-core]

TASK [Extract Kibana in the installation directory] **********************************************************************************************************************************************************
skipping: [fedore-core]

TASK [Set environment Kibana] ********************************************************************************************************************************************************************************
ok: [fedore-core]

PLAY RECAP ***************************************************************************************************************************************************************************************************
fedore                     : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
fedore-core                : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
ubuntu                     : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0 
```

9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

**Ответ:**

Содержимое README.md

```yml
---
# Данный ansible-playbook демонстрационный и показывает структуру с описанием задач, модулей, методов, переменных и их значений.
# 

#  Первый Play по установке Java
- name: Install Java    # Название Play
  hosts: all            # Play будет запускатсья на всех хостах нашего инвентори
  tasks:                # Список задач в составе Play
  
  #  Задача первая
  # Цель задачи - создать динамическую переменую, определяющую зависимое от версии дистрибутива имя домашнего каталога для распакованных фалов Java 
    - name: Set facts for Java 11 vars    #  Название задачи. 
      set_fact:         # Создаем новую динамическую переменную чере модуль `set_fact`
        java_home: "/opt/jdk/{{ java_jdk_version }}"    # Ключ перменной, значение которого содержит хардкор /opt/jdk/`  и пеерменная `java_jdk_version` из варсов
      tags: java        # Тег, позволяющий запускать таску по условию запуска по тегам
      
      #  Задача вторая. 
      # Цель задачи - перенос файла с архивом из control_node  на  manage_node
    - name: Upload .tar.gz file containing binaries from local storage     #  Название задачи. 
    
    # Цель задачи: Закачивает на manage_node файл с архивом который находится на 
                 # control_node по пути, указанному в переменной `java_oracle_jdk_package ` 
                 # в файле `group_vars/all/vars.yml`
     
      copy:         # Модуль copy ищет файл на локалхосте и отправляет его на manage_node по пути в dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
        src: "{{ java_oracle_jdk_package }}"    #  Ищет в локальной директории /files
        dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"    #  Отправляет на manage_node
      register: download_java_binaries          #  register записывает результат в переменную download_java_binaries
      until: download_java_binaries is succeeded    #  Цикл будет выполнять таску, пока не произойдет условие цикла `download_java_binaries is succeeded`
      tags: java     # Тег, позволяющий запускать таску по условию запуска по тегам
      
      #  Задача третья.
      # Цель задачи - создать поддиректории для переноса в них распакованных файлов из архива
    - name: Ensure installation dir exists    #  Название задачи
      become: true        # Модуль повышения привелегий пользователя для выполнения действия. По умолчению это root. Может запускаться с ключем become-user=root. 
                          # При этом на manage_node должен быть установлен sudo
      file:           # Модуль file для создания state-ом директорий. 
        state: directory    #  Метод state. При помощи переменнх group_vars будут созданы все поддиректории, 
                            # которые в этом пути указаны.
        path: "{{ java_home }}"      #  Путь до домашнего каталога Java на manage_node
      tags: java      # Тег, позволяющий запускать таску по условию запуска по тегам
      
      #  Задача четвертая.
      # Цель задачи - разархивировать файлы и скопировать их в домашнюю директорию.
    - name: Extract java in the installation directory     #  Название задачи
      become: true      # Модуль повышения привелегий пользователя для выполнения действия.
      unarchive:    # с помощью модуля ` unarchive ` мы из `src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"`  распаковываем архив, 
                    # который распакуется и будет находится на `manage_node` по пути в `dest: "{{ java_home }}"`

        copy: false
        src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"     # путь до местонахождения архива 
        dest: "{{ java_home }}"                           # путь до директории, куда будет распакован архив
        mode: 0755                                        # установление системных прав доступа к директории
        extra_opts: [--strip-components=1]                # опция для длинных путей
        creates: "{{ java_home }}/bin/java"     # модуль `creates` после того, как распакует архив, проверяет, что по `{{ java_home }}/bin/java` пути
                                                # созданы файлы. Если файлы не найдутся, то таска зафейлится
        
      tags:
        - java          # Тег, позволяющий запускать таску по условию запуска по тегам
        
      #  Задача пятая.  
      # Цель задачи - выполнить перенос переменных окружения из шаблонов .j2 в каталог сценариев приложений etc/profile.d/
    - name: Export environment variables        #  Название задачи
      become: true                              # Модуль повышения привелегий пользователя для выполнения действия.
      template:         # template - модуль для проброса файла шаблона .j2 на manage-node в файл jdk.sh который создается с наполнением, котороее сть в teamplate
                        # Есть папка template. Здесь лежать файлы .j2. И они вызываются по пути имя папки/имя файла. 
                        # Директорию назначеня модуль создавать не может, надо чтобы директория уже была создана.
                        # Системня директория /etc/profile.d/ уже существует.
        src: jdk.sh.j2    # файл шаблона из папки t/emplate
        dest: /etc/profile.d/jdk.sh   # путь на  manage_node, куда надо перенести шаблон и сделать его сценарием .sh
      tags: java    # Тег, позволяющий запускать таску по условию запуска по тегам
      
      
 #  Второй Play по установке Elasticsearch
- name: Install Elasticsearch     # Название Play
  hosts: elasticsearch            # Play будет запускатсья на хостах из группы elasticsearch нашего инвентори
  tasks:                          # Список задач в составе Play
  
  # Задача первая. 
  # Цель задачи - скачать с официального сайта файла с архивом Elasticsearch на manage_node
    - name: Upload tar.gz Elasticsearch from remote URL     #  Название задачи
      get_url:        # Модуль для скачивания файла и переноса его в указанноую директорию
        url: "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{{ elastic_version }}-linux-x86_64.tar.gz"   # Адрес расположения архива 
                          # параметризирован при помощи group_vars {{ elastic_version }} на то, какую именно версию искать
                          #  Здесь нет модуля delegate_to, поэтому скачивание будет происходить сразу на manage_node
        
        dest: "/tmp/elasticsearch-{{ elastic_version }}-linux-x86_64.tar.gz"    # Папка, куда будет сохраняться архив
        mode: 0755      # Установление прав доступа к файлу-архиву
        timeout: 60     # Ожидание 60 секунд для get_url
        force: true     # Если архив Elasticsearch уже ранее был скачан и существует, то будет принудительно перезакачивание архива
        validate_certs: false    # get_url не будет реагировать ошибки свзанные с отсутствием сертификата SSL сайта
      register: get_elastic      # результат записываем в переменную get_elastic
      until: get_elastic is succeeded      # цикл until будет запускать задачу скачивания архива до тех пор, пока не будет удачное скачивание
      
      #  Пример работы цикла
      
      # TASK [Upload tar.gz Elasticsearch from remote URL] 
      # *******************************************************************************************************************************************************
      # FAILED - RETRYING: [fedore]: Upload tar.gz Elasticsearch from remote URL (3 retries left).
      # ok: [fedore]
      
      tags: elastic     # Тег, позволяющий запускать таску по условию запуска по тегам
      
      
  # Задача вторая. 
  # Цель задачи - создать директорию для Elasticsearch
    - name: Create directrory for Elasticsearch     #  Название задачи
      become: true        # Модуль повышения привелегий пользователя для выполнения действия.
      file:               # Модуль file для создания state-ом директорий. 
        state: directory    #  Создание модулем state директории без помощи фактов
        path: "{{ elastic_home }}"    #  Путь к домашней директории взят из group_vars
      tags: elastic       # Тег, позволяющий запускать таску по условию запуска по тегам
      
  # Задача третья. 
  # Цель задачи - разархивировать файлы и скопировать их в домашнюю директорию.
  # Действия и модули аналогичные из Play для Java
    - name: Extract Elasticsearch in the installation directory     #  Название задачи
      become: true      
      unarchive:
        copy: false
        src: "/tmp/elasticsearch-{{ elastic_version }}-linux-x86_64.tar.gz"
        dest: "{{ elastic_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ elastic_home }}/bin/elasticsearch"
      tags:
        - elastic
        
        
   # Задача четвертая. 
  # Цель задачи -  выполнить перенос переменных окружения из шаблонов .j2 в каталог сценариев приложений etc/profile.d/ 
  # Действия и модули аналогичные из Play для Java
    - name: Set environment Elastic
      become: true
      template:
        src: templates/elk.sh.j2
        dest: /etc/profile.d/elk.sh
      tags: elastic
      
```


10. Готовый playbook выложите в свой репозиторий, в ответ предоставьте ссылку на него.

**Ответ:**
https://github.com/zakharovnpa/ansible-02-playbook/blob/main/README.md
