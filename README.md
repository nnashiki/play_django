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
- 出力した model の class Meta を削除する
  - 削除しないと Migrate ができない
- `INSTALLED_APPS` に アプリ(pythonモジュール) 追加する
  - https://docs.djangoproject.com/ja/3.2/intro/tutorial02/#activating-models
- mirgarion ファイルを作成する
  - `python manage.py makemigrations polls`
  - https://docs.djangoproject.com/ja/3.2/intro/tutorial02/#activating-models
- mirgarion の確認をする
  - `python manage.py sqlmigrate polls 0001`
- migration を実行する
  - `python manage.py migrate`

# modelの修正
- model に変更を加える
- mirgarion ファイルを作成する
  - `python manage.py makemigrations polls`
- mirgarion の確認をする
  - `python manage.py sqlmigrate polls 0002`
- migration を実行する
  - `python manage.py migrate`

# 認証用のユーザーを作成する
- 認証用のユーザを作成する
  - `python manage.py createsuperuser --email admin@example.com --username admin --password admin`
  - `select * from auth_user`

# その他
- HyperlinkedModelSerializer とは
  - https://leben.mobi/blog/django_rest_framework/python/
- ModelViewSet だと  
  - CRUD が全て実行できてしまう
  - https://qiita.com/AJIKING/items/29327b7f7c46e2245505
- Djangoに typed view を持ち込む
  - https://github.com/rsinger86/drf-typed-views
- Django Pydantic
  - https://testdriven.io/blog/django-and-pydantic/
- django でデータロードとダンプ
  - https://www.coderedcorp.com/blog/how-to-dump-your-django-database-and-load-it-into-/
- マイグレーションまとめ
  - https://qiita.com/okoppe8/items/c9f8372d5ac9a9679396
- DDD クリーンアーキテクチャー
  - https://www.youtube.com/watch?v=9-OIHTJdDew
  - https://www.youtube.com/watch?v=9-OIHTJdDew&t=1140s
  - https://little-hands.hatenablog.com/entry/2018/12/10/ddd-architecture
  - https://codehero.jp/python/12578908/separation-of-business-logic-and-data-access-in-django
  - https://qiita.com/NaoyukiSakai/items/cd04d206c7dc835db6bb
  - https://github.com/gaiax/django-ddd-demo
- [[django]テストでユーザログインしたい - Qiita](https://qiita.com/ponsuke/items/03e45d6f6aa309baed38)
- [Djangoのviewでloginした状態をテストする - Qiita](https://qiita.com/haessal/items/2c4077f3600bc3039e06)
- [DjangoでViewのリクエスト前後に任意の処理を差し込む - JoTech](https://hiroki-sawano.hatenablog.com/entry/django-pre-request-and-post-response-decorators)
- [[Django] 自動テストについてのまとめ - Qiita](https://qiita.com/okoppe8/items/eb7c3be5b9f6be244549)
- [gaiax/django-ddd-demo: Djangoでドメイン駆動設計を実践する際に、オニオンアーキテクチャを採用したときのデモ](https://github.com/gaiax/django-ddd-demo)
- Django は MySQL の default や on_updateに対応していない
  - https://qiita.com/tng527/items/be49cdc90fa7f846d8af
- swagger
  - [axnsan12/drf-yasg: Automated generation of real Swagger/OpenAPI 2.0 schemas from Django REST Framework code.](https://github.com/axnsan12/drf-yasg)
  - [DjangoRestFrameworkのコードからSwaggerドキュメントを生成しAPI設計を共有 - Qiita](https://qiita.com/T0000N/items/c982fd9586763747fb11#%E3%81%A9%E3%81%86%E3%82%84%E3%81%A3%E3%81%A6%E6%9B%B8%E3%81%84%E3%81%A6%E3%81%84%E3%82%8B%E3%81%AE%E3%81%8B)
  - [django rest framework : swagger - Qiita](https://qiita.com/Satoshi_Numasawa/items/7ff86e103bd07fb6ba4c)
- カスタムユーザー
  - [Djangoではカスタムユーザを作るべきらしい - Qiita](https://qiita.com/gaku3601/items/9ca3695bb8b18bed5d5e)
  - [Django ユーザー カスタマイズ方法 - Qiita](https://qiita.com/okoppe8/items/10ae61808dc3056f9c8e)
  - [Django の認証方法のカスタマイズ | Django ドキュメント | Django](https://docs.djangoproject.com/ja/3.1/topics/auth/customizing/#substituting-a-custom-user-model)
  - [Django + django-rules + 独自Userモデルで、has_permテンプレートタグを使うときの注意点 - メモ的な思考的な](https://thinkami.hatenablog.com/entry/2020/04/18/215826)
  - [3-11. 認証バックエンドをカスタマイズしてログイン方法を変更する – Django学習帳](https://django.kurodigi.com/customize-auth-backend/)
- DB
  - [Python初心者がDjangoでハマったこと - Qiita](https://qiita.com/tng527/items/be49cdc90fa7f846d8af#%E6%9C%AC%E9%A1%8C)
- ModelSerializerで使う場合、 fields に含まれてないと以下のようなエラーになります。なお、自動的に read_only なフィールドとなるため fields だけに指定すれば良いです。
  - https://note.crohaco.net/2018/django-rest-framework-serializer/
- permission を分ける
  - [Django REST Framework:1つのAPIViewの中でリクエストメソッド毎にpermission_classesを分ける - Qiita](https://qiita.com/xKxAxKx/items/a4a1b225d92ffa041793)


# 実装方針
- Django から乗り換えない
    - 少なくとも fastapi に乗り換えるなどはない
    - テストツールは django にロックインする
- Pythonを使う可能性があるし、Python実装者が多い
- 必要な分離を行う
    - 将来的にフレームワークを取り換えるためではない
    - ロジック や ドメイン や テスト観点はわかりやすくするため
    - テスタブルにするため
        - (DBを除いて) 外部に問い合わせる部分はインターフェースを用意して、テスト時にモックに差し替えられるようにする

- view は基本的に method 毎の input(request) と output(response) が定義するところ
    - 見通しをよくする必要あり
    - データを ユースケースに投げる
    - slim contoroller にする
    - デコレーターを使えば簡単に

- ユースケースそうを作る
    - タスクの組み立て(権限チェック + オブジェクトの再生 + 業務ロジックに処理依頼 )
    - repository のセットを行う
    - 権限チェックはデコレータを使う

- 業務ロジック = サービス
    - アプリ固有の複雑な処理 や 問合せ
        - [やはりお前たちのRepositoryは間違っている - Qiita](https://qiita.com/mikesorae/items/ff8192fb9cf106262dbf)
    アプリ固有の複雑な処理
- リポジトリ
    - オブジェクトの再生 + 外部への問合せ 
    - エンティティの永続化や取得