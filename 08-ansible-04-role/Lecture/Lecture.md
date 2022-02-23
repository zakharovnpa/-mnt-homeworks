## Лекция по теме "8.4. Работа с Roles"

### Работа с Roles
Алексей
Метляков

### 1Алексей Метляков
DevOps Engineer
OpenWay
Алексей Метляков

### 2План занятия
1. Что такое Role?
2. Для чего нужна Role?
3. Из чего состоит Role?
4. Где хранить Role?
5. Как создать Role?
6. Хранение и использование Role
7. Итоги
8. Домашнее задание

### 3Что такое Role?
Role – группа tasks, которая нацелена на выполнение действий,
приводящих к единому результату.
● Role – выполняет список действий;
● Список может состоять из одного действия;
● Действия должны приводить к одному общему результату
(например, установка и настройка nginx);
● Если в рамках действий role необходимо получить отдельный
результат, стоит написать для этого отдельную role;
● Если ваш playbook использует roles, то использование tasks
нежелательно, при этом можно использовать pre_tasks и
post_tasks;
● Если ваш playbook использует roles, то для расширения
функционала стоит писать role, даже если она состоит из
атомарного действия.

### 4Для чего нужна Role?
Использование role помогает достигнуть таких целей, как:
● Повышение читаемости кода;
● Создание верхнеуровневых playbook;
● Решение вопроса версионирования;
● Повышение универсализации.

### 5Из чего состоит Role?
Стандартная общая структура директории с role состоит из:
● Defaults – директория, которая содержит в себе yaml файл с
переменными по умолчанию, необходимыми для выполнения role;
● Handlers – директория с yaml, в котором содержатся все handlers от
role;
● Meta – содержит информацию о самой роли для обеспечения
работоспособности с ansible-galaxy;
● Tasks – директория содержит в себе yaml файлы с plays и tasks;
● Templates – директория с шаблонами конфигурационных файлов (в
случае, если они нужны);
● Tests – тестовый inventory и playbook, которые обычно позволяют
запустить роль на localhost;
● Vars – директория, которая содержит yaml файлы с остальными
переменными.

### 6Из чего состоит Role?
● В каждой из этих директорий, ansible ищет main.yml;
● В некоторых случаях можно добавлять свои .yml файлы с
наполнением и подключать их в main.yml;
● Роль можно дополнить своим собственным module или другим
plugin, для этого его нужно добавить в директорию library.

### 7Как создать Role?
```
Стартовый набор директорий можно получить при помощи
команды: ansible-galaxy role init <rolename>
Команда создаст директорию <rolename> с базовым набором
директорий и файлов, которые необходимо наполнить своими
действиями.
```
  
### 8Как создать Role?
Так как мы свою role делаем из playbook, то нам нужно:
● Скопировать все tasks из playbook в файл main.yml директории
tasks;
● Перенести все нужные для tasks handlers в файл main.yml
директории handlers;
● Перенести все templates в соответствующую директорию role;
● Все переменные, необходимые для tasks, перенести в файлы
main.yml директорий defaults и vars, в зависимости от
внутренней логики.

### 9Как создать Role?
Так как мы свою role делаем из playbook, то нам нужно:
● Расширить функционал tasks, возможно, использовать
несколько уровней вложенности tasks-файлов;
● Заполнить meta информацию, она нужна для работы
ansible-galaxy;
● Заполнить README.md файл, он нужен пользователям для
использования.

### 10Где хранить Role?
● Директория roles в плейбуке
● По пути /etc/ansible/roles
● По пути /usr/share/ansible/roles
● Кастомный путь
Для кастомного пути нужно:
● Переопределять путь в ansible.cfg в параметре
DEFAULT_ROLE_PATH
● Создать переменную окружения ANSIBLE_ROLES_PATH

