# RDS作成
## マネジメントコンソールからRDSを作成
1. RDSのサービスのページ開く
1. 「データベースの作成」をクリック
1. パラメータを設定
    1. データベース作成方法を選択：簡単に作成
    1. エンジンのタイプ：MySQL
    1. DB インスタンスサイズ：無料利用枠
    1. DB インスタンス識別子: アカウント名+RDS(例：tachikatRDS)
    1. マスターユーザー名：admin
    1. マスターパスワード：アカウント名+Pass1!(例：tachikatPass1!)
    1. EC2 接続をセットアップする：{EC2 コンピューティングリソースに接続、EC2 インスタンス：自分の作成したEC2}
1. 「VPCを作成」をクリック

## EC2を踏み台にして、RDSに接続
~~~
# mysqlクライアントインストール
$ sudo dnf install mariadb105

# mysqlコマンド使えるようになったか確認
$ mysql --version

# RDSログイン
$ mysql -u admin -h <作成したRDSのエンドポイント> -p
パスワードを聞かれるので、パスワードを入力

mysqlのプロンプトが、表示されればOK
~~~

## SQL操作

# DB・テーブル作成

~~~
# DB作成（itopeを作成する）
MySQL [(none)]> create database itope;

# DB一覧
MySQL [(none)]> show databases;

# 使用するDBを設定
MySQL [(none)]> use itope;

# テーブルを作成(members)
MySQL [(itope)]> CREATE TABLE members (
ID       INT(3) PRIMARY KEY AUTO_INCREMENT,
Name     VARCHAR(50),
team VARCHAR(10),
role VARCHAR(10)
);

# 想定通りのカラム情報を持ったテーブルを作成できたか確認
MySQL [(itope)]> show columns from members;

# membersテーブルにレコード挿入
MySQL [(itope)]> insert into members (name, team, role) VALUES ('花谷', 'A', 'チーム長');

# membersテーブルのレコードを確認
MySQL [(itope)]> select * from members;


# membersテーブルにどんどん挿入
川村　A　チーム長
大谷　C　メンバー
松山　A　メンバー
野村　C　メンバー
雑賀　B　メンバー
吉村　B　メンバー
安田　C　チーム長
を作成

MySQL [(itope)]> insert into members (name, team, role) VALUES ('李', 'B' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('川村', 'A' , 'チーム長');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('大谷', 'C' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('松山', 'A' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('野村', 'C' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('雑賀', 'B' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('吉村', 'B' , 'メンバー');
MySQL [(itope)]> insert into members (name, team, role) VALUES ('安田', 'C' , 'チーム長');


# membersテーブルのレコードを確認
MySQL [(itope)]> select * from members;

# Aチームのみ抽出
MySQL [(itope)]> select * from members where team = 'A';

# Aチームのかつ、役割がメンバーのみ抽出
MySQL [(itope)]> select * from members where team = 'A' and role = 'メンバー';

# 吉村さんの役割をリーダーに変更する
MySQL [(itope)]> update members set role = 'リーダー' WHERE name = '吉村';

# 安田さんのレコードを削除する
MySQL [(itope)]> delete from members where name = '安田';

~~~
