# Ход выполнения ДЗ к занятию "09.03 CI\CD"

Директория выполнения ДЗ: 
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Yota#
```

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
Проект `zsn-netology`  Создать токен и сохранить его в cicd/credential.yml

2. Скачиваем пакет sonar-scanner, который нам предлагает скачать сам sonarqube
- 00:58:30
```

```

3. Делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ)
```
root@PC-Ubuntu:/home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux# echo $PATH
/root/yandex-cloud/bin:/root/yandex-cloud/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/usr/local/go/bin:/usr/local/GoLand-2021.3.2/bin
root@PC-Ubuntu:/home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux# 
root@PC-Ubuntu:/home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux# export PATH=$PATH:$(pwd)/bin

```

4. Проверяем `sonar-scanner --version`
```
root@PC-Ubuntu:/home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux# sonar-scanner --version
INFO: Scanner configuration file: /home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.7.0.2747
INFO: Java 11.0.14.1 Eclipse Adoptium (64-bit)
INFO: Linux 5.13.0-28-generic amd64
```

5. Запускаем анализатор против кода из директории [example](./example)
- 01:02:10 - 
- 01:06:10 - пояснение. Несколько прогонов файла fail.py с исправлением багов

```
sonar-scanner \
  -Dsonar.projectKey=zsn-netology \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://178.154.229.213:9000 \
  -Dsonar.login=748866d8350423ccb89886906aaf7bb0be642198
```
Запускаем анализатор против кода из директории [example](./example) с дополнительным ключом `-Dsonar.coverage.exclusions=fail.py`
```
sonar-scanner \
  -Dsonar.projectKey=zsn-netology \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://178.154.229.213:9000 \
  -Dsonar.login=748866d8350423ccb89886906aaf7bb0be642198
  -Dsonar.coverage.exclusions=fail.py
```


6. Смотрим результат в интерфейсе
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Yota/ansible/example# ls -l
итого 4
-rw-r--r-- 1 root root 255 фев  4 17:10 fail.py
```
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Yota/ansible/example# 
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Yota/ansible/example# sonar-scanner \
>   -Dsonar.projectKey=zsn-netology \
>   -Dsonar.sources=. \
>   -Dsonar.host.url=http://178.154.229.213:9000 \
>   -Dsonar.login=748866d8350423ccb89886906aaf7bb0be642198
INFO: Scanner configuration file: /home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.7.0.2747
INFO: Java 11.0.14.1 Eclipse Adoptium (64-bit)
INFO: Linux 5.13.0-28-generic amd64
INFO: User cache: /root/.sonar/cache
INFO: Scanner configuration file: /home/maestro/Загрузки/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: Analyzing on SonarQube server 9.1.0
INFO: Default locale: "ru_RU", source code encoding: "UTF-8" (analysis is platform dependent)
INFO: Load global settings
INFO: Load global settings (done) | time=216ms
INFO: Server id: 9CFC3560-AX-DdSMsa-l0rGcTdMKX
INFO: User cache: /root/.sonar/cache
INFO: Load/download plugins
INFO: Load plugins index
INFO: Load plugins index (done) | time=104ms
INFO: Load/download plugins (done) | time=32154ms
INFO: Process project properties
INFO: Process project properties (done) | time=12ms
INFO: Execute project builders
INFO: Execute project builders (done) | time=2ms
INFO: Project key: zsn-netology
INFO: Base dir: /root/ansible-learning/yandex-cloud/Yota/ansible/example
INFO: Working dir: /root/ansible-learning/yandex-cloud/Yota/ansible/example/.scannerwork
INFO: Load project settings for component key: 'zsn-netology'
INFO: Load project settings for component key: 'zsn-netology' (done) | time=61ms
INFO: Load quality profiles
INFO: Load quality profiles (done) | time=114ms
INFO: Load active rules
INFO: Load active rules (done) | time=2234ms
WARN: SCM provider autodetection failed. Please use "sonar.scm.provider" to define SCM of your project, or disable the SCM Sensor in the project settings.
INFO: Indexing files...
INFO: Project configuration:
INFO: 1 file indexed
INFO: Quality profile for py: Sonar way
INFO: ------------- Run sensors on module zsn-netology
INFO: Load metrics repository
INFO: Load metrics repository (done) | time=78ms
INFO: Sensor Python Sensor [python]
WARN: Your code is analyzed as compatible with python 2 and 3 by default. This will prevent the detection of issues specific to python 2 or python 3. You can get a more precise analysis by setting a python version in your configuration via the parameter "sonar.python.version"
INFO: Starting global symbols computation
INFO: 1 source file to be analyzed
INFO: Load project repositories
INFO: Load project repositories (done) | time=52ms
INFO: 1/1 source file has been analyzed
INFO: Starting rules execution
INFO: 1 source file to be analyzed
INFO: 1/1 source file has been analyzed
INFO: Sensor Python Sensor [python] (done) | time=1069ms
INFO: Sensor Cobertura Sensor for Python coverage [python]
INFO: Sensor Cobertura Sensor for Python coverage [python] (done) | time=12ms
INFO: Sensor PythonXUnitSensor [python]
INFO: Sensor PythonXUnitSensor [python] (done) | time=1ms
INFO: Sensor CSS Rules [cssfamily]
INFO: No CSS, PHP, HTML or VueJS files are found in the project. CSS analysis is skipped.
INFO: Sensor CSS Rules [cssfamily] (done) | time=0ms
INFO: Sensor JaCoCo XML Report Importer [jacoco]
INFO: 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
INFO: No report imported, no coverage information will be imported by JaCoCo XML Report Importer
INFO: Sensor JaCoCo XML Report Importer [jacoco] (done) | time=3ms
INFO: Sensor C# Project Type Information [csharp]
INFO: Sensor C# Project Type Information [csharp] (done) | time=1ms
INFO: Sensor C# Analysis Log [csharp]
INFO: Sensor C# Analysis Log [csharp] (done) | time=20ms
INFO: Sensor C# Properties [csharp]
INFO: Sensor C# Properties [csharp] (done) | time=0ms
INFO: Sensor JavaXmlSensor [java]
INFO: Sensor JavaXmlSensor [java] (done) | time=2ms
INFO: Sensor HTML [web]
INFO: Sensor HTML [web] (done) | time=4ms
INFO: Sensor VB.NET Project Type Information [vbnet]
INFO: Sensor VB.NET Project Type Information [vbnet] (done) | time=1ms
INFO: Sensor VB.NET Analysis Log [vbnet]
INFO: Sensor VB.NET Analysis Log [vbnet] (done) | time=20ms
INFO: Sensor VB.NET Properties [vbnet]
INFO: Sensor VB.NET Properties [vbnet] (done) | time=0ms
INFO: ------------- Run sensors on project
INFO: Sensor Zero Coverage Sensor
INFO: Sensor Zero Coverage Sensor (done) | time=10ms
INFO: SCM Publisher No SCM system was detected. You can use the 'sonar.scm.provider' property to explicitly specify it.
INFO: CPD Executor Calculating CPD for 1 file
INFO: CPD Executor CPD calculation finished (done) | time=18ms
INFO: Analysis report generated in 102ms, dir size=103,1 kB
INFO: Analysis report compressed in 15ms, zip size=14,3 kB
INFO: Analysis report uploaded in 81ms
INFO: ANALYSIS SUCCESSFUL, you can browse http://178.154.229.213:9000/dashboard?id=zsn-netology
INFO: Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
INFO: More about the report processing at http://178.154.229.213:9000/api/ce/task?id=AX-DrBz4a-l0rGcTdRPe
INFO: Analysis total time: 6.374 s
INFO: ------------------------------------------------------------------------
INFO: EXECUTION SUCCESS
INFO: ------------------------------------------------------------------------
INFO: Total time: 47.312s
INFO: Final Memory: 7M/30M
INFO: ------------------------------------------------------------------------

