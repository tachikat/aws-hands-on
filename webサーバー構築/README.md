# Webサーバ構築
## nginxインストール
* nginxインストール
~~~
# nginxインストール
$ sudo dnf nginx -y

# nginx起動
$ sudo systemctl start nginx

# 起動確認
$ sudo systemctl status nginx
~~~

* ブラウザから確認
http://EC2のIPアドレス

## 静的ページ作成
* htmlページを配置
~~~
# nginxのドキュメントルートへ移動
$ cd /usr/share/nginx/html

# htmlファイルを配置　test.htmlを配置する
# VScodeでコピペするか、viでコピペするか
~~~
* ブラウザから確認
http://EC2のIPアドレス/test.html

