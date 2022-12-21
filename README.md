# Docker LEMP (Linux, NGINX, MySQL, PHP)

## Налаштування

### Створення локального сайту

1. У теці sites створюємо теку, наприклад `mysite` (сам сайт можна вказати типу _mysite.loc_)
2. У теці `config/nginx` створюємо конфіг для нашого сайту, наприклад _mysite.conf_
3. За прикладом конфігу hello.conf у нашому конфігу замінюємо `server_name hello.loc;` та `root /var/www/hello;` на новий сайт
4. Логін для бази даних _root_. Пароль: _secret_. Змінити пароль можна у файлі `docker-compose.yml` в налаштуваннях `MYSQL_ROOT_PASSWORD`
4. У хості додаємо наш сайт, наприклад:
```
127.0.0.1 mysite.loc
```

### Запуск Docker-контейнера

1. Запускаємо команду (збірка без використання кешу)
```
docker-compose build --no-cache
```
2. Далі запускаємо сам контейнер 
```
docker-compose up -d
```

## Перебудова Docker-контейнера

1. Зупинка Docker контейнера (видалення контейнерів)
```
docker-compose down
```
2. Видалення даних Docker
```
docker system prune -a
docker image prune
docker volume prune
```
5. Rebuild without using cache 
```
docker-compose build --no-cache
```
6. Start Container 
```
docker-compose up -d
```
