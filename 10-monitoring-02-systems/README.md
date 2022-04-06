# Домашнее задание к занятию "10.02. Системы мониторинга" - Захаров Сергей Николаевич

## Обязательные задания

1. Опишите основные плюсы и минусы pull и push систем мониторинга.

**Ответ:** 

1. Плюсы pull модели. 
  * централизованное регулирование процесса опроса агентов
  * единая точка конфигурирования процесса пороса хостов и агентов
  * получение данных от авторизованных источников. использовние SNMPv2, SNMPv3, RADIUS и пр.
  * использование ICMP для мониторинга доступности
  * использование шаблонов настройки сбора данных для однотипного оборудования
  * данные запрашиваются и принимаются от множества источников в той очередности, которую определяет сама система мониторинга 
  * использование прокси-серверов в случае невозможности прямого доступа по сети к агентам
  * возможность прямого доступа к агенту и запросу данных в ручном режиме
2. Минусы pull модели
  * необходимсоть администрирования системы мониторинга
  * нет возможности быстро обнаружить хосты динамического инвентори
3. Плюсы push модели
  * использование протокола UDP, снижающего накладные расходы на транспорт
  * испоьзование несколько серверов для опроса агентов
  * гибко настраивать на каждом агенте параметры отправки данных (частоту отправки, величину данных)
  * освобождает систему мониторинга от процесса контроля настроек и от процесса опроса агентов. Она просто ждет данные
  * удобство применения в системах с динамическим инвентори
4. Минусы push модели
  * необходимость установки агентов мониторинга на контролируемые хосты
  * Возможен нерегулируемый и лавинообразный поток данных от агентов
  * необходимость использования промежуточной точки сбора данных от агентов в 
  * множество точек конфигурирования

2. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

    - Prometheus 
    - TICK
    - Zabbix
    - VictoriaMetrics
    - Nagios

**Ответ:**

* К системам с pull моделью относятся:
  * Nagios
  * Prometheus

* К системам с push моделью относятся:
  * TICK

* К гибридным соистемам относятся:
  * VictoriaMetrics
  * Zabbix

