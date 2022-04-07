### Ход выполнения ДЗ по теме "10.03. Grafana"

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

## Задание 4
Сохраните ваш Dashboard.

Для этого перейдите в настройки Dashboard, выберите в боковом меню "JSON MODEL".

Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.

В решении задания - приведите листинг этого файла.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
