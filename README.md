## Описание
REST API YaMDb - база отзывов пользователей о фильмах, книгах и музыке. Здесь можно оставить отзыв о произведении и подискутировать о нем в комментариях.


# REST API YamDB
![Workflow status](https://github.com/yonvik/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg) 

## Стек технологий

При разработке использован следующий стек технологий:

* Python 3.7
* Django 2.2.16
* Django Rest Framework
* Simple-GWT
* PostgreSQL
* Docker
* nginx
* Yandex.Cloud

### Подготовка репозитория
1. Клонируйте репозиторий на локальную машину командой:
 ```
 git clone git@github.com:yonvik/yamdb_final.git
 ```
2. В вашем репозитории на гитхаб в  ```Settings - Secrets - Actions``` добавьте ключи
> DOCKER_USERNAME - имя пользователя docker;  
> DOCKER_PASSWORD - пароль docker;  
> HOST - ip-адрес сервера;  
> USER - имя пользователя для сервера;  
> SSH_KEY - приватный ключ с компьютера, имеющего доступ к боевому серверу ``` cat ~/.ssh/id_rsa ```;  
> PASSPHRASE - пароль для сервера;  
> DB_ENGINE=django.db.backends.postgresql - указываем, что работаем с postgresql;  
> DB_NAME=postgres - имя базы данных;  
> POSTGRES_USER - логин для подключения к базе данных;  
> POSTGRES_PASSWORD - пароль для подключения к БД;  
> DB_HOST=db - название сервиса (контейнера);  
> DB_PORT=5432 - порт для подключения к БД;  
> TELEGRAM_TO - id своего телеграм-аккаунта (можно узнать у @userinfobot, команда /start);  
> TELEGRAM_TOKEN - токен бота (получить токен можно у @BotFather, /token, имя бота);
3. Измените имя пользователя DockerHub в docker-compose.yaml на ваше
   
### Подготовка сервера
- Запустите сервер и зайдите на него ``` ssh username@ip_address ```;
- Установите обновления apt:
``` sudo apt update ```;
``` sudo apt upgrade -y ```;  
- Установите nginx ``` sudo apt install nginx -y ```;
- Остановите службу nginx ``` sudo systemctl stop nginx ```;
- Установите docker ``` sudo apt install docker.io ```;
- Установите docker-compose: 
Выполните команду, чтобы загрузить текущую стабильную версию Docker Compose:  
``` sudo curl -SL https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose ```;  
Примените к файлу права доступа:  
``` sudo chmod +x /usr/local/bin/docker-compose	```;  
Проверьте установку (должна вернуться версия docker-compose):  
``` docker-compose --version ```;  
- Создайте на сервере два файла и скопируйте в них код из проекта на GitHub:  
> docker-compose.yaml в home/<username>/docker-compose.yaml  
``` sudo nano docker-compose.yaml ```  
> nginx/default.conf в home/<username>/nginx/default.conf  
``` mkdir nginx ```  
``` sudo nano nginx/default.conf ```
#### Развертывание приложения на боевом сервере
При первоначальном развертывании будут автоматически применены миграции
и загружена первоначальная база данных, если не хотите этого, закомментируйте 
команды ```sudo docker-compose exec web ...``` внутри файла yamdb_workflow.yml  
Для запуска автоматического развертывания на сервере с помощью Actions workflow 
закоммитьте изменения в docker-compose.yaml и запуште их.  
За статусом работы можно проследить на вкладке Actions на GitHub.
Для создания суперользователя введите команду:  
```
sudo docker-compose exec web python createsuperuser
```
Подробную информацию о api можно узнать по адресу:
```
ip-адрес_вашего_сервера/redoc/
```
Проект доступен по ссылкам:
```
http://130.193.37.216/api/v1/titles/
```
Автор:  
Андрей Янковский - https://github.com/yonvik
