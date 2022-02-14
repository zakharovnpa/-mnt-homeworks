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

В лекции "8.3. Использование Yandex Cloud" описано 

использование фактов хостов: 01:12:30
создание инвентори: 01:13:50
Создание в Яндекс.Облаке ВМ: 01:18:00
и запуск playbook:01:21:00



В соответствии с тем, что у нас есть
``` yml
el:
   hosts:
     centos7:
        ansible_connection: docker

```


```yml
---
centos7:
  hosts:
    localhost:
      ansible_connection: ssh
      ansible_user: root

```

2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.
Точно также как настривать эластик. Все рубль- в рубль.
скачать тар-гз
сделать тимплейт с-ашника
разархивировать тар-гз
создать директорию


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
name: Install Kibana
  hosts: ubuntu
  ansible_connext: docker
    tasks: Download kibana
      - name:Get Kibana
        get_url: "https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz"

```
```yml
- name: Install Java
  hosts: all
  tasks:
    - name: Set facts for Java 11 vars
      set_fact:
        java_home: "/opt/jdk/{{ java_jdk_version }}"
      tags: java
    - name: Upload .tar.gz file containing binaries from local storage
      copy:
        src: "{{ java_oracle_jdk_package }}"
        dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
      register: download_java_binaries
      until: download_java_binaries is succeeded
      tags: java
    - name: Ensure installation dir exists
      become: true
      file:
        state: directory
        path: "{{ java_home }}"
      tags: java
    - name: Extract java in the installation directory
      become: true
      unarchive:
        copy: false
        src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
        dest: "{{ java_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ java_home }}/bin/java"
      tags:
        - java
    - name: Export environment variables
      become: true
      template:
        src: jdk.sh.j2
        dest: /etc/profile.d/jdk.sh
      tags: java

```

3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.

**Ответ:**

```yml
- name: Install Kibana
  hosts: all
  tasks:
    - name: Set facts for Kibana 11 vars
      set_fact:
        java_home: "/opt/jdk/{{ java_jdk_version }}"
      tags: kibana
    - name: Upload .tar.gz file containing binaries from local storage
      copy:
        src: "{{ java_oracle_jdk_package }}"
        dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
      register: download_java_binaries
      until: download_java_binaries is succeeded
      tags: java
    - name: Ensure installation dir exists
      become: true
      file:
        state: directory
        path: "{{ java_home }}"
      tags: java
    - name: Extract java in the installation directory
      become: true
      unarchive:
        copy: false
        src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
        dest: "{{ java_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ java_home }}/bin/java"
      tags:
        - java
    - name: Export environment variables
      become: true
      template:
        src: jdk.sh.j2
        dest: /etc/profile.d/jdk.sh
      tags: java


```

4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.

**Ответ:**

```yml

```

5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

**Ответ:**
Проверка идет на таком окружении: локалхост и три различных докер-контейнера.
Линтер собщает о том, что не установлены права доступа к файлам в следующих тасках:
  - Upload .tar.gz file containing binaries from local storage
  - Ensure installation dir exists
  - Extract java in the installation directory

Данные директории еще не созданы

```yml
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-lint 2-site.yml 
WARNING  Overriding detected file kind 'yaml' with 'playbook' for given positional argument: 2-site.yml
WARNING  Listing 3 violation(s) that are fatal
risky-file-permissions: File permissions unset or incorrect
2-site.yml:10 Task/Handler: Upload .tar.gz file containing binaries from local storage

risky-file-permissions: File permissions unset or incorrect
2-site.yml:17 Task/Handler: Ensure installation dir exists

risky-file-permissions: File permissions unset or incorrect
2-site.yml:33 Task/Handler: Export environment variables

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - experimental  # all rules tagged as experimental

Finished with 0 failure(s), 3 warning(s) on 1 files.
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
- Успешная отработка плейбука:
```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/4-prod.yml 4-site.yml

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
changed: [ubuntu]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
changed: [ubuntu]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
changed: [ubuntu]

TASK [Export environment variables] **************************************************************************************************************************************************************************
changed: [ubuntu]

PLAY RECAP ***************************************************************************************************************************************************************************************************
ubuntu                     : ok=6    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   


```


7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

Также можно зайти на систему и там посмотреть
**Ответ:**

```yml

```

8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

**Ответ:**

```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/4-prod.yml 4-site.yml --diff

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
ok: [ubuntu]

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
ok: [ubuntu]

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
skipping: [ubuntu]

TASK [Export environment variables] **************************************************************************************************************************************************************************
ok: [ubuntu]

PLAY RECAP ***************************************************************************************************************************************************************************************************
ubuntu                     : ok=5    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   


```

9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

**Ответ:**

10. Готовый playbook выложите в свой репозиторий, в ответ предоставьте ссылку на него.

**Ответ:**
