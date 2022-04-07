### Ход выполнения ДЗ по теме "10.03. Grafana"

#### Директория выполнения ДЗ:
* На ВМ, запускаемой Vagrant из директории `root@PC-Ubuntu:~/vagrant-project/Betta/vagrant#`
```
root@server1:~/learning-monitoring/Grafana#
```
```
root@server1:~/learning-monitoring/Grafana# tree
.
├── docker-compose.yml
├── prometheus
│   └── prometheus.yml
└── README.md

1 directory, 3 files

```

### Предваритеотная подготовка:
1. Запуск ВМ на Docker-compose
```
root@server1:~/learning-monitoring/Grafana# docker-compose up -d
[+] Running 4/4
 ⠿ Network grafana_monitor-net  Created                                                                                                                                                                  0.1s
 ⠿ Container nodeexporter       Started                                                                                                                                                                  0.9s
 ⠿ Container prometheus         Started                                                                                                                                                                  1.9s
 ⠿ Container grafana            Started               
```


2. Файл `Docker-compose.yml`

```yml
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:v2.24.1
    container_name: prometheus
    volumes:
      - ./prometheus:/etc/prometheus:Z
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--storage.tsdb.retention.time=200h'
      - '--web.enable-lifecycle'
    restart: unless-stopped
    depends_on:
      - nodeexporter
    ports:
      - 9090:9090
    expose:
      - 9090
    networks:
      - monitor-net

  nodeexporter:
    image: prom/node-exporter:v1.0.1
    container_name: nodeexporter
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.ignored-mount-points=^/(sys|proc|dev|host|etc)($$|/)'
    restart: unless-stopped
    ports:
      - 9100:9100
    expose:
      - 9100
    networks:
      - monitor-net


  grafana:
    image: grafana/grafana:7.4.0
    container_name: grafana
    volumes:
      - grafana_data:/var/lib/grafana
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
      - GF_USERS_ALLOW_SIGN_UP=false
    restart: unless-stopped
    depends_on:
      - prometheus
    ports:
      - 3000:3000
    expose:
      - 3000
    networks:
      - monitor-net

networks:
  monitor-net:
    driver: bridge

volumes:
  prometheus_data: {}
  grafana_data: {}

```

3. Файл `prometheus.yml`
```yml
global:
  scrape_interval:     15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'nodeexporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['nodeexporter:9100']

```

4. Запущенные контейнеры:
* В директории с файлом `Docker-compose.yml` запускаем команду:
```
docker-compose up -d
```
* Запущенные контейнеры:
```
root@server1:~/learning-monitoring/Grafana# docker-compose ps
NAME                COMMAND                  SERVICE             STATUS              PORTS
grafana             "/run.sh"                grafana             running             0.0.0.0:3000->3000/tcp, :::3000->3000/tcp
nodeexporter        "/bin/node_exporter …"   nodeexporter        running             0.0.0.0:9100->9100/tcp, :::9100->9100/tcp
prometheus          "/bin/prometheus --c…"   prometheus          running             0.0.0.0:9090->9090/tcp, :::9090->9090/tcp

```

5. Проверяем доступность портов:

* Коннект к nodeexporter
```
root@server1:~/learning-monitoring/Grafana# curl http://192.168.56.11:9100
<html>
			<head><title>Node Exporter</title></head>
			<body>
			<h1>Node Exporter</h1>
			<p><a href="/metrics">Metrics</a></p>
			</body>
			</html>
```

```
root@server1:~/learning-monitoring/Grafana# curl -v http://127.0.0.1:9100   # или можно http://192.168.56.11:9100
*   Trying 127.0.0.1:9100...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 9100 (#0)
> GET / HTTP/1.1
> Host: 127.0.0.1:9100
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Thu, 07 Apr 2022 08:39:51 GMT
< Content-Length: 150
< Content-Type: text/html; charset=utf-8
< 
<html>
			<head><title>Node Exporter</title></head>
			<body>
			<h1>Node Exporter</h1>
			<p><a href="/metrics">Metrics</a></p>
			</body>
* Connection #0 to host 127.0.0.1 left intact
</html>

```
* Коннект к prometheus
```
root@server1:~/learning-monitoring/Grafana# curl http://192.168.56.11:9090
<a href="/graph">Found</a>.

```

