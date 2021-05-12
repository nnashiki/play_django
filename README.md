# play_django
play django




# DB
- MySQLのチュートリアルから作成した
    - https://www.mysqltutorial.org/mysql-sample-database.aspx

- init db

```
docker run --rm --name djungomysql \
    --rm \
    -e MYSQL_ROOT_PASSWORD=mydb_pass \
    -e MYSQL_USER=mydb_user \
    -e MYSQL_PASSWORD=mydb_pass \
    -e MYSQL_DATABASE=mydb \
    -v `pwd`/mysql/db_init:/docker-entrypoint-initdb.d \
    -v `pwd`/mysql/cnf:/etc/mysql/conf.d \
    -p 3306:3306 mysql:8.0 
```

use db

```
$ mysql -u root -p -h 127.0.0.1 mydb
mysql> show databases;
mysql> 
```

`python manage.py dbshell`


# init 

- `django-admin startproject mysite`
  - https://docs.djangoproject.com/ja/3.2/intro/tutorial01/
- モデルを table 定義から出力する
  - `python manage.py inspectdb > mysite/model.py`
  - https://docs.djangoproject.com/en/2.2/ref/settings/#databases
  - https://docs.djangoproject.com/en/3.2/howto/legacy-databases/
- `INSTALLED_APPS` に アプリ(pythonモジュール) 追加する
