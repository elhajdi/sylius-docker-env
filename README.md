
Easy Environment where you can 

# Run with docker compose
Run this command to build image and run containers.
```
docker compose up -d --build
```

# install your poject 
clone your project inside the web folder
*or you can clone sylius from github repositoyr* 1.11 is the sable one
```
cd web
git clone -b 1.11 git@github.com:Sylius/Sylius-Standard.git

```

## Configure your database first 
- create database on http://localhost:8888?server=mysql&username=db_&db=db_db
- modify **DATABASE_URL** within **.env** in your project with *DATABASE_URL=mysql://[root]:[thepassword]@mysql/[database_name]*


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

open http://localhost:9900/admin