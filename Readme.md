## Laravel Setup With Docker

#### The below in the sequence of commands this project

* cd projectname and composer install
* cd laradock
* docker-compose up -d nginx mysql redis
* docker-compose exec workspace bash
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

#### once loginto to mysql execute below queries one by one

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';
ALTER USER 'default'@'%' IDENTIFIED WITH mysql_native_password BY 'secret';
```

now go back to ``docker-compose exec workspace bash`` and run ```php artisan migrate``` now it will successfully migrate everything to the database
