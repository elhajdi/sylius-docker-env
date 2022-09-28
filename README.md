
Docker Environment where you can run and work easilly on Sylius project

# Run with docker compose
Run this command to build image and run containers.
```
docker compose up -d --build
```
# Configure vhosts
Add your [domain] to /etc/hosts
Create a virtual hosts file in this directory *.docker/nginx/vhosts*
Sample example below :
```
server {
    listen 80;
    server_name [domain];

    root  /var/www/html/[project_name];
    index index.php;

    access_log /var/log/nginx/[project_name]-access.log;
    error_log /var/log/nginx/[project_name]-error.log info;

    location / {
    	proxy_pass http://localhost:8000
    }
    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass sylius:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        #fastcgi_pass_header Authorization;
    }
}
```
# install your poject 
clone your project inside the web folder
*or you can clone sylius from github repositoyr* 1.11 is the sable one
```
cd web
git clone -b 1.11 git@github.com:Sylius/Sylius-Standard.git

```

## Configure your database first 
- create database on http://localhost:8888?server=mysql&username=sylius_du&db=sylius_db
- modify **DATABASE_URL** within **.env** in your project with :
  - *DATABASE_URL=mysql://[sylius_du]:[thesecret]@mysql/[sylius_db]*



# Working on sylius project

```
docker compose exec sylius bash
cd [your_project_name_inside_web]
composer install
bin/console sylius:install
yarn install
yarn build
symfony serve
```
# You access to your project using 
- Admin: *http://localhost:9900/admin*, FRONT:*http://localhost:9900*
- Admin: *http://[domain]/admin*, FRONT:*http://[domain]:9900*


