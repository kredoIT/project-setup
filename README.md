# Project Setup

### versions
```
- PHP:  7.4.22 
- Nginx: 1.18.0
- Mysql: 8.0.26
```

### Create Laravel Docker Project Setup
#### make sure that all files inside the ./backend folder is empty
```


1. $ git clone this repository
2. $ cd project

3. $ cp .env.template .env
4. $ make create-project
5. $ make init
6. edit db info and app_url on backend/.env file

APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=kredo
DB_USERNAME=kredo
DB_PASSWORD=password

7. $ docker-compose exec app php artisan migrate
```


### check browswer
```
web server:     http://localhost/
php my admin:   http://localhost:8888/
```

### usage
```
# up default container
$ docker-compose up -d

# build no cache and force remake container
$ docker-compose build --no-cache --force-rm

# check container
$ docker ps

# stop container
$ docker-compose stop

# remove container
$ docker-compose down

# remove all of container stuff
# docker-compose down --rmi all --volumes

# log for laravel
$ docker-compose logs
```


### FYI
#### create laravel project inside backend folder
```

# laravel 8
$ make create-project

# laravel storage log errors  / laravel storage permission
$ docker-compose exec app chown www-data storage/ -R
$ docker-compose exec app chmod -R 777 storage/
```

#### when using windows, copy the line of code below and change the infra/mysql/Dockerfile
```
FROM mysql:8.0.26

COPY ./my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf
```
