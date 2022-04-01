## Ход выполнения Домашнего задания к занятию "10.02. Системы мониторинга"

### Рабочая директория:
```
root@server1:~/learning-monitoring/sandbox#
```

## Обязательные задания

1. Опишите основные плюсы и минусы pull и push систем мониторинга.

2. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

    - Prometheus 
    - TICK
    - Zabbix
    - VictoriaMetrics
    - Nagios

3. Склонируйте себе [репозиторий](https://github.com/influxdata/sandbox/tree/master) и запустите TICK-стэк, 
используя технологии docker и docker-compose.
```
root@server1:~/learning-monitoring# git clone https://github.com/influxdata/sandbox.git
Cloning into 'sandbox'...
remote: Enumerating objects: 1718, done.
remote: Counting objects: 100% (32/32), done.
remote: Compressing objects: 100% (32/32), done.
remote: Total 1718 (delta 13), reused 1 (delta 0), pack-reused 1686
Receiving objects: 100% (1718/1718), 7.17 MiB | 6.96 MiB/s, done.
Resolving deltas: 100% (946/946), done.
```
* запускаем `./sandbox`
```
root@server1:~/learning-monitoring/sandbox# ./sandbox up
Using latest, stable releases
Spinning up Docker Images...
If this is your first time starting sandbox this might take a minute...
Sending build context to Docker daemon     226B
Step 1/2 : ARG KAPACITOR_TAG
Step 2/2 : FROM kapacitor:$KAPACITOR_TAG
latest: Pulling from library/kapacitor
0030cc4ce25c: Pull complete 
7ab54d469df6: Pull complete 
0c84a1692804: Pull complete 
64afa4a187b8: Pull complete 
802dfe951f93: Pull complete 
b78a94103e0b: Pull complete 
0bb7417a363f: Pull complete 
4b5ab80f68f0: Pull complete 
Digest: sha256:d3c8afc4ebfe2c82f6205bc340f325b04259da11499174cefe60218b008620d2
Status: Downloaded newer image for kapacitor:latest
 ---> 137553572bf1
Successfully built 137553572bf1
Successfully tagged kapacitor:latest
Sending build context to Docker daemon     513B
Step 1/4 : ARG CHRONOGRAF_TAG
Step 2/4 : FROM chronograf:$CHRONOGRAF_TAG
latest: Pulling from library/chronograf
21fb02cbac85: Pull complete 
56b9c16e1754: Pull complete 
b0bda37b43ac: Pull complete 
e091fb54b38b: Pull complete 
1d3ce8d41d7d: Pull complete 
1032cdb5990d: Pull complete 
Digest: sha256:390710b78ab8172b84fd3902efb9768e3b78428fe9796a23af8945250a114ebc
Status: Downloaded newer image for chronograf:latest
 ---> 53ba73fe4ae1
Step 3/4 : ADD ./sandbox.src ./usr/share/chronograf/resources/
 ---> 2d6d04c5cf39
Step 4/4 : ADD ./sandbox-kapa.kap ./usr/share/chronograf/resources/
 ---> bf31dbb78f69
Successfully built bf31dbb78f69
Successfully tagged chrono_config:latest
Sending build context to Docker daemon  5.968MB
Step 1/6 : FROM alpine:3.12
3.12: Pulling from library/alpine
9c4930dab762: Extracting [================================================>  ]   2.72MB/2.808MB
Sending build context to Docker daemon     248B
Step 1/2 : ARG INFLUXDB_TAG
Step 2/2 : FROM influxdb:$INFLUXDB_TAG
1.8: Pulling from library/influxdb
0030cc4ce25c: Already exists 
7ab54d469df6: Already exists 
0c84a1692804: Already exists 
ff77374c2e1b: Pull complete 
6ca272d9f078: Pull complete 
2740ef6abdea: Pull complete 
62a5ae9b7700: Pull complete 
2bc28277163b: Pull complete 
Digest: sha256:4d8267af494f3f6f0d42cc0d096e190a411e9762566fe525a1a37adc38a9c152
Status: Downloaded newer image for influxdb:1.8
 ---> cc9eb7b5252d
Successfully built cc9eb7b5252d
Successfully tagged influxdb:latest
Sending build context to Docker daemon     225B
Step 1/2 : ARG TELEGRAF_TAG
Step 2/2 : FROM telegraf:$TELEGRAF_TAG
latest: Pulling from library/telegraf
dbba69284b27: Pull complete 
9baf437a1bad: Pull complete 
6ade5c59e324: Pull complete 
0680c11313d7: Pull complete 
80f43e04d384: Pull complete 
7762e1308d94: Pull complete 
b6c37f1343ec: Pull complete 
Digest: sha256:1ff45b21d3e3c2de446ea01f14de3bcfa563e4211e6a7b35292ea89230224242
Status: Downloaded newer image for telegraf:latest
 ---> a9e2b2b32583
Successfully built a9e2b2b32583
Successfully tagged telegraf:latest
1 error occurred:
	* Status: failed to register layer: Error processing tar file(gzip: invalid checksum): , Code: 1


root@server1:~/learning-monitoring/sandbox# 

```
* Новые докер-образы
```
root@server1:~/learning-monitoring/sandbox# docker image list
REPOSITORY                        TAG        IMAGE ID       CREATED         SIZE
chrono_config                     latest     bf31dbb78f69   7 minutes ago   182MB
telegraf                          latest     a9e2b2b32583   34 hours ago    358MB
kapacitor                         latest     137553572bf1   36 hours ago    340MB
influxdb                          1.8        cc9eb7b5252d   36 hours ago    287MB
influxdb                          latest     cc9eb7b5252d   36 hours ago    287MB
chronograf                        latest     53ba73fe4ae1   3 days ago      182MB
<none>                            <none>     834eb9e51514   3 weeks ago     2.51GB
registry.redhat.io/rhel8/podman   latest     f58db8adf7bb   2 months ago    399MB
postgres                          13         e01c76bb1351   2 months ago    371MB
postgres                          12         58bff7631346   2 months ago    371MB
dockerlesson                      1.0        24ef0db48b2f   3 months ago    85.3MB
zakharovnpa/debian                009        888b869de873   3 months ago    124MB
zakharovnpa/centos7               001        62ad6751e301   3 months ago    261MB
zakharovnpa/nginx                 13.12.21   4b8b755d634a   3 months ago    141MB
zakharovnpa/ansible               8.12.21    06b6ca73286e   3 months ago    227MB
python                            3-alpine   eb5bc7d10d52   3 months ago    45.4MB
nginx                             latest     f652ca386ed1   4 months ago    141MB
debian                            latest     05d2318291e3   4 months ago    124MB
alpine                            3.14       0a97eee8041e   4 months ago    5.61MB
ubuntu                            latest     ba6acccedd29   5 months ago    72.8MB
hello-world                       latest     feb5d9fea6a5   6 months ago    13.3kB
centos                            7          eeb6ee3f44bd   6 months ago    204MB
centos                            latest     5d0da3dc9764   6 months ago    231MB
pycontribs/fedora                 latest     c31790496329   11 months ago   586MB
pycontribs/centos                 8          fec8cb567d93   11 months ago   749MB
pycontribs/centos                 7          bafa54e44377   11 months ago   488MB
pycontribs/ubuntu                 latest     42a4e3b21923   2 years ago     664MB
teikadev/postgres12-partman       latest     63db8bbf0186   2 years ago     155MB
root@server1:~/learning-monitoring/sandbox# 

```
* вторая попытка запуска `./sandbox`
```
root@server1:~/learning-monitoring/sandbox# ./sandbox up
Using latest, stable releases
Spinning up Docker Images...
If this is your first time starting sandbox this might take a minute...
Sending build context to Docker daemon     226B
Step 1/2 : ARG KAPACITOR_TAG
Step 2/2 : FROM kapacitor:$KAPACITOR_TAG
 ---> 137553572bf1
Successfully built 137553572bf1
Successfully tagged kapacitor:latest
Sending build context to Docker daemon     513B
Step 1/4 : ARG CHRONOGRAF_TAG
Step 2/4 : FROM chronograf:$CHRONOGRAF_TAG
 ---> 53ba73fe4ae1
Step 3/4 : ADD ./sandbox.src ./usr/share/chronograf/resources/
 ---> Using cache
 ---> 2d6d04c5cf39
Step 4/4 : ADD ./sandbox-kapa.kap ./usr/share/chronograf/resources/
 ---> Using cache
 ---> bf31dbb78f69
Successfully built bf31dbb78f69
Successfully tagged chrono_config:latest
Sending build context to Docker daemon  5.968MB
Step 1/6 : FROM alpine:3.12
3.12: Pulling from library/alpine
9c4930dab762: Pull complete 
Digest: sha256:e42c1b8e03bdaa471deb198d981b52ac421441975195a20004aea624890f8b1c
Status: Downloaded newer image for alpine:3.12
 ---> d7db87feda9d
Step 2/6 : EXPOSE 3010:3000
 ---> Running in 9ebe3103b292
 ---> e650381003cc
Step 3/6 : RUN mkdir -p /documentation
 ---> Running in 362677b4f094
 ---> d1a19b846666
Step 4/6 : COPY builds/documentation /documentation/
 ---> f86c526743e9
Step 5/6 : COPY static/ /documentation/static
 ---> bf3439aa620e
Step 6/6 : CMD ["/documentation/documentation", "-filePath", "/documentation/"]
 ---> Running in 3d4224a38b64
 ---> 0bfbc19d85f8
Successfully built 0bfbc19d85f8
Successfully tagged sandbox_documentation:latest
Sending build context to Docker daemon     248B
Step 1/2 : ARG INFLUXDB_TAG
Step 2/2 : FROM influxdb:$INFLUXDB_TAG
 ---> cc9eb7b5252d
Successfully built cc9eb7b5252d
Successfully tagged influxdb:latest
Sending build context to Docker daemon     225B
Step 1/2 : ARG TELEGRAF_TAG
Step 2/2 : FROM telegraf:$TELEGRAF_TAG
 ---> a9e2b2b32583
Successfully built a9e2b2b32583
Successfully tagged telegraf:latest

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
[+] Running 6/6
 ⠿ Network sandbox_default            Created                                                                                                                                                            0.1s
 ⠿ Container sandbox-influxdb-1       Started                                                                                                                                                            2.2s
 ⠿ Container sandbox-documentation-1  Started                                                                                                                                                            2.1s
 ⠿ Container sandbox-telegraf-1       Started                                                                                                                                                            4.7s
 ⠿ Container sandbox-kapacitor-1      Started                                                                                                                                                            4.3s
 ⠿ Container sandbox-chronograf-1     Started                                                                                                                                                            6.8s
Opening tabs in browser...
./sandbox: line 91: xdg-open: command not found
root@server1:~/learning-monitoring/sandbox# 
root@server1:~/learning-monitoring/sandbox# 
root@server1:~/learning-monitoring/sandbox# docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS         PORTS                                                                                                                             NAMES
fb0d798dd2f2   chrono_config           "/entrypoint.sh chro…"   2 minutes ago   Up 2 minutes   0.0.0.0:8888->8888/tcp, :::8888->8888/tcp                                                                                         sandbox-chronograf-1
622ab070ed27   telegraf                "/entrypoint.sh tele…"   2 minutes ago   Up 2 minutes   8092/udp, 8125/udp, 8094/tcp                                                                                                      sandbox-telegraf-1
0de143563cd7   kapacitor               "/entrypoint.sh kapa…"   2 minutes ago   Up 2 minutes   0.0.0.0:9092->9092/tcp, :::9092->9092/tcp                                                                                         sandbox-kapacitor-1
9eb37da3eef3   sandbox_documentation   "/documentation/docu…"   2 minutes ago   Up 2 minutes   0.0.0.0:3010->3000/tcp, :::3010->3000/tcp                                                                                         sandbox-documentation-1
053e50a14ffb   influxdb                "/entrypoint.sh infl…"   2 minutes ago   Up 2 minutes   0.0.0.0:8082->8082/tcp, :::8082->8082/tcp, 0.0.0.0:8086->8086/tcp, :::8086->8086/tcp, 0.0.0.0:8089->8089/udp, :::8089->8089/udp   sandbox-influxdb-1

```

В виде решения на это упражнение приведите выводы команд с вашего компьютера (виртуальной машины):

    - curl -v http://localhost:8086/ping
 ```
    *   Trying ::1:8086...
* TCP_NODELAY set
* Connected to localhost (::1) port 8086 (#0)
> GET /ping HTTP/1.1
> Host: localhost:8086
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 204 No Content
< Content-Type: application/json
< Request-Id: d27c0a48-b1d6-11ec-86ab-0242ac120002
< X-Influxdb-Build: OSS
< X-Influxdb-Version: 1.8.10
< X-Request-Id: d27c0a48-b1d6-11ec-86ab-0242ac120002
< Date: Fri, 01 Apr 2022 16:14:35 GMT
< 
* Connection #0 to host localhost left intact

```
    
    - curl -v http://localhost:8888
    ```
    <!DOCTYPE html>
     <html>
       <head>
         <meta http-equiv="Content-type" content="text/html; charset=utf-8">
           <title>Chronograf</title>
           <link rel="icon shortcut" href="/favicon.fa749080.ico">
           <link rel="stylesheet" href="/src.9cea3e4e.css">
       </head>
         <body> 
           <div id="react-root" data-basepath="">
           </div> 
             <script src="/src.a969287c.js">
             </script> 
         </body>
     </html>
    ```
    
    - curl http://localhost:9092/kapacitor/v1/ping
    
    ```
    {
    "error": "Not Found",
    "message": "Not Found"
    }
    ```

А также скриншот веб-интерфейса ПО chronograf (`http://localhost:8888`). 

P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим `Z`, например
`./data:/var/lib:Z`

4. Перейдите в веб-интерфейс Chronograf (`http://localhost:8888`) и откройте вкладку `Data explorer`.

    - Нажмите на кнопку `Add a query`
    - Изучите вывод интерфейса и выберите БД `telegraf.autogen`
    - В `measurments` выберите mem->host->telegraf_container_id , а в `fields` выберите used_percent. 
    Внизу появится график утилизации оперативной памяти в контейнере telegraf.
    - Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. 
    Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.

Для выполнения задания приведите скриншот с отображением метрик утилизации места на диске 
(disk->host->telegraf_container_id) из веб-интерфейса.



5. Изучите список [telegraf inputs](https://github.com/influxdata/telegraf/tree/master/plugins/inputs). 
Добавьте в конфигурацию telegraf следующий плагин - [docker](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker):
```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```

Дополнительно вам может потребоваться донастройка контейнера telegraf в `docker-compose.yml` дополнительного volume и 
режима privileged:
```
  telegraf:
    image: telegraf:1.4.0
    privileged: true
    volumes:
      - ./etc/telegraf.conf:/etc/telegraf/telegraf.conf:Z
      - /var/run/docker.sock:/var/run/docker.sock:Z
    links:
      - influxdb
    ports:
      - "8092:8092/udp"
      - "8094:8094"
      - "8125:8125/udp"
```

После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список `measurments` в 
веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.

Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

В веб-интерфейсе откройте вкладку `Dashboards`. Попробуйте создать свой dashboard с отображением:

    - утилизации ЦПУ
    - количества использованного RAM
    - утилизации пространства на дисках
    - количество поднятых контейнеров
    - аптайм
    - ...
    - фантазируйте)
    
    ---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

