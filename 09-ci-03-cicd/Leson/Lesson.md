# Ход выполнения ДЗ к занятию "09.03 CI\CD"

- 02:14:20
## Подготовка к выполнению

1. Создаём 2 VM в yandex cloud со следующими параметрами: 2CPU 4RAM Centos7(остальное по минимальным требованиям)
2. Прописываем в [inventory](./infrastructure/inventory/cicd/hosts.yml) [playbook'a](./infrastructure/site.yml) созданные хосты
3. Добавляем в [files](./infrastructure/files/) файл со своим публичным ключом (id_rsa.pub). Если ключ называется иначе - найдите таску в плейбуке, которая использует id_rsa.pub имя и исправьте на своё
4. Запускаем playbook, ожидаем успешного завершения
5. Проверяем готовность Sonarqube через [браузер](http://localhost:9000)
6. Заходим под admin\admin, меняем пароль на свой
7.  Проверяем готовность Nexus через [бразуер](http://localhost:8081)
8. Подключаемся под admin\admin123, меняем пароль, сохраняем анонимный доступ

## Знакомоство с SonarQube
- 00:37:20 - что такое  система Сонар.
- 00:40:20 - о том что такое `ansible_connection_type: paramiko`
- 00:41:10 - `ansible-doc -t connection paramiko`
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Eta/ansible/playbook/roles/elasticsearch_roles# ansible-doc -t connection paramiko
> ANSIBLE.BUILTIN.PARAMIKO    (/usr/local/lib/python3.8/dist-packages/ansible/plugins/connection/paramiko_ssh.py)

        Use the python ssh implementation (Paramiko) to connect to targets The paramiko transport is provided because many distributions, in particular EL6 and
        before do not support ControlPersist in their SSH implementations. This is needed on the Ansible control machine to be reasonably efficient with
        connections. Thus paramiko is faster for most users on these platforms. Users with ControlPersist capability can consider using -c ssh or configuring the
        transport in the configuration file. This plugin also borrows a lot of settings from the ssh plugin as they both cover the same protocol.

ADDED IN: version 0.1 of ansible-core

OPTIONS (= is mandatory):
.
.
.

```

- 00:43:20 - [Mitigen](https://mitogen.networkgenomics.com/ansible_detailed.html) - для ускорения работы Ansible по сети
- 00:46:04 - вход в SonarQube

### Основная часть      02:17:30

1. Создаём новый проект, название произвольное
2. Скачиваем пакет sonar-scanner, который нам предлагает скачать сам sonarqube
3. Делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ)
4. Проверяем `sonar-scanner --version`
5. Запускаем анализатор против кода из директории [example](./example) с дополнительным ключом `-Dsonar.coverage.exclusions=fail.py`
- 01:06:10 - пояснение. Несколько прогонов файла fail.py с исправлением багов

6. Смотрим результат в интерфейсе
7. Исправляем ошибки, которые он выявил(включая warnings)
8. Запускаем анализатор повторно - проверяем, что QG пройдены успешно
9. Делаем скриншот успешного прохождения анализа, прикладываем к решению ДЗ

## Знакомство с Nexus     02:20:00

### Основная часть

1. В репозиторий `maven-public` загружаем артефакт с GAV параметрами:
   1. groupId: netology
   2. artifactId: java
   3. version: 8_282
   4. classifier: distrib
   5. type: tar.gz
2. В него же загружаем такой же артефакт, но с version: 8_102
3. Проверяем, что все файлы загрузились успешно
4. В ответе присылаем файл `maven-metadata.xml` для этого артефекта
Откуда брать `maven-metadata.xml` показано на 01:31:40 и 01:32:10


### Знакомство с Maven

### Подготовка к выполнению     01:36:45 - 

1. Скачиваем дистрибутив с [maven](https://maven.apache.org/download.cgi)
2. Разархивируем, делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ) 
-  01:40:35 - выполнение `export PATH=$PATH:$(pwd)`, ``mvn --version
-  01:42:05 - скачивается из Maven с помощью файлов `pom.xml`
-  01:43:05 - указание на зависимости нашего артифакта от каких-то других артифактов


3. Удаляем из `apache-maven-<version>/conf/settings.xml` упоминание о правиле, отвергающем http соединение( раздел mirrors->id: my-repository-http-unblocker)
4. Проверяем `mvn --version`
5. Забираем директорию [mvn](./mvn) с pom

### Основная часть

1. Меняем в `pom.xml` блок с зависимостями под наш артефакт из первого пункта задания для Nexus (java с версией 8_282)
2. Запускаем команду `mvn package` в директории с `pom.xml`, ожидаем успешного окончания
- 01:45:05

3. Проверяем директорию `~/.m2/repository/`, находим наш артефакт
- 01:47:25 - 
- 01:53:00 - нужно бороться за чистоту кода

4. В ответе присылаем исправленный файл `pom.xml`

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
- 00:37:20 - что такое  система Сонар. 
- 00:37:30 - Про ДЗ



---

