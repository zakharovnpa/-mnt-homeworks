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
  
image: docker:20.10.5
services:docker:20.10.5-dind

builder:
  stage: build
  script:
    - docker build -t some_docker_build: latest .
  except:
    - main
    
deployer:
  stage: deploy
  script:
    - docker build -t $CI_REGISTRY/zakharovnpa/gitlablesson/python-api: latest
    - docker login -u $CI_REGISTY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker push $CI_REGISTRY/zakharovnpa/gitlablesson/python-api: latest
  only:
    - main
    
#rules:
#  - if: $CI_COMMIT_BRANCH   # уточнить что иенно надо здесь записать
#    exists:
#      - Dockerfile

```

5. После создания файлов делаем commit на ветку main
6. Переходим к CI/CD. Т.к. был создан файл `.gitlab-ci.yml`, то после commit сборка сразу начинается, как только все эт опопало в ветку main. и мы это можем видеть

### Product Owner

Вашему проекту нужна бизнесовая доработка: необходимо поменять JSON ответа на вызов метода GET `/rest/api/get_info`, необходимо создать Issue в котором указать:
1. Какой метод необходимо исправить
2. Текст с `{ "message": "Already started" }` на `{ "message": "Running"}`
3. Issue поставить label: feature

### Developer

Вам пришел новый Issue на доработку, вам необходимо:
1. Создать отдельную ветку, связанную с этим issue
2. Внести изменения по тексту из задания
3. Подготовить Merge Requst, влить необходимые изменения в `master`, проверить, что сборка прошла успешно


### Tester

Разработчики выполнили новый Issue, необходимо проверить валидность изменений:
1. Поднять докер-контейнер с образом `python-api:latest` и проверить возврат метода на корректность
2. Закрыть Issue с комментарием об успешности прохождения, указав желаемый результат и фактически достигнутый

## Итог

После успешного прохождения всех ролей - отправьте ссылку на ваш проект в гитлаб, как решение домашнего задания

## Необязательная часть

Автомазируйте работу тестировщика, пусть у вас будет отдельный конвейер, который автоматически поднимает контейнер и выполняет проверку, например, при помощи curl. На основе вывода - будет приниматься решение об успешности прохождения тестирования

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
