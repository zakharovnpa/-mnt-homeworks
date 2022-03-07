## Ход выполнения ДЗ по теме "08.05 Тестирование Roles"

## Подготовка к выполнению
1. Установите molecule: `pip3 install "molecule==3.4.0"`
```ps
root@server1:~/learning-ansible/Lesson-ansible-05# molecule --version
molecule 3.6.1 using python 3.8 
    ansible:2.12.2
    delegated:3.6.1 from molecule
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

1. Запустите  `molecule test` внутри корневой директории `elasticsearch-role`, посмотрите на вывод команды.
Необходимо, чтобы было установлено: - `molecule`, `docker`, `molecule-docker` пакетик.

2. Перейдите в каталог с ролью `kibana-role` и создайте сценарий тестирования по умолчаню при помощи `molecule init scenario --driver-name docker`.
Можно использовать любые драверы. (а какме есть?)

3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

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
