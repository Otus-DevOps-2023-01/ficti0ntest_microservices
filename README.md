[![Test Actions Status](https://github.com/Otus-DevOps-2023-01/ficti0ntest_microservices/workflows/Run%20tests%20for%20OTUS%20homework/badge.svg)](https://github.com/Otus-DevOps-2023-01/ficti0ntest_microservices/actions)
# ficti0ntest_microservices
ficti0ntest microservices repository

##  Docker образы. Микросервисы
1. Разделяем наше приложение на несколько контейнеров
```bash
docker build -t ficti0n/post:1.0 ./post-py
docker build -t ficti0n/comment:1.0 ./comment
docker build -t ficti0n/ui:1.0 ./ui
```
2. Запускаем приложение с помощью созданных контейнеров
```bash
docker network create reddit

docker run -d --network=reddit \
--network-alias=post_db --network-alias=comment_db mongo:latest

docker run -d --network=reddit \
--network-alias=post ficti0n/post:1.0

docker run -d --network=reddit \
--network-alias=comment ficti0n/comment:1.0

docker run -d --network=reddit \
-p 9292:9292 ficti0n/ui:1.0
```
3. Оптимизируем наше приложение
4. Используем volume для сохранения данных в mongodb
```bash
docker volume create reddit_db

docker run -d --network=reddit --network-alias=post_db \
--network-alias=comment_db -v reddit_db:/data/db mongo:latest
...

```

## Docker контейнеры. Docker под капотом
1. Установили docker, docker-compose, docker-machine (у меня все стояло уже)
2. Создали свой образ
3. Создали docker host
4. Зарегистрировались на Docker Hub
5. Загрузили образ в публичное хранилище
6. Выполнили различные проверки, использовали команды из ДЗ для мзучения контейнера
