## Laravel Setup With Docker

#### The below is the sequence of commands this project

* clone this repo and ```cd Laravel-docker``` and ```composer install```
* now inside Laravel-docker type ```cd laradock```
* docker-compose up -d nginx mysql redis
* docker-compose exec workspace bash (go to ````http://localhost```)
* php artisan migrate

#### If you get an error like below while executing ``php artisan migrate``

```mysql
  Illuminate\Database\QueryException  : SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client (SQL: select * from information_schema.tables where table_schema = testdocker and table_name = migrations and table_type = 'BASE TABLE')
```

#### to get rid of above error follow below steps

* cd laradock
* docker-compose exec mysql bash

#### Now here just loginto mysql using below credentials

```mysql
mysql -uroot -proot
```

#### once log into to mysql execute below queries one by one and also create database by name of ```testdocker```

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'default'@'%' IDENTIFIED WITH mysql_native_password BY 'secret';
CREATE DATABASE testdocker;
```

now go back to laradock folder and run ``docker-compose exec workspace bash`` and run ```php artisan migrate``` now it will successfully migrate everything to the database

now go to ```http://localhost```  and you'll see a default laravel page if there is not login and registration button run this command ```php artisan make:auth``` it will create the default authentication scaffolding.
in ```workspace bash``` and also run this command to see list of laravel commands and what they do  ```php artisan``` with description

#### Thanks
