# 10.02. Системы мониторинга


## 1. Опишите основные плюсы и минусы pull и push систем мониторинга.

  - Push-системы    
     Достоинства   
     - все централизовано, поэтому очень легко вносить глобальные изменения. Легко добавлять или удалять новые метрики
     - позволяют создавать четко определенные графики, карты и оповещения, поскольку все данные, типы, единицы измерения и т. д. известны заранее и определяются администраторами систем    
     Недостатки     
     - не гибкая система, периодически экспортируется предварительно определенный фиксированный набор метрик.
     - сложнее контролировать подлинность данных
  - Pull-системы
     Достоинства   
     - обновления накатываются изнутри, внешний клиент не может внести изменения
     - Pull-инструменты могут быть распределены по разным пространствам имен с разными репозиториями Git и правами доступа. Можно применять multitenant-модель. То есть, каждая команда использует свое пространствот имен, а определенная команда может использоват глобальное пространство.
     - метрики собираются из одного места
     - секреты могут храниться в зашифрованном виде в репозитории Git и извлекаться внутри кластера
     - можно запросить любую метрику в любое время
     Недостатки    
     -протокол опроса потенциально может открыть систему для удаленного доступа и атак типа «отказ в обслуживании».     


## 2. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?
##    - Prometheus
##    - TICK
##    - Zabbix
##    - VictoriaMetrics
##    - Nagios

  Prometheus - преимущественно Pull, в редких случаях используется Pushgateway     
  TICK - собирает метрики, значит относится к Push модели, но может получать данные от Kapasitor по Pull модели     
  Zabbix - гибридная, поддерживает и Push и Pull модель. Чаще используется в режиме  Push.    
  VictoriaMetrics - гибридная    
  Nagios - относится к Pull модели    

## 3. Склонируйте себе репозиторий и запустите TICK-стэк, используя технологии docker и docker-compose.

   Вывод curl http://localhost:8086/ping
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
< Request-Id: 70c53e2a-c959-11ec-8118-0242ac170002
< X-Influxdb-Build: OSS
< X-Influxdb-Version: 1.8.10
< X-Request-Id: 70c53e2a-c959-11ec-8118-0242ac170002
< Date: Sun, 01 May 2022 14:17:32 GMT
<
* Connection #0 to host localhost left intact
```

  Вывод curl http://localhost:8888
```
*   Trying ::1:8888...
* TCP_NODELAY set
* Connected to localhost (::1) port 8888 (#0)
> GET / HTTP/1.1
> Host: localhost:8888
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
< Date: Sun, 01 May 2022 14:19:08 GMT
<
* Connection #0 to host localhost left intact
<!DOCTYPE html><html><head><meta http-equiv="Content-type" content="text/html; charset=utf-8"><title>Chronograf</title><link rel="icon shortcut" href="/favicon.fa749080.ico"><link rel="stylesheet" href="/src.9cea3e4e.css"></head><body> <div id="react-root" data-basepath=""></div> <script src="/src.a969287c.js"></script> </body></html>
```

  Вывод curl http://localhost:9092/kapacitor/v1/ping
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
< Request-Id: c3a7579e-c959-11ec-813d-000000000000
< X-Kapacitor-Version: 1.6.4
< Date: Sun, 01 May 2022 14:19:51 GMT
<
* Connection #0 to host localhost left intact
```

  [Скриншот веб-интерфейса ПО chronograf](https://github.com/chuckberry321/netology-10-monitoring-02-systems/blob/main/screenshots/screenshot_chronograf.png)

## 4. Для выполнения задания приведите скриншот с отображением метрик утилизации места на диске (disk->host->telegraf_container_id) из веб-интерфейса.

  [Скриншот с отображением метрик утилизации места на диске](https://github.com/chuckberry321/netology-10-monitoring-02-systems/blob/main/screenshots/disk_metric.png)

## 5. После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список measurments в веб-интерфейсе базы telegraf.autogen.

  [Скриншот списка measurments](https://github.com/chuckberry321/netology-10-monitoring-02-systems/blob/main/screenshots/docker_metrics.png)