```
root@server1:~/learning-monitoring/Grafana# curl -v http://127.0.0.1:9090   # или можно http://192.168.56.11:9100
*   Trying 127.0.0.1:9090...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 9090 (#0)
> GET / HTTP/1.1
> Host: 127.0.0.1:9090
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 Found
< Content-Type: text/html; charset=utf-8
< Location: /graph
< Date: Thu, 07 Apr 2022 08:55:13 GMT
< Content-Length: 29
< 
<a href="/graph">Found</a>.

* Connection #0 to host 127.0.0.1 left intact

```
* Коннект к grafana
```
root@server1:~/learning-monitoring/Grafana# curl http://192.168.56.11:3000
<a href="/login">Found</a>.
```

```
root@server1:~/learning-monitoring/Grafana# curl -v http://192.168.56.11:3000
*   Trying 192.168.56.11:3000...
* TCP_NODELAY set
* Connected to 192.168.56.11 (192.168.56.11) port 3000 (#0)
> GET / HTTP/1.1
> Host: 192.168.56.11:3000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 Found
< Cache-Control: no-cache
< Content-Type: text/html; charset=utf-8
< Expires: -1
< Location: /login
< Pragma: no-cache
< Set-Cookie: redirect_to=%2F; Path=/; HttpOnly; SameSite=Lax
< X-Content-Type-Options: nosniff
< X-Frame-Options: deny
< X-Xss-Protection: 1; mode=block
< Date: Thu, 07 Apr 2022 15:06:26 GMT
< Content-Length: 29
< 
<a href="/login">Found</a>.

* Connection #0 to host 192.168.56.11 left intact

```

6. После всех проверок подключаемся через браузер к Графане:
```
http://192.168.56.11:3000
```

7. Войдя в Графану, заменить пароль пользователя.
8. Далее выполнить подключение Прометеуса через меню Configuration --> DataSource
![screen-DataSource-grafana](/10-monitoring-03-grafana/Files/screen-DataSource-grafana.png)



## Задание повышенной сложности

**В части задания 1** не используйте директорию [help](./help) для сборки проекта, самостоятельно разверните grafana, где в 
роли источника данных будет выступать prometheus, а сборщиком данных node-exporter:
- grafana
- prometheus-server
- prometheus node-exporter

За дополнительными материалами, вы можете обратиться в официальную документацию grafana и prometheus.

В решении к домашнему заданию приведите также все конфигурации/скрипты/манифесты, которые вы 
использовали в процессе решения задания.

**В части задания 3** вы должны самостоятельно завести удобный для вас канал нотификации, например Telegram или Email
и отправить туда тестовые события.

В решении приведите скриншоты тестовых событий из каналов нотификаций.

## Обязательные задания

### Задание 1
Используя директорию [help](./help) внутри данного домашнего задания - запустите связку prometheus-grafana.

Зайдите в веб-интерфейс графана, используя авторизационные данные, указанные в манифесте docker-compose.

Подключите поднятый вами prometheus как источник данных.

Решение домашнего задания - скриншот веб-интерфейса grafana со списком подключенных Datasource.

**Ответ:**

![screen-dashboard-grafana](/10-monitoring-03-grafana/Files/screen-dashboard-grafana.png)

