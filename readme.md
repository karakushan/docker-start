# Стартовый проект для создания сервера (DOCKER)

##Пример создания хоста

```server {
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
   }```