3. Склонируйте себе [репозиторий](https://github.com/influxdata/sandbox/tree/master) и запустите TICK-стэк, 
используя технологии docker и docker-compose.

В виде решения на это упражнение приведите выводы команд с вашего компьютера (виртуальной машины):

    - curl http://localhost:8086/ping
    - curl http://localhost:8888
    - curl http://localhost:9092/kapacitor/v1/ping

А также скриншот веб-интерфейса ПО chronograf (`http://localhost:8888`). 

P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим `Z`, например
`./data:/var/lib:Z`

**Ответ:**

* Запрос `curl -v http://localhost:8086/ping`
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
*  Запрос `curl -v http://localhost:8888`
```html
*   Trying 127.0.0.1:8888...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8888 (#0)
> GET / HTTP/1.1
> Host: 127.0.0.1:8888
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Accept-Ranges: bytes
< Cache-Control: public, max-age=3600
< Content-Length: 336
< Content-Security-Policy: script-src 'self'; object-src 'self'
< Content-Type: text/html; charset=utf-8
< Etag: "3362220244"
< Last-Modified: Tue, 22 Mar 2022 20:02:44 GMT
< Vary: Accept-Encoding
< X-Chronograf-Version: 1.9.4
< X-Content-Type-Options: nosniff
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
< Date: Wed, 06 Apr 2022 12:00:47 GMT
* Connection #0 to host 127.0.0.1 left intact
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
* Запрос `curl -v http://localhost:9092/kapacitor/v1/ping`
```
*   Trying ::1:9092...
* TCP_NODELAY set
* Connected to localhost (::1) port 9092 (#0)
> GET /kapacitor/v1/ping HTTP/1.1
> Host: localhost:9092
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 204 No Content
< Content-Type: application/json; charset=utf-8
< Request-Id: 01de3cc1-b5a2-11ec-8423-000000000000
< X-Kapacitor-Version: 1.6.4
< Date: Wed, 06 Apr 2022 12:06:36 GMT
< 
* Connection #0 to host localhost left intact
```

4. Перейдите в веб-интерфейс Chronograf (`http://localhost:8888`) и откройте вкладку `Data explorer`.

    - Нажмите на кнопку `Add a query`
    - Изучите вывод интерфейса и выберите БД `telegraf.autogen`
    - В `measurments` выберите mem->host->telegraf_container_id , а в `fields` выберите used_percent. 
    Внизу появится график утилизации оперативной памяти в контейнере telegraf.
    - Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. 
    Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.

Для выполнения задания приведите скриншот с отображением метрик утилизации места на диске 
(disk->host->telegraf_container_id) из веб-интерфейса.

**Ответ:**

Секеция "disk" отстутсвовала в `measurments` при первоначальной кнофигурации Telegraf.

* После изменения конфигурации Telegraf, перезапуска Telegraf видим секцию "disk" и необходимые параметры:
![screen-disk-host](/10-monitoring-02-systems/Files/screen-disk-host.png)

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

**Ответ:**

* После добавления плагина `docker`:
![screen-docker-host](/10-monitoring-02-systems/Files/screen-docker-host.png)

Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.

**Ответ:**

[Метрики описаны здесь](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker#metrics)

Примеры:
### Metrics

- docker
  - tags:
    - unit
    - engine_host
    - server_version
  - fields:
    - n_used_file_descriptors
    - n_cpus
    - n_containers
    - n_containers_running
    - n_containers_stopped
    - n_containers_paused
    - n_images
    - n_goroutines
    - n_listener_events
    - memory_total
    - pool_blocksize (requires devicemapper storage driver) (deprecated see: `docker_devicemapper`)

- docker_data (deprecated see: `docker_devicemapper`)
  - tags:
    - unit
    - engine_host
    - server_version
  - fields:
    - available
    - total
    - used

- docker_metadata (deprecated see: `docker_devicemapper`)
  - tags:
    - unit
    - engine_host
    - server_version
  - fields:
    - available
    - total
    - used

- docker_container_mem
  - tags:
    - engine_host
    - server_version
    - container_image
    - container_name
    - container_status
    - container_version
  - fields:
    - total_pgmajfault
    - cache
    - mapped_file
    - total_inactive_file
    - pgpgout
    - rss
    - total_mapped_file
    - writeback
    - unevictable
    - pgpgin
    - total_unevictable
    - pgmajfault
    - total_rss
    - total_rss_huge
    - total_writeback
    - total_inactive_anon
    - rss_huge
    - hierarchical_memory_limit
    - total_pgfault
    - total_active_file
    - active_anon
    - total_active_anon
    - total_pgpgout
    - total_cache
    - inactive_anon
    - active_file
    - pgfault
    - inactive_file
    - total_pgpgin
    - max_usage
    - usage
    - failcnt
    - limit
    - container_id

- docker_container_cpu
  - tags:
    - engine_host
    - server_version
    - container_image
    - container_name
    - container_status
    - container_version
    - cpu
  - fields:
    - throttling_periods
    - throttling_throttled_periods
    - throttling_throttled_time
    - usage_in_kernelmode
    - usage_in_usermode
    - usage_system
    - usage_total
    - usage_percent
    - container_id

- docker_container_net
  - tags:
    - engine_host
    - server_version
    - container_image
    - container_name
    - container_status
    - container_version
    - network
  - fields:
    - rx_dropped
    - rx_bytes
    - rx_errors
    - tx_packets
    - tx_dropped
    - rx_packets
    - tx_errors
    - tx_bytes
    - container_id

- docker_container_blkio
  - tags:
    - engine_host
    - server_version
    - container_image
    - container_name
    - container_status
    - container_version
    - device
  - fields:
    - io_service_bytes_recursive_async
    - io_service_bytes_recursive_read
    - io_service_bytes_recursive_sync
    - io_service_bytes_recursive_total
    - io_service_bytes_recursive_write
    - io_serviced_recursive_async
    - io_serviced_recursive_read
    - io_serviced_recursive_sync
    - io_serviced_recursive_total
    - io_serviced_recursive_write
    - container_id


## Дополнительное задание (со звездочкой*) - необязательно к выполнению

В веб-интерфейсе откройте вкладку `Dashboards`. Попробуйте создать свой dashboard с отображением:
(это по хронографу):
- утилизации ЦПУ
- количества использованного RAM
- утилизации пространства на дисках
- количество поднятых контейнеров
- аптайм
- ...
- фантазируйте)
    
**Ответ:**

[screen-dasboard-host](/10-monitoring-02-systems/Files/screen-dasboard-host.png)
    ---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