```

7. Исправляем ошибки, которые он выявил(включая warnings)

8. Запускаем анализатор повторно - проверяем, что QG пройдены успешно
9. Делаем скриншот успешного прохождения анализа, прикладываем к решению ДЗ

## Знакомство с Nexus     02:20:00

### Основная часть
- 01:30:00
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
Была проблема: не установлена Java
```
root@PC-Ubuntu:~/Downloads/apache-maven-3.8.5/bin# mvn --version
The JAVA_HOME environment variable is not defined correctly,
this environment variable is needed to run this program.

```

Решение:

Method 2: Install OpenJDK 14 on Ubuntu / Debian manually
The JDK 14 releases are available on the releases & downloads page. We’ll download the latest available version using curl.
```
curl -O https://download.java.net/java/GA/jdk14/076bab302c7b4508975440c56f6cc26a/36/GPL/openjdk-14_linux-x64_bin.tar.gz
```
Extract the downloaded OpenJDK 14 archive file using tar command.
```
tar xvf openjdk-14_linux-x64_bin.tar.gz
```
Move the resulting folder to /opt directory.
```
sudo mv jdk-14 /opt/
```
Configure Java environment:
```
sudo tee /etc/profile.d/jdk14.sh <<EOF
export JAVA_HOME=/opt/jdk-14
export PATH=\$PATH:\$JAVA_HOME/bin
EOF
```
Source your profile file and check java command
```
source /etc/profile.d/jdk14.sh
```
Confirm Java version.

```
$ echo $JAVA_HOME
/opt/jdk-14
```
```
$ java -version
openjdk version "14" 2020-03-17
OpenJDK Runtime Environment (build 14+36-1461)
OpenJDK 64-Bit Server VM (build 14+36-1461, mixed mode, sharing)
You now have Java 14 / JDK 14 installed on Debian / Ubuntu Linux Desktop or server edition.
```

Выполнение:
```
root@PC-Ubuntu:~# sudo mv jdk-14 /opt/
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# sudo tee /etc/profile.d/jdk14.sh <<EOF
> export JAVA_HOME=/opt/jdk-14
> export PATH=\$PATH:\$JAVA_HOME/bin
> EOF

```
```
export JAVA_HOME=/opt/jdk-14
export PATH=$PATH:$JAVA_HOME/bin
```
```
root@PC-Ubuntu:~# source /etc/profile.d/jdk14.sh
``` 
```
root@PC-Ubuntu:~# echo $JAVA_HOME
/opt/jdk-14
```
Результат:
```
root@PC-Ubuntu:~# mvn --version
Apache Maven 3.8.5 (3599d3414f046de2324203b78ddcf9b5e4388aa0)
Maven home: /root/Downloads/apache-maven-3.8.5
Java version: 14, vendor: Oracle Corporation, runtime: /opt/jdk-14
Default locale: ru_RU, platform encoding: UTF-8
OS name: "linux", version: "5.13.0-28-generic", arch: "amd64", family: "unix"

```

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

