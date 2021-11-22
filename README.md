# Project Setup

### versions
```
- PHP:  7.4.22 
- Nginx: 1.18.0
- Mysql: 8.0.26
```

## FOR LINUX/MAC ENVIRONMENT

#### create the project
```
1. $ git clone this repository
2. $ cd project
```

#### setting up the project
```
1. $ cp .env.template .env
2. $ cd backend
3. $ ls -la                               [to check the current files / folders existing inside the ./backend folder]
4. $ sudo rm -rf your_file_or_folder_name [to delete your file/folder]
5. $ cd ..                                [return to the main folder]
5. $ make create-project
6. Edit db info and app_url inside the ./backend/.env file


APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=kredo
DB_USERNAME=kredo
DB_PASSWORD=password

6. $ docker-compose exec app php artisan migrate
```


### check browser
```
web server:     http://localhost/
php my admin:   http://localhost:8888/
```

### executables
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

# seeding the database
$ docker-compose exec app php artisan db:seed
```



## FOR WINDOWS ENVIRONMENT
### MAKE SURE TO EXECUTE THE COMMANDS UNDER GIT BASH TERMINAL. IF YOU DON'T HAVE GIT BASH IN YOUR SYSTEM, KINDLY REFER TO THIS LINK
```
1. https://git-scm.com/downloads 
2. Select the installer for windows
```
### installation

```
1. git clone this repository
2. cd project
```

#### Prioritize this change. Copy the line of code below and change the infra/mysql/Dockerfile code
```
FROM mysql:8.0.26

COPY ./my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf
```

#### create a project
```
1. mkdir -p ./docker/php/bash/psysh
2. touch ./docker/php/bash/.bash_history
3. cp .env.template .env
4. [unhide ALL FILES AND FOLDERS inside the ./backend and delete it manually]
5. winpty docker-compose up --build -d
6. winpty docker-compose exec app composer create-project --prefer-dist laravel/laravel . "8.*"
```
### project setup
```
1. cp backend/.env.example backend/.env
2. winpty docker-compose exec app composer install
3. winpty docker-compose exec app php artisan key:generate

# modify this to your ./backend/.env file 
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=kredo
DB_USERNAME=kredo
DB_PASSWORD=password


4. winpty docker-compose exec app php artisan config:cache
5. winpty docker-compose exec app php artisan storage:link
6. winpty docker-compose exec app chown www-data storage/ -R
7. winpty docker-compose exec app php artisan migrate
```

#### executables

```
# up default container
winpty docker-compose up -d

# build no cache and force remake container
winpty docker-compose build --no-cache --force-rm

# check container
winpty docker ps

# stop container
winpty docker-compose stop

# remove container
winpty docker-compose down

# remove all of container stuff
winpty docker-compose down --rmi all --volumes

# log for laravel
winpty docker-compose logs

# seeding the database
winpty docker-compose exec app php artisan db:seed
```


## FYI
#### laravel storage log errors  / laravel storage permission
```
# [LINUX/MAC]
$ docker-compose exec app chown www-data storage/ -R
$ docker-compose exec app chmod -R 777 storage/

------------------

# [WINDOWS]
winpty docker-compose exec app chown www-data storage/ -R
winpty docker-compose exec app chmod -R 777 storage/
```
