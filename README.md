# yamdb_final

![example workflow](https://github.com/KirillAAbramov/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

Проект yamdb_final демонстрирует методику DevOps (Development Operations) и идею CI (Continuous Integration). Методика DevOps направлена на увеличение скорости, качества и безопасности разработки. Идея CI состоит в том, чтобы после внесения изменений в любую часть кода проводилось тестирование не только того модуля, который был изменён, но и всего проекта.

Для автоматизации процессов при CI в данном проекте используется GitHub Actions. Для того, чтобы GitHub Actions начал работу, необходимо описать последовательность команд, которые должны выполняться после того, как случится какое-то событие. Такие последовательности команд называются workflow. А событие в текущем проекте - push в репозиторий GitHub.

В текущем проекте автоматизированы следующие процессы:
 - сборка, запуск, тестирование приложения;
 - деплой приложения на сервер после успешного прохождения тестов и отправки docker-образа на DockerHub;
 - отправка уведомления в телеграм об успешном выполнении workflow.

### Как развернуть приложение локально:
 - сборка контейнеров и запуск
 ```
 docker-compose up -d --build
 ``` 
 - выполнение миграции
 ```
 docker-compose exec web python manage.py migrate
 ```
 - создание суперпользователя для входа в админку и создания записей
 ```
 docker-compose exec web python manage.py createsuperuser
 ```
 - сборка статики
 ```
 docker-compose exec web python manage.py collectstatic --no-input
 ```
### Как развернуть проект на боевом сервере:
 - установка соединения с сервером
 ```
 ssh username@server_address
 ```
 - просмотр работающих контейнеров
 ```
 sudo docker container ls
 ```
 - вход в контейнер
 ```
 sudo docker exec -it yamdb_final_web_1 bash
 ```
 - выполнение миграций внутри контейнера
 ```
 python manage.py migrate
 ```
 - при необходимости возможно создать суперпользователя
 ```
 python manage.py createsuperuser
 ```

### Адрес развернутого приложения
```
http://84.201.178.73
```

### Автор
Абрамов Кирилл