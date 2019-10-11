# Java spring prometheus grafana sandbox

Песочница для java spring prometheus grafana

## Конфигурация и запуск

1. Необходимо подключить в build.gradle необхдоимые библиотеки

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-actuator'

    compile 'io.micrometer:micrometer-core'
    compile 'io.micrometer:micrometer-registry-prometheus:1.1.4'
    compile 'org.springframework.metrics:spring-metrics:latest.release'
    compile 'io.prometheus:simpleclient_common:latest.release'
}
```

2. Настроить application.properties 

```properties
management.endpoints.web.exposure.include=prometheus
management.endpoint.metrics.enabled=true
management.endpoint.prometheus.enabled=true
management.metrics.export.prometheus.enabled=true

```

3. Запустить `docker-compose up -d` будут запущены 2 контейнера с prometheus и grafana. 
Prometheus будет смотреть в actuator приложения и загружать данные в зависимости от настроек в etc/prometheus.yml
Детальней с настройкой prometheus можно ознакомиться на [официальном сайте](https://prometheus.io/docs/prometheus/latest/configuration/configuration)

4. По умолчанию приложения находятся на портах:

    * 8090 - основное приложение вместе с actuator
    * 9090 - prometheus
    * 3000 - grafana
    
5. Что бы зайти в grafana необходимо перейти в [localhost:3000](localhost:3000) и настроить подключение в качестве хоста указать [sandbox-prometheus:9090](sandbox-prometheus:9090) 
Если вы изменили название контейнеров то нужно укзывать другое имя контейнера или хоста машины

6. Сохраняете и настраивайте dashboarad в grafana 

## Прочее

По умолчанию actuator для prometheus находится по адресу [http://localhost:8090/actuator/prometheus](http://localhost:8090/actuator/prometheus)
Список актуаторов доступен здесь [http://localhost:8090/actuator](http://localhost:8090/actuator) их можно конфигурировать в application.properties
В prometheus можно передавать кастомные метрики


