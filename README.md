wordpress template

mysql:8.4.0
wordpress:latest

1. mysqlに接続する
2. user作成
3. localhost:XXXXで起動確認
4. wps-hide-loginをインストール
5. 不要なテーマを削除
4. WordPress REST API Authenticationをインストール
5. WordPress REST API Authenticationの設定を完了する
6. `.htaccess`をルートディレクトリに新規作成
7. `wp-config.php`をルートディレクトリに新規作成
8. `wp-config.php`の権限を変更

```.htaccess
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTP:Authorization} ^(.*)
RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]
</IfModule>
SetEnvIf Authorization "(.*)" HTTP_AUTHORIZATION=$1
```

```wp-config.php
<?php
  define('JWT_AUTH_SECRET_KEY', getenv('JWT_AUTH_SECRET_KEY'));
  define('JWT_AUTH_CORS_ENABLE', true);

  if ( isset( $_SERVER['HTTP_AUTHORIZATION'] ) ) {
      $_SERVER['REDIRECT_HTTP_AUTHORIZATION'] = $_SERVER['HTTP_AUTHORIZATION'];
  }
```
