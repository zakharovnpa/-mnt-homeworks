## Дополнительное задание (со звездочкой*) - необязательно к выполнению

#### Пояснения:
1. Написать на Python, 

2. Для того, чтобы увидеть как собирать кастомные метрики, можно curl запустить на Prometeus.

[Prometeus + PushGateway + curl](https://prometheus.io/docs/practices/pushing/) 
[Пример](https://github.com/prometheus/pushgateway#command-line)

3. Самый простой способ как можно собирать кастомные метрики: Grep лога Ngnix, потом отправлять на curl, потом curl пушить PushGateway
4. или Zabbix Agent
5. или создать грепалку

### 1.
Вы устроились на работу в стартап. На данный момент у вас нет возможности развернуть полноценную систему 
мониторинга, и вы решили самостоятельно написать простой python3-скрипт для сбора основных метрик сервера. 

Вы, как опытный системный администратор, знаете, что системная информация сервера лежит в директории `/proc`. 

Также, вы знаете, что в системе Linux есть  планировщик задач cron, который может запускать задачи по расписанию.

* Суммировав все, вы спроектировали приложение, которое:
  - является python3 скриптом
  - собирает метрики из папки `/proc`
  - складывает метрики в файл 'YY-MM-DD-awesome-monitoring.log' в директорию /var/log (YY - год, MM - месяц, DD - день)
  - каждый сбор метрик складывается в виде json-строки, в виде:
    + timestamp (временная метка, int, unixtimestamp)
    + metric_1 (метрика 1)
    + metric_2 (метрика 2)
  
     ...
     
    + metric_N (метрика N)
  
  - сбор метрик происходит каждую 1 минуту по cron-расписанию

### 2.
Для успешного выполнения задания нужно привести:
  - работающий код python3-скрипта, или грепалка
  - конфигурацию cron-расписания,
  - пример верно сформированного 'YY-MM-DD-awesome-monitoring.log', имеющий не менее 5 записей,

P.S.: количество собираемых метрик должно быть не менее 4-х.
P.P.S.: по желанию можно себя не ограничивать только сбором метрик из `/proc`.

**Ответ:**

[ДЗ на Python](https://github.com/zakharovnpa/01-devops-admin-homeworks/tree/main/04-script-02-py)

### Основные метрики сервера

1. Системная информация сервера лежит в директории `/proc`
2. Состав метрик:

|Директория|Файл|Метрика|Примечание|
|-|-|-|-|
|/proc|meminfo|MemFree|Размер свободной память|
|/proc|meminfo|SwapFree|Размер свободного раздела Swap|
|/proc|meminfo|MemAvailable|Размер доступной памяти|
|/proc|stat|cpu||
|/proc|stat|processes||
|/proc|vmstat|nr_free_pages||
|/proc|zoneinfo|||
|/proc|uptime||Время работы системы|
|/proc|loadavg||Средняя нагрузка на систему
|/proc|diskstats|sda5|Статистика ввода и вывода HDD


### Создаем скрипт на Python


```py
#!/usr/bin/env python3
#  /home/maestro/PycharmProjects/learning-python/venv/bin/python /home/maestro/PycharmProjects/learning-python/my-script-2.py

# Скрипт чтения содержимого файлов в локальной директории /proc

# Импортируем модуль
import os
import datetime


bashCommand = ["cd /proc", "cat stat", "cat meminfo", "cat loadavg", "cat vmstat", "cat diskstats"]  # переменной `bashCommand` присваиваем масив команд, выполняемые в целевой
# директории

result_os = os.popen(' && '.join(bashCommand)).read()			# переменной `result_os` присвоиваем результаты выполнения функции `os.popen`
# print(result_os)

for result in result_os.split('\n'):		# для каждого элемента из результата `result_os` применить метод split и выполнить разделение построчно

    if result.find('MemFree') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\tMemFree:   ', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('MemAvailable') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\tMemAvailable:   ', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('cpu ') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\tcpu :   ', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('0.') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\t:0.', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('1.') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\t:1.', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('nr_free_p') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\t:nr_free_p', '')
        print(prepare_result)  # вывести результат на экран
    elif result.find('sda5') != -1:  # условие, если результаты вывода команд соответствуют значению поиска
        prepare_result = result.replace('\t:sda5', '')
        print(prepare_result)  # вывести результат на экран

# Результат: идет сбор данных
cpu  1394898 1062 313401 19509245 17768 0 69307 0 0 0
MemFree:         4716636 kB
MemAvailable:    8465480 kB
0.44 0.36 0.36 2/1648 37568
nr_free_pages 1179159
   8       5 sda5 55096 18314 5219622 41736 499493 404351 110318330 983550 0 446736 1025287 0 0 0 0 0 0


#  Продолжение следует. 
# Необходимо создать вторую часть - для сбора данных в файл .json


```
### Необходимо создать вторую часть - для сбора данных в файл .json

Json - это словарь. Состоит из даных формата Key: Value

```py




```
```py
# Блоки сборки  результатов проверок в файлы

# Образец:
# json
#   with open(fpath+host+'.json', 'w') as jsf:
#        json_data = json.dumps({host:ip})
#        jsf.write(json_data)
#	

# Рабочий вариант:
with open("logs.json", 'w') as jsf:
# with open("logs.json", 'a') as jsf:
    json_data= json.dumps(prepare_result_1, indent=0)
    jsf.write(json_data)
with open("logs.json", 'w') as jsf:
# with open("logs.json", 'a') as jsf:
    json_data= json.dumps(prepare_result_2, indent=0)
    jsf.write(json_data)
	
	
```
### Готовый рабочий Script

* Расписание запуска скрипта в crontab

```
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# vim start-cron-log-script.sh
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# 
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# 
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# crontab -u root start-cron-log-script.sh 
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# 
root@PC-Ubuntu:~/PycharmProjects/python-lesson-10.1# crontab -l
* * * * * /root/PycharmProjects/python-lesson-10.1/./my-log-script.py
```

```py
#!/usr/bin/env python3

# Скрипт сбора логов на основе метрик из локальной директории /proc

# Импортируем модуль
import os
import json
import datetime

# Директория для складывания логов
flog = "/var/log/"

bashCommand = ["cd /proc", "cat stat", "cat meminfo", "cat loadavg", "cat vmstat", "cat diskstats"]
result_os = os.popen(' && '.join(bashCommand)).read()
for result in result_os.split('\n'):
    if result.find('MemFree') != -1:
        prepare_result_1 = result.replace('', '')
        print(prepare_result_1[18:-2])
    elif result.find('MemAvailable') != -1:
        prepare_result_2 = result.replace('', '')
        print(prepare_result_2[17:-2])  # вывести результат на экран
    elif result.find('cpu ') != -1:
        prepare_result_3 = result.replace('', '')
        print(prepare_result_3[5:-41])  # вывести результат на экран
    elif result.find('0.') != -1:
        prepare_result_4 = result.replace('', '')
        print(prepare_result_4[:-12])  # вывести результат на экран
    elif result.find('1.') != -1:
        prepare_result_4 = result.replace('', '')
        print(prepare_result_4[:-12])  # вывести результат на экран
    elif result.find('nr_free_p') != -1:
        prepare_result_6 = result.replace('', '')
        print(prepare_result_6[14:])  # вывести результат на экран
    elif result.find('sda5') != -1:
        prepare_result_7 = result.replace('', '')
        print(prepare_result_7[18:-80])  # вывести результат на экран

# Фиксируем время сбора логов:
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'w') as jsf:
    json_data = json.dumps({'Date': str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M"))}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику MemFree
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'MemFree, kB':prepare_result_1[18:-2]}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику MemAvailable
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'MemAvailable, kB':prepare_result_2[17:-2]}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику cpu
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'CPU, %':prepare_result_3[5:-41]}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику avgCPU
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'avgCPU, %':prepare_result_4[:-12]}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику avgCPU 0.99-1.99
# with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
#     json_data = json.dumps({'avgCPU, %':prepare_result_5[:-12]}, indent=2)
#     jsf.write(json_data)
# Фиксируем метрику nr_free_p
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'nr_free_p':prepare_result_6[14:]}, indent=2)
    jsf.write(json_data)
# Фиксируем метрику HDD sda5
with open(flog + str(datetime.datetime.now().strftime("%Y-%m-%d--%H:%M")) + '-awesome-monitoring.log', 'a') as jsf:
    json_data = json.dumps({'HDD sda5':prepare_result_7[18:-80]}, indent=2)
    jsf.write(json_data)

```

* Разработка скрипта для сбора метрик из директории логов ОС Ubuntu 20.04
```py
#!/usr/bin/env python3

# Скрипт проверки измененных файлов в локальной директории

# Импортируем модуль
import os
    
bashCommand = ["cd ~/netology-project/virt-homeworks-1", "git status"]	# переменной `bashCommand` присваиваем масив команд, выполняемые в целевой
									# директории
									
									
result_os = os.popen(' && '.join(bashCommand)).read()			# переменной `result_os` присвоиваем результаты выполнения функции `os.popen`
								# 

for result in result_os.split('\n'):		# для каждого элемента из результата `result_os` применить метод split и выполнить разделение построчно


    if result.find('изменено') != -1:		# условие, если результаты вывода команд соответствуют значению поиска
    
#is_change = False	#удалили неработающую переменную

        prepare_result = result.replace('\tизменено:   ', '')	# перезаписать с добавлением знаков
        prepare_result = result.replace('\tизменено:', '/root/netology-project/virt-homeworks-1/')  #внесли путь до директории
        prepare_result = prepare_result.replace(' ', '')	#удаляем лишние пробелы
        print(prepare_result)					# вывести результат на экран
	
# break		#удалили останавливающую цикл команду

# The END

```



```py
#!/usr/bin/env python3

# Ранее это был скрипт для фиксации момента изменения IP адреса сервиса. Из него будем делать
# Скрипт для сбора метрик из директории логов ОС Ubuntu 20.04

# Алгоритм работы скрипта:
# 1. собирать метрики из папки `/proc`
#	1.1 - определить какие метрики собираем
#	1.2 - указать абсолютный путь до директории с метриками
#	1.3 - написать код для открытия файлов с метриками на чтение с указанием пути
#	1.4 - для каждой метрики присвоить переменную
#	1.5 - переменная для даты YY-MM-DD
#	1.6 - открыть файл
	1.7 - считать с него построчно
	1.8 - строки определенным образом обрабатывать для образования json-строки


# 2. складывает метрики в файл 'YY-MM-DD-awesome-monitoring.log' в директорию /var/log (YY - год, MM - месяц, DD - день)
#	2.1 - создать файл YY-MM-DD-awesome-monitoring.log. Создается файл автоматически при `with open(name_file) as f:`
#  	2.2 - открыть файл для дозаписи 
#		with open('YY-MM-DD-awesome-monitoring.log', 'a') as logfile:
#		  data = logfile.read()
#
# 3. каждый сбор метрик складывается в виде json-строки, в виде:
    + timestamp (временная метка, int, unixtimestamp)
    + metric_1 (метрика 1)
    + metric_2 (метрика 2)
  
     ...
     
    + metric_N (метрика N)
# 
# 

# Импортируем модули
import socket 
import time
import datetime
import json
import yaml
import os - ?
import time

fpath = "/root/scripts/Lesson-4.3/test3/" # путь к файлам

# Переменные с актуальными IP адресами сервисов на момент начала проверки
f = socket.gethostbyname('google.com')
g = socket.gethostbyname('drive.google.com')
h = socket.gethostbyname('mail.google.com')

# Массив для вывода результатов на экран
#server = ['     - google.com - '+f, '     - mail.google.com - '+h, '     - drive.google.com - '+g]

#Блок вывода результатов на экран
print('---       Внимание! Работает скрипт, определяющий актуальные IP адреса сервисов')
print('---       Результаты находятся здесь: /root/scripts/Lesson-4.3/test3/')
print('---       Для остановки скрипта и выхода нажмите Ctrl+C')
#print('---    Актуальные сейчас IP адреса сервисов:')
#print(server[0])
#print(server[1])
#print(server[2])
#print('Смены IP адресов:')
#print('---       Внимание! Работает скрипт, определяющий актуальные IP адреса сервисов')
#print('---       Результаты сохраняются в файлах')

# Массив для работы в цикле проверок
service = {'google.com':f, 'mail.google.com':h, 'drive.google.com':g}

# Переменные для работы цикла
i = 1              # Начальное значение переменной
waiting = 2        # интервал запуска тестов в секундах
init=0             # Значение для сброса счетчика итераций

#Блок цикла
while True:                    # бесконечное число проверок 
  for host in service:          # условие для каждого элемента (host )в массиве (service) 
    ip = socket.gethostbyname(host)     # получение ip адреса по имени хоста
    if ip != service[host]:    # сравнение полученного на предыдущем шаге ip адреса с адресом на начало проверки 
      if i==1 and init !=1:    # проверка условий для счетчиков

        # Строка, формирующая таблицу значений результатов проверок
        print(str(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")) +' [ERROR] ' + str(host) +' IP mistmatch: '+service[host]+' '+ip)


# Блоки сборки  результатов проверок в файлы
# json
    with open(fpath+host+'.json', 'w') as jsf:
        json_data = json.dumps({host:ip})
        jsf.write(json_data)

# yaml
    with open(fpath+host+".yaml",'w') as ymf:
        yaml_data= yaml.dump([{host:ip}])
        ymf.write(yaml_data)

    service[host]=ip    # запись нового полученного ip адреса в массив

  time.sleep(waiting)     # таймер паузы в проверках

# The END




```

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
