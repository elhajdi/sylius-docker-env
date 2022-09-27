# install your poject 
clone your project inside the web folder
*or you can clone sylius from github repositoyr* 1.11 is the sable one
```
cd web
git clone -b 1.11 git@github.com:Sylius/Sylius-Standard.git

```

# Run with docker compose

```
docker compose up -d --build
```

# Working on sylius project

```
docker compose exec sylius bash
cd [your_project_name_inside_web]
```
## Configure your database first 
- create database on http://localhost:8888?server=mysql&username=db_&db=db_db
- modify **DATABASE_URL** within **.env** in your project with *DATABASE_URL=mysql://[root]:[thepassword]@mysql/[database_name]*

