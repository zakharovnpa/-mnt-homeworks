# Ход выполнения ДЗ к занятию "09.05 Gitlab"

## Подготовка к выполнению

1. Необходимо [зарегистрироваться](https://about.gitlab.com/free-trial/)

**Ответ:**

1. Решистрация была ранее создана

2. Создайте свой новый проект

**Ответ:**

1. Создан проект `gitlablesson`

3. Создайте новый репозиторий в gitlab, наполните его [файлами](./repository)

**Ответ:**

1. Созданы директории `test`, 

4. Проект должен быть публичным, остальные настройки по желанию

## Основная часть

### DevOps

В репозитории содержится код проекта на python. Проект - RESTful API сервис. Ваша задача автоматизировать сборку образа с выполнением python-скрипта:
1. Образ собирается на основе [centos:7](https://hub.docker.com/_/centos?tab=tags&page=1&ordering=last_updated)
2. Python версии не ниже 3.7
3. Установлены зависимости: `flask` `flask-jsonpify` `flask-restful`
4. Создана директория `/python_api`
5. Скрипт из репозитория размещён в /python_api
6. Точка вызова: запуск скрипта
7. Если сборка происходит на ветке `master`: Образ должен пушится в docker registry вашего gitlab `python-api:latest`, иначе этот шаг нужно пропустить


**Ответ:**

1. Создать директорию `/python_api` для п.4
2. В директории `/python_api` размещен скрипт `python-api.py` для п.5

```py
from flask import Flask, request
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class Info(Resource):
    def get(self):
        return {'version': 3, 'method': 'GET', 'message': 'Already started'} # Fetches first column that is Employee ID

api.add_resource(Info, '/get_info') # Route_1

if __name__ == '__main__':
     app.run(host='0.0.0.0', port='5290')

```
3. Создать Dockerfile с учетом п. 1, 2, 3

```sh
FROM Centos:7

RUN yml install python3 python3-pip -y
RUN pip3 install flask flask_restful

COPY api.py /opt/api/api.py
CMD ["python3", "/opt/api/api.py"]

```

4. `.gitlab-ci.yml`

```yml
stages:
  - build
  - deploy
  
image: docker:latest       # docker:20.10.5
services: 
    - docker:latest        # docker:20.10.5-dind

builder:
  stage: build
  script:
    - docker build -t some_docker_build:latest .
  except:
    - main
    
deployer:
  stage: deploy
  script:
    - docker build -t $CI_REGISTRY/zakharovnpa/gitlablesson/python-api:latest .
    - docker login -u $CI_REGISTY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker push $CI_REGISTRY/zakharovnpa/gitlablesson/python-api:latest
  only:
    - main
    
#rules:
#  - if: $CI_COMMIT_BRANCH   # уточнить что иенно надо здесь записать
#    exists:
#      - Dockerfile

```

5. После создания файлов делаем commit на ветку main
6. Переходим к CI/CD. Т.к. был создан файл `.gitlab-ci.yml`, то после commit сборка сразу начинается, как только все эт опопало в ветку main. и мы это можем видеть
7. Создан коммит на ветку main. Успешно
8. После коммита автоматом запустилась сборка. Неуспешно. 
  * Была синтаксическая ошибка
  * Не настроены Runner - процессы CI/CDдля запуска пайплайн сборки. Необходима регистрация раннера
  * Процесс регистрации раннера не проходит, т.к. требуется зарегистрировать банковскую карту. В настоящее время это не возможно.
  * Альтернатива - зарегистрировать раннер локально по [инструкции](https://docs.gitlab.com/runner/register/)

9. Процесс регитрации ранера:

* [Инструкция](https://docs.gitlab.com/runner/register/)

* Прежде чем зарегистрировать бегуна, вы должны сначала:
    - [Установите](https://docs.gitlab.com/runner/install/index.html) его на сервере отдельно от того, на котором установлен GitLab.
    - Получите токен:
* Устанавливаем раннер в [Docker](https://docs.gitlab.com/runner/install/docker.html) контейнер
* [Регистрация раннера](https://docs.gitlab.com/runner/register/index.html#docker)
  * [Пример регистрации раннера](https://docs.gitlab.com/runner/examples/gitlab.html)
* 

10. В итоге раннер запустился
11. Сборка нового образа прошла успешно. Образ выложен в гитлаб реджистри и его можно скачать.
12. Скачивание собранного образа. - 01:30:28  - 01:31:30. Ссылку на скачивание образа берем на странице `Container Registry`

```
root@PC-Ubuntu:~# docker pull registry.gitlab.com/zakharovnpa/gitlablesson/python-api:latest
latest: Pulling from zakharovnpa/gitlablesson/python-api
Digest: sha256:0281164e4d963499b7be3029e159e5f4ea6211858df5e3ca72bdbbab6da8cfdd
Status: Image is up to date for registry.gitlab.com/zakharovnpa/gitlablesson/python-api:latest
registry.gitlab.com/zakharovnpa/gitlablesson/python-api:latest

```
```
root@PC-Ubuntu:~# docker image list
REPOSITORY                                                          TAG               IMAGE ID       CREATED             SIZE
registry.gitlab.com/zakharovnpa/gitlablesson/python-api             latest            e87a0e154f99   About an hour ago   427MB
registry.gitlab.com/zakharovnpa/gitlablesson                        latest            e87a0e154f99   About an hour ago   427MB
docker                                                              dind              c89d806adeb8   4 days ago          236MB
docker                                                              latest            da88b5cbcdd8   4 days ago          219MB
gitlab/gitlab-runner                                                latest            89944ac4ab2c   7 days ago          691MB
registry.gitlab.com/gitlab-org/gitlab-runner/gitlab-runner-helper   x86_64-f761588f   257667c17e33   7 days ago          66.9MB
centos                                                              7                 eeb6ee3f44bd   7 months ago        204MB
docker                                                              20.10.5-dind      0a9822c8848d   13 months ago       258MB
docker                                                              20.10.5           1588477122de   13 months ago       241MB

```

13. Запуск контейнера и проверка что все работает как положено.  - 01:33:50

```
docker run -d -p 5290:5290 registry.gitlab.com/zakharovnpa/gitlablesson/python-api 
```
14. Проверяем работу веб-приложения
```
root@PC-Ubuntu:~# curl http://localhost:5290/get_info
{"version": 3, "method": "GET", "message": "Already started"}
```
* Все работает. С другим контейнером тоже работает.
```
root@PC-Ubuntu:~# docker run -d -p 5290:5290 registry.gitlab.com/zakharovnpa/gitlablesson/python-api
e07106816190060def9144ed65da3b395c32e88f896ed1c1dfa19ff428ab075a
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl http://localhost:5290/get_info
{"version": 3, "method": "GET", "message": "Already started"}

```



### Product Owner

Вашему проекту нужна бизнесовая доработка: необходимо поменять JSON ответа на вызов метода GET `/rest/api/get_info`, необходимо создать Issue в котором указать:
1. Какой метод необходимо исправить
2. Текст с `{ "message": "Already started" }` на `{ "message": "Running"}`
3. Issue поставить label: feature

**Ответ:**

- 00:30:45 Issue Trackers - отдельная компонента GitLab, позволяющая создавать issue или incident для конкретного проекта.
- 00:32:40 - create New Issue. Name: ... , Type: Issue, Description, Assignes - zakharovnpa
- 00:33:32 - Milestone - analog Apics in Jira. Создаем новый Milestone. Называем его.
- 00:35:20 - только что созданная Issue
- 00:35:35 - кнопка для создани Merge Request. Здесь нужно указать делать сейчас Merge Request или просто сделать новую ветку.  Для этой задачи создатся отдельная ветка. Указать Brance name, от какой ветки создавать Source branche
- 

1. Создано письмо на почту `contact-project+zakharovnpa-gitlablesson-35980166-issue-@incoming.gitlab.com` с постановкой задачи.
2. Письмо получено в Service Descks GitLab.

* Текст письма:
```
Нашему проекту нужна бизнесовая доработка
Задача: Необходимо поменять JSON ответа на вызов метода GET /rest/api/get_info

Пояснение: Изменить текст с { "message": "Already started" } на { "message": "Running"}

С уважением, Product Owner
```

3. Даем ответ на письмо
4. Создаем новую Issue
5. В новой Issue добавляем параметров 
6. Создалась новая Issue
7. По кнопке `Confidential Merge Request` ставим галочку Create branch и создаем новую задачу-Issue и новую ветку. Создаем имя для новой ветки `add_feature` и от какой ветки оветвляться (от main). 
8. 


### Developer

Вам пришел новый Issue на доработку, вам необходимо:
1. Создать отдельную ветку, связанную с этим issue
2. Внести изменения по тексту из задания
3. Подготовить Merge Requst, влить необходимые изменения в `master`, проверить, что сборка прошла успешно

**Ответ:**
1. Создана новая ветка 
2. Внесены изменения в файл `python-api.py`
3. Создан новый комит в ветку `add_feature`
4. Запустилась автоматическая сборка. в ветке `add_feature` Успешная сборка.
5. Выполняем MergeRequest. Он выполняется из меню Проект --> MergeRequest. From add_feature into main
6. Для создания MergeRequest надо нажать кнопку `Merge`
7. После мерджа автоматом запускается пайплайн сборки

### Tester

Разработчики выполнили новый Issue, необходимо проверить валидность изменений:
1. Поднять докер-контейнер с образом `python-api:latest` и проверить возврат метода на корректность
2. Закрыть Issue с комментарием об успешности прохождения, указав желаемый результат и фактически достигнутый

**Ответ:**

1. Изменения применились в новом образе.
2. В контейнере, запущенном на новом образе, првильный ответ

```
curl http://localhost:5290/get_info
{"version": 3, "method": "GET", "message": "Running"}

```

## Итог

После успешного прохождения всех ролей - отправьте ссылку на ваш проект в гитлаб, как решение домашнего задания

## Необязательная часть

Автомазируйте работу тестировщика, пусть у вас будет отдельный конвейер, который автоматически поднимает контейнер и выполняет проверку, например, при помощи curl. На основе вывода - будет приниматься решение об успешности прохождения тестирования

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
