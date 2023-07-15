# DOCKER_NETWORK из двух контейнеров: бэкенд php, фронтенд React

## Давайте создадим сеть с именем project_network
```
docker network create project_network
```
## посмотреть
```
docker network inspect project_network
```
## И как говорилось выше, это сеть без контейнеров и мы можем пойти дальше и добавить запущенные контейнеры в эту сеть, используя следующие команды:
```
docker network connect project_network DOСKER_NAMES_1
docker network connect project_network DOСKER_NAMES_2
```

## добавить в реакт внешний ссылки (http://DOSKER_NAMES_1/api-web по названию проходит но картинки не идут, но картинки проходят по ip?! т.е. ip - бэкенда необходим)
```
NEXT_PUBLIC_WEB_API_URL=http://172.31.0.2/api-web
SSR_WEB_API_URL=http://172.31.0.2/api-web
```

## И как было сказано выше, контейнеры могут взаимодействовать друг с другом используя имя контейнера или IPv4 адрес.

## Запуск - войти нужно в директорию в которой Docker
```
docker-compose up -d # запуск сервера
docker-compose up -d --build  # запуск с обновлением и т.д.
docker-compose up -d --force-recreate # запуск с востановлением сети
docker-compose stop  # остановка сервера
docker ps  # посмотреть процессы на сервере 
```

## убрать конфликты и т.д.
```
docker network ls
docker-compose down
docker network prune
```

## работа с базой данных создание новой базы и т.д.
```
docker stop $(docker ps -a -q) // остановить все докеры
docker rm $(docker ps -a -q) // удалить все докеры
docker rm 8373ded91583 ed4a0aceee8c 74d6aa22e9e1 5fddda669693
docker update --restart=no $(docker ps -a -q)  // Используйте приведенное ниже, чтобы отключить ВСЕ контейнеры с автоматическим перезапуском (демон).
docker ps  # посмотреть путь процесса CONTAINER ID для mysql
docker exec -it f7c2a16f56c9 bash
root@f7c2a16f56c9:/# mysql -u root -p bitrix
mysql> show databases;
mysql> CREATE DATABASE `my_db` CHARACTER SET utf8 COLLATE utf8_general_ci;  
mysql> DROP DATABASE `my_db`
```

## выйти из bash exit
```
// предварительно войти в php --  docker exec -it f7c2a16f56c9 bash   
docker exec -it 7a31663a0c5d bash
composer require enqueue/amqp-lib  
composer remove phpseclib/phpseclib
composer update
// посмотреть хосты
docker exec -it a4fd79ed4faa bash
cat /etc/hosts
// импорт sql через MariaDB
docker exec -i CONTAINER_ID /bin/bash -c "export TERM=xterm && mysql -proot -uroot database" < import.sql
// эскпорт с мускула в докере, спросит пароль от базы данных
sudo docker exec -i 95b673a3c483 mysqldump -u buroburo -p buroburo > buroburo_old.`date +%d.%m.%Y-%H:%M:%S`.sql
```