# Стартовый проект для создания сервера (DOCKER)

Этот проект содержит самое необходимое для старта любого проекта на php.
* PHP-FPM 7.4
* MYSQL 5.7 
* NGINX - latest

Для создания и управления базой также включен образ adminer. 
Доступ к нему можно получить указав порт 8080 к хосту.

В images/php/Dockerfile вы можете менять необходимые расширения для PHP, но после не забудьте пересобрать Docker.
В images/php/php.ini вы можете настроить конфигурация PHP по своему усмотрению.

## Пример создания хоста

В папке hosts необходимо создать файл *.conf примерно такого содержания: 

```
server {
       listen 80;
       index index.php;
       server_name mysli.localhost;
       error_log  /var/log/nginx/error.log;
       access_log /var/log/nginx/access.log;
       root /var/www/mysli.localhost/public/;
   
       location ~ \.php$ {
           try_files $uri =404;
           fastcgi_split_path_info ^(.+\.php)(/.+)$;
           fastcgi_pass php:9000;
           fastcgi_index index.php;
           include fastcgi_params;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           fastcgi_param PATH_INFO $fastcgi_path_info;
       }
   
       location / {
               try_files $uri $uri/ /index.php?$query_string;
               gzip_static on;
           }
}
```

Желаю всем успешного использования!



