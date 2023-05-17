# Домашнее задание №5.3
## Задача №1

Сценарий выполения задачи:

1) создайте свой репозиторий на https://hub.docker.com;
2) выберете любой образ, который содержит веб-сервер Nginx;
3) создайте свой fork образа;
3) реализуйте функциональность: запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:

```sh
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Решение задачи 1:
Я зарегистрировался hub.docker.com Использовать образ nginx:stable-alpine - 1.20.2 на момент выполнения.

```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker pull nginx:stable-alpine
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker images
REPOSITORY   TAG             IMAGE ID       CREATED       SIZE
nginx        stable-alpine   1266a3a46e96   4 weeks ago   41.1MB
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker build -t glisikh/nginx-nl:1.20.2 .
Sending build context to Docker daemon  3.584kB
Step 1/2 : FROM nginx:1.20.2-alpine
1.20.2-alpine: Pulling from library/nginx
8663204ce13b: Pull complete 
a1484661dfe6: Pull complete 
2f78a3560d10: Pull complete 
a517401f7a94: Pull complete 
294d17c34d13: Pull complete 
7051f5a2f4b1: Pull complete 
Digest: sha256:016789c9a2d021b2dcb5e1c724c75ab0a57cc4e8cd7aab7bb28e69fec7c8c4fc
Status: Downloaded newer image for nginx:1.20.2-alpine
 ---> 6cf0c840a5a4
Step 2/2 : COPY index.html /usr/share/nginx/html/
 ---> 378be2a95b38
Successfully built 378be2a95b38
Successfully tagged glisikh/nginx-nl:1.20.2
```
Запускаю контейнер
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker run -d -p 81:80 glisikh/nginx-nl:1.20.2 
dad4ef77013076e60202eb27f3e5df9e64ec546fc0d5fd5db600da6315ec5cee
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS          PORTS                               NAMES
dad4ef770130   glisikh/nginx-nl:1.20.2   "/docker-entrypoint.…"   23 seconds ago   Up 22 seconds   0.0.0.0:81->80/tcp, :::81->80/tcp   heuristic_brown
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker exec -it heuristic_brown sh
/ # cat /usr/share/nginx/html/index.html
<html>
    <head>Hey, this is homework№3</head>
    <body>
        <h1>Working with Docker and Docker containers</h1>
    </body>
</html>
/ # exit
```
(Текст файла html я изменил, потому что изначально не правильно прочитал условие).

Позже я переименовал образ, потому что он не хотел скачивать на мою учётную запись в DockerHub.
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3$ docker tag glisikh/nginx-nl:1.20.2 egorsolt64/nginx-nl:1.20.2
```
ссылка на docker-репозиторий: https://hub.docker.com/r/egorsolt64/nginx-nl

## Задача №2
Посмотрите на сценарий ниже и ответьте на вопрос: "Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.

Сценарий:

Высоконагруженное монолитное java веб-приложение; Лучше всего, использовать виртуальные или физические машины, docker для этого менее пригоден, т.к. типичное монолитное приложение обычно тяжеловесно, имеет боле>

Nodejs веб-приложение; Подойдет Docker, так как это - простота развертывания приложения, лёгковесность и масштабирование.

Мобильное приложение c версиями для Android и iOS; Я не очень уверен что docker является здесь целевым, есть решения для организации сборки мобильных приложений (apk, deb, ipa), если под версией имеется ввиду о>

Шина данных на базе Apache Kafka; Так как шина данных является специфическим связующим звеном, в текущих проектах мы используем физические и виртуальные сервера - в основном связано с тем что при переконфигурир>

Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana; При организации логгирования с использованием elk-стека есть несколько воп>

Мониторинг-стек на базе Prometheus и Grafana; docker, так как это - масштабируемость, лёгкость и скорость развёртывания.

MongoDB, как основное хранилище данных для java-приложения; Склоняюсь к физическим или виртуальным серверам, ввиду сложности администрирования MongoDB внутри контейнера и вероятности потери данных при потере ко>

Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry. Docker не подходит в данном случае, т.к. при потере контейнера будет сложно восстановить частоизменяемые данные. Здесь больше>

## Задача №3
Запустите первый контейнер из образа centos c любым тэгом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
Запустите второй контейнер из образа debian в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data;
Добавьте еще один файл в папку /data на хостовой машине;
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.

```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ mkdir data
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ docker run -it --rm -d --name centos -v $(pwd)/data:/data centos:latest
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
a1d0c7532777: Pull complete 
Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
Status: Downloaded newer image for centos:latest
2f943484abab08660ef2d6195e877c9a85ce0146575179dcbca6172ab7b2649b
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ docker run -it --rm -d --name debian -v $(pwd)/data:/data debian:latest
Unable to find image 'debian:latest' locally
latest: Pulling from library/debian
918547b94326: Pull complete 
Digest: sha256:63d62ae233b588d6b426b7b072d79d1306bfd02a72bff1fc045b8511cc89ee09
Status: Downloaded newer image for debian:latest
891bc7bcef6ba7e20615d2c31719ac3cbab3ae227fab8d73ef45be3b36faec75
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ echo "Это хостовая машина" >> data/host.txt
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ docker exec -it centos bash
[root@2f943484abab /]# echo "Это машина CentOS" > /data/centos.txtentos.txt
[root@2f943484abab /]# echo "Это машина CentOS" > /data/centos.txt
[root@2f943484abab /]# cat /data/centos.txt 
Это машина CentOS
[root@2f943484abab /]# exit
exit
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.3/Задание3$ docker exec -it debian bash
root@891bc7bcef6b:/# ls data/
centos.txt  host.txt
root@891bc7bcef6b:/# exit
```