## Задание 2
Изучите самостоятельно ресурсы:
- [promql-for-humans](https://timber.io/blog/promql-for-humans/#cpu-usage-by-instance)
- [understanding prometheus cpu metrics](https://www.robustperception.io/understanding-machine-cpu-usage)

Создайте Dashboard и в ней создайте следующие Panels:
- Утилизация CPU для nodeexporter (в процентах, 100-idle)
- CPULA 1/5/15
- Количество свободной оперативной памяти
- Количество места на файловой системе

Для решения данного ДЗ приведите promql запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

**Ответ:**
1. Утилизация CPU для nodeexporter (в процентах, 100-idle)

* Запрос:
```
100 * (1 - avg by(instance)(irate(node_cpu_seconds_total{mode="idle"}[5m])))
```
* Результат:
![screen-CPU-nodeexporter](/10-monitoring-03-grafana/Files/screen-CPU-nodeexporter.png)

2. CPULA 1/5/15
* Запрос A:
```
node_load1{job="nodeexporter"}
```
* Запрос B:
```
node_load5{job="nodeexporter"}
```
* Запрос C:
```
node_load15{job="nodeexporter"}
```

* Результат:
![screen-CPULA-nodeexporter](/10-monitoring-03-grafana/Files/screen-CPULA-nodeexporter.png)

3. Количество свободной оперативной памяти
* Запрос:
```
node_memory_Active_bytes / on (instance) node_memory_MemTotal_bytes
```
* Результат:
![screen-Free-mem-nodeexporter](/10-monitoring-03-grafana/Files/screen-Free-mem-nodeexporter.png)

4. Количество места на файловой системе
* Запрос:
```
node_filesystem_avail_bytes{fstype!~"tmpfs|fuse.lxcfs|squashfs"} / node_filesystem_size_bytes{fstype!~"tmpfs|fuse.lxcfs|squashfs"}
```
* Результат:
![screen-Free-space-nodeexporter](/10-monitoring-03-grafana/Files/screen-Free-space-nodeexporter.png)

## Задание 3
Создайте для каждой Dashboard подходящее правило alert (можно обратиться к первой лекции в блоке "Мониторинг").

Для решения ДЗ - приведите скриншот вашей итоговой Dashboard.

**Ответ:**

* Результат:
![screen-Dash-Learning-nodeexporter](/10-monitoring-03-grafana/Files/screen-Dash-Learning-nodeexporter.png)

## Задание 4
Сохраните ваш Dashboard.

Для этого перейдите в настройки Dashboard, выберите в боковом меню "JSON MODEL".

Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.

В решении задания - приведите листинг этого файла.

**Ответ:**

* Файл учебной dasboard `Dash-Learninig.json`

```json
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": "-- Grafana --",
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "gnetId": null,
  "graphTooltip": 0,
  "id": 4,
  "links": [],
  "panels": [
    {
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "custom": {},
          "unit": "percent"
        },
        "overrides": []
      },
      "fill": 1,
      "fillGradient": 0,
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 0,
        "y": 0
      },
      "hiddenSeries": false,
      "id": 8,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.4.0",
      "pointradius": 2,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "node_load1{instance=\"nodeexporter:9100\", job=\"nodeexporter\"}",
          "interval": "",
          "legendFormat": "",
          "refId": "A"
        },
        {
          "expr": "node_load5{instance=\"nodeexporter:9100\", job=\"nodeexporter\"}",
          "hide": false,
          "interval": "",
          "legendFormat": "",
          "refId": "B"
        },
        {
          "expr": "node_load15{instance=\"nodeexporter:9100\", job=\"nodeexporter\"}",
          "hide": false,
          "interval": "",
          "legendFormat": "",
          "refId": "C"
        }
      ],
      "thresholds": [],
      "timeFrom": null,
      "timeRegions": [],
      "timeShift": null,
      "title": "CPULA 1/5/15",
      "tooltip": {
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "$$hashKey": "object:1239",
          "format": "percent",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "$$hashKey": "object:1240",
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "alert": {
        "alertRuleTags": {},
        "conditions": [
          {
            "evaluator": {
              "params": [
                0.4368
              ],
              "type": "gt"
            },
            "operator": {
              "type": "and"
            },
            "query": {
              "params": [
                "A",
                "1m",
                "now"
              ]
            },
            "reducer": {
              "params": [],
              "type": "avg"
            },
            "type": "query"
          }
        ],
        "executionErrorState": "alerting",
        "for": "5m",
        "frequency": "1m",
        "handler": 1,
        "name": "Free Memory alert",
        "noDataState": "no_data",
        "notifications": []
      },
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "custom": {},
          "unit": "decgbytes"
        },
        "overrides": []
      },
      "fill": 1,
      "fillGradient": 0,
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 12,
        "y": 0
      },
      "hiddenSeries": false,
      "id": 6,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.4.0",
      "pointradius": 2,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "node_memory_Active_bytes / on (instance) node_memory_MemTotal_bytes",
          "interval": "",
          "legendFormat": "",
          "refId": "A"
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": true,
          "line": true,
          "op": "gt",
          "value": 0.4368,
          "visible": true
        }
      ],
      "timeFrom": null,
      "timeRegions": [],
      "timeShift": null,
      "title": "Free Memory",
      "tooltip": {
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "$$hashKey": "object:880",
          "format": "decgbytes",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "$$hashKey": "object:881",
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "custom": {},
          "unit": "mbytes"
        },
        "overrides": []
      },
      "fill": 1,
      "fillGradient": 0,
      "gridPos": {
        "h": 8,
        "w": 12,
        "x": 0,
        "y": 8
      },
      "hiddenSeries": false,
      "id": 4,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.4.0",
      "pointradius": 2,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "node_filesystem_avail_bytes{fstype!~\"tmpfs|fuse.lxcfs|squashfs\"} / node_filesystem_size_bytes{fstype!~\"tmpfs|fuse.lxcfs|squashfs\"}",
          "interval": "",
          "legendFormat": "",
          "refId": "A"
        }
      ],
      "thresholds": [],
      "timeFrom": null,
      "timeRegions": [],
      "timeShift": null,
      "title": "Disk Space",
      "tooltip": {
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "$$hashKey": "object:824",
          "format": "mbytes",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "$$hashKey": "object:825",
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "alert": {
        "alertRuleTags": {},
        "conditions": [
          {
            "evaluator": {
              "params": [
                2
              ],
              "type": "gt"
            },
            "operator": {
              "type": "and"
            },
            "query": {
              "params": [
                "A",
                "5m",
                "now"
              ]
            },
            "reducer": {
              "params": [],
              "type": "avg"
            },
            "type": "query"
          }
        ],
        "executionErrorState": "alerting",
        "for": "5m",
        "frequency": "1m",
        "handler": 1,
        "name": "CPU idle alert",
        "noDataState": "no_data",
        "notifications": []
      },
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": null,
      "description": "",
      "fieldConfig": {
        "defaults": {
          "custom": {},
          "unit": "percent"
        },
        "overrides": []
      },
      "fill": 1,
      "fillGradient": 0,
      "gridPos": {
        "h": 9,
        "w": 12,
        "x": 12,
        "y": 8
      },
      "hiddenSeries": false,
      "id": 2,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.4.0",
      "pointradius": 2,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "100 * (1 - avg by(instance)(irate(node_cpu_seconds_total{mode=\"idle\"}[5m])))",
          "interval": "",
          "legendFormat": "",
          "refId": "A"
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": true,
          "line": true,
          "op": "gt",
          "value": 2,
          "visible": true
        }
      ],
      "timeFrom": null,
      "timeRegions": [],
      "timeShift": null,
      "title": "CPU idle",
      "tooltip": {
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "$$hashKey": "object:718",
          "format": "percent",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "$$hashKey": "object:719",
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    }
  ],
  "refresh": "5s",
  "schemaVersion": 27,
  "style": "dark",
  "tags": [],
  "templating": {
    "list": []
  },
  "time": {
    "from": "now-3h",
    "to": "now"
  },
  "timepicker": {},
  "timezone": "",
  "title": "Dash-Learninig",
  "uid": "iwXdYM87z",
  "version": 2
}

```

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
