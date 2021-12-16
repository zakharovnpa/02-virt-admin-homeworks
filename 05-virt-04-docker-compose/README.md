# "5.4. Оркестрация группой Docker контейнеров на примере Docker Compose" - Захаров Сергей Николаевич

## Задача 1

Создать собственный образ операционной системы с помощью Packer.

Для получения зачета, вам необходимо предоставить:
- Скриншот страницы, как на слайде из презентации (слайд 37).

**Ответ:**
#### 1. Создан новый образ 
![образ](/05-virt-04-docker-compose/img/new-images-in-yandex-cloud.png)
#### 2. Утилита Яндекса ` yc ` показывает доступные ресурсы
![yc-compute-image-list](/05-virt-04-docker-compose/img/yc-compute-image-list.png)

## Задача 2

Создать вашу первую виртуальную машину в Яндекс.Облаке.

Для получения зачета, вам необходимо предоставить:
- Скриншот страницы свойств созданной ВМ, как на примере ниже:


<p align="center">
  <img width="1200" height="600" src="./img/yc_01.png">
</p>

**Ответ:**
#### 1. Скриншот страницы свойств созданной ВМ
![running-node01](/05-virt-04-docker-compose/img/running-node01.png)

## Задача 3

Создать ваш первый готовый к боевой эксплуатации компонент мониторинга, состоящий из стека микросервисов.

Для получения зачета, вам необходимо предоставить:
- Скриншот работающего веб-интерфейса Grafana с текущими метриками, как на примере ниже
<p align="center">
  <img width="1200" height="600" src="./img/yc_02.png">
</p>

**Ответ:**
#### 1. Скриншот работающего веб-интерфейса Grafana с текущими метриками
![running-grafana](/05-virt-04-docker-compose/img/running-grafana.png)

![running-prometheus](/05-virt-04-docker-compose/img/running-prometheus.png)

## Задача 4 (*)

Создать вторую ВМ и подключить её к мониторингу развёрнутому на первом сервере.

Для получения зачета, вам необходимо предоставить:
- Скриншот из Grafana, на котором будут отображаться метрики добавленного вами сервера.

**Ответ:**

### 1. На первой ВМ 62.84.118.134 с  названием "node01" запущен сервис мониторинга Grafana.
### 2. Создана вторая ВМ 51.250.14.30 с названием "node02"
![settings-node02](/05-virt-04-docker-compose/img/settings-node02.png)

### 3. На второй ВМ запущены микросервисы точно такие же, как и на первой ВМ
```bash
[root@node02 stack]# docker-compose ps
    Name                  Command                  State                                                   Ports                                             
-------------------------------------------------------------------------------------------------------------------------------------------------------------
alertmanager   /bin/alertmanager --config ...   Up             9093/tcp                                                                                      
caddy          /sbin/tini -- caddy -agree ...   Up             0.0.0.0:3000->3000/tcp, 0.0.0.0:9090->9090/tcp, 0.0.0.0:9091->9091/tcp, 0.0.0.0:9093->9093/tcp
cadvisor       /usr/bin/cadvisor -logtostderr   Up (healthy)   8080/tcp                                                                                      
grafana        /run.sh                          Up             3000/tcp                                                                                      
nodeexporter   /bin/node_exporter --path. ...   Up             9100/tcp                                                                                      
prometheus     /bin/prometheus --config.f ...   Up             9090/tcp                                                                                      
pushgateway    /bin/pushgateway                 Up             9091/tcp                                                                                      
[root@node02 stack]# 
```
### 4. На первой ВМ добавили в файле ` prometheus.yml ` 
```bash
  - job_name: 'nodeexporter-2'
    scrape_interval: 5s
    static_configs:
      - targets: ['51.250.14.30:9100']

  - job_name: 'cadvisor-2'
    scrape_interval: 5s
    static_configs:
      - targets: ['51.250.14.30:8080']

```
### 5. Добавлен на мониторинг новый источник данных от второй ВМ
![Configuration-grafana](/05-virt-04-docker-compose/img/Configuration-grafana.png)
### 6. Создан дашборд для второй ВМ 
![dashboard-node02](/05-virt-04-docker-compose/img/dashboard-node02.png)
### 7. Состояние дашборда второй ВМ при ее перезагрузке
![reload-node02](/05-virt-04-docker-compose/img/reload-node02.png)
### 8. Состояние дашборда второй ВМ после ее перезагрузки
![after-reload-node02](/05-virt-04-docker-compose/img/after-reload-node02.png)
