## Ход процесса регистрации Runner для GitLab

### Пояснение ситуацми
> В связи с ограничениями на сайте gitlab невозможно запустить runner для запуска процессов pipeline CI/CD. Требуется регистрация банковской карты, а карты сейчас не прнимаются.

### Альтернатива
* Альтернатива - зарегистрировать раннер локально по [инструкции](https://docs.gitlab.com/runner/register/)
> Локальный раннер - это раннер, запущенный, например в докер-контейнере и работающий для обработки очередей сборки. Для настройки надо запустить контейнер с раннеро и привязать его к проекту на сайте GitLab.com

### Процесс регитрации ранера:

* [Инструкция](https://docs.gitlab.com/runner/register/)

* Прежде чем зарегистрировать бегуна, вы должны сначала:
    - [Установите](https://docs.gitlab.com/runner/install/index.html) его на сервере отдельно от того, на котором установлен GitLab.
    - Получите токен:
* Устанавливаем раннер в [Docker](https://docs.gitlab.com/runner/install/docker.html) контейнер
* [Регистрация раннера](https://docs.gitlab.com/runner/register/index.html#docker)
  * [Пример регистрации раннера](https://docs.gitlab.com/runner/examples/gitlab.html)

### Запуск GitLab Runner в контейнере

1. Запуск контейнера

```
root@PC-Ubuntu:~# docker run -d -it gitlab/gitlab-runner
Unable to find image 'gitlab/gitlab-runner:latest' locally
latest: Pulling from gitlab/gitlab-runner
d5fd17ec1767: Pull complete 
b72ae3311b2d: Pull complete 
8321a833c290: Pull complete 
Digest: sha256:0f8ee21c2ef77d5ffacdb8343c709ab7945c1760b492f8e0877973630a5d935f
Status: Downloaded newer image for gitlab/gitlab-runner:latest
a970a9351a4d7fb972e13d52e835e355cefa4716f6769eee273ffefc47913427
root@PC-Ubuntu:~# 
```
```
root@PC-Ubuntu:~# docker image list
REPOSITORY             TAG       IMAGE ID       CREATED      SIZE
gitlab/gitlab-runner   latest    89944ac4ab2c   6 days ago   691MB

```

* Смотрим версию `gitlab-runner` в контейнере
```
root@PC-Ubuntu:~# docker exec admiring_antonelli gitlab-runner --help
NAME:
   gitlab-runner - a GitLab Runner

USAGE:
   gitlab-runner [global options] command [command options] [arguments...]

VERSION:
   14.10.1 (f761588f)

AUTHOR:
   GitLab Inc. <support@gitlab.com>

COMMANDS:
     exec                  execute a build locally
     list                  List all configured runners
     run                   run multi runner service
     register              register a new runner
     install               install service
     uninstall             uninstall service
     start                 start service
     stop                  stop service
     restart               restart service
     status                get status of a service
     run-single            start single runner
     unregister            unregister specific runner
     verify                verify all registered runners
     artifacts-downloader  download and extract build artifacts (internal)
     artifacts-uploader    create and upload build artifacts (internal)
     cache-archiver        create and upload cache artifacts (internal)
     cache-extractor       download and extract cache artifacts (internal)
     cache-init            changed permissions for cache paths (internal)
     health-check          check health for a specific address
     read-logs             reads job logs from a file, used by kubernetes executor (internal)
     help, h               Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --cpuprofile value           write cpu profile to file [$CPU_PROFILE]
   --debug                      debug mode [$DEBUG]
   --log-format value           Choose log format (options: runner, text, json) [$LOG_FORMAT]
   --log-level value, -l value  Log level (options: debug, info, warn, error, fatal, panic) [$LOG_LEVEL]
   --help, -h                   show help
   --version, -v                print the version

```

2. Контейнер запущен

```
root@PC-Ubuntu:~# docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS          PORTS     NAMES
a970a9351a4d   gitlab/gitlab-runner   "/usr/bin/dumb-init …"   37 seconds ago   Up 34 seconds             admiring_antonelli

```
3. Временно останавливаем конетйнер для подключения волюма


### Создаем Volume

1. Создаем Volume

```
root@PC-Ubuntu:~# docker volume create gitlab-runner-config
gitlab-runner-config

```
2. Запускаем контейнер с подключенным volume

```
root@PC-Ubuntu:~# docker run -d --name gitlab-runner --restart always \
>     -v /var/run/docker.sock:/var/run/docker.sock \
>     -v gitlab-runner-config:/etc/gitlab-runner \
>     gitlab/gitlab-runner:latest
44e681f99687f668c82e02102f737ee2cdda601c0e3cbb982d884d4d03e35af0
root@PC-Ubuntu:~# 
```
```
root@PC-Ubuntu:~# docker ps
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS          PORTS     NAMES
44e681f99687   gitlab/gitlab-runner:latest   "/usr/bin/dumb-init …"   13 seconds ago   Up 12 seconds             gitlab-runner

```


### Регистрация раннера

1. Инструкции 
* [Регистрация раннера](https://docs.gitlab.com/runner/register/index.html#docker)
  * [Пример регистрации раннера](https://docs.gitlab.com/runner/examples/gitlab.html)
2. Для регистрации необходимо подготовить файл шаблона и разместить его в локаоьной директории настроенной для Volume

* Пример создания файла-шаблона

```
$ cat > /tmp/test-config.template.toml << EOF
[[runners]]
[runners.docker]
[[runners.docker.services]]
name = "mysql:latest"
[[runners.docker.services]]
name = "redis:latest"
EOF
```
* Наш шаблон:
``
$ cat > /tmp/test-config.template.toml << EOF
[[runners]]
[runners.docker]
[[runners.docker.services]]
name = "mysql:latest"
[[runners.docker.services]]
name = "redis:latest"
EOF
``


```
docker run --rm -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register \
  --non-interactive \
  --executor "docker" \
  --docker-image alpine:latest \
  --url "https://gitlab.com/" \
  --registration-token "PROJECT_REGISTRATION_TOKEN" \
  --description "docker-runner" \
  --maintenance-note "Free-form maintainer notes about this runner" \
  --tag-list "docker,aws" \
  --run-untagged="true" \
  --locked="false" \
  --access-level="not_protected"
```
2. Регистрационный токен можно найти по адресу `https://gitlab.com/project_namespace/project_name/runners`
3. Создаем команду для регистрации:

```
docker run --rm -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register \
  --non-interactive \
  --executor "docker" \
  --docker-image gitlab/gitlab-runner:latest \
  --url "https://gitlab.com/" \
  --registration-token "PROJECT_REGISTRATION_TOKEN" \
  --description "docker-runner" \
  --maintenance-note "Free-form maintainer notes about this runner" \
  --tag-list "docker,aws" \
  --run-untagged="true" \
  --locked="false" \
  --access-level="not_protected"

```
* Команда не прошла успешно.

4. Другой вариант регистрации

* Создаем файл конфигурации:
```
root@44e681f99687:/etc/gitlab-runner# gitlab-runner register
Runtime platform                                    arch=amd64 os=linux pid=60 revision=f761588f version=14.10.1
Running in system-mode.                            
                                                   
Enter the GitLab instance URL (for example, https://gitlab.com/):
https://gitlab.com/
Enter the registration token:
GR1348941aDbJ5hLqEha-sGVV72uF
Enter a description for the runner:
[44e681f99687]: gitlablesson-runner
Enter tags for the runner (comma-separated):
1.0.1
Enter optional maintenance note for the runner:
Yes
Registering runner... succeeded                     runner=GR1348941aDbJ5hLq
Enter an executor: kubernetes, docker, parallels, ssh, virtualbox, docker+machine, docker-ssh+machine, custom, docker-ssh, shell:
docker
Enter the default Docker image (for example, ruby:2.7):
docker:latest
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 


```
* Файл создан. Он находится в контейнере (и в папке волюме)
```
root@44e681f99687:/etc/gitlab-runner# cat config.toml 
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "gitlablesson-runner"
  url = "https://gitlab.com/"
  token = "YyZG39jkbdsUzum9WBiv"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]
    shm_size = 0

```
* Была попытка запуска piplent CI/CD. Неуспешно
* Проведена вторая попытка регистрации Runner
```
root@44e681f99687:/etc/gitlab-runner# gitlab-runner register   --non-interactive   --url "https://gitlab.com"   --registration-token "$GR1348941aDbJ5hLqEha-sGVV72uF"   --template-config /etc/gitlab-runner/config.toml
Runtime platform                                    arch=amd64 os=linux pid=94 revision=f761588f version=14.10.1
Running in system-mode.                            
                                                   
Merging configuration from template file "/etc/gitlab-runner/config.toml" 
Token specified trying to verify runner...         
WARNING: If you want to register use the '-r' instead of '-t'. 
Verifying runner... is alive                        runner=YyZG39jk
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 

```
* На странице в репозитрии с раннерами появилась информация о зарегитрированном раннере.
* Содержимое файла - конфигурации

```
root@44e681f99687:/etc/gitlab-runner# cat config.toml 
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "gitlablesson-runner"
  url = "https://gitlab.com/"
  token = "YyZG39jkbdsUzum9WBiv"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]
    shm_size = 0

[[runners]]
  name = "44e681f99687"
  url = "https://gitlab.com"
  token = "YyZG39jkbdsUzum9WBiv"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]
    shm_size = 0

```
* Перезапуск контейнера
```
docker run -d --name gitlab-runner --restart always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v gitlab-runner-config:/etc/gitlab-runner \
gitlab/gitlab-runner:latest

```
* Перезапуск регисрации был неудачный

### Локальная установка и регистрация раннера на ОС Ubuntu

* Инсталляция раннера в ОС Ubuntu
```
root@PC-Ubuntu:~# sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 47.4M  100 47.4M    0     0  5978k      0  0:00:08  0:00:08 --:--:-- 6893k
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# sudo chmod +x /usr/local/bin/gitlab-runner
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# users
maestro
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
Runtime platform                                    arch=amd64 os=linux pid=26078 revision=f761588f version=14.10.1
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# sudo gitlab-runner start
Runtime platform                                    arch=amd64 os=linux pid=26147 revision=f761588f version=14.10.1
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# echo $REGISTRATION_TOKEN

root@PC-Ubuntu:~# 

```
* Регистрация раннера
```
root@PC-Ubuntu:~# sudo gitlab-runner register --url https://gitlab.com/ --registration-token GR1348941aDbJ5hLqEha-sGVV72uF
Runtime platform                                    arch=amd64 os=linux pid=26326 revision=f761588f version=14.10.1
Running in system-mode.                            
                                                   
Enter the GitLab instance URL (for example, https://gitlab.com/):
[https://gitlab.com/]: 
Enter the registration token:
[GR1348941aDbJ5hLqEha-sGVV72uF]: 
Enter a description for the runner:
[PC-Ubuntu]: 
Enter tags for the runner (comma-separated):
1.0.1
Enter optional maintenance note for the runner:
1
Registering runner... succeeded                     runner=GR1348941aDbJ5hLq
Enter an executor: ssh, virtualbox, docker+machine, docker-ssh, parallels, shell, kubernetes, custom, docker, docker-ssh+machine:
docker 
Enter the default Docker image (for example, ruby:2.7):
docker:latest
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 
root@PC-Ubuntu:~# 

```
* Результат: Runner работает

### Устранение ошибки "error during connect: Post "http://docker:2375/v1.24"

* Ошибка при сборке:
```

Skipping Git submodules setup
Executing "step_script" stage of the job script
Using docker image sha256:da88b5cbcdd82afd42d2aedfc14ae3ffbbde9b2b6632ab38f3e67f826eb613f5 for docker:latest with digest docker@sha256:462f7ada37612b16adf56972b362b60c488861670b906a42e7a84319f2d1ff23 ...
$ docker build -t $CI_REGISTRY/zakharovnpa/gitlablesson/python-api:latest .
error during connect: Post "http://docker:2375/v1.24/build?buildargs=%7B%7D&cachefrom=%5B%5D&cgroupparent=&cpuperiod=0&cpuquota=0&cpusetcpus=&cpusetmems=&cpushares=0&dockerfile=Dockerfile&labels=%7B%7D&memory=0&memswap=0&networkmode=default&rm=1&shmsize=0&t=registry.gitlab.com%2Fzakharovnpa%2Fgitlablesson%2Fpython-api%3Alatest&target=&ulimits=null&version=1": dial tcp: lookup docker on 192.168.1.1:53: no such host
Cleaning up project directory and file based variables
ERROR: Job failed: exit code 1
```
* Причина: docker не мог получить доступ. Эта ошибка возникает с gitlab runners на основе докеров, такими как тот, который мы настроили с помощью dockerexecutor. Сообщение об ошибке означает, что  внутренний док - контейнер не подключен к хост-  docker демону. 
* Решение: Чтобы это исправить, установите следующие параметры в [runners.docker]gitlab  -runner config.toml :
```
тома = [ "/cache" , "/var/run/docker.sock:/var/run/docker.sock" ]
```
#### Выполнено:

```
root@PC-Ubuntu:~# cat /etc/gitlab-runner/config.toml
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "PC-Ubuntu"
  url = "https://gitlab.com/"
  token = "chxg1JAhi1pHa2eNznJA"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]        # Здесь отсутсвует запись о подключении к сокету докера
    shm_size = 0
root@PC-Ubuntu:~# 
```

* Вносим исправления:
```

root@PC-Ubuntu:~# vim /etc/gitlab-runner/config.toml
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
```
root@PC-Ubuntu:~# cat /etc/gitlab-runner/config.toml
concurrent = 1
check_interval = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "PC-Ubuntu"
  url = "https://gitlab.com/"
  token = "chxg1JAhi1pHa2eNznJA"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock"]       # внесенные исправления
    shm_size = 0

```

```
root@PC-Ubuntu:~# gitlab-runner --help
NAME:
   gitlab-runner - a GitLab Runner

USAGE:
   gitlab-runner [global options] command [command options] [arguments...]

VERSION:
   14.10.1 (f761588f)

AUTHOR:
   GitLab Inc. <support@gitlab.com>

COMMANDS:
     exec                  execute a build locally
     list                  List all configured runners
     run                   run multi runner service
     register              register a new runner
     install               install service
     uninstall             uninstall service
     start                 start service
     stop                  stop service
     restart               restart service
     status                get status of a service
     run-single            start single runner
     unregister            unregister specific runner
     verify                verify all registered runners
     artifacts-downloader  download and extract build artifacts (internal)
     artifacts-uploader    create and upload build artifacts (internal)
     cache-archiver        create and upload cache artifacts (internal)
     cache-extractor       download and extract cache artifacts (internal)
     cache-init            changed permissions for cache paths (internal)
     health-check          check health for a specific address
     read-logs             reads job logs from a file, used by kubernetes executor (internal)
     help, h               Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --cpuprofile value           write cpu profile to file [$CPU_PROFILE]
   --debug                      debug mode [$DEBUG]
   --log-format value           Choose log format (options: runner, text, json) [$LOG_FORMAT]
   --log-level value, -l value  Log level (options: debug, info, warn, error, fatal, panic) [$LOG_LEVEL]
   --help, -h                   show help
   --version, -v                print the version
root@PC-Ubuntu:~# 

```
* Проверяем статус раннера на локальной ОС. Запущен.
```
root@PC-Ubuntu:~# gitlab-runner status
Runtime platform                                    arch=amd64 os=linux pid=49997 revision=f761588f version=14.10.1
gitlab-runner: Service is running
root@PC-Ubuntu:~# 
```
* Делаем рестарт раннера
```
root@PC-Ubuntu:~# gitlab-runner restart
Runtime platform                                    arch=amd64 os=linux pid=50021 revision=f761588f version=14.10.1
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
* Проверяем статус раннера на локальной ОС. Запущен.
```
root@PC-Ubuntu:~# gitlab-runner status
Runtime platform                                    arch=amd64 os=linux pid=50042 revision=f761588f version=14.10.1
gitlab-runner: Service is running
root@PC-Ubuntu:~# 

```