### 11Хранение и использование role   00:48:00
Общедоступные роли хранятся по адресу [alaxy.ansible.com](https://galaxy.ansible.com)
- Покрывают ~90% необходимого функционала;
- Большинство распространяются по лицензии MIT;
- Есть возможность как стать соавтором роли, так и написать
собственную.

### 12Хранение и использование role   00:50:15
Традиционно, для версионирования и хранения role
используется git. Для определения текущей версии используют
семантический подход:
- major – добавление feature ломает совместимость с
предыдущей версией;
- minor – добавление feature не ломает совместимость;
- patch – исправление багов, рефакторинг и прочие схожие.
Номер версии необходимо выставлять при помощи git tag или
интерфейсов вашего инструмента для git.

### 13Хранение и использование role   00:53:09

Чтобы использовать role в playbook, необходимо объявить её в
файле requirements.yml и использовать команду ansible-galaxy для
последующего скачивания нужной версии роли. Список команд:
```ps
- ansible-galaxy install -r -requirements.yml
```
```ps
- ansible-galaxy install -r -requirements.yml -p roles
```
```ps
- ansible-galaxy install -r -requirements.yml --force
```
```ps
- ansible-galaxy install <rolename>
- ansible-galaxy install <namespace.collection.rolename>
```

### 14Итоги     00:56:50
### 15Итоги
● Role необходимо использовать в том случае, если снижается
текущая читаемость playbook.
● Разделение playbook на отдельные role позволяет жить каждой
логической единице независимыми жизненными циклами и
обрастать дополнительным функционалом.
● Дополнительный функционал можно принудительно не
использовать, оставаясь на старой версии role.
● Множество готовых role находятся в открытом доступе с
лицензиями MIT.
● Собственные role можно хранить в частных хранилищах git и
использовать напрямую оттуда.

### Практическая часть. 00:57:10

- 00:57:12 - показан репозиторий с ролью от Нетологии `netology-code/mnt-homeworks-ansible`
- 00:57:15 - описание файла README.md
- 01:00:15 - описание структуры репозитория
- 01:01:35 - описание директории `/task`. Кроме файла `main.yml`, в котором описаны импорты и инкулды, здесь лежат другие файлы.

- имппорт - это для стстичеких задач (у которых переменные заданы статически)
- инклуд - это для динамических задач (у которых переменные заданы динамически). Это то, что будет выполняться в Runtime
- 01:05:05 - В чем ключевая разница между импортом и инклудом. Более подробное пояснение идет в конце лекции на 02:24:00 

```yml
---
  - import_tasks: precheck.yml
  - include_tasks: "download {{ ansible_facts.pkg_mgr }}.yml"  #Находит файл download_yam.yml и делает то, что там написано. 
                                                               # А там написана отдельная задача (или несколько)
                                                               
  - include_tasks: "install {{ ansible_facts.pkg_mgr }}.yml"
  - import_tasks: configure.yml
  
```
- 01:06:40 - про вызов handler. Их также можно вызывать после выполнения тасок по директиве `noify: restart Elasticsearc`, только они хранятся теперь в других файлах в отдельной директории `handlers/main.yml`. И если таска прошла с `change`, то тогда `handler` запустится
- 01:08:00 - не надо пытаться заставить работать в докер-контейнере `system.d` Это ошибка.
- 01:08:35 - все хендлеры можно внести в оди файл `handlers/main.yml`. Их обычно не так много (хендлеров)
- 01:09:13 - пояснение инклудов и импортов для тасок
- 01:09:27 - показ директории `tasks`с файлами
```ps
/tasks
    config_vector_apt.yml
    install_vector_yum.yml
    install_vector_dnf.yml
    main,yml
    manage_vector.yml
    precheck_vector.yml
    remove_vector_apt.yml
    remove_vector_yum.yml
    remove_vector_dnf.yml
```
- 01:09:40 - пояснение про `main.yml`. На все инклуды навешены теги.
```yml
  - include_tasks: "download {{ ansible_facts.pkg_mgr }}.yml" 
    tags: [always]
                                                               
  - include_tasks: "remove_vector {{ ansible_facts.pkg_mgr }}.yml"
    when:
      - force_reinstall
    tags: [install]
  - include_tasks: "install_vector {{ ansible_facts.pkg_mgr }}.yml"
    when:
      - skip_instal is undefinde
      - ansible_distributon in support_system
    tags: [install]
    
    tags: [config]
    
    
    tags: [service]
  
```
- 01:09:55 - инклуды и импорты могу быть привязаны к какому-то событию.
Например этот инклуд будет выполняться всегда.
```yml
---
- include: precheck_vector.yml
  tags: [always]
```
- 01:10:25 - разбор файла `precheck_vector.yml`
```yml
---
- name: Check Vector | Check Vector already installed
  command: vactor --version
  register: current_vector_version
  ignore_errors: true
  changed_when: false
  tags: ["precheck_vector"]
  
```
- 01:12:05 - показано как динамически создавать разные штуки с помощью `set facts`. Заодно можно проверить против какой системы 
- 01:12:20 - как вместо модуля `debug:` использовать модуль `fail:`
```yml
---
- name: Check environments | Skip OS support reason
  fail:
    msg: "Susyem {{ ansible_distribution }} is not support to install Vector by this version of role"  # `ansible_distribution` - это из фактов
  when:
  - ansible_distribution is not supported_systems     #Этот параметр `supported systems` лежит в vars/main.yml
  tags: ["precheck_vector"]
```
- 01:12:50 - про параметр `supported_systems` , который лежит в `vars/main.yml`
```yml
---
support_systems: ['CentOS', 'Red Hat Enterprise Linux', 'Ubuntu']

```
Этот переметр `supported_systems` пользователь определить как дефолт не сможет. И если пользователь запустит эту роль против Windows, например, то эта роль  в этом моменте сразу выйдет в `fail`, потому что тип ОС не соответствует и дальше задача не пойдет.

- 01:13:50 - продолжение описания файла `tasks/main.yml`
- 01:15:12 - описание таски по безусловному запуску `hendlers` модулем `meta`. `hendlers` запустится здесь и сейчас даже при условии, что роль до конца не дошла.
```yml
- name: Create service | Flush handlers
  meta: flush_handlers 
```

```yml
---
-include: manage_vector.yml
 when:
  - ansible_didstribution in support _systems
  - ansible_service_mgr == "systemd"
  - vector_service_state is definde
  - vector_service_state | lenght > 0
 tags: [service]

```
- 01:16:10 - про модуль метатаски. Поиск в Google meta ansible. [Ansible.builtin.meta](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/meta_module.html) параметр `free_form`
- 01:16:58 - пояснение про то, что в некоторых ролях ворсы подключаются с помощью инклуд ворсов в рамках тасок и подключаются они в зависимости от типа систем
Прмер можно посмотреть [тут](https://github.com/AlexeySetevoi/ansible-clickhouse/tree/master/vars)
- 01:17:30 - пояснение работы этого примера подключения ворсов:
```yml
 ---
 - name: 'Include OS Family Specific Variables'
  include_vars: "{{ lookup('first_found', params) }}"
  vars:
    params:
      files:
        - "{{ ansible_os_family | lower }}.yml"
        - 'empty.yml'
      paths:
        - 'vars'
  tags: [always]
```
- 01:18:10 - с помошью плагина `lookup` находится первый подходящий по `params` `ansible_os_family.yml`  или `lower.yml`. Если из этого ничего не нашлось, то тогда будет использоваться `empty.yml`. Т.е. здесь мы видим, что переменные в имени файла участвуют в условии поиска нужного файла для запуска.

```yml
---
# tasks file for clickhouse
- name: 'Include OS Family Specific Variables'
  include_vars: "{{ lookup('first_found', params) }}"
  vars:
    params:
      files:
        - "{{ ansible_os_family | lower }}.yml"
        - 'empty.yml'
      paths:
        - 'vars'
  tags: [always]

- include_tasks: precheck.yml
  tags: [always]

- include_tasks: params.yml
  tags: [always]

- include_tasks:
    file: "{{ lookup('first_found', params) }}"
    apply:
      tags: [install]
  vars:
    params:
      files:
        - "install/{{ ansible_pkg_mgr }}.yml"
        - 'empty.yml'
  tags: [install]
  when: not clickhouse_remove|bool

- include_tasks: 
    file: configure/sys.yml
    apply:
      tags: [config, config_sys]
  tags: [config, config_sys]
  when: not clickhouse_remove|bool

- name: "Notify Handlers Now"
  meta: flush_handlers

- include_tasks: service.yml
  tags: [always]

- name: "Wait for Clickhouse Server to Become Ready"
  wait_for:
    port: "{{ clickhouse_tcp_port }}"
    delay: "{{ clickhouse_ready_delay }}"
  when: not clickhouse_remove|bool

- include_tasks:
    file: configure/db.yml
    apply:
      tags: [config, config_db]
  tags: [config, config_db]
  when: not clickhouse_remove|bool

- include_tasks:
    file: configure/dict.yml
    apply:
      tags: [config, config_dict]
  tags: [config, config_dict]
  when: not clickhouse_remove|bool

- include_tasks:
    file: remove.yml
    apply:
      tags: [remove]
  tags: [remove]
  when: clickhouse_remove|bool

```
- 01:21:05 - создание плейбука для нашей роли
```ps
mkdir playbook
cd playbook
touch site.yml
touch requirement.yml

```

```ps
mkdir inventory
cd inventory
touch hosts.yml
```
- Создание интвентори файла на основе ВМ Я.Облака
```yml
- el:
  hosts:
    centos:
      ansible_host: <ip_adress>
    debian:
      ansible_host: <ip_adress>
  vars:
    ansible_user: centos

```
- 01:27:05 - описываем файл `requirement.yml`. Ссылку ssh [берем эту](git@github.com:netology-code/mnt-homeworks-ansible.git)
- 01:28:00 - В качестве версии, кроме тегов, можно указать еще и имя ветки ` main` и тогда скачается последняя ревизия мейна. 
- 01:28:17 - Можно указать хэш коммита и тогда  ansible-galaxy на этот коммит и зачекаутит эту роль. По факту он скачивает репозиторий, делает чекаут на нужную версию, а потом удаляет гит директорию и говорит точ все сделал. 
      

```yml
---
- src: git@github.com:netology-code/mnt-homeworks-ansible.git
  scm: git
  name:
  version: main
```

- 01:28:42 - в качестве версии можно указать все что угодно, но мы выберем тег 2.0.3, потому что мы говорили про семантическое версионирование.
```yml
---
- src: git@github.com:netology-code/mnt-homeworks-ansible.git
  scm: git
  version: 2.0.3
  name: elasticsearch_role
```
- 01:29:00 - файл `site.yml`
```yml
---
- name: Assert elasticrole
  hosts: all
  roles:
    - elasticsearch_role
```
- 01:30:15 - Плейбук готов.
- 01:30:30 - перед тем, как запустить плейбук выполняем команду
```
ansible-galaxy install -r requirement.yml -p roles
```
- Появится директория `roles` в нашей директории с плейбуком.
- 01:31:25 - Потом запускаем плейбук:
```
ansible-playbook -i inventory/hosts.yml site.yml
```
- 01:33:10 - создать в директории плейбука поддиректорию `/files`
- 




### 16Домашнее задание - 02:01:20
Давайте посмотрим ваше домашнее задание.
● Вопросы по домашней работе задавайте в чате мессенджера
Slack.
● Задачи можно сдавать по частям.
● Зачёт по домашней работе проставляется после того, как приняты
все задачи.

### 17Задавайте вопросы и
пишите отзыв о лекции!
Алексей Метляков
Алексей Метляков

### Разбор ДЗ 02:01:20
- 01:55;00 - пояснение как сделать репозиторий с первой ролью.
- 02:01:20 - начало разбора ДЗ
- 02:02:30 - подготовить три разных репозитория
- 02:02:37 - пояснение по Задача №1
- 02:03:20 - пояснение по Задаче №2
- 02:03:29 - пояснение по Задаче №3
- 02:04:20 - пояснение по Задаче №4
- 02:04:25 - пояснение по Задаче №5
- 02:04:28 - пояснение по Задаче №6
- 02:04:32 - пояснение по Задаче №7 и 8
- 02:04:45 - пояснение по Задаче №9 - о правильности названий переменных. О синхронизации переменных. Сделать одну общую переменую для всех версий, а потом для каждой задачи добавлять свою переменну. По аналогии и прошлой лекции. Чтобы с точки зрения ролей была возможность установки разных переменных. Образец: {{ elk_для_чего_переменая }}, {{ nginx_для_чего_переменная }}
- 02:06:40 - пояснение по Задаче №10. Добавлять теги Git для разных уровней готовности ролей. Семантичесая нумерация. 1.2.3. Баги фиксили, фичи придуиывали
- 02:06:54 - пояснение по Задаче №11. Когда все роли застабилизировались, добавить роль в `requirements.yml`  в playbook
- 02:07:22 - пояснение по Задаче №12
- 02:07:28 - пояснение по Задаче №13
- 02:08:05 - пояснение по Задаче №14
- 02:09:20 - показана полная структура каталогов ролей

По необязательной части ДЗ:
- 02:08:14 - пояснение по Задаче №1
- 02:08:33 - пояснение по Задаче №2
- 02:08:45 - пояснение по Задаче №3
- 02:08:58 - пояснение по Задаче №4

----------------


---
### Play №1.
```yml
- name: Install Elasticsearch
  hosts: elasticsearch
```
```yml
  handlers:
    - name: restart Elasticsearch
      become: true
      service:
        name: elasticsearch
        state: restarted
```

###  tasks:

```yml
    - name: "Download Elasticsearch's rpm"
      get_url:
        url: "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-{{ elk_stack_version }}-x86_64.rpm"
        dest: "/tmp/elasticsearch-{{ elk_stack_version }}-x86_64.rpm"
      register: download_elastic
      until: download_elastic is succeeded
```
```yml
    - name: Install Elasticsearch
      become: true
      yum:
        name: "/tmp/elasticsearch-{{ elk_stack_version }}-x86_64.rpm"
        state: present
```
```yml
    - name: Configure Elasticsearch
      become: true
      template:
        src: elasticsearch.yml.j2
        dest: /etc/elasticsearch/elasticsearch.yml
      notify: restart Elasticsearch

```

### Play №2.
```yml
- name: Install Kibana
  hosts: kibana
```
```yml
  handlers:
    - name: restart kibana
      become: true
      service:
        name: kibana
        state: restarted
 ```

###  tasks:

```yml
    - name: "Download Kibana's rpm"
      get_url:
        url: "https://artifacts.elastic.co/downloads/kibana/kibana-{{ elk_stack_version }}-x86_64.rpm"
        dest: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
      register: download_kibana
      until: download_kibana is succeeded
```
```yml
    - name: Install Kibana
      become: true
      yum:
        name: "/tmp/kibana-{{ elk_stack_version }}-x86_64.rpm"
        state: present
      notify: restart kibana
```
```yml
    - name: Configure Kibana
      become: true
      template:
        src: kibana.yml.j2
        dest: /etc/kibana/kibana.yml
      notify: restart kibana
```
### Play №3.
```yml
- name: Install Filebeat
  hosts: filebeat
```
* `/roles/filebeat/handlers/main.yml`
```yml
  handlers:
    - name: restart filebeat
      become: true
      systemd:
        name: filebeat
        state: restarted
        enabled: true
```

 #### tasks:
* `/roles/filebeat/tasks/download_filebeat_rpm.yml`
```yml
    - name: "Download Filebeat's rpm"
      get_url:
        url: "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-{{ elk_stack_version }}-x86_64.rpm"
        dest: "/tmp/filebeat-{{ elk_stack_version }}-x86_64.rpm"
      register: download_filebeat
      until: download_filebeat is succeeded
```
* `/roles/filebeat/tasks/install_filebeat.yml`
```yml
    - name: Install Filebeat
      become: true
      yum:
        name: "/tmp/filebeat-{{ elk_stack_version }}-x86_64.rpm"
        state: present
      notify: restart filebeat
```
* `/roles/filebeat/tasks/configure_filebeat.yml`
```yml
    - name: Configure Filebeat
      become: true
      template:
        src: filebeat.yml.j2
        dest: /etc/filebeat/filebeat.yml
      notify: restart filebeat
```
* `/roles/filebeat/tasks/set_filebeat_systemwork.yml`
```yml
    - name: Set filebeat systemwork
      become: true
      command:
        cmd: filebeat modules enable system
        chdir: /usr/share/filebeat/bin
      register: filebeat_modules
      changed_when: filebeat_modules.stdout != 'Module system is alredy enabled'
```
* `/roles/filebeat/tasks/load_kibana_dashboard.yml`
```yml
    - name: Load Kibana dashboard
      become: true
      command:
        cmd: filebeat setup
        chdir: /usr/share/filebeat/bin
      register: filebeat_setup
      changed_when: false
      until: filebeat_setup is succeeded
```
