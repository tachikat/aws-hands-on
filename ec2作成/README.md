# EC2作成
## マネジメントコンソールからEC2を作成
1. EC2のサービスのページ開く
1. 「インスタンスを起動」をクリック
1. パラメータを設定
    1. 名前：自分のアカウント名＋Web(例：tachikatWeb)
    1. アプリケーションおよび OS イメージ ：Amazon Linux 2023 AMI
    1. インスタンスタイプ：t2.micro
    1. キーペア: 新しいキーペアの作成(キーペア名：アカウント+key(例：tachikatkey)、あとはデフォルト)
    1. 「キーペアを作成」をクリックし、キーをダウンロードしておく
    1. ネットワーク設定：編集をクリック
    1. VPC：自分が作ったVPC
    1. サブネット：自分が作ったパブリックサブネット
    1. パブリック IP の自動割り当て：有効化
    1. ファイアウォール (セキュリティグループ) ：セキュリティグループを作成する
    1. セキュリティグループ名：自分のアカウント+SG(例：tachikatSG)
    1. 説明：適当に
    1. インバウンドセキュリティグループのルール：なし
    1. セキュリティグループルール 1 : {タイプ：ssh , ソースタイプ：自分のIP}
    1. 「セキュリティグループルールを追加」をクリック
    1. セキュリティグループルール 1 : {タイプ：HTTP , ソースタイプ：任意の場所}
1. 「インスタンスを起動」をクリック



## EC2へログイン
任意のターミナルを使用して、sshログイン
* VScodeの場合：リモートエクスプローラーからプロパティマークをクリックし、以下を記載する
~~~
Host ec2
  Hostname 起動したec2のIPアドレス
  User ec2-user
  PasswordAuthentication no
  IdentityFile 秘密鍵の絶対パス　（例 C:\Users\XXXXXX\Desktop\XXXXX.pem）　
  IdentitiesOnly yes
~~~

* コマンドラインでログインする場合
~~~
$ ssh -i "秘密鍵.pem" ec2-user@起動したEC2のIPアドレス
~~~