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